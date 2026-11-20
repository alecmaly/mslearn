# https://learn.microsoft.com/en-us/azure/data-explorer/anomaly-detection

Source: https://learn.microsoft.com/en-us/azure/data-explorer/anomaly-detection

---

id="main"
 role="main"
 class="layout-body-main "
 data-bi-name="content"
 lang="en-us"
 dir="ltr"
 >
 
 
 
 
 
 Table of contents 
 
 
 
 Exit editor mode
 
 

 
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 

 

 
 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 Reading mode
 
 
 
 
 Table of contents
 
 
 
 
 
 
 Read in English
 
 
 
 
 
 
 
 Add
 
 
 
 
 
 
 Add to Plans
 
 
 
 
 
 
 
 Edit
 
 
 
 
 
 
 
 
 
 
 Copy Markdown
 
 
 
 
 
 
 Print
 
 
 
 

 
 

 
 

 

 
 
 
 
 
 
 
 
 Note
 

 
 Access to this page requires authorization. You can try signing in or changing directories.
 

 
 Access to this page requires authorization. You can try changing directories.
 

 

 

 

 
 
# Anomaly detection and forecasting

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Switch services using the Version drop-down list. Learn more about navigation. 

Applies to: â Microsoft Fabric â Azure Data Explorer â Azure Monitor â Microsoft Sentinel

Cloud services and IoT devices generate telemetry you use to monitor service health, production processes, and usage trends. Time series analysis helps you spot deviations from each metric's baseline pattern.

Kusto Query Language (KQL) includes native support for creating, manipulating, and analyzing multiple time series. Use KQL to create and analyze thousands of time series in seconds for near real time monitoring.

This article describes KQL time series anomaly detection and forecasting capabilities. The functions use a robust, well known decomposition model that splits each time series into seasonal, trend, and residual components. Detect anomalies by finding outliers in the residual component. Forecast by extrapolating the seasonal and trend components. KQL adds automatic seasonality detection, robust outlier analysis, and a vectorized implementation that processes thousands of time series in seconds.

## Prerequisites

- Use a Microsoft account or a Microsoft Entra user identity. You don't need an Azure subscription.

- Read about time series capabilities in Time series analysis.

## Time series decomposition model

The KQL native implementation for time series prediction and anomaly detection uses a well known decomposition model. Use this model for time series with periodic and trend behaviorâlike service traffic, component heartbeats, and periodic IoT measurementsâto forecast future values and detect anomalies. The regression assumes the remainder is random after removing the seasonal and trend components. Forecast future values from the seasonal and trend components (the baseline) and ignore the residual. Detect anomalies by running outlier analysis on the residual component.
Use the `series_decompose()` function to create a decomposition model. It decomposes each time series into seasonal, trend, residual, and baseline components.

Example: Decompose internal web service traffic:

Run the query

`let min_t = datetime(2017-01-05);
let max_t = datetime(2017-02-03 22:00);
let dt = 2h;
demo_make_series2
| make-series num=avg(num) on TimeStamp from min_t to max_t step dt by sid 
| where sid == 'TS1' // Select a single time series for cleaner visualization
| extend (baseline, seasonal, trend, residual) = series_decompose(num, -1, 'linefit') // Decompose each time series into seasonal, trend, residual, and baseline (seasonal + trend)
| render timechart with(title='Web app traffic for one month, decomposition', ysplit=panels)
`

- The original time series is labeled num (in red).

- The process autodetects seasonality using the `series_periods_detect()` function and extracts the seasonal pattern (purple).

- Subtract the seasonal pattern from the original time series, then run a linear regression with the `series_fit_line()` function to find the trend component (light blue).

- The function subtracts the trend, and the remainder is the residual component (green).

- Finally, add the seasonal and trend components to generate the baseline (blue).

## Time series anomaly detection

The function `series_decompose_anomalies()` finds anomalous points on a set of time series. This function calls `series_decompose()` to build the decomposition model and then runs `series_outliers()` on the residual component. `series_outliers()` calculates anomaly scores for each point of the residual component using Tukey's fence test. Anomaly scores above 1.5 or below -1.5 indicate a mild anomaly rise or decline respectively. Anomaly scores above 3.0 or below -3.0 indicate a strong anomaly.

The following query allows you to detect anomalies in internal web service traffic:

Run the query

`let min_t = datetime(2017-01-05);
let max_t = datetime(2017-02-03 22:00);
let dt = 2h;
demo_make_series2
| make-series num=avg(num) on TimeStamp from min_t to max_t step dt by sid 
| where sid == 'TS1' // select a single time series for a cleaner visualization
| extend (anomalies, score, baseline) = series_decompose_anomalies(num, 1.5, -1, 'linefit')
| render anomalychart with(anomalycolumns=anomalies, title='Web app. traffic of a month, anomalies') //use "| render anomalychart with anomalycolumns=anomalies" to render the anomalies as bold points on the series charts.
`

- The original time series (in red).

- The baseline (seasonal + trend) component (in blue).

- The anomalous points (in purple) on top of the original time series. The anomalous points significantly deviate from the expected baseline values.

## Time series forecasting

The function `series_decompose_forecast()` predicts future values of a set of time series. This function calls `series_decompose()` to build the decomposition model and then, for each time series, extrapolates the baseline component into the future.

The following query allows you to predict next week's web service traffic:

Run the query

`let min_t = datetime(2017-01-05);
let max_t = datetime(2017-02-03 22:00);
let dt = 2h;
let horizon=7d;
demo_make_series2
| make-series num=avg(num) on TimeStamp from min_t to max_t+horizon step dt by sid 
| where sid == 'TS1' // select a single time series for a cleaner visualization
| extend forecast = series_decompose_forecast(num, toint(horizon/dt))
| render timechart with(title='Web app. traffic of a month, forecasting the next week by Time Series Decomposition')
`

- Original metric (in red). Future values are missing and set to 0, by default.

- Extrapolate the baseline component (in blue) to predict next week's values.

## Scalability

Kusto Query Language syntax enables a single call to process multiple time series. Its unique optimized implementation allows for fast performance, which is critical for effective anomaly detection and forecasting when monitoring thousands of counters in near real-time scenarios.

The following query shows the processing of three time series simultaneously:

Run the query

`let min_t = datetime(2017-01-05);
let max_t = datetime(2017-02-03 22:00);
let dt = 2h;
let horizon=7d;
demo_make_series2
| make-series num=avg(num) on TimeStamp from min_t to max_t+horizon step dt by sid
| extend offset=case(sid=='TS3', 4000000, sid=='TS2', 2000000, 0) // add artificial offset for easy visualization of multiple time series
| extend num=series_add(num, offset)
| extend forecast = series_decompose_forecast(num, toint(horizon/dt))
| render timechart with(title='Web app. traffic of a month, forecasting the next week for 3 time series')
`

## Summary

This document details native KQL functions for time series anomaly detection and forecasting. Each original time series is decomposed into seasonal, trend, and residual components for detecting anomalies and/or forecasting. These functionalities can be used for near real-time monitoring scenarios, such as fault detection, predictive maintenance, and demand and load forecasting.

## Related content

- Learn about Anomaly diagnosis capabilities with KQL

 
 

 
 

 

 
 
 
 
 
 
## Feedback

 
 
 Was this page helpful?
 

 
 
 
 
 
 Yes
 
 
 
 
 
 No
 
 
 
 
 
 
 No
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix? 
 
 

 
 

 
 

 

 

 
 
 

 
 
 
 
## 
 Additional resources
 

 
 

 
 

 
 

 
 

 
 
 
 
 
- 
 
 Last updated on 
 2025-09-30
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
