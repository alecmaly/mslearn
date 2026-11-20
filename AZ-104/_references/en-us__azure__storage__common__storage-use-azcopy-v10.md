# https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10

Source: https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10

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
 

 

 

 

 
 
# Get started with AzCopy

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Note

If you plan to migrate data into Azure Storage, use Azure Storage Mover. Azure Storage Mover is a managed service that's designed for high-scale transfers (more than 1 TB). It simplifies planning, execution, and monitoring at scale. For more information about migration tools for your scenario, see aka.ms/migratemydata.

AzCopy is a command-line utility that you can use to copy data to, from, or between storage accounts. This article helps you download AzCopy, connect to your storage account, and transfer data.

AzCopy v10 is the currently supported version of AzCopy. It's supported only on versions of Windows, Linux, or macOS that are officially maintained. If you need to use a previous version of AzCopy, see the Use the previous version of AzCopy section of this article.

## AzCopy use cases

Use AzCopy to copy your data to, from, or between Azure storage accounts. Common use cases include:

- Copying data from an on-premises source to an Azure storage account

- Copying data from an Azure storage account to an on-premises source

- Copying data from one storage account to another storage account

AzCopy supports each use case with specific commands and options. For example, AzCopy has native commands for copying and synchronizing data, making it a flexible tool for one-time copy activities and ongoing synchronization scenarios. You can target specific storage services such as Azure Blob Storage or Azure Files, and you can also copy between them. For example, you can copy data from Azure Blob Storage containers to Azure File shares or vice versa.

For a complete list of data transfer guides, see the Transfer data section of this article.

## Get AzCopy

If you're using AzCopy on a Linux machine, you can use a package manager. For all other operating systems, download a portable binary file. For detailed information on AzCopy releases, see the AzCopy release page.

### Use a package manager (Linux only)

Installing AzCopy through your Linux distribution's package manager is the most convenient and maintainable approach. Package manager installation provides automatic dependency resolution, simplified updates, and integration with your system's software management. For step-by-step guidance, see Install AzCopy on Linux by using a package manager.

### Download a portable binary

An installation package is available only for Linux. For all other operating systems, download the AzCopy v10 executable file to any directory on your computer.

- Windows 64-bit (zip)

- Windows 32-bit (zip)

- Windows ARM64 (zip)

- Linux x86-64 (tar)

- Linux ARM64 (tar)

- macOS (zip)

- macOS ARM64 (zip)

These files are compressed as a zip file (Windows and macOS) or a tar file (Linux). To download and decompress the tar file on Linux, see the documentation for your Linux distribution.

### Run AzCopy in a Docker container

You can run AzCopy in a Linux container instead of installing the executable on your host. Install Docker, and then select the image that matches your host architecture. To see the available image tags, refer to the tag list for your architecture:

- AMD64 image tags

- ARM64 image tags

For repeatable deployments, use a version-specific tag instead of `latest`. The following example pulls an AMD64 image and verifies the installed AzCopy version. Replace `<tag>` with an available tag.

`docker pull mcr.microsoft.com/azcopy/linux/amd64:<tag>
docker run --rm mcr.microsoft.com/azcopy/linux/amd64:<tag> azcopy --version
`

To use the ARM64 image, replace `amd64` with `arm64`. To run another AzCopy command, replace `azcopy --version` with the command and arguments that you want to use. If the command accesses files on the host, mount the local directory into the container by using the Docker `--volume` option. For example:

`docker run --rm --volume "<local-directory>:/data" mcr.microsoft.com/azcopy/linux/amd64:<tag> azcopy copy "/data/<file-name>" "<destination-url>"
`

### Add AzCopy to your system path

For convenience, consider adding the directory location of the AzCopy executable to your system path. This addition allows you to type `azcopy` from any directory on your system. If you don't add the AzCopy directory to your path, you need to change directories to the location of your AzCopy executable and type `azcopy` or `.\azcopy` in a command shell.

## Authorize AzCopy

As an owner of your Azure Storage account, you aren't automatically assigned permissions to access data. Before you can do anything meaningful with AzCopy, you need to decide how you'll provide authorization credentials to the storage service. You can provide credentials by using Microsoft Entra ID or by using a SAS token.

### Authorize with Microsoft Entra ID

By using Microsoft Entra ID, you provide credentials once instead of appending a SAS token to each command. Start by choosing what type of security principal you want to authorize. Use the following table as a guide.

Security principal
Guidance

User identity
Authorize access for AzCopy with a user identity

Managed identity
Authorize access for AzCopy with a managed identity

Service principal
Authorize access for AzCopy with a service principal

### Authorize with a SAS token

Append a SAS token to each source or destination URL that you use in your AzCopy commands. This example command recursively copies data from a local directory to a blob container. A fictitious SAS token is appended to the end of the container URL.

`azcopy copy "C:\local\path" "https://account.blob.core.windows.net/mycontainer1/?sv=2018-03-28&ss=bjqt&srt=sco&sp=rwddgcup&se=2019-05-01T05:01:17Z&st=2019-04-30T21:01:17Z&spr=https&sig=MGCXiyEzbtttkr3ewJIh2AR8KrghSy1DGM9ovN734bQF4%3D" --recursive=true
`

The SAS token in the example above contains query parameters that define the access granted to the storage resource. For example, `sv` specifies the storage service version, `sp` specifies the permitted operations, `st` and `se` define the validity period, `spr` specifies the allowed protocol, and `sig` contains the cryptographic signature. The `--recursive=true` flag copies all files and subdirectories from the specified local directory. To learn more about SAS tokens and how to obtain one, see shared access signatures (SAS).

## Transfer data

After you authorize your identity or obtain a SAS token, you can start transferring data.

For example commands, see any of these articles.

Service
Article

Azure Blob Storage
Upload files to Azure Blob Storage

Azure Blob Storage
Download blobs from Azure Blob Storage

Azure Blob Storage
Copy blobs between Azure storage accounts

Azure Blob Storage
Synchronize with Azure Blob Storage

Azure Files
Transfer data with AzCopy and file storage

Amazon S3
Copy data from Amazon S3 to Azure Storage

Google Cloud Storage
Copy data from Google Cloud Storage to Azure Storage (preview)

Azure Stack Storage
Transfer data with AzCopy and Azure Stack storage

You can run AzCopy commands interactively. You can also incorporate AzCopy into automated scripts for batch operations, scheduled data transfers, or continuous integration pipelines. For more information, see Use AzCopy in scripts and scheduled transfers.

Note

AzCopy does not support scenarios where the source or destination is being actively changed during the transfer.

## Get command help

To see a list of commands, type `azcopy -h` and then press the ENTER key.

To learn about a specific command, include the command name (for example: `azcopy list -h`).

### List of commands

The following table lists all AzCopy v10 commands. Each command links to a reference article.

Command
Description

azcopy bench
Runs a performance benchmark by uploading or downloading test data to or from a specified location.

azcopy copy
Copies source data to a destination location.

azcopy doc
Generates documentation for the tool in Markdown format.

azcopy env
Shows the environment variables that can configure AzCopy's behavior.

azcopy jobs
Subcommands related to managing jobs.

azcopy jobs clean
Removes all log and plan files for all jobs.

azcopy jobs list
Displays information on all jobs.

azcopy jobs remove
Removes all files associated with the given job ID.

azcopy jobs resume
Resumes the existing job with the given job ID.

azcopy jobs show
Shows detailed information for the given job ID.

azcopy list
Lists the entities in a given resource.

azcopy login
Signs in to Microsoft Entra ID to access Azure Storage resources.

azcopy login status
Displays the current Azure authentication status.

azcopy logout
Signs the user out and terminates access to Azure Storage resources.

azcopy make
Creates a container or file share.

azcopy remove
Deletes blobs or files from an Azure storage account.

azcopy sync
Replicates the source location to the destination location.

azcopy set-properties
Changes the access tier of one or more blobs and replaces (overwrites) the metadata and index tags of one or more blobs.

Note

AzCopy doesn't have a command to rename files.

## Configure, optimize, and troubleshoot AzCopy

See any of the following resources:

- AzCopy configuration settings

- Optimize the performance of AzCopy

- Find errors and resume jobs by using log and plan files in AzCopy

- Troubleshoot problems with AzCopy v10

## Opt out of AzCopy telemetry

Starting with AzCopy v10.34.0, AzCopy collects usage telemetry. You can opt out of sending telemetry by using the `--disable-telemetry` option.

To disable telemetry, add the option to your AzCopy command:

`--disable-telemetry=true`

When this option is enabled, AzCopy doesn't send usage telemetry, including Azure Storage account names and pseudonymous installation and job identifiers.

## Next steps

If you have questions, issues, or general feedback, submit them on GitHub.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-05
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
