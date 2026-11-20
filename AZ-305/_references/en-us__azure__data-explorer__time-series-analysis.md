# https://learn.microsoft.com/en-us/azure/data-explorer/time-series-analysis

Source: https://learn.microsoft.com/en-us/azure/data-explorer/time-series-analysis

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
 

 

 

 

 
 
# Time series analysis

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Switch services using the Version drop-down list. Learn more about navigation. 

Applies to: â Microsoft Fabric â Azure Data Explorer â Azure Monitor â Microsoft Sentinel

Cloud services and IoT devices generate telemetry you can use to gain insights into service health, production processes, and usage trends. Time series analysis helps you identify deviations from typical baseline patterns.

Kusto Query Language (KQL) has native support for creating, manipulating, and analyzing multiple time series. This article shows how to use KQL to create and analyze thousands of time series in seconds to enable near real-time monitoring solutions and workflows.

## Time series creation

Create a large set of regular time series using the `make-series` operator and fill in missing values as needed.
Partition and transform the telemetry table into a set of time series. The table usually contains a timestamp column, contextual dimensions, and optional metrics. The dimensions are used to partition the data. The goal is to create thousands of time series per partition at regular time intervals.

The input table demo_make_series1 contains 600K records of arbitrary web service traffic. Use the following command to sample 10 records:

Run the query

`demo_make_series1 | take 10 
`

The resulting table contains a timestamp column, three contextual dimension columns, and no metrics:

TimeStamp
BrowserVer
OsVer
Country/Region

2016-08-25 09:12:35.4020000
Chrome 51.0
Windows 7
United Kingdom

2016-08-25 09:12:41.1120000
Chrome 52.0
Windows 10

2016-08-25 09:12:46.2300000
Chrome 52.0
Windows 7
United Kingdom

2016-08-25 09:12:46.5100000
Chrome 52.0
Windows 10
United Kingdom

2016-08-25 09:12:46.5570000
Chrome 52.0
Windows 10
Republic of Lithuania

2016-08-25 09:12:47.0470000
Chrome 52.0
Windows 8.1
India

2016-08-25 09:12:51.3600000
Chrome 52.0
Windows 10
United Kingdom

2016-08-25 09:12:51.6930000
Chrome 52.0
Windows 7
Netherlands

2016-08-25 09:12:56.4240000
Chrome 52.0
Windows 10
United Kingdom

2016-08-25 09:13:08.7230000
Chrome 52.0
Windows 10
India

Because there are no metrics, build time series representing the traffic count, partitioned by OS:

Run the query

`let min_t = toscalar(demo_make_series1 | summarize min(TimeStamp));
let max_t = toscalar(demo_make_series1 | summarize max(TimeStamp));
demo_make_series1
| make-series num=count() default=0 on TimeStamp from min_t to max_t step 1h by OsVer
| render timechart 
`

- Use the `make-series` operator to create three time series, where:

- `num=count()`: traffic count.

- `from min_t to max_t step 1h`: creates the time series in one hour bins from the table's oldest to newest timestamp.

- `default=0`: specifies the fill method for missing bins to create regular time series. Alternatively, use `series_fill_const()`, `series_fill_forward()`, `series_fill_backward()`, and `series_fill_linear()` for different fill behavior.

- `by OsVer`: partitions by OS.

- The time series data structure is a numeric array of aggregated values for each time bin. Use `render timechart` for visualization.

The table above has three partitions (Windows 10, Windows 7, and Windows 8.1). The chart shows a separate time series for each OS version:

## Time series analysis functions

In this section, we'll perform typical series processing functions. Once a set of time series is created, KQL supports a growing list of functions to process and analyze them. We'll describe a few representative functions for processing and analyzing time series.

### Filtering

Filtering is a common practice in signal processing and useful for time series processing tasks (for example, smooth a noisy signal, change detection).

- There are two generic filtering functions:

- `series_fir()`: Applying FIR filter. Used for simple calculation of moving average and differentiation of the time series for change detection.

- `series_iir()`: Applying IIR filter. Used for exponential smoothing and cumulative sum.

- `Extend` the time series set by adding a new moving average series of size 5 bins (named ma_num) to the query:

Run the query

`let min_t = toscalar(demo_make_series1 | summarize min(TimeStamp));
let max_t = toscalar(demo_make_series1 | summarize max(TimeStamp));
demo_make_series1
| make-series num=count() default=0 on TimeStamp from min_t to max_t step 1h by OsVer
| extend ma_num=series_fir(num, repeat(1, 5), true, true)
| render timechart
`

### Regression analysis

A segmented linear regression analysis can be used to estimate the trend of the time series.

- Use series_fit_line() to fit the best line to a time series for general trend detection.

- Use series_fit_2lines() to detect trend changes, relative to the baseline, that are useful in monitoring scenarios.

Example of `series_fit_line()` and `series_fit_2lines()` functions in a time series query:

Run the query

`demo_series2
| extend series_fit_2lines(y), series_fit_line(y)
| render linechart with(xcolumn=x)
`

- Blue: original time series

- Green: fitted line

- Red: two fitted lines

Note

The function accurately detected the jump (level change) point.

### Seasonality detection

Many metrics follow seasonal (periodic) patterns. User traffic of cloud services usually contains daily and weekly patterns that are highest around the middle of the business day and lowest at night and over the weekend. IoT sensors measure in periodic intervals. Physical measurements such as temperature, pressure, or humidity may also show seasonal behavior.

The following example applies seasonality detection on one month traffic of a web service (2-hour bins):

Run the query

`demo_series3
| render timechart 
`

- Use series_periods_detect() to automatically detect the periods in the time series, where:

- `num`: the time series to analyze

- `0.`: the minimum period length in days (0 means no minimum)

- `14d/2h`: the maximum period length in days, which is 14 days divided into 2-hour bins

- `2`: the number of periods to detect

- Use series_periods_validate() if we know that a metric should have specific distinct periods and we want to verify that they exist.

Note

It's an anomaly if specific distinct periods don't exist

Run the query

`demo_series3
| project (periods, scores) = series_periods_detect(num, 0., 14d/2h, 2) //to detect the periods in the time series
| mv-expand periods, scores
| extend days=2h*todouble(periods)/1d
`

periods
scores
days

84
0.820622786055595
7

12
0.764601405803502
1

The function detects daily and weekly seasonality. The daily scores less than the weekly because weekend days are different from weekdays.

### Element-wise functions

Arithmetic and logical operations can be done on a time series. Using series_subtract() we can calculate a residual time series, that is, the difference between original raw metric and a smoothed one, and look for anomalies in the residual signal:

Run the query

`let min_t = toscalar(demo_make_series1 | summarize min(TimeStamp));
let max_t = toscalar(demo_make_series1 | summarize max(TimeStamp));
demo_make_series1
| make-series num=count() default=0 on TimeStamp from min_t to max_t step 1h by OsVer
| extend ma_num=series_fir(num, repeat(1, 5), true, true)
| extend residual_num=series_subtract(num, ma_num) //to calculate residual time series
| where OsVer == "Windows 10" // filter on Win 10 to visualize a cleaner chart 
| render timechart
`

- Blue: original time series

- Red: smoothed time series

- Green: residual time series

## Time series workflow at scale

This example shows anomaly detection running at scale on thousands of time series in seconds. To see sample telemetry records for a DB service read count metric over four days, run the following query:

Run the query

`demo_many_series1
| take 4 
`

TIMESTAMP
Loc
Op
DB
DataRead

2016-09-11 21:00:00.0000000
Loc 9
5117853934049630089
262
0

2016-09-11 21:00:00.0000000
Loc 9
5117853934049630089
241
0

2016-09-11 21:00:00.0000000
Loc 9
-865998331941149874
262
279862

2016-09-11 21:00:00.0000000
Loc 9
371921734563783410
255
0

View simple statistics:

Run the query

`demo_many_series1
| summarize num=count(), min_t=min(TIMESTAMP), max_t=max(TIMESTAMP) 
`

num
min_t
max_t

2177472
2016-09-08 00:00:00.0000000
2016-09-11 23:00:00.0000000

A time series in 1-hour bins of the read metric (four days Ã 24 hours = 96 points) shows normal hourly fluctuation:

Run the query

`let min_t = toscalar(demo_many_series1 | summarize min(TIMESTAMP)); 
let max_t = toscalar(demo_many_series1 | summarize max(TIMESTAMP)); 
demo_many_series1
| make-series reads=avg(DataRead) on TIMESTAMP from min_t to max_t step 1h
| render timechart with(ymin=0) 
`

This behavior is misleading because the single normal time series is aggregated from thousands of instances that can have abnormal patterns. Create a time series per instance defined by Loc (location), Op (operation), and DB (specific machine).

How many time series can you create?

Run the query

`demo_many_series1
| summarize by Loc, Op, DB
| count
`

Count

18339

Create 18,339 time series for the read count metric. Add the `by` clause to the make-series statement, apply linear regression, and select the top two time series with the most significant decreasing trend:

Run the query

`let min_t = toscalar(demo_many_series1 | summarize min(TIMESTAMP)); 
let max_t = toscalar(demo_many_series1 | summarize max(TIMESTAMP)); 
demo_many_series1
| make-series reads=avg(DataRead) on TIMESTAMP from min_t to max_t step 1h by Loc, Op, DB
| extend (rsquare, slope) = series_fit_line(reads)
| top 2 by slope asc 
| render timechart with(title='Service Traffic Outage for 2 instances (out of 18339)')
`

Display the instances:

Run the query

`let min_t = toscalar(demo_many_series1 | summarize min(TIMESTAMP)); 
let max_t = toscalar(demo_many_series1 | summarize max(TIMESTAMP)); 
demo_many_series1
| make-series reads=avg(DataRead) on TIMESTAMP from min_t to max_t step 1h by Loc, Op, DB
| extend (rsquare, slope) = series_fit_line(reads)
| top 2 by slope asc
| project Loc, Op, DB, slope 
`

Loc
Op
DB
slope

Loc 15
37
1151
-104,498.46510358342

Loc 13
37
1249
-86,614.02919932814

In under two minutes, the query analyzes nearly 20,000 time series and detects two with a sudden read count drop.

These capabilities and the platform performance provide a powerful solution for time series analysis.

## Related content

- Anomaly detection and forecasting with KQL.

- Machine learning capabilities with KQL.

 
 

 
 

 

 
 
 
 
 
 
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
