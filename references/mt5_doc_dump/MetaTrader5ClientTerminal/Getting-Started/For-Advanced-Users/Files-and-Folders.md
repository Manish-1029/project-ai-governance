[🏠 Document Start](../../README.md) / [Getting Started](../../Getting-Started.md) / [For Advanced Users](../For-Advanced-Users.md) / Files and Folders

[Previous](One-Time-Passwords-2FATOTP.md) | [Next](Manage-Trading-Accounts.md)

# Files and Folders

This section contains the description of how the platform's files and folders are stored. In the [main mode (#guest)](Platform-Start.md#guest) of platform start, modifiable and read-only files of the platform are stored separately.

## Read-only Files of the Platform

These files are located in /Program Files/platform folder/. They are:

  * Terminal.exe — the executable file of the trading platform;
  * MetaEditor.exe — the executable file of the built-in [MQL5 language editor (#mql5)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#mql5);
  * Sounds/*.wav — a set of standard audio files of the trading platform;



## Modifiable Files

The main platform directory contains several folders: Bases, Config, Logs, MQL5, Profiles, Templates, Tester. For quick access to the desired storage location, use command "![Open data folder](images/terminal_data_icon_1.png) Open data folder" in the [File](../User-Interface.md) menu.

> All text files are of Unicode format. Use appropriate software to edit them.

The Bases directory contains the platform's data bases grouped by servers, as well as some settings:

Folders and Files | Description | Sub-folders | Description  
---|---|---|---  
Default | Default folder of the platform database | History | The folder stores history data of financial instruments. Each security is stored in a separate directory that contains files yyyy.hcc, ticks.dat and the cache folder. Files yyyy.hcc contain one-minute data of a symbol, the file name reflects the year to which the data belong. The file ticks.dat contains tick data of a symbol. Files *.hc stored in the "Cache" folder contain bars of different timeframes calculated for a symbol from one-minute data. They are automatically created when you select the appropriate [chart period (#operations)](../../Price-Charts-Technical-and-Fundamental-Analysis/View-and-Configure-Charts.md#operations).  
Mail | The folder stores all emails received or sent from the platform. Mail databases are stored in *.dat files; a separate file is created for each account opened in the platform. For example, mail-xxxxx.dat, where xxxxx is the account number.  
Server 1 — N | Platform database folders for different trade servers | News | The folder only stores one file news.dat containing the database of all [newsletters (#news)](../../Price-Charts-Technical-and-Fundamental-Analysis/Fundamental-Analysis.md#news) ever received in the platform from a selected trade server.  
Symbols | File selected-xxxxx.dat contains the database of symbol currently selected in the [Market Watch](../../Trading-Operations/Market-Watch.md) window. File symbols-xxxxx.dat contains the common database of symbols available on this trade server.  
Trades | Contains subfolders named by [account](../Open-an-Account.md) numbers ever opened in the platform. Each account folder contains files deals_yyyy.mm.dat and history_yyyy.mm.dat with the information about trade and order [history (#trade-history)](../../Trading-Operations/Executing-Trades.md#trade-history) respectively. Separate files are created for each month. Here yyyy means the year, and mm — month.  
alerts.dat | Contains the database of created [alerts (#alert)](../../Trading-Operations/Executing-Trades.md#alert).  
books.dat | Contains a list of currently open windows of request queues.  
favourites.dat | Contains a database of elements added to Favorites of the [Navigator](../User-Interface.md) window.  
gvariables.dat | Contains information about [global variables](../../Algorithmic-Trading-Trading-Robots/Global-Variables.md) used in the platform.  
hotkeys.ini | Contains a database of keyboard shortcuts.  
indicators.dat | Contains usage statistics of [indicators](../../Price-Charts-Technical-and-Fundamental-Analysis/Technical-Indicators.md) to display in the [Insert](../User-Interface.md) menu.  
objects.dat | Contains usage statistics of [objects](../../Price-Charts-Technical-and-Fundamental-Analysis/Analytical-Objects.md) to display in the [Insert](../User-Interface.md) menu.  
  
Directory Config contains platform configuration files:

Folders and Files | Description  
---|---  
certificates | Folder containing certificate files *.pfx  
accounts.dat | Contains a database of [accounts](../Open-an-Account.md) and their settings.  
common.ini | Contains common platform settings available in the [Options](../Platform-Settings.md) window opened through the [Tools](../User-Interface.md) menu.  
metaeditor.ini | Contains common settings of [MetaEditor (#metaeditor)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#metaeditor).  
terminal.ini | Contains platform interface settings and last used values (for window positioning, attached indicators, etc.)  
servers.dat | Trade server settings for [connection (#server)](../Connect-to-an-Account.md#server).  
  
The Logs directory contains [log files](Platform-Logs.md) of the platform and [MetaEditor (#metaeditor)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#metaeditor), as well as crash logs:

Folders and Files | Description  
---|---  
/Crash/crash.log.* | Directory /crash contains files of the platform crashes. These files are automatically sent to the developer company to determine and eliminate their causes.  
yyyymmdd.log | Log files containing information about events occurring in the platform. Platform logs are stored in separate files for each day it runs. Here yyyy stands for the year, mm — month, dd — day.  
metaeditor.log | [MetaEditor (#metaeditor)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#metaeditor) log files.  
  
The MQL5 directory contains all the information related to programs written in this language:

Folders and Files | Description  
---|---  
/Experts | Contains [Expert Advisor](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md), compiled files (*.ex5) and source code files (*.mq5).  
/Files | Contains files used by Expert Advisors and scripts.  
/Images | Contains image files in *.bmp format.  
/Include | Contains common *.mqh include files.  
/Indicators | Contains files [custom indicators](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md).  
/Libraries | Contains [MQL5 (#mql5)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#mql5) libraries.  
/Logs | Contains Expert Advisor log files (yyyymmdd.log). These files are created separately for each day of the EA operation, their names correspond to their creation date: yyyy stands for the year, mm — month, dd — date.  
/Presets | Parameters of Expert Advisors start are stored in this folder (["Input Parameters" (#run)](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md#run)).  
/Profiles | Contains various profiles and templates:

  * /Charts — chart [profiles (#profiles)](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md#profiles). Templates of default chart settings are stored in the Default subdirectory. Custom and built-in profiles are stored in separate subdirectories with their names corresponding to the names of the profiles. Each profile contains *.chr files with chart descriptions and order.wnd file with the windows placement order.
  * /Deleted — [templates](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md) [of deleted charts](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Deleted-Charts.md) for subsequent re-opening.
  * /SymbolSets — sets of symbols (including displayed information columns) for the ["Market Watch"](../../Trading-Operations/Market-Watch.md) window.
  * /Templates — chart [templates (#template)](../../Price-Charts-Technical-and-Fundamental-Analysis/View-and-Configure-Charts.md#template) as *.tpl files and ReportHistory.htm — [trading history (#trade-history)](../../Trading-Operations/Executing-Trades.md#trade-history) report template.
  * /Tester — *.set files with the last used [sets of input parameters (#inputs)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#inputs) for each Expert Advisor that has ever been tested.

  
/Scripts | Contains files of [scripts (#type)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#type).  
experts.dat | Contains usage statistics of [MQL5 (#mql5)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#mql5) programs to display in the [Insert](../User-Interface.md) menu.  
  
The Tester directory contains files and folders used by the [Strategy Tester](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md):

Folders and Files | Description | Sub-folders | Description  
---|---|---|---  
Agent-IP-address-port | These folders are created for each agent of the tester. The folder name contains the IP address and port number the agent runs on. | MQL5 | The file of the Expert Advisor that was tested last is stored in this folder. Expert Advisors are not saved in the folders of [remote agents](../../Algorithmic-Trading-Trading-Robots/MetaTester-and-Remote-Agents.md).  
logs | The entries of the agent operation journal are stored in this folder.  
bases | History data used by the agent are stored in this folder.  
logs | This folder contains Strategy Tester [log (#result)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#result) files (yyyymmdd.log). These files are created separately for each day of the EA operation, their names correspond to their creation date: yyyy — year, mm — month, dd — day.  
/Manager | This directory contains log entries of the [MetaTester](../../Algorithmic-Trading-Trading-Robots/MetaTester-and-Remote-Agents.md) component.  
/Cache | This folder contains the XML-file of cache of last [Expert Advisor optimization (#cache)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#cache).
