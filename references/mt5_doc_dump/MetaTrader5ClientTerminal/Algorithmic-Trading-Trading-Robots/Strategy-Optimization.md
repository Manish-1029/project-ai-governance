[🏠 Document Start](../README.md) / [Algorithmic Trading, Trading Robots](README.md) / Strategy Optimization

[Previous](Strategy-Testing.md) | [Next](Testing-Features.md)

<a id="strategy-optimization"></a>
# Strategy Optimization (#strategy-optimization)

The Strategy Tester allows you to test and optimize trading strategies ([Expert Advisors (#type)](How-to-Create-an-Expert-Advisor-or-an-Indicator.md#type)) before using them for live trading. During testing, an Expert Advisor with initial parameters is once run on history data. During optimization, a trading strategy is run several times with different sets of parameters which allows selecting the most appropriate combination thereof.

The Strategy Tester is a multi-currency tool for testing and optimizing strategies trading multiple financial instruments. The tester automatically processes information of all symbols that are used in the trading strategy, so you do not need to manually specify the list of symbols for testing/optimization.

The Strategy Tester is multi-threaded, thus allowing to use all available computer resources. Testing and optimization are carried out using special computing agents that are installed as services on the user's computer. Agents work independently and allow parallel processing of optimization passes.

An unlimited number of remote agents can be connected to the Strategy Tester. In addition, the Strategy Tester can access the [MQL5 Cloud Network](../MQL5-Cloud-Network/README.md). It brings together thousands of agents around the world, and this computational power is available to any user of the trading platform.

In addition to Expert Advisor testing and optimization, you can use the Strategy Tester to test the operation of custom indicators in the [visual mode](Testing-Visualization.md). This feature allows to easily test the operation of demo versions of indicators downloaded from the [Market](../Market-App-Store/README.md).

<a id="optimize"></a>
## How to Optimize (#optimize)

Optimization means multiple runs of an Expert Advisor using history data with different sets of parameters, aimed at finding their best combination. During multiple runs, different combinations of the input parameters of an Expert Advisor are tested to find the best ones.

[![Watch the video: How to test Expert Advisors and Indicators before purchase](images/video_market_test.png)](https://www.metatrader5.com/video/1/ouEh29q3QJ4/video.mp4 "Watch the video: How to test Expert Advisors and Indicators before purchase") | Watch the video: How to test Expert Advisors and Indicators before purchase Watch the video to learn how to test a trading robot before you purchase it from the Market. Every product on the Market is provided with a free demo version, which can be tested in the Strategy Tester. Please watch the video for further details.  
---|---  
  
<a id="start-page"></a>
### Quick Selection of Optimization Tasks (#start-page)

After tester launch, instead of multiple settings the user sees a list of standard tasks, by selecting which they can quickly start testing. This will be especially useful for users without previous experience.

Some of the major strategy testing and optimization tasks are presented in the start page. In addition, one of the previously performed tasks can be restarted from this page. If you have run a lot of tasks and they do not fit into the start page, use the search bar. You can find a test by any parameter: program name, symbol, timeframe, modeling mode, etc.

![Select one of the popular tasks on the start page for a quick testing start.](images/tester_start_page.png)

After selecting a task, the user proceeds to further testing parameters setup: selection of an Expert Advisor, symbol, testing period, etc. All irrelevant parameters which are not required for the selected tasks are hidden from the setup page. For example, if mathematical calculations are selected, only two parameters should be specified: selection of a program to be tested and the optimization mode. Testing period, delay and tick generation settings will be hidden.

All available optimization options will be explained below.

<a id="ea"></a>
### How to select a trading robot for testing (#ea)

Click "![Test](images/test_icon.png) Test" in the context menu of an Expert Advisor in the [Navigator](../Getting-Started/User-Interface.md) window. 

![How to select a trading robot for testing](images/test_select_ea.png)

After that the Expert Advisor is selected in the Strategy Tester.

<a id="mw"></a>
### Enable required symbols in Market Watch for multi-currency Expert Advisors (#mw)

The Strategy Tester allows backtesting strategies that trade multiple symbols. Such trading robots are conventionally called multicurrency Expert Advisors.

The tester automatically downloads the history of required symbols from the trading platform (not from the trade server!) during the first call of the symbol data. Only the missing price history data are additionally downloaded from the trading server.

Before you start optimization of a multi-currency Expert Advisor, enable the symbols required for testing in the Market Watch. In the context menu, click "![Symbols](images/symbols_icon.png) Symbols" and enable the required instruments.

![Enable required symbols in Market Watch for multi-currency Expert Advisors](images/test_show_symbols.png)

<a id="settings"></a>
### Specifying Optimization Settings (#settings)

Before you start optimization, select the financial instrument to test the trading robot operation on, the period and the mode.

![Selecting testing parameters](images/tester_settings_optimization.png)

<a id="symbol-and-period"></a>
### Symbol and period (#symbol-and-period)

Select the main chart for testing and optimization. Symbol selection is required to provide the triggering of OnTick() events contained in Expert Advisors. Also, the selected symbol and period affect special functions in the Expert Advisor code that use current chart parameters (for example, Symbol() and Period()). In other words, the chart to which the Expert Advisor is attached should be selected here.

<a id="date"></a>
### Date (#date)

Select testing and optimization period. You can select one of predefined periods or set a custom time interval. To set a custom period, enter the start and end dates in the appropriate fields to the right.

The specific feature of the tester is that it additionally downloads some data preceding the specified period (to form no less than 100 bars). This is required for a more accurate testing and optimization. For example, if you test on a one-week timeframe, two additional years are downloaded.

If there is not enough history data for forming additional 100 bars (it is especially significant for the monthly and weekly timeframes), for example, when specifying a start of testing close to the start of existing history data, then the start date of testing will be automatically shifted. An appropriate message is added to the Strategy Tester [journal (#result)](Strategy-Testing.md#result).

<a id="forward"></a>
### Forward (#forward)

This option enables the verification of optimization results using a preset forward period in an effort to avoid overfitting in optimization time intervals. During forward optimization, the period set in the Date field is divided into two parts in accordance with the selected forward period (a half, one third, one fourth or a custom period when you specify the forward testings tart date).

Expert Advisor optimization is performed using the data of the first period. After that 10% (in the full search) or 25% (in the genetic algorithm) of best runs are selected and tested on the forward period. The results of the best optimization runs on both periods can be compared on tabs Optimization Results and Forward Results.

<a id="execution"></a>
### Execution (#execution)

Strategy tester enabled the emulation of network delays during an Expert Advisor operation in order to provide close-to-real conditions for testing. A certain time delay is inserted between placing a trade request and its execution in the strategy tester. From the moment of request sending till its execution the price can change. This allows users to evaluate how trade processing speed affects the trading results.

In the [instant execution (#execution-type)](../Trading-Operations/Basic-Principles.md#execution-type) mode, users can additionally check the EA's response to a requote from the trade server. If the difference between requested and execution prices exceeds the [deviation (#deviation)](../Trading-Operations/Executing-Trades.md#deviation) value specified in the order, the EA receives a requote.

Please note that delays work only for trades performed by an EA (placing [orders (#order-type)](../Trading-Operations/Basic-Principles.md#order-type), changing [stop levels (#position-modify)](../Trading-Operations/Executing-Trades.md#position-modify), etc.). For example, if an EA uses pending orders, delays are only applied to order placing but not to order execution (in real conditions, execution occurs on the server without a network delay).

**No Delay**

In this mode, all orders are executed at requested prices without requotes. The mode is used to check how an EA would perform in "ideal" conditions.

**Random Delay**

The Random Delay mode allows testing an Expert Advisor in conditions maximally close to real ones. The delay value is generated as follows: a number from 0 to 9 is selected randomly - this is the number of seconds for a delay; if a selected number is equal to 9, another number from the same range is selected randomly and added to the first one.

Thus, the possibility of a delay for 0-8 seconds is 90%, possibility of a 9-18 second delay is 10%.

**Fixed Delay**

You can select one of the predefined delay values or set a custom one. The platform measures the ping to the trade server and allows you to set that value as a delay in the tester so that you are able to test a robot in the conditions that are as close to the real ones as possible.

<a id="tick-generation-mode"></a>
### Tick generation mode (#tick-generation-mode)

Select one of the tick generation modes:

  * Every tick â the most accurate but the slowest mode. All ticks are simulated in this mode.
  * Every tick based on real ticks provides conditions close to real ones. Testing is performed using [real ticks (#real)](Real-and-Generated-Ticks.md#real) of financial instruments, accumulated by brokers. No simulation is performed. Due to a large size of tick data, downloading them from a broker's server during the first testing run may take a long time.
  * 1 minute OHLC â in this mode only 4 prices (Open, High, Low and Close) of each minute bar are emulated.
  * Open prices only â in this mode OHLC prices are also modeled, however only the open price is used for testing/optimization.
  * Math calculations â in this mode the tester does not download history data and information on symbols, as well as does not generate ticks. Only functions OnInit(), OnTester() and OnDeinit() are called. Thus a tester can be used for various mathematical calculations where the selection of parameters is required.



For more information about tick generation, please read the [appropriate section (#tick-mode)](Real-and-Generated-Ticks.md#tick-mode).

Profit calculation in pips can speed up the testing process while there is no need to recalculate profit to deposit currency using conversion rates (and thus there is no need to download the appropriate price history). Swap and commission calculations are eliminated in this mode.

Please note that margin control is not performed in this mode. You should only use it for quick and rough strategy estimation and then check the obtained results using more accurate modes.

<a id="initial-deposit-and-leverage"></a>
### Initial deposit and leverage (#initial-deposit-and-leverage)

Specify the amount of the initial deposit used for testing and optimization. The deposit currency of the currently [connected](../Getting-Started/Connect-to-an-Account.md) account is used by default, but you can specify any other currency. Please note that cross rates for converting profit and margin to the specified deposit currency must be available on the account, to ensure proper testing. Only symbols with the "Forex" or "Forex No Leverage" calculation type can be used as cross rates.

Next select the leverage for testing and optimization. The leverage influences [the amount of funds reserved on the account as the margin on positions and orders](../Trading-Operations/For-Advanced-Users/Margin-Calculation-Retail-Forex-Futures.md).

<a id="quick-jump-to-ea-editing"></a>
### Quick jump to EA editing (#quick-jump-to-ea-editing)

If you have the source code of the selected Expert Advisor, you can click this button to switch to its editing in [MetaEditor (#metaeditor)](How-to-Create-an-Expert-Advisor-or-an-Indicator.md#metaeditor).

<a id="managing-optimization-settings"></a>
### Managing optimization settings (#managing-optimization-settings)

Use this menu to manage tester settings: save sets of settings for various Expert Advisors in ini files and access them in a couple of clicks later. Current optimization settings can also be copied to the clipboard by pressing Ctrl+C. You can edit them in your preferred text editor, then copy and upload them to the tester using Ctrl+V.

From the same menu, you can quickly select the last used programs, last chart settings and testing periods.

Furthermore, you can quickly access any of the previous optimization results, as well as the settings with which the result was achieved.

<a id="custom-symbol-settings-for-testing"></a>
### Custom symbol settings for testing (#custom-symbol-settings-for-testing)

You can change the settings of the main trading instrument used for testing/optimization. Almost all specification parameters can be overwritten: volumes, trading modes, margin requirements, execution mode and other settings.

<a id="advanced-testing-settings"></a>
### Advanced testing settings (#advanced-testing-settings)

Set your own trading account parameters when testing strategies, such as trading limits, margin settings and commissions. This option enables the simulation of different trading conditions offered by brokers.

<a id="optimization"></a>
### Optimization (#optimization)

Select the optimization mode:

  * Slow complete algorithm â testing all possible combinations of selected input parameters.
  * Fast genetic algorithm â search for the best values of input parameters based on the genetic algorithm.
  * All symbols selected in Market Watch â testing of the same set of input parameters with different trading instruments. 



For more details about the available types please read the [appropriate section](Optimization-Types.md).

<a id="optimization-criterion"></a>
### Optimization criterion (#optimization-criterion)

[Optimization criterion (#criterion)](Optimization-Types.md#criterion) is a certain factor, which value defines the quality of a tested set of parameters. The higher the value of the optimization criterion, the better the testing result with the given set of parameters. It is only used for genetic optimization.

  * Note that symbol specification does not mean that the tester will use only these history data. The tester automatically downloads information on all the symbols used in the Expert Advisor.
  * Before testing/optimization, all the available price data of the symbol on the main chart are automatically downloaded from the server. It may take quite a long time if the internet connection is slow.
  * Downloading of all data is performed once, only the missing information is downloaded during the next starts.
  * Only the symbols that are currently selected in the [Market Watch](../Trading-Operations/Market-Watch.md) are available for testing/optimization.


  * The price data of all necessary symbols are automatically downloaded from the server during testing and optimization.
  * Testing starts and ends at 00hr.00m.00s. of the specified dates. Thus the start date of testing/optimization is included in the testing period, while the end date is not included. Testing ends on the last tick of the previous date. Also you cannot specify the end date, which is greater than the current one. In such case, the testing anyway will be performed to the current date (not including it).

  
---  
  
The quick optimization based on the genetic algorithm is enabled by selecting [optimization criteria (#criterion)](Optimization-Types.md#criterion) in the field located to the right. This field sets the parameter, based on which the most successful Expert Advisor runs are selected. The larger the value of a selected parameter, the better the result.

After setting all the parameters click "Start". This launches the process of testing and optimization.

  * The settings of the strategy tester are memorized as testing/optimization is started.
  * In case of a regular optimization stop (when you press the Stop button) all the previously calculated runs are saved. When the optimization process is resumed, it continues from the last calculated run.

  
---  
  
<a id="inputs"></a>
### Selection of Input Parameters (#inputs)

Input parameters allow you to control the behavior of the Expert Advisor, adapting it to different market conditions and a specific financial instrument. For example, you can explore the Expert Advisor performance with different [Stop Loss (#stop-loss)](../Trading-Operations/Basic-Principles.md#stop-loss) and [Take Profit (#take-profit)](../Trading-Operations/Basic-Principles.md#take-profit) values, different periods of the moving average used for market analysis and decision-making, etc.

Optimization is testing different values ​​and combinations of input parameters to obtain the best result.

![Selection of input parameters to optimize](images/optimization_inputs.png)

To enable the optimization of a parameter, mark the appropriate checkbox. Next set the start and end of the range of values, as well as the step for testing. You can select one or more parameters. The total number of possible combinations is displayed beneath the list of parameters.

Parameter sets. You can at any time return to the current settings of your MQL5 program by saving a set of its parameters using a context menu:

  * To save the parameters as a set-file on your computer, click "Save". These files can be moved between platforms on different computers or sent to other users.
  * To save parameters for future use in the current platform, click "Save Version". These saved presets will be available then in the "Load Version" sub-menu. They can be applied at any time by selecting an appropriate version from the list.



<a id="extended-settings"></a>
### Advanced Testing Settings (#extended-settings)

You can specify custom trading account settings during strategy testing, such as trading limits, margin settings and commissions. This option enables the simulation of different trading conditions offered by brokers.

![Advanced testing settings enable the simulation of different trading conditions offered by brokers.](images/tester_extended_settings.png)

Common

In this section, you can set the maximum number of open orders and positions, which can simultaneously exist on the account. Additionally, you can configure sessions during which the program is not allowed to trade.

Margin

The section allows configuration of margin reserving rules and position accounting systems to be used in testing:

![Margin settings](images/tester_extended_settings_margin.png)

[Risk management model](../Trading-Operations/For-Advanced-Users.md): OTC and Exchange, netting or hedging.

When this level is reached, the account switches to the Margin Call state.

When this level is reached, all orders are canceled and all trading positions are closed. These levels can be indicated in money and in percentage. In the former case, they are determined as the account's Equity value. If "In percent" is selected, levels are defined as the account "Margin level" value (Equity/Margin*100).

The method of accounting for the current floating profit/loss in the free margin calculation is specified here:

  * Do not use unrealized profit/loss â do not include profit/loss of open positions in the calculation.
  * Use unrealized profit/loss â include open positions' profit/loss in the calculation.
  * Use unrealized profit â include only profit.
  * Use unrealized loss â include only loss.



The method of accounting for the trader's daily realized profit/loss in the free margin calculation is specified here:

  * Use daily fixed profit/loss â include in the free margin profit and loss received during a trading day.
  * Use daily fixed loss â include only loss received during the trade day. During the day, the obtained profit is accumulated in the special account field ("Blocked"). At the end of the trading day, the accumulated profit is released (reset) and is added to the account balance (included in the free margin).



Release fixed profit at the end of day â this option becomes available only if the option "Use daily fixed loss" is selected. If it is enabled, the accumulated profit will be released (and thus included in the free margin) at the end of the day. Otherwise this profit amount will remain blocked.

Commission

This section provides control over commissions charged on all trading operations:

  * Commission may be single-level and multilevel, i.e. be equal regardless of the deal volume/turnover or can depend on their size.
  * Commission can be charged immediately upon deal execution or at the end of a trading day/month.
  * Separate commissions can be charged depending on deal direction: entry, exit or both operation types.
  * Commission can be charged per lot or deal.
  * Commission can be calculated in money, percentage or points.



To apply commission settings of the current trading account, enable the option "Use predefined commissions".

![Commission settings](images/tester_extended_settings_commission.png)

Enable the option to use current trading account commission settings instead of custom settings specified below.

Specify the name of the symbol for which you are configuring commissions. Several settings can be added for each symbol. Thus, you can set up multi-level commissions that depend on the deal volume or turnover.

Commission can be charged immediately after each trade, or it can be accumulated during the trading day or month and then charged in one operation:

  * Instant â commissions are charged instantly during execution of each deal. The instant commission size is displayed in the Commission field of deals. In the instant mode, only commission in volume can be specified (not in turnover).
  * Daily â the commission amount is accumulated during a day in a special account state field "Blocked". At the end of the day, the accumulated amount is debited from the account in a separate balance operation (a deal of the Daily commission or Daily agent commission type).
  * Monthly â the commission amount is accumulated during the month in a special account state field "Blocked". At the end of the month the accumulated amount is charged from the account with a separate balance operation (a deal of the Monthly commission or Monthly agent commission type).



Also, commission can be charged depending on each deal volume or on daily/monthly turnover. The selected option determines the entity whose volumes are indicated in the "From" and "To" fields: deal or turnover.

  * Volume â commission levels are set based on the volume (amount of lots) of each deal executed in a trading operation. For example, if you set levels as 0 â 10 and 12 â 20, a 15-lot deal will be subject to the second level commission. This option is used in modes Daily, Monthly or Instant.
  * Overturn Money â commission levels are set based on turnover in money over the selected period (day or month). For example, the levels are set as 0 â 500, 501 â 1000, and commission is charged on a monthly basis. The first-level commission will be charged until the total cost of operations exceeds 500 units. As soon as the money turnover exceeds the value of 500, all further trades will be subject to the second-level commission.  
By default, the money turnover is calculated in the deposit currency: the price of each trade is calculated and converted into the deposit currency. For example, the price of Buy 1 lot EURUSD with a contract size of 100,000 is EUR 100,000. If your deposit currency is USD, the position price is converted to EURUSD at the time of the transaction (in this case, it is the deal price).
  * Overturn Volume â commission levels are set based on the volume of trading operations (amount of lots) over the selected period (day or month).



In the daily and monthly mode, commissions are charged for deals in both directions (when opening/increasing a position and when closing a position or part of it). For instant commissions, trade direction can be set manually.

For reversal deals with the in/out type, "In" means that commission is only charged on the volume of the newly opened position, "Out" means commission on the closed volume. The following rules shall apply for Close By deals:

  * No commission is charged on Close By deals when "All" or "In" is selected, since the commission is charged on two original deals. For example, a commission of USD 1 is charged for each deal. When a trader performs an entry Buy 1.00 EURUSD deal and an entry Sell 1.00 EURUSD deal, a commission of 2 USD will be charged. When the 1.00 EURUSD position is closed by the Sell 1.00 EURUSD position, the client will not be charged additional commission.
  * If "Out" is selected, commission on both Close By deals will be charged, and the total commission value will be written to the main exit deal (in which profit/loss is specified). For example, a commission of USD 1 is charged for each deal. When a trader performs an entry Buy 1.00 EURUSD deal and an entry Sell 1.00 EURUSD deal, no commission will be charged. When the 1.00 EURUSD position is closed by the Sell 1.00 EURUSD position, a commission of USD 2 will be charged. A commission of 2 USD will be specified in the first 'out by' deal, and a zero commission will be specified in the second deal.



The minimum deal volume (turnover) from which the commission will be charged. The ranges must not overlap. Otherwise, the commission will be charged for all the ranges, in which the operation falls.

The maximum deal volume (turnover) from which the commission will be charged. The ranges must not overlap.. Otherwise, the commission will be charged for all the ranges, in which the operation falls.

Commission fee amount. Commission units depend on the commission calculation method selected in the Mode field.

Minimum commission amount. Value units depend on the selected calculation mode (in the base currency, group currency, points. etc.). If you do not want to limit the minimum commission amount, set the 0 value.

Maximum commission amount. Value units depend on the selected calculation mode (in the base currency, group currency, points. etc.). The maximum commission value cannot be less than the minimum commission. If you do not want to limit the maximum commission amount, set the 0 value.

Commission fee calculation units:

  * Deposit currency â commission is calculated in the deposit currency specified for the group.
  * Base currency â commission is calculated in the base currency of the traded symbol.
  * Profit currency â commission is calculated in the profit currency of the traded symbol.
  * Margin currency â commission is calculated in the margin requirements currency specified for the traded symbol.
  * Points â commission is calculated in price points of the traded symbol. The point value is calculated as the profit of a position in the same direction, with the volume of 1 lot and the difference between the open and close prices is equal to 1 pip (point).
  * Percents â this calculation method allows charging commission in % of the actual cost of the deal/turnover. The cost is calculated in the base currency of the symbol as the product of its price, contract size and volume in lots (for futures and options symbols: volume in lots * Tick Size / Tick Price). By default, deal/turnover value calculated in the base currency is converted to the deposit currency; then the final commission (the specified percent) is calculated based in the resulting value.



Commission charging type:

  * Per deal â commission will be charged for each conducted deal.
  * Per volume â commissions are charged per lot (volume) of executed deals. Only the executed volume of trade requests is taken into account.



<a id="custom-symbol"></a>
### Custom Testing Symbol Settings (#custom-symbol)

You can overwrite settings of the main trading instrument, for which testing/optimization is performed. Almost all [specification (#specification)](../Trading-Operations/Market-Watch.md#specification) parameters can be overwritten: volumes, trading modes, margin requirements, execution mode and other settings. Thus, if you need to check an Expert Advisor under different conditions, there is no need to create a separate [custom symbol](../Trading-Operations/For-Advanced-Users/Custom-Financial-Instruments.md) and download its history. This can be done by changing standard symbol settings.

![Edit any settings of the main testing symbol to test the strategy in different trading conditions](images/tester_custom_symbol_settings.png)

If the symbol specification is customized, the gear icon and the symbol icon are marked with an asterisk. This shows that custom parameters are used for the current test.

![If the instrument settings have been changed, this instrument is marked with a special icon](images/tester_custom_symbol_settings_modified.png)

<a id="start"></a>
### Optimization Launch (#start)

To start optimization, click "Start" on the "Settings" tab. The optimization progress is displayed to the left.

<a id="result"></a>
## Where to View the Optimization Results (#result)

Detailed results of each optimization run are displayed on the "Optimization" tab. The tab contains general testing results, including profit and the number of trades, as well as many statistical values to help assess the performance of the trading robot.

See the [Testing report](Testing-Report.md) section for details.

The optimization report can be sorted by any parameter by clicking on the column header. Use sorting to find the most profitable combination of parameters and run a [single test](Strategy-Testing.md) for a detailed report.

![Optimization results](images/optimization_result.png)

The following values are displayed for each optimization run:

  * Pass â the number of the testing run;
  * Result â the resulting value of the parameter that is the [optimization criterion (#criterion)](Optimization-Types.md#criterion) for selecting the best runs;
  * Profit â profit/loss received after the run;
  * Total trades â the total number of trades (deals that resulted in fixing a profit or loss) executed for the run;
  * Profit factor â the ratio of the total profit to the total loss in percents. A value of one means that these parameters are equal;
  * Expected payoff â a statistically calculated value that reflects the average profitability/loss of one trade;
  * Drawdown â the relative drawdown of equity, the largest loss in percents from the maximal value of equity. Withdrawal of assets by an Expert Advisor during optimization is [taken into account during drawdown calculation (#drawdown)](Testing-Report.md#drawdown);
  * Recovery factor â this parameter displays the risk level of the strategy (the funds that are put to risk to earn the obtained profit). It is calculated as the ratio of gained profit to the maximum drawdown;
  * Sharpe Ratio â a classic measure which is commonly used to evaluate the performance of a portfolio manager, fund results or a trading system. The ratio is calculated as (Return  Risk-Free Rate)/Standard Deviation of Return. In the strategy tester, the Risk-Free Rate is assumed to be zero. The ratio values are usually interpreted as follows:


  * Sharpe Ratio < 0 â the strategy is unprofitable. Bad.
  * 0 < Sharpe Ratio < 1.0 â the risk does not pay off. Such strategies can be considered when there are no alternatives. Indefinite.
  * Sharpe Ratio ≥ 1.0 â this can mean that the risk pays off and that the portfolio/strategy can show results. Good.
  * Sharpe Ratio ≥ 3.0 â a high value indicates that the probability of obtaining a loss in each particular deal is very low. Very good.
  * Optimized inputs â in addition to the common statistical values, values of input parameters set for this run are shown here.



Using context menu commands you can show/hide some of the above columns. For convenience, check the "Switch to Optimization Results" option: once the optimization process is complete, the Strategy Tester will automatically switch to the Results tab. The same command is available in the context menu of the Journal tab.

Use filters to hide unsuccessful passes from the list:

  * Passes without trades
  * Loss-making passes
  * Passes with the drawdown greater than 50%
  * Passes with the Recovery Factor less than 1
  * Passes with the Sharpe Ratio less than 0.5



The table with optimization results is colored as follows to enable a more efficient visual analysis:

  * Balance: values greater than the initial deposit are colored in blue, and those less than the initial deposit are shown in red.
  * Profit: blue is used for values greater than zero, and red is used for values less than zero.
  * Expected Payoff: blue is used for values greater than zero, and red is used for values less than zero.
  * Drawdown: from green (0-5%) to red (greater than 30%).
  * Sharpe Ratio: from green (greater than 2) to red (less than 0).
  * Recovery Factor: from green (greater than 2) to red (less than 1).
  * Complex Criterion â from dark green (greater than 80) to red (less than 20).



  * If optimization includes forward testing, this tab also contains the corresponding values of the optimization parameter (optimization criterion) for the back and forward tests. You can switch between results of back and forward testing using the context menu.
  * A double click on one of the optimization results starts Expert Advisor [testing](Strategy-Testing.md) with the parameters of this run (provided that the optimization is over).
  * During [genetic optimization](Optimization-Types.md) one of the test runs (a population member) can have the same parameters (genes) as the previous test run. In this case, this run is not displayed on the results tab, because it has the same testing result. However, the optimization graph display all test runs to visualize the process of searching for the best result.
  * If a line of an optimization run has the red background, it means that an [error](https://www.mql5.com/en/docs/runtime/errors "Runtime errors") occurred during Expert Advisor operation. An appropriate message is also added to the tester log ("tested with error").

  
---  
  
<a id="cache"></a>
## Optimization Cache (#cache)

The cache stores data about previously calculated optimization passes. The strategy tester stores the data to enable resuming of optimization after a pause and to avoid recalculation of already calculated test passes.

The optimization cache is stored in [Platform Data Directory]\Tester\cache as separate binary files for each set of optimized parameters of each Expert Advisor. Files are named according to the following rule: ExpertName.Symbol.Period.StartDate.EndDate.GenerationModeOptimizationMode.Hash.opt. Where:

  * ExpertName â the name of the optimized Expert Advisor.
  * Symbol â financial instrument.
  * Period â timeframe (M1,H1,...).
  * StartDate â the date of the optimization beginning.
  * EndDate â the end date of the optimization.
  * GenerationMode â [tick generation mode (#tick-mode)](Real-and-Generated-Ticks.md#tick-mode): 0 â "Every tick", 1 â "Every tick based on real ticks", 2 â "1 minute OHLC", 3 â "Open price only", 4 â "Math calculations".
  * OptimizationMode â [optimization type](Optimization-Types.md): 0 â "Slow complete algorithm", 1 â "Fast genetic based algorithm", 2 â "All symbols selected in Market Watch".
  * Hash â the hash derivative of all above parameters, which is used to find cache files.



Cache files allow viewing results of previous optimizations. Open the "Optimization results" tab, select an Expert Advisor and a file with the desired optimization cache:

![Viewing results of previous optimizations](images/tester_cache.png)

The list contains all Expert Advisor optimization cache files available on the disk Optimization date, testing settings (symbol, timeframe and interval) and input parameters are shown for each file. You can additionally filter optimization results by the trade server.

From the result viewing mode, you can also change the [optimization criterion (#criterion)](Optimization-Types.md#criterion), which you selected at the start of optimization. It is displayed in the Results tab and determines the quality of a tested set of input parameters. The higher the value of the optimization criterion, the better the testing pass is considered to be. Select the desired criterion from the list at the top of the tab, and the tester will automatically recalculate all values ​​in the "Result" column.

To analyze results in third-party programs, for example, Office Excel, optimization report can be saved as a file through the "![Export to XML](images/export_xml_icon.png)Export to XML" command of the context menu. Also, the context menu features commands for exporting and importing cache files. Use these commands to transfer optimization results between different platforms.

  * For optimize disk space usage, cache files are automatically deleted if they are not accessed within 30 days.


  * During the [genetic optimization](Optimization-Types.md), intermediate results are saved in the cache after the calculation of each generation (in a file platform_data_folder/tester/cache/*.gen). Thus the optimization process can be interrupted at any time. Even if the process of genetic optimization is interrupted as a result of an external factor (for example, a black out), the optimization will be automatically continued from the last calculated generation once you restart it. The genetic optimization cache is stored until the optimization settings are changed or the optimization process is completed.
  * In case of a regular optimization stop (when you press the Stop button) all the previously calculated runs are saved. When the optimization process is resumed, it continues from the last calculated run.

  
---  
  
<a id="visual"></a>
## The Visualization of Optimization Results (#visual)

The Strategy Tester in the trading platform provides a powerful visualization system for presenting optimization results. Open "Optimization graph". The tab contains several types of charts, you can switch between them using the context menu.

> ### Graph of results and linear chart (1D)

A graph with optimization results opens by default. Each pass of an Expert Advisor with certain input parameters is displayed as a point on the graph. The number of a pass is shown on the horizontal axis, the value of the parameter that is the optimization criterion is shown on the vertical axis. The graph is colored with a green-to-red gradient, depending on the value of the optimization criterion.

![Graph of results and linear chart (1D)](images/optimization_graph.png)

The linear chart (1D) shows the variation of the parameter selected as the optimization criterion (vertical axis) depending on one of the optimization parameters selected for the horizontal axis. To select a parameter for the horizontal axis, use the "X Axis" command in the context menu.

<a id="2d"></a>
### Flat chart (2D) and three-dimensional chart (3D) (#2d)

In the two-dimensional graph mode, variations of the selected parameters used for optimization are shown on both axes. Variation of the optimization criterion is shown using the color gradient. The deeper the color, the higher the value of the optimization criterion.

![Flat chart (2D) and three-dimensional chart (3D)](images/optimization_graph_2d3d.png)

In the three-dimensional visualization mode, changes of the selected parameters used for optimization are shown on the X and Y axes. Variation of the optimization criterion is displayed on the vertical Z axis and using a color gradient.

To select a parameters for the horizontal and vertical axes, use commands "X Axis" and "Y Axis" in the context menu.

3D chart management using a mouse

  * To move a chart, grab its central part using the left mouse button and move the cursor.
  * To rotate a chart around its vertical axis, grab it outside the center and move the cursor.
  * To rotate a chart around its horizontal axis, rotate the mouse wheel holding down the "Ctrl" key.
  * To zoom in/out a chart, press "Ctrl" and move the mouse cursor vertically in the central part of the chart holding down the left mouse button.
  * To move the zero plane, press "Ctrl" and move the mouse cursor vertically outside the central part of the chart holding down the left mouse button.
  * To return to the initial position of the chart, double click in its central part.



3D chart management using a keyboard

Action | Keys  
---|---  
Show/hide the grid. | G  
Switching between solid filling and filling with lines. | Space  
The camera moves up (the chart moves down). | Up Arrow  
The camera moves down (the chart moves up). | Down Arrow  
The camera moves to the right (the chart moves to the left). | Right Arrow  
The camera moves to the left (the chart moves to the right). | Left Arrow  
The camera moves closer (zoom in the chart). | Plus  
The camera moves away (zoom out the chart). | Minus  
Rotate the graph downward around its horizontal axis. | Home  
Rotate the graph upward around its horizontal axis. | Page Up  
Rotate the graph around the vertical axis counterclockwise. | End  
Rotate the graph around the vertical axis in a clockwise direction. | Page Down  
Moving the zero plane upward by one. | Ctrl+Arrow up  
Moving the zero plane downward by one. | Ctrl+Arrow down  
Moving the zero plane upward by 10 units. | Ctrl+Page Up  
Moving the zero plane downward by 10 units. | Ctrl+Page Down  
Moving the zero plane to the maximum value of the graph. | Ctrl+Home  
Moving the zero plane to the minimum value of the graph. | Ctrl+End  
Increasing the transparency of the zero plane. | Ctrl+Plus  
Reducing the transparency of the zero plane. | Ctrl+Minus  
Setting the maximum transparency of the zero plane (it disappears). | Ctrl+Right Arrow  
Setting the minimum transparency of the zero plane (it becomes nontransparent). | Ctrl+Left Arrow  
Reset to default graph settings. | "5" key on the num pad.  
  
<a id="forward"></a>
## Testing a Trading Robot on a Forward Non-Optimized Period (#forward)

Forward testing is the repeated run of the best optimization results on a different time period. This feature allows you to avoid parameters fitting in certain areas of historical data.

To start the forward testing, in the Forward field of the Settings tab select the part of the total period for it:

  * No â forward testing is not used;
  * 1/2 â half of the specified period is used for the forward test;
  * 1/3 â one third of the specified period is used for the forward test;
  * 1/4 â a quarter of the specified period is used for the forward test;
  * Custom â specify the forward test start day manually.



![Forward period](images/forward_period.png)

  * The second (latest) part of the total period is always taken for the forward testing.
  * The forward test start date is displayed as a vertical line on the optimization graph.

  
---  
  
The selected part is separated from the period specified in the "Date" field. The first part is the period of back testing, and the second one is the period of forward testing.

The full optimization (slow or fast) of the Expert Advisor is conducted on the back testing period. After that 10% (in the full search) or 25% (in the genetic algorithm) of best runs are selected and then tested on the forward period.

> There is a lower limit for the number of passes of forward testing. If the number of best runs is less than 256, the additional best runs are used for forward testing until their number reaches 256. If the number of all runs is less than 256, all of them participate in forward testing.

Results of back and forward testing can be compared on the "Optimization Results" (select "Forward testing results" in the context menu) and "Forward Results" tabs. The better the results coincide, the more likely it is that the Expert Advisor will show good results in real trading.

The visualization of optimization results on the forward period is available on the "Forward optimization graph" tab. To compare these results with the backtest, switch between them using the context menu.

![Forward optimization results](images/optimization_forward.png)

For details about testing results please read sections "Where to view the optimization results" and "Visualization of optimization results".

<a id="agents"></a>
## Multithreaded Testing Using Agents (#agents)

The multithreaded Strategy Tester uses all available computer resources. Testing and optimization are carried out using special computing agents that are installed as services on the user's computer. Agents work independently and calculate optimization passes in parallel.

Three types of agents are available: local, remote and cloud (MQL5 Cloud Network). Local agents are installed automatically when you install the trading platform. Their number is equal to the number of logical cores of the computer.

Remote and cloud agents run on other computers. For detailed information about agents, please read "How to speed up optimization using a local farm of agents" and "How to speed up optimization using MQL5 Cloud Network".

Open the "Agents" section in the Strategy Tester and select the type of agents you want to use for optimization.

![Testing agents](images/optimization_agents.png)

<a id="tips-and-features"></a>
### Tips and features: (#tips-and-features)

  * To conserve the laptop battery, you can disable local agents and use only the remote and cloud ones.
  * If testing/optimization is not finished manually (neither by pressing the Stop button at the settings tab nor by closing the trading platform), the processes of used local agents are not unloaded from the computer memory for 5 minutes. This feature allows avoiding delays connected with preparing the price history and starting the agent processes when re-testing/re-optimizing the same Expert Advisor at the same symbol, timeframe and time period.
  * Only local agents are installed together with the platform installation. They are only used in the Strategy Tester of the local platform. [Remote agents](MetaTester-and-Remote-Agents.md) that can also be connected to the global MQL5 Cloud Network can be installed only [manually](../MQL5-Cloud-Network/README.md).



<a id="farm"></a>
## How to Speed up Optimization Using a Local Farm of Agents (#farm)

You can purchase a processor with more cores, but it does not allow to multiply the number of concurrent tasks. You can create your own farm of processing agents in your local network.

<a id="farm-create"></a>
### How to Create a Farm of Agents (#farm-create)

Install agents on each computer of the local network. If the platform is installed on a computer, open testing agents manager using the "Tools" menu.

![Strategy Tester Agents Manager](images/remote_agents_install.png)

Otherwise, download a separate application for managing agents [MetaTrader 5 Strategy Tester Agent](MetaTester-and-Remote-Agents.md) and go through the simple installation process.

On the Services tab of the manager:

  * Select the number of agents to be installed. They are installed based on the number of logical cores.
  * Enter the password for connecting to the agent.
  * Select a range of ports for connection.
  * Click Add.



After installation, the agents are available for use from other computers on the local network.

> Remote agents can only be used in 64 bit systems.

<a id="farm-connect"></a>
### How to Connect Agents (#farm-connect)

Open the Strategy Tester. On tab "Agents", select "Local Network Farm" and click "Add" in the context menu.

![How to Add Remote Agents](images/add_remote_agents.png)

The easiest and fastest way is to automatically scan the local network for a range of IP addresses and ports. Select them and enter the agent connection password that was specified during installation.

![Search for agents on the LAN](images/network_scan.png)

Click "Finish" and all the found agents become available for testing.

Other options to add agents:

  * Add agents (by IP address or domain name) â specify the IP address or domain name of a server where agents are installed, as well as the range of ports and password for connecting to the agents.
  * Import from file *.mt5 â select this option, click "Next" and specify the *.mt5 file from which you want to import agents.



  * Agents installed on the computer using MetaTester 5 Agents Manager, can be connected as remote on the same computer. If the processor cores have extra computation power during calculations, they can take a higher load to use all the computing capacity.
  * If agents cannot connect or are not found when scanning the network, open Windows firewall settings on the remote machine and add an allowing incoming rule for the application \\[platform installation directory]\metatester64.exe.

  
---  
  
<a id="farm-modify"></a>
### How to Change Agent Settings (#farm-modify)

To change the settings, click the "![Edit](images/agent_edit_icon.png) Edit" command in its context menu.

![Agent Setup](images/agent_edit.png)

The following fields are available in the settings window:

  * Name â the name of the agent;
  * Address â IP address and port for connecting to an agent, separated by a colon;
  * Password â password for connection;
  * Enable â this option allows to enable or disable the use of the agent during testing and optimization.



In settings of local agents only the option of enabling/disabling them is available.

<a id="farm-impexp"></a>
### Import and Export of Settings of Remote Agents (#farm-impexp)

To make setting up of remote agents easier, the platform provides a feature for importing and exporting their settings. The files of settings have the *.mt5 extension. The import and export commands are located in the context menu of the "Agents" tab.

Files of settings have the following format: Name;Address:port;Password;Description;Enable.

  * Name â the name of the agent;
  * Address:port â IP address and port for connecting to an agent, separated by a colon;
  * Password â password for connection;
  * Description â description of the hardware the agent is running on;
  * Enable â agent operation mode: 1 â the agent is enabled, 0 â the agent is disabled.



Settings of different agents are separated from each other with line breaks.

<a id="cloud"></a>
## How to Speed Up Optimization Using the MQL5 Cloud Network (#cloud)

[The MQL5 Cloud Network](https://cloud.mql5.com/en "Official site of the MQL5 Cloud Network") allows you to quickly optimize your Expert Advisors using the power of thousands of computers. The network combines remote agents and distributes optimization tasks among them. The Strategy Tester connects to the cloud network through multiple access points, which are distributed on a territorial basis (e.g., MQL5 Cloud Europe).

<a id="cloud-features"></a>
### Features of the MQL5 Cloud Network (#cloud-features)

  * The entire power of the MQL5 Cloud Network is used only for [Complete slow optimization](Optimization-Types.md).
  * During [genetic optimization](Optimization-Types.md), only agents of one access point are used. It is connected with the specific features of the genetic algorithm.
  * The genetic optimization mode is automatically enabled when the total number of optimization steps exceeds 100 million.
  * MQL5 Cloud Network can be used in 64 bit systems only.
  * In addition to using the MQL5 Cloud Network, you can provide your CPU computing power in the network. To install the remote agents and include them into the network, use a special utility [MetaTester](MetaTester-and-Remote-Agents.md).
  * Read more about the MQL5 Cloud Network on [the official site](https://cloud.mql5.com/en "MQL5 Cloud Network").



<a id="cloud-pay"></a>
### Payments for the Use of the MQL5 Cloud Network (#cloud-pay)

  * Using agents of the MQL5 Cloud Network is paid. The formula for calculating the cost is described in [a separate section](../MQL5-Cloud-Network/Price-Calculation.md). The current MQL5.community account balance is displayed above the list of cloud agents.
  * To use MQL5 Cloud Network a user needs to have at least 1 US dollar on the MQL5.community account. Tasks are passed in packages to several access points simultaneously, and the user must be able to pay for completion of that tasks. The Network is not able to calculate the exact cost as the time and resources required for calculations cannot be estimated precisely before the start of calculations.



<a id="cloud-enable"></a>
### Enabling MQL5 Cloud Network (#cloud-enable)

To use the network agents, enable them using command "![Enable](images/enable_agent_icon.png) Enable" in the context menu. Since the MQL5 Cloud Network is a paid service, a user must have an account at the [MQL5.community](https://www.mql5.com/ "MQL5.community") website, through which all the accounting operations are performed. Account details are specified on the [MQL5.community (#community)](../Getting-Started/Platform-Settings.md#community) tab of the platform settings.

If you do not specify the details of your MQL5.community account before enabling the MQL5 Cloud Network agents, you will be offered to do this.

![Enabling MQL5 Cloud Network](images/tester_cloud_enable.png)

If you have not registered on the website, use the [new account creation](https://www.mql5.com/en/auth_register) link.

<a id="cloud-start"></a>
### Starting Calculations Using the MQL5 Cloud Network (#cloud-start)

Like with a conventional optimization, you need to set all the testing options and Expert Advisor input parameters. On the Agents tab, you can monitor how the Strategy Tester distributes tasks to available agents. The number of available and currently used agents is displayed for each access point.

![Running distributed computing using the MQL5 Cloud Network Agents](images/cloud_start.png)

Traders may need to run hundreds of thousands of optimization passes in a reasonable time. With the multi-threaded Strategy Tester and the MQL5 Cloud Network, in one hour you can complete the calculations that would require a few days without the network. The computing power of thousands of cores is available straight on the trading platform.

> There are limitations for each optimization pass. During optimization, the Expert Advisor cannot write more than 4GB of information to disk and use more than 4GB of RAM. If the limit is exceeded, the network agent will not be able to complete the calculation correctly, and you will not receive the result. However, you will be charged for all the time spent on the calculations.
