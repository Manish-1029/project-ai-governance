[🏠 Document Start](../../README.md) / [Getting Started](../../Getting-Started.md) / [For Advanced Users](../For-Advanced-Users.md) / Platform Start

[Previous](Installation-on-Linux.md) | [Next](Extended-Authentication.md)

<a id="how-to-start-the-trading-platform"></a>
# How to Start the Trading Platform (#how-to-start-the-trading-platform)

After installation, a group of programs of the trading platform is added to the Start menu, and the program shortcut is created on the desktop. Use them to run the platform.

> Two copies of the platform cannot run from the same directory. If you need to run multiple copies at the same time, install the appropriate number of programs in different directories.

There are two main modes of trading platform start, as well as some [additional (#command-line)](Platform-Start.md#command-line) methods.

<a id="guest"></a>
## Main Mode (#guest)

Starting from MS Windows Vista, applications installed to Program Files are not allowed to store their data in the installation folder on default. All data should be stored in a separate Windows user directory.

Thus, if the platform is installed in the Program Files directory and user rights to write to that directory are limited, it is run in the main mode. The main mode is also used in the following situations:

  * If the UAC (User Activity Control) system is enabled.
  * If remote connection to a computer is used (RDP, Remote Desktop Protocol).



In this mode, the editable files of the platform are stored in a specific Windows user directory, and the immutable files are stored in Program Files. Immutable files include executables of the platform, of MetaEditor, standard sounds, etc. Editable files are:

  * all platform settings, configuration files;
  * all the databases (price history);
  * platform and expert [journals](Platform-Logs.md);
  * all profiles.



All the editable files of the platform are stored in the following directories (depending on the operating system used):

Microsoft Windows XP SP3:

  * C:\Documents and Settings\username\Application Data\MetaQuotes\Terminal\instance_id\



Microsoft Windows Vista and higher:

  * C:\Users\username\AppData\Roaming\MetaQuotes\Terminal\instance_id\



Here 'C' is the logical drive letter on which Windows is installed, "username" is the account name in the operating system under which the platform has been installed, "instance_id" is a unique identifier generated based on the path to the directory where the platform is installed.

For quick access to these folders, use the command "![Open data folder](images/terminal_data_icon.png) Open Data Folder" in the [File](../User-Interface.md) menu. Each data folder contains a special text file origin.txt. This file contains the path to the platform installation folder, which corresponds to this data directory.

  * In the main mode, the catalog where editable files are stored is different for each Windows account.
  * A detailed description of the platform file structure and their purpose is given in the [appropriate section](Files-and-Folders.md). 

  
---  
  
<a id="portable-mode"></a>
## Portable Mode (#portable-mode)

When installed to Program Files, the platform works in the main mode described above on default. All the platform data are stored in a special Windows user directory. However you can force the platform to store its data in the installation folder. To do it, run the platform in the portable mode. To use this mode, start the platform from the command line with the additional [/portable (#portable)](Platform-Start.md#portable) key. For example, "C:\Program Files\MyTerminal\terminal.exe /portable".

> To run the platform in the Portable mode, the following conditions must be met:

<a id="command-line"></a>
## Running from the Command Line (#command-line)

The trading platform can be run manually with predefined parameters. This can be done by using different keys for starting from a command line and alternative [configuration files (#configuration-file)](Platform-Start.md#configuration-file).

The platform can be run with the keys from the command line. Specify there a path to the executable platform file (path to the file\terminal.exe) and after a space add one or several of the below keys:

  * /login:login number — running a platform under a certain [account](../Open-an-Account.md). For example, terminal.exe / login:100000.
  * /config:path to a configuration file — running a platform with an alternative configuration file. For example, terminal.exe /config:c:\myconfiguration.ini. The default configuration file is [common.ini (#common)](Files-and-Folders.md#common).
  * /profile:profile name — running the platform with a definite [profile (#profiles)](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md#profiles). The profile must be pre-created and located in the [/profiles/charts/ (#profiles)](Files-and-Folders.md#profiles) of the platform. For example, terminal.exe /profile:Euro.
  * /portable — set the platform to run in the [Portable mode](Platform-Start.md). Running in this mode may be needed if the platform was earlier launched in the [main mode (#guest)](Platform-Start.md#guest). To run the platform in the portable mode, the operating system user requires appropriate permissions.



> If the key assignment is set incorrectly (invalid login, profile name or configuration file), the default value will be used.

<a id="configuration-file"></a>
## Running with a Custom Configuration File (#configuration-file)

The trading platform can be run with a custom set of parameters. Create your own configuration file based on the default [common.ini (#common)](Files-and-Folders.md#common). To start the platform with a custom configuration file, run the following command in the [command line (#command-line)](Platform-Start.md#command-line):

path_to_platform\terminal64.exe /config:c:\myconfiguration.ini

where "c:\myconfiguration.ini" is the path to the custom configuration file.

> Custom configuration files are used in the "read only" mode during the work of the platform. Changes in settings made from the platform interface are not written to the used custom configuration file.

The configuration file parameters are divided into several blocks and correspond to the settings on [platform configuration](../Platform-Settings.md) window tabs. Below are the most important settings in the configuration file:

<a id="common"></a>
### [Common] (#common)

Common platform settings similar to the [Server (#server)](../Platform-Settings.md#server) tab:

  * Login — account number. The platform tries to read additional authorization information from a configuration file (server, password and certificate password specified in the parameters described below). If the authorization information for the account is not specified, the platform tries to read it from its own account database;
  * Server — address and port number of a trade server separated with a colon;
  * Password — password for connecting to the account specified in the Login parameter;
  * CertPassword — certificate password. This parameter is required if the [extended authentication](Extended-Authentication.md) mode is enabled for the account. If the used certificate is not installed in the operating system storage, its file should be placed in platform_folder/config/certificates/;
  * ProxyEnable — allow (1) or prohibit (0) connection through a proxy server;
  * ProxyType — type of a proxy server: 0 (SOCKS4), 1 (SOCKS5), 2 (HTTP);
  * ProxyAddress — IP address and port of the proxy server separated by a colon;
  * ProxyLogin — login for authorizing on a proxy server;
  * ProxyPassword — password for authorizing on a proxy server;
  * KeepPrivate — saving the password between connections: 1 — to save, 0 — not to save.
  * NewsEnable — enable (1) or disable (0) news letters;
  * CertInstall — install (1) or do not install (0) new certificates in the system storage (for [extended authentication](Extended-Authentication.md)).
  * MQL5Login — account on [MQL5.community](https://www.mql5.com/ "MQL5.community"). 
  * MQL5Password — password for the specified account on [MQL5.community](https://www.mql5.com/ "MQL5.community"). 



<a id="charts"></a>
### [Charts] (#charts)

[Chart (#charts)](../Platform-Settings.md#charts) settings:

  * ProfileLast — the name of the current [profile (#profiles)](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md#profiles);
  * MaxBars — the maximum number of bars in a chart;
  * PrintColor — chart print mode: 1 — color printing, 0 — black-and-white printing;
  * SaveDeleted — save (1) or not (0) [deleted chart](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Deleted-Charts.md) to reopen later.



<a id="experts"></a>
### [Experts] (#experts)

[Expert Advisor (#ea)](../Platform-Settings.md#ea) settings:

  * AllowLiveTrading — enable (1) or disable (0) automated trading using [Expert Advisors](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md).
  * AllowDllImport — DLL import allowed (1) or not (0);
  * Enabled — enable or disable use of Expert Advisors;
  * Account — disable (1) or not (0) Expert Advisors when connecting with a different [account](../Open-an-Account.md);
  * Profile — disable (1) or not (0) Expert Advisors after change after change of the active [profile (#profiles)](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md#profiles).



<a id="objects"></a>
### [Objects] (#objects)

[Object (#charts)](../Platform-Settings.md#charts) settings:

  * ShowPropertiesOnCreate — show (1) or do not show (0) properties of objects being created;
  * SelectOneClick — select (1) or not (0) objects at a single mouse click;
  * MagnetSens — docking sensitivity of objects;



<a id="email"></a>
### [Email] (#email)

[Email (#mail)](../Platform-Settings.md#mail) settings:

  * Enable — enable (1) or disable (0) use of email;
  * Server — address of the SMTP server;
  * Auth — encrypted information for authentication on the mail server;
  * Login — login for the SMTP server;
  * Password — password for the SMTP server;
  * From — sender's name and address;
  * To — recipient's name and address.



<a id="startup"></a>
### [StartUp] (#startup)

Settings of [Expert Advisors (#ea)](../Platform-Settings.md#ea) and [scripts (#type)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#type), that open automatically when you start the platform:

  * Expert — file name of the [Expert Advisor](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md) that opens automatically when you start the platform. The Expert Advisor runs on the chart that opens in accordance with the Symbol and Period parameters. If the Symbol parameter is not set, no additional chart will be opened in the platform. The Expert Advisor will run on the first chart of the current [profile (#profiles)](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md#profiles) in this case. If the current profile has no charts, the Expert Advisor will not be started. If the Expert parameter is not set, no Expert Advisors will be started.
  * Symbol — the symbol of the [chart](../../Price-Charts-Technical-and-Fundamental-Analysis/View-and-Configure-Charts.md) that opens straight after the platform start. An Expert Advisor or a script will be added to this chart. No information about this additional chart will be saved as the platform is closed. During the next start of the platform without the configuration file, this chart will not be opened. If this parameter is not set, no additional chart will be opened.
  * Period — the [timeframe (#operations)](../../Price-Charts-Technical-and-Fundamental-Analysis/View-and-Configure-Charts.md#operations) of the chart, to which an Expert Advisor or a script will be added (any of the 21 periods available in the platform). If the parameter is not set, default H1 is used.
  * Template — the name of the [template](../../Price-Charts-Technical-and-Fundamental-Analysis/Additional-Features/Templates-and-Profiles.md) to be applied to the chart.
  * ExpertParameters — the name of the file that contains Expert Advisor [parameters (#run)](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md#run). The file must be located in the folder MQL5\presets of the [platform data directory](Files-and-Folders.md). If this parameter is not set, default settings will be used.
  * Script — the name of the [script (#type)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#type) that opens automatically when you start the platform. Scripts are run by the same rules as Expert Advisor.
  * ScriptParameters — the name of the file that contains script [parameters (#run)](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md#run). The file must be located in the folder MQL5\presets of the [platform data directory](Files-and-Folders.md). If this parameter is not set, default settings will be used.


  * ShutdownTerminal — enable/disable trading platform shutdown upon completion of script operation (0 — disable, 1 — enable). If this parameter is not set, the value "0" is used (shutdown disabled). The parameter is used for scripts only, other program types are not supported.



<a id="tester"></a>
### [Tester] (#tester)

Parameters of [testing](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md) that starts automatically when you run the platform:

  * Expert — the file name of the Expert Advisor that will automatically run in the testing (optimization) mode. If this parameter is not present, testing will not run.
  * ExpertParameters — the name of the file that contains Expert Advisor [parameters (#run)](../../Algorithmic-Trading-Trading-Robots/Expert-Advisors-and-Custom-Indicators.md#run). This file must be located in the MQL5\Profiles\Tester folder of the platform installation directory.
  * Symbol — the name of the symbol that will be used as the [main testing symbol (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings). If this parameter is not added, the last selected symbol in the tester is used.
  * Period — testing chart period (any of the 21 periods available in the platform). If the parameter is not set, default H1 is used.
  * Login — this parameter communicates to the Expert Advisor the value of an account, on which testing is allegedly performed. The need for this parameter is set in the source [MQL5 code (#mql5)](../../Algorithmic-Trading-Trading-Robots/How-to-Create-an-Expert-Advisor-or-an-Indicator.md#mql5) of the Expert Advisor (in the AccountInfoInteger function).
  * Model — [tick generation mode (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) (0 — "Every tick", 1 — "1 minute OHLC", 2 — "Open price only", 3 — "Math calculations", 4 — "Every tick based on real ticks"). If this parameter is not specified, Every Tick mode is used.
  * ExecutionMode — trading mode emulated by the strategy tester (0 — normal, -1 — with a random delay in the execution of trading orders, >0 — trade execution delay in milliseconds, it cannot exceed 600 000).
  * Optimization — enable/disable [optimization](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md), its type (0 — optimization disabled, 1 — "Slow complete algorithm", 2 — "Fast genetic based algorithm", 3 — "All symbols selected in Market Watch").
  * OptimizationCriterion — [optimization criterion (#criterion)](../../Algorithmic-Trading-Trading-Robots/Optimization-Types.md#criterion): (0 — the maximum balance value, 1 — the maximum value of product of the balance and profitability, 2 — the product of the balance and expected payoff, 3 — the maximum value of the expression (100% - Drawdown)*Balance, 4 — the product of the balance and the recovery factor, 5 — the product of the balance and the Sharpe Ratio, 6 — a custom optimization criterion received from the OnTester() function in the Expert Advisor), 7 — the maximum of complex criterion.
  * FromDate — starting date of the [testing range (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) in format YYYY.MM.DD. If this parameter is not set, the date from the corresponding field of the strategy tester will be used.
  * ToDate — end date of the [testing range (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) in format YYYY.MM.DD. If this parameter is not set, the date from the corresponding field of the strategy tester will be used.
  * ForwardMode — [forward testing (#forward)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#forward) mode (0 — off, 1 — 1/2 of the testing period, 2 — 1/3 of the testing period, 3 — 1/4 of the testing period, 4 — custom interval specified using the ForwardDate parameter).
  * ForwardDate — starting date of forward testing in the format YYYY.MM.DD. The parameter is valid only if ForwardMode=4.
  * Report — the name of the file to save the report on [testing (#result)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#result) or [optimization (#result)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#result) results. The file is created in the trading platform directory. You can specify a path to save the file, relative to this directory, for example, \reports\tester.htm. The subdirectory where the report is saved should exist. If no extension is specified in the file name, the ".htm" extension is automatically used for testing reports, and ".xml" is used for optimization reports. If this parameter is not set, the testing report will not be saved as a file. If forward testing is enabled, its results will be saved in a separate file with the ".forward" suffix. For example, tester.forward.htm.
  * ReplaceReport — enable/disable overwriting of the report file (0 — disable, 1 — enable). If overwriting is forbidden and a file with the same name already exists, a number in square brackets will be added to the file name. For example, tester[1].htm. If this parameter is not set, default 0 is used (overwriting is not allowed).
  * ShutdownTerminal — enable/disable platform shutdown after completion of testing (0 — disable, 1 — enable). If this parameter is not set, the "0" value is used (shutdown disabled). If the testing/optimization process is manually stopped by a user, the value of this parameter is automatically reset to 0.
  * Deposit — initial deposit for testing optimization. The amount is specified in the account deposit currency. If the parameter is not specified, a value from the appropriate field of the [strategy tester (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) is used.
  * Currency — deposit currency for testing/optimization purposes. Specified as a three-letter name, e.g. EUR, USD, CHF etc. Please note that cross rates for converting profit and margin to the specified deposit currency must be available on the account, to ensure proper testing. If the parameter is not specified, a value from the appropriate field of the [strategy tester (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) is used.
  * Leverage — leverage for testing/optimization. For example, 1:100. If the parameter is not specified, a leverage from the appropriate field of the [strategy tester (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) is used.
  * UseLocal — enable/disable the use of [local agents (#agents)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#agents) for testing and optimization (0 — disable, 1 — enable). If the parameter is not specified, current platform settings are used.
  * UseRemote — enable/disable use of [remote agents (#farm)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#farm) for testing and optimization (0 — disable, 1 — enable). If the parameter is not specified, current platform settings are used.
  * UseCloud — enable/disable use of agents from the [MQL5 Cloud Network (#cloud)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#cloud) (0 — disable, 1 — enable). If the parameter is not specified, current platform settings are used.
  * Visual — enable (1) or disable (0) the visual test mode. If the parameter is not specified, the current setting is used.
  * Port — the port, on which the [local testing agent (#agents)](../../Algorithmic-Trading-Trading-Robots/Strategy-Optimization.md#agents) is running. The port should be specified for the parallel start of testing on different agents. For example, you can run parallel tests of the same Expert Advisor with different parameters. During a single test port can be omitted.



  * [Input parameters (#inputs)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#inputs) from the file specified in ExpertParameters are used for testing/optimization.
  * If the ExpertParameters setup is not available, [parameters (#inputs)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#inputs) from the file Expert_name.set located in [platform_folder]\MQL5\Profiles\Tester are used. The last specified set of input parameters of an Expert Advisor is automatically saved in this file.
  * If there is no such file, then the default parameters specified in the Expert Advisor code are used for testing. Optimization is not possible.
  * To create or edit the set of parameters, select the Expert Advisor on the [Settings (#settings)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#settings) tab of the strategy tester, and specify input parameters and their modification range on the [corresponding tab (#inputs)](../../Algorithmic-Trading-Trading-Robots/Strategy-Testing.md#inputs).

  
---  
  
<a id="example-of-a-configuration-file"></a>
### Example of a Configuration File (#example-of-a-configuration-file)

[Common] Login=1000575 ProxyEnable=0 ProxyType=0 ProxyAddress=192.168.0.1:3128 ProxyLogin=10 ProxyPassword=10 KeepPrivate=1 NewsEnable=1 CertInstall=1 [Charts] ProfileLast=Euro MaxBars=50000 PrintColor=0 SaveDeleted=1 [Experts] AllowLiveTrading=0 AllowDllImport=0 Enabled=1 Account=0 Profile=0 [Objects] ShowPropertiesOnCreate=0 SelectOneClick=0 MagnetSens=10 ;+------------------------------------------------------------------------------+ ;| Running an EA and/or script on the specified chart at the platform start | ;+------------------------------------------------------------------------------+ [StartUp] ;--- The Expert Advisor is located in platform_data_directory\MQL5\Experts\Examples\MACD\ Expert=Examples\MACD\MACD Sample ;--- EA start parameters are available in platform_data_directory\MQL5\Presets\ ExpertParameters=MACD Sample.set ;--- The script is located in platform_data_directory\MQL5\Scripts\Examples\ObjectSphere\ Script=Examples\ObjectSphere\SphereSample ;--- Symbol chart, which will be opened when you start the platform, and EA and/or script will run on it Symbol=EURUSD ;--- Chart timeframe, which will be opened when you start the platform, and EA and/or script will run on it Period=M1 ;--- The template to apply to a chart is located in platform_installation_directory\Profiles\Templates Template=macd.tpl ;--- Set automatic platform shutdown upon completion of script operation ShutdownTerminal=1 ;+------------------------------------------------------------------------------+ ;| Start Expert Advisor testing or optimization | ;+------------------------------------------------------------------------------+ [Tester] ;--- The Expert Advisor is located in platform_data_directory\MQL5\Experts\Examples\MACD\ Expert=Examples\MACD\MACD Sample ;--- The Expert Advisor parameters are available in platform_installatoin_directory\MQL5\Profiles\Tester\ ExpertParameters=macd sample.set ;--- The symbol for testing/optimization Symbol=EURUSD ;--- The timeframe for testing/optimization Period=M1 ;--- Emulated account number Login=123456 ;--- Initial deposit Deposit=10000 ;--- Leverage for testing Leverage=1:100 ;--- The "All Ticks" mode Model=0 ;--- Execution of trade orders with a random delay ExecutionMode=1 ;--- Genetic optimization Optimization=2 ;--- Optimization criterion - Maximum balance value OptimizationCriterion=0 ;--- Dates of beginning and end of the testing range FromDate=2011.01.01 ToDate=2011.04.01 ;--- Custom mode of forward testing ForwardMode=4 ;--- Start date of forward testing ForwardDate=2011.03.01 ;--- A file with a report will be saved to the folder platform_installation_directory Report=test_macd ;--- If the specified report already exists, it will be overwritten ReplaceReport=1 ;--- Set automatic platform shutdown upon completion of testing/optimization ShutdownTerminal=1  
---
