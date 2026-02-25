[🏠 Document Start](../README.md) / [Algorithmic Trading, Trading Robots](README.md) / Testing Features

[Previous](Strategy-Optimization.md) | [Next](Testing-Report.md)

<a id="testing-features"></a>
# Testing Features (#testing-features)

The idea of automated trading is attractive because a trading robot can work non-stop for 24 hours a day and seven days a week. The robot is totally free from fatigue, doubt, fear, and psychological problems. You only need to clearly formalize trading rules and implement them in algorithms, and the robot is ready to work tirelessly. But first, you must make sure that the following two important conditions are met:

  * The Expert Advisor performs trading operations in accordance with the rules of the trading system;
  * The trading strategy implemented in the EA shows profit during backtests.



All these questions can be answered using the built-in [strategy tester](Strategy-Testing.md) of the trading platform.

<a id="order-triggering-and-execution"></a>
## Order Triggering and Execution (#order-triggering-and-execution)

For non-exchange instruments, triggering of all kinds of pending orders and SL/TP is performed by Bid and Ask prices. Execution is performed by the current Bid and Ask market prices at the moment of triggering.

For exchange instruments, charts are plotted and stop orders are triggered by last performed deal prices (Last). Limit orders are triggered by Bid and Ask prices. Limit orders are executed at the price specified in the order (without a slippage), while orders of other types are executed at the current Bid and Ask market prices (slippage is possible).

Let's use Si-6.16 as an example. At the current prices of Bid=72570, Ask=72572, and Last=72552, a Buy Stop order with the execution price of 72580 is placed. We have received the new prices in the price flow:

  * Bid=72588
  * Ask=72590
  * Last=72580



For exchange instruments, the Last price is used as a trigger activating stop orders. Therefore, occurrence of Last=72580 in the flow resulted in Buy Stop order activation. The order is to be executed (market buy operation) at the current market price Ask=72590.

![Triggering and execution of a Buy Stop order for an exchange instrument](images/tester_execution_example.png)

> In the "Open prices only" and "1 minute OHLC" [testing modes (#tick-mode)](Real-and-Generated-Ticks.md#tick-mode), pending orders, as well as SL and TP are executed at the prices specified in the orders. The algorithm of execution at market prices used in accurate modes (every tick and real ticks), is not suitable for less accurate modes. In some modes intermediate ticks are not generated, therefore the difference between the requested order price and the current price (Open or OHLC) can be significant. Execution of orders at the requested price in the "Open prices only" and "1 minute OHLC" provides more accurate testing results.

<a id="creating-bars"></a>
## Creating Bars (#creating-bars)

In the strategy tester, exchange symbol bars are created only by ticks having non-zero Last price. Bid and Ask prices may arrive, indicators are calculated, but bars are not formed. There are no zero Last prices in "Every tick" mode. Therefore, a bar is changed by each incoming tick.

<a id="spread"></a>
## Spread Simulation (#spread)

The difference between the Bid and the Ask prices is called the spread. During testing, the spread is not modeled but is taken from historical data. If the historical spread is less than or equal to zero, then the last known (at the moment of generation) spread is used.

In the Strategy Tester, the spread is always considered floating.

<a id="globals"></a>
## Global Variables of the Trading Platform (#globals)

Global variables of the trading are also emulated during testing, but they are not related to real [global variables of the platform](Global-Variables.md), which can be viewed by pressing F3. It means that all operations with the global variables of the platform are performed outside the trading platform during testing (on the testing agent).

<a id="history"></a>
## History Download during Testing (#history)

The platform synchronizes and downloads the history of a symbol to be tested from the trade server before starting the testing process. During the first time, the platform downloads all available history data of a symbol and does not request it later. Further only new data are downloaded.

A testing agent receives the history of a symbol to be tested from the trading platform right after the start of testing. If data of other instruments are used during testing (for example, it is a multicurrency Expert Advisor), the testing agent requests the required history from the trading platform during the first call of such data. If historical data are available in the platform, they are immediately transferred to the testing agent. If data are not available, the platform requests and downloads them from the server, and then passes to the testing agent.

Data of additional instruments are also required for calculating cross-rates for trade operations. For example, when testing a strategy on EURCHF with the deposit currency in USD, prior to processing the first trading operation, the testing agent requests the history data of EURUSD and USDCHF from the trading platform, although the strategy does not contain direct call of these symbols.

Additional trading history download can be started when calling certain functions from an MQL5 application:

History download | No history download  
---|---  
When calling SymbolInfoDouble with the following parameters:

  * SYMBOL_BID
  * SYMBOL_BIDHIGH
  * SYMBOL_BIDLOW
  * SYMBOL_ASK
  * SYMBOL_ASKHIGH
  * SYMBOL_ASKLOW
  * SYMBOL_LAST
  * SYMBOL_LASTHIGH
  * SYMBOL_LASTLOW
  * SYMBOL_TRADE_TICK_VALUE
  * SYMBOL_TRADE_TICK_VALUE_PROFIT
  * SYMBOL_TRADE_TICK_VALUE_LOSS

When calling SymbolInfoInteger with the following parameters:

  * SYMBOL_VOLUME
  * SYMBOL_VOLUMEHIGH
  * SYMBOL_VOLUMELOW
  * SYMBOL_TIME
  * SYMBOL_SPREAD

When calling SymbolInfoTick | When calling:

  * SymbolInfoString
  * SymbolName
  * SymbolSelect
  * SymbolInfoMarginRate
  * SymbolInfoSessionQuote
  * SymbolInfoSessionTrade
  * Other functions not specified here
  * SymbolInfoDouble and SymbolInfoInteger with other parameters not specified in the left column

  
  
Before testing a multi-currency strategy, it is recommended to download all the necessary historical data to the trading platform. This will help to avoid delays in testing/optimization associated with download of the required data. You can download history, for example, by opening the appropriate charts and scrolling them to the history beginning.

The testing agents receive the history data from the platform in a compressed form. During a re-testing, the tester does not download data from the platform, because it has data from the previous tester run.

  * The platform downloads history data from the trading server only once, when the agent accesses the platform for the first time to download the history of the tested symbol. The history is downloaded in a packed form to reduce the traffic.
  * Ticks are not sent over the network, they are generated on testing agents.

  
---  
  
<a id="multicurrency"></a>
## Multi-Currency Testing (#multicurrency)

The Strategy Tester allows backtesting strategies that trade multiple symbols. Such EAs are conventionally referred to as multi-currency Expert Advisors, since originally, in the previous platforms, testing was performed only for a single symbol. In the platform tester, we can model trading for all the available instruments.

The tester automatically downloads the history of required symbols from the trading platform (not from the trade server!) during the first call of the symbol data.

The testing agent downloads only the missing history data and a little more to provide the required data for the indicator calculation at the beginning of testing. For the timeframes D1 and below, the minimum volume of the downloaded history is one year. Thus, for a one-month testing on an interval of 2010.11.01-2010.12.01 with a period of M15 (each bar is equal to 15 minutes), the agent requests the symbol history for the entire year of 2010 from the platform. For the one-week timeframe, the agent requests a history of 100 bars, which is about two years (a year has 52 weeks). For testing on a monthly timeframe, the agent requests the history for 8 years (12 months * 8 years = 96 months).

If the required bars are not available for whatever reason, the starting date of testing is automatically shifted from the past to the present to provide the necessary amount of bars.

[Market Watch](../Trading-Operations/Market-Watch.md) is also emulated during testing. By default, only one symbol is available in the tester's Market Watch at the beginning of testing - the symbol, on which the testing is running. All the required symbols being accessed are automatically connected to the Market Watch of the Strategy Tester (not the platform!).

Before you start testing of a multi-currency Expert Advisor, select symbols required for testing in the Market Watch of the trading platform and download the required data. During the first call of a "foreign" symbol, its history is automatically synchronized between the testing agent and the trading platform. A "foreign" symbol is the one that differs from the symbol, on which testing is running.  
---  
  
When such a symbol is called for the first time, the testing process is paused and the symbol/period history is downloaded from the platform to the testing agent. The generation of a tick sequence for this symbol is enabled at the same time.

An individual tick sequence is generated for each symbol according to the selected tick generation mode.

It means multi-currency testing in the trading platform does not require any extra effort. You only need to open the charts of the appropriate symbols in the platform. The history of all the required symbols is automatically downloaded from the trading server, provided the data are available.

<a id="time"></a>
## Time Simulation in the Strategy Tester (#time)

During testing, the local time is always equal to the server time. The server time always corresponds to the GMT time.

The GMT, the local and the server time are equal in the Strategy Tester deliberately in case there is no connection to the server. Testing results should always be the same, regardless of whether the server connection is established or not. Information about the server time is not stored locally, and is taken from the server.

<a id="objects"></a>
## Graphical Objects during Testing (#objects)

During testing/optimization graphical objects are not plotted. Thus, when referring to the properties of a created object during testing/optimization, an Expert Advisor receives zero values.

This limitation does not apply to testing in visual mode.  
---  
  
<a id="bar-synchro"></a>
## Synchronization of Bars in "Open prices only" (#bar-synchro)

The Strategy Tester allows testing the so-called "multi-currency" Expert Advisors. A multi-currency EA is an EA that trades two or more symbols.

Testing of strategies trading multiple symbols imposes a few additional technical requirements on the tester:

  * generation of ticks for these symbols;
  * calculation of indicator values for these symbols;
  * calculation of margin requirements for these symbols;
  * synchronization of generated tick sequences for all trading symbols.



The Strategy Tester generates and plays a tick sequence for each instrument in accordance with the selected trading mode. [A new bar](https://www.mql5.com/en/articles/159 "Article "New Bar" Event Handler") for each symbol is opened regardless of how the bar has opened on another symbol. This means that during multi-currency testing, a situation may occur (and often does), when a new bar has already opened for one instrument, and there is no new bar for the other one. It's all like with realtime quotes.

This authentic history simulation in the tester does not cause any problems as long as the "Every tick" and "1 minute OHLC" testing modes are used. For these modes, the number of ticks generated on one candlestick is enough to be able to wait for the synchronization of bars from different symbols. But how do we test multi-currency strategies in the "Open prices only" mode, where the synchronization of bars on trading instruments is required? In this mode, the EA is only called on one tick, which corresponds to the bar open time.

Example: We are testing an Expert Advisor on EURUSD, and a new one-hour EURUSD candlestick has opened. We can easily recognize this fact - in the "Open prices only" mode, the event of a new tick arrival corresponds to the moment of bar opening. But there is no guarantee that a new candlestick has opened on GBPUSD, which is used in the EA.

<a id="agents"></a>
## Testing Agents (#agents)

Testing in the platform is performed using [testing agents (#agents)](Strategy-Optimization.md#agents). Local agents are created and enabled automatically. The number of local agents is equal to the number of logical cores.

Every testing agent has its own copy of [global variables](Global-Variables.md), which is not related to the platform. The platform is a manager, which distributes tasks to local and remote agents. Once a task of Expert Advisor testing with specified parameters is complete, the agent returns the results to the platform. Only one agent is used for a single test.

The agent stores the history received from the platform in separate folders based on the symbol name, so the history of EURUSD is stored in a folder named EURUSD. In addition, the history of the instruments is separated based on their sources. The structure for storing the history is as follows:

tester_catalog\Agent-IPaddress-Port\bases\name_source\history\symbol_name  
---  
  
For example, EURUSD history downloaded from the MetaQuotes-Demo server can be stored in the folder tester_catalog\Agent-127.0.0.1-3000\bases\MetaQuotes-Demo\EURUSD.

A local agent enters a standby mode after finishing testing and waits for the next task for another 5 minutes, so as not to waste time on launching for the next call. Only after the waiting period, the local agent shuts down and unloads from the CPU memory.

If testing is interrupted by a user (button "Cancel" pressed) or the trading platform is closed, all local agents immediately stop operation and are unloaded from the memory.

<a id="data"></a>
## Data Exchange between the Platform and the Agent (#data)

When you start a test, the platform prepares multiple blocks of parameter to be sent to an agent:

  * Input parameters for testing (simulation mode, testing interval, instruments, optimization criterion, etc.)
  * The list of symbols selected in the Market Watch
  * The specification of the testing instrument (contract size, minimum stop-level requirements for Stop Loss and Take Profit, etc)
  * The Expert Advisor to be tested and the values of its input parameters
  * Information about additional files (libraries, indicators, data files)



For each block of parameters, a digital fingerprint in the form of MD5 hash is created and sent to an agent. MD5 hash is unique for each set, its volume is much smaller than the amount of information used for its calculation.

The agent receives hashes and compares them with the sets it stores. If the fingerprint of the given parameter block is not available on the agent, or the received hash differs from the existing one, the agent requests the block of parameters. This reduces the traffic between the platform and the agent.

After testing, the agent returns to the platform test run results displayed in tabs "Test Results" and "Optimization Results": the profit, the number of deals, Sharpe ratio, the result of the OnTester() function, etc.

During optimizing, the platform distributes testing tasks to agents in small packages, each package containing several tasks (each task means a single test with a set of input parameters). This reduces the time of data exchange between the platform and the agent.

Agents never record EX5 files received from the platform (EA, indicators, libraries, etc.) to a hard disk for security reasons, so that a computer with a running agent could not use the received data. All other files, including DLL, are recorded in a sandbox. You cannot test Expert Advisors with DLL calls on remote agents.

Testing results are added by the platform to a special cache of results from which they can be easily accessed if needed. For each set of parameters, the platform searches the result cache for available results of previous runs in order to avoid re-runs. If no result is found for a set of parameters, the agent is given a task to run testing.

Traffic between the platform and agents is encrypted.

Ticks are not sent over the network, they are generated on testing agents.  
---  
  
<a id="common-folder"></a>
## Using the Shared Folder of Trading Platforms (#common-folder)

All testing agents are isolated from each other and from the trading platform: each agent has its own folder in which its logs are recorded. In addition, all the agent's file operations during testing are performed in the folder agent_name/MQL5/Files. However, you can implement the interaction between the local agents and the trading platform using a shared folder of platforms.

<a id="dll"></a>
## Using DLLs (#dll)

To speed up the optimization you can use [remote agents (#farm)](Strategy-Optimization.md#farm) in addition to local ones. In this case, there are some limitations for remote agents. First of all, results of the Print() function, as well as messages about position opening and closing are not recorded to the remote agent logs. A minimum of information is added to log to prevent the computer hard drive from a huge amount of messages of incorrectly operating Expert Advisors.

A second limitation - the use of DLL during Expert Advisor testing is prohibited. DLL calls are absolutely prohibited on remote agents for security reasons. On local agent, DLL calls in tested Expert Advisors are only allowed if "Allow import DLL" permission is enabled.

![Expert Advisors](images/options_ea.png)

When using third-party Expert Advisors (scripts, indicators) that require DLL calls, you should be aware of the risks when allowing this option in the platform settings. Regardless of how the Expert Advisor is used - for testing or for running on a chart.  
---
