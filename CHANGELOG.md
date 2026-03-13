# 16.1.326030310 (release)

- Improved multi-step Command Palette workflows by adding visible step counts and in-place progress
  indication while performing background validation of user input, avoiding shifting focus from the
  Command Palette to a progress notification.

### Requirements

- Changed the minimum supported Zowe Explorer version to 3.2.0 to improve compatibility.
- Raised the minimum supported VS Code version to 1.101.0.

# 16.1.226011417 (release)

- No user-facing changes.  
  This release focuses on internal refactors to improve and consolidate the extension's quality.

# 16.1.225110416 (release)

### History File

- Added the ability to reset the visible columns to their original configuration.
- Added filtering support for textual columns.  
  You can now specify a single text filter to perform a case-insensitive match on each column's content.
- Improved table rendering performance.  
  Extremely large history files can now be displayed without any UI lag.

# 16.1.225101614 (release)

### History File

- Enabled selecting and resizing visible columns (closes [fa-vs-code-extension#2][issue-2]).  
  Per-column filtering is currently WIP.
- Fixed highlighting of the focused row when the Fault Entries' sort order changes.

### Fault Report

- Added hyperlinks to data set names to make it easier to open them using IBM File Manager, if installed.
- Improved navigation to an Event from the Event Summary section.  
  The event details are now immediately visible on screen, without requiring any manual scrolling.

### Other

- Sorted Zowe profile selection by last used, aligning the Command Palette behavior with other extensions.
- Improved the overall presentation and consistency of UI elements in custom editors.

# 16.1.125082220 (release)

- Improved synchronization between the History Files tree and available ADFzCC connections.  
  Connections for Zowe profiles that no longer exist are no longer shown.
- Skipped parsing CICS trace diagram data since trace diagrams are currently unsupported,
  preventing unintended information from being displayed in the Fault Report.

# 16.1.125072314 (release)

- Added support for pass tokens (e.g., for Multi-factor Authentication).
- Added Japanese language support for resources such as Fault Reports.  
  The resource language can be selected via the **IBM Fault Analyzer** > **Language** setting.

# 16.1.25061109 (release)

- Increased the minimum required Zowe Explorer version to `3.1.0`.

# 16.1.25032015 (release)

- No changes.

# 16.1.25021416 (pre-release)

- Updated the product's icon.

# 16.1.25013008 (pre-release)

- Enabled the basic find widget for the history file webview.
- Cleaned up the extension's code.

# 16.1.24121614 (pre-release)

- Fixed an issue where clicking the 'Add history file' button on the Fault Analyzer tree
  (visible only with an empty tree) provided no feedback.
- Improved protocol APIs to deliver better performance and reliability.

[issue-2]: https://github.com/IBM/fa-vs-code-extension/issues/2
