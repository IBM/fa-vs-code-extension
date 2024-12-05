# IBM Fault Analyzer for z/OS&reg; Beta

The IBM Fault Analyzer for z/OS&reg; VS Code extension works in conjunction with the [Zowe Explorer][link-zowe] VS Code extension.
IBM Fault Analyzer for z/OS&reg; helps developers analyze and fix application and system failures.

When applications abnormally end (ABEND) it is crucial to understand the root-cause.
IBM Fault Analyzer for z/OS&reg; can discover ABENDs faster, more confidently, and in less time
by automatically harvesting real-time information of the ABEND and its environment at the time of failure.

## General requirements

- Assumes knowledge of IBM Fault Analyzer for z/OS&reg; product [installation][link-fa-install] and [features][link-features]
- The Fault Analyzer VS Code extension connectivity to the Fault Analyzer host is similar to using
  the Application Delivery Foundation for z/OS&reg; common component (ADFzCC) server
  - Assumes knowledge of how to [install][link-adfz-install] and [configure][link-adfz-config]
    the Application Delivery Foundation for z/OS&reg; common component server
  - [ADFzCC][link-adfz-customize] must use the [AT-TLS][link-adfz-attls] feature when configuring TLS support

## VS Code extension requirements

- [VS Code][link-vscode] `1.90.0`+
- [Zowe Explorer][link-zowe] `2.17.0`+
  - Assumes that the user has knowledge of the Zowe Explorer extension before using the IBM Fault Analyzer extension

## Optional VS Code extensions

- [IBM Z&reg; Open Editor][link-open-editor]
  - Provides color coded sources when viewing side files in fault reports
  - Provides color coded job spool data sets

## Beta host requirements

- [IBM Fault Analyzer for z/OS&reg;][link-fa] `15.1.4`+
- [IBM Application Delivery Foundation for z/OS&reg; Common Components][link-adfz-docs] `1.9.4`+
  - There must be at least one ADFz common component server configured and deployed
    on the host that you want to work with

## Beta limitations

- Does not support all platforms that Zowe Explorer supports:
  - &#9989; Windows
  - &#10060; Linux (untested)
  - &#10060; macOS (untested)
- Does not support all Integrated Development Environments:
  - &#9989; VS Code
  - &#10060; Eclipse Theia (untested)
  - &#10060; Eclipse Che (untested)
  - &#10060; Red Hat CodeReady Workspaces (untested)
- Does not support Multi-Factor Authentication (MFA)
- Does not ask to trust self-signed certificates when connecting to the ADFz common component server

## Beta features

This is a beta version of the IBM Fault Analyzer extension and does not support the full
functionality of the ISPF Fault Analyzer client, or of the Eclipse Fault Analyzer client.

Itemized below are the features supported and not supported in broad terms.

### History files

- Open history files in a separate view
- Add history files to the Fault Analyzer tree view:
  - From the Zowe Data Sets tree view
  - From the Fault Analyzer tree view
  - From the Command Palette
- Remove history files from the Fault Analyzer tree view

### Fault reports

- Reanalyze and show fault reports in a separate view:
  - From the history file view's context menu, or by clicking on a fault entry reference
  - From a job's context menu in the Zowe Jobs tree view
  - From a job's JESMSGLG editor as hyperlinks, and from the context menu
  - From the Command Palette
- Navigate to sections of the report:
  - Event Detail hyperlinks to jump to a specific event
  - Source code hyperlinks to open a source file at a specific line

### ADFz Common Component server connections

- Associate an ADFz port with a Zowe Profile
- Remove the association between an ADFz port and a Zowe profile

## Unsupported features

### History files

- Add default and recent history files
- Copy/Rename/Remove fault entries from the history file
- Filter fault entries
- Choose column ordering and visibility
- View fault entry properties

### Fault reports

- Side files:
  - IDITrace logs
  - JCL for the job causing the ABEND
  - Minidump
- Hyperlinks:
  - Lookup view links for viewing ABEND explanations
  - Data Set links
  - Memory links jumping to minidump
  - CICS links

### Views

- Add view
- Create view
- Show and navigate views

### Fault analytics

- Manage and display charts

# Getting started

## Specifying the ADFz connection port

Before you begin, all the above requirements must be fulfilled.

1. Open VS Code
2. If necessary, create at least one Zowe profile: team configuration profile or v1 profile (deprecated)
3. Switch to the Zowe Explorer toolwindow
4. Right-click on the profile that matches the z/OS subsystem your ADFz common component server is running on
5. From the _Application Delivery Foundation for z/OS_ menu item, choose _Configure ADFz port_
6. Enter the port that your ADFz common component server is configured to use

You are now ready to use the IBM Fault Analyzer VS Code extension.

**NOTE**: if you access a Fault Analyzer feature before configuring the port number,
you will be prompted to specify the port the first time only.

## The Fault Analyzer tree

When the Zowe Explorer toolwindow is selected in VS Code, the toolwindow has three tree views by default:
_Data Sets_, _Unix System Services_, and _Jobs_.

The Fault Analyzer extension adds a _Fault Analyzer_ tree view as well to manage the history files that have been added.  
When an ADFz common component server port is associated with a profile, that connection will be displayed in the _Fault
Analyzer_ tree view.

![Fault Analyzer tree](./docs/images/fa-tree.gif)

### Tree structure

#### Connection nodes

There will be one root node representing each host and port of an ADFz common component server connection.

#### Browse History Files nodes

These are the parent nodes of any history file that have been added for the connection.

- The _Add history file_ inline button (or context menu item) prompts for a data set name
  for a new history file to open and add to the tree

#### History file nodes

These are nodes representing a history file that has already been added.

- The _Open history file_ inline button (or context menu item) opens the history file or reveals it if already open
- The _Remove history file_ inline button (or context menu item) removes the history file from the _Fault Analyzer_ tree

## Adding history files from Zowe Explorer's Data Sets tree

History Files can also be added from Zowe Explorer's _Data Sets_ tree:

1. From a profile in Zowe Explorer's _Data Sets_ tree, select its _Search Data Sets_ inline button or context menu item
2. Select an existing filter or create a new filter that will show the history file that you want to open and add to the
   _Fault Analyzer_ tree
3. From the context menu, select _Fault Analyzer_ > _Add history file_
4. If an ADFz common component server port has not already been specified for this profile, the port will be prompted for
   and a new ADFz connection will be created in the _Fault Analyzer_ tree
5. The history file will be added to the _Fault Analyzer_ tree if it does not already exist in the tree, and will be
   opened in a new tab

![Add history file from Data Sets view](./docs/images/add-hist-from-dsv.gif)

## Viewing fault reports from a history file

Once a history file has been added to the Fault Analyzer tree, it can be displayed by clicking on it in the tree.  
Once the history file is displayed, you can open a fault report by double-clicking on a fault entry row.

An additional path to achieve the same result is to open the context menu over a fault entry row, and select _Reanalyze_.

![Open report from history file](./docs/images/open-fr-from-hf.gif)

## Viewing fault reports from Zowe Explorer's Jobs tree

When jobs that have generated one or more ABEND are viewed from Zowe Explorer's _Jobs_ tree,
you will be able to view the fault report in multiple ways.

### From the _Jobs_ tree node

1. Right-click on the job that completed with an ABEND
2. Select _Fault Analyzer_ > _Open fault report_

   **NOTE**: if there is more than one ABEND in the job, you will be prompted
   to select which fault report you want to open

![Open report from Jobs tree node](./docs/images/open-fr-job.gif)

### From a job's JESMSGLG output data set (hyperlinks)

1. Expand the tree node for the job that completed with an ABEND
2. Click on the _JES2:JESMSGLG_ output data set to open it
3. Hyperlinks will be displayed for each ABEND that occurred.  
   Ctrl-clicking a hyperlink will open the fault report associated with the ABEND

![Open report from JESMSGLG hyperlinks](./docs/images/open-fr-link.gif)

### From a job's JESMSGLG output data set (context menu)

1. Expand the tree node for the job that completed with an ABEND
2. Click on the _JES2:JESMSGLG_ output data set to open it
3. Open the editor's context menu and select _Open fault report_

![Open report from JESMSGLG context menu](./docs/images/open-fr-context.gif)

## Fault Analyzer VS Code commands

The Fault Analyzer extension adds new commands to the VS Code Command Palette.

### Add history file

Adds a history file to the _Fault Analyzer_ tree in the Zowe Explorer toolwindow.  
You will be prompted for:

- An ADFz common component server connection if there is more than one connection defined
- A data set name for the history file you want to open and add to the _Fault Analyzer_ tree

![Add history file from command palette](./docs/images/add-hist-cp.gif)

### Open fault report

Performs reanalysis on a fault report and opens that report.  
You will be prompted for:

- An ADFz common component server connection if there is more than one connection defined
- The data set name for the history file containing the fault entry you want to reanalyze and open
- The fault entry ID for the report you want to reanalyze and open

![Open report from command palette](./docs/images/open-fr-cp.gif)

## Overview of the Fault Report view

The Fault Report view is a collection of tabs that enable the user to view different sections of the report.

Some sections have hyperlinks that will open source files at a specific line number.  
The _Event Details_ section displays event hyperlinks to jump to the definition of the event in another section.

The layout is similar to the Fault Reports view in the IBM Fault Analyzer Eclipse client.

![Overview of the Fault Report view](./docs/images/reports.gif)

[link-vscode]: https://code.visualstudio.com
[link-zowe]: https://marketplace.visualstudio.com/items?itemName=Zowe.vscode-extension-for-zowe
[link-open-editor]: https://marketplace.visualstudio.com/items?itemName=IBM.zopeneditor
[link-fa]: https://www.ibm.com/products/fault-analyzer-for-zos
[link-fa-install]: https://help.blueproddoc.com/faultanalyzer/hadqf1001_FA_Program_Directory_V151.pdf
[link-features]: https://help.blueproddoc.com/faultanalyzer/15.1.5/en/index.html
[link-adfz-docs]: https://help.blueproddoc.com/adfz_common_components/welcome/index.html#
[link-adfz-install]: https://help.blueproddoc.com/adfz_common_components/i1356270_Program_Directory_V1.9.pdf
[link-adfz-config]: https://help.blueproddoc.com/adfz_common_components/1.9.0/en/index.html
[link-adfz-customize]: https://help.blueproddoc.com/adfz_common_components/1.9.0/en/svrauth.html
[link-adfz-attls]: https://help.blueproddoc.com/adfz_common_components/1.9.0/en/attls.html
