[🏠 Document Start](../README.md) / [Algorithmic Trading, Trading Robots](README.md) / Journal of Testing

[Previous](Testing-Visualization.md) | [Next](Optimization-Types.md)

# Journal of Testing

The entire process of testing and optimization is logged in the journal in details. Let's see what happens after Start button is clicked in the strategy tester.

## Preparing price history

Before launching testing/optimization, the tester prepares the environment. The presence of a tested symbol history is checked and the entire history stored in the trade server is synchronized. If the platform has no history for a tested symbol, synchronization with the trade server may take a few minutes.

Tester EURCAD: preliminary downloading of M1 history started | starting the preliminary download of EURCAD M1 history  
---|---  
Tester EURCAD: 20% history downloaded | 20% of download complete  
Tester EURCAD: 95% history downloaded | 95% of download complete  
Tester EURCAD: preliminary downloading of M1 history completed in 0:14.640 | download complete in 0:14.640  
Tester EURCAD: history data begins from 2014.12.29 00:00 | symbol's minute data are present from 2014.12.29 00:00  
  
If testing is performed based on real ticks, the platform synchronizes the existing ticks within testing dates. Tick download may take a long time.

Tester EURCAD: preliminary downloading of history ticks started, it may take quite a long time | starting preliminary download of EURCAD ticks, it may take quite a long time  
---|---  
Tester EURCAD: "bases\MetaQuotes-Demo\ticks\EURCAD\201609.tkc" download | ticks for September 2016 downloaded to the specified path  
Tester EURCAD: "bases\MetaQuotes-Demo\ticks\EURCAD\201608.tkc" download (823.38 Kb/sec) | ticks for October 2016 downloaded to the specified path  
Tester EURCAD: 21% ticks downloaded (796.02 Kb/sec) | 21% of download complete, download speed - 796.02 Kb/sec  
Tester EURCAD: "bases\MetaQuotes-Demo\ticks\EURCAD\201604.tkc" download (764.22 Kb/sec) | ticks for April 2016 downloaded to the specified path  
Tester EURCAD: preliminary downloading of history ticks completed, 116.78 Mb in 2:32.063 (786.40 Kb/sec) | tick download complete in 2:32.063, downloaded ticks size - 116.78 MB  
Tester EURCAD: ticks data begins from 2016.04.01 00:00 | EURCAD tick data are present from 2016.04.01 00:00  
  
The presence of cross pairs is checked afterwards. For example, if testing is performed on EURCAD, while the deposit currency is USD, EURUSD and USDCAD symbols are necessary to calculate profit and margin requirements when performing trades. Therefore, full synchronization of history and these symbols is performed. If necessary, tick data are synchronized as well. Price data preparation is described in the tester journal in details:

Tester EURUSD: preliminary downloading of history ticks started, it may take quite a long time | starting preliminary download of EURUSD ticks, it may take quite a long time  
---|---  
Tester EURUSD: preliminary downloading of history ticks completed, 1021.82 Kb in 0:03.218 (317.53 Kb/sec) | tick download complete in 0:03.218, downloaded ticks size - 1021.82 KB  
Tester EURUSD: ticks data begins from 2011.12.19 00:00 | EURUSD tick data are present from 2011.12.19 00:00  
Tester USDCAD: preliminary downloading of M1 history started | starting the preliminary download of USDCAD M1 history  
Tester USDCAD: preliminary downloading of M1 history completed in 0:00.203 | download complete in 0:00.203  
Tester USDCAD: preliminary downloading of history ticks started, it may take quite a long time | starting preliminary download of USDCAD ticks, it may take quite a long time  
Tester USDCAD: "bases\MetaQuotes-Demo\ticks\USDCAD\201609.tkc" download | ticks for September 2016 downloaded to the specified path  
Tester USDCAD: "bases\MetaQuotes-Demo\ticks\USDCAD\201608.tkc" download (683.69 Kb/sec) | ticks for August 2016 downloaded to the specified path, download speed - 683.69 Kb/sec  
Tester USDCAD: preliminary downloading of history ticks completed, 103.25 Mb in 2:30.109 (704.36 Kb/sec) | tick download complete in 2:30.109, downloaded ticks size - 103.25 MB  
Tester USDCAD: ticks data begins from 2015.01.01 00:00 | USDCAD tick data are present from 2015.01.01 00:00  
  
## Testing/optimization start

Testing/optimization starts only after all necessary history (as well as ticks if you test/optimize strategy using real ticks) is synchronized.

Connection to a selected [testing agent (#agents)](Strategy-Optimization.md#agents) is established during a single test. The agent can be either local or network.

Core 1 agent process started | agent process launched at the first processor core  
---|---  
Core 1 connecting to 127.0.0.1:3000 | connecting to 127.0.0.1:3000  
Core 1 connected | connection established  
Core 1 authorized (agent build 1395) | authorization passed, agent build - 1395  
  
Local agent data folder name corresponds to its address and port.

After connection is established, the environment is synchronized according to testing settings.

Tester EURCAD,H1 (MetaQuotes-Demo): testing of Experts\Moving Average.ex5 from 2016.04.01 00:00 to 2016.06.01 00:00 | launching Moving Average EA testing on EURCAD H1, MetaQuotes-Demo server, testing period - from 2016.04.01 00:00 to 2016.06.01 00:00  
---|---  
Core 1 common synchronization completed | total synchronization complete  
  
From this moment on, the agent starts keeping its own journal sending its data to the tester one. Local agent journal can be opened from the tester journal context menu. The journal shows environment synchronization details between the terminal and the agent.

Environment initialization and synchronization:

Startup MetaTester 5 x64 build 1395 (19 Aug 2016) | launching testing agent, build 1395 as of August 19, 2016  
---|---  
Server MetaTester 5 started on 127.0.0.1:3000 | testing agent launched on 127.0.0.1:3000  
Startup initialization finished | initialization finished  
127.0.0.1 login (build 1395) | platform has been connected to the agent  
Network 38520 bytes of account info loaded | agent downloaded 38520 bytes of information about the trading account parameters  
Network 1482 bytes of tester parameters loaded | agent downloaded 1482 bytes of information about the testing parameters  
Network 2236 bytes of input parameters loaded | agent downloaded 2236 bytes of information about the EA inputs  
Network 22730 bytes of symbols list loaded | agent downloaded 22730 bytes of information about symbols  
  
Synchronizing testing parameters and tested symbol data:

Tester expert file added: Experts\Examples\Moving Average\Moving Average.ex5. 53048 bytes loaded | agent downloaded the EA file, the file size is 53048 bytes  
---|---  
Tester initial deposit 10000.00 USD, leverage 1:100 | initial deposit before testing - 10 000 USD, leverage - 1:100  
Tester successfully initialized | testing initialized  
Network 68 Kb of total initialization data received | total volume of the data obtained by the agent during initialization - 68 KB  
Tester Intel Core i7-3770 @ 3.40GHz, 16351 MB | configuration of the PC the agent is launched at  
Symbols EURCAD: symbol to be synchronized | EURCAD symbol synchronization  
Symbols EURCAD: symbol synchronized, 3384 bytes of symbol info received | symbol synchronized, 3384 bytes of data received  
History EURCAD: load 4.51 Mb of history data to synchronize in 0:00:00.594 | downloaded 4.51 MB of history data within 594 milliseconds  
History EURCAD: history synchronized from 2015.01.02 to 2016.06.01 | EURCAD history synchronized from 2015.01.02 to 2016.06.01  
Ticks EURCAD: ticks synchronization started | starting EURCAD tick synchronization  
Ticks EURCAD: load 48.66 Mb of tick data to synchronize in 0:00:00.969 | 48.66 MB of data downloaded during synchronization within 969 milliseconds  
Ticks EURCAD: history ticks synchronized from 2016.04.01 to 2016.05.31 | EURCAD tick history synchronized from 2016.04.01 to 2016.05.31  
History EURCAD,H1: history cache allocated for 8862 bars and contains 7729 bars  
from 2015.01.02 09:00 to 2016.03.31 23:00 | history cache of 8862 bars created, the cache contains 7729 bars from 2015.01.02 09:00 to 2016.03.31 23:00  
History EURCAD,H1: history begins from 2015.01.02 09:00 | EURCAD history starts from 2015.01.02 09:00  
Tester EURCAD,H1 (MetaQuotes-Demo): generating based on real ticks | testing is to be launched on real ticks  
Tester EURCAD,H1: testing of Experts\Examples\Moving Average\Moving Average.ex5  
from 2016.04.01 00:00 to 2016.06.01 00:00 started with inputs: | testing Moving Average EA from 2016.04.01 00:00 to 2016.06.01 00:00 is to be launched with the following inputs:  
Tester MaximumRisk=0.02 | MaximumRisk=0.02  
Tester DecreaseFactor=3.00 | DecreaseFactor=3.00  
Tester MovingPeriod=12 | MovingPeriod=12  
Tester MovingShift=6 | Tester MovingShift=6  
Moving Average (EURCAD,H1) 2016.04.01 00:00:00 expert initialized | Moving Average EA initialized  
Ticks EURCAD : real ticks begin from 2016.04.01 00:00:00 | EURCAD real ticks are present from 2016.04.01 00:00:00  
  
Synchronizing cross rates:

Symbols EURUSD: symbol to be synchronized | synchronizing EURUSD symbol  
---|---  
Symbols EURUSD: symbol synchronized, 3384 bytes of symbol info received | symbol synchronized, 3384 bytes of data received  
History EURUSD: load 27 bytes of history data to synchronize in 0:00:00.000 | downloaded 27 bytes of history data within 000 milliseconds  
History EURUSD: history synchronized from 2014.01.01 to 2016.09.02 | EURUSD history synchronized from 2014.01.01 to 2016.09.02  
Ticks EURUSD: ticks synchronization started | starting EURUSD tick synchronization  
Ticks EURUSD: load 34 bytes of tick data to synchronize in 0:00:00.000 | 48.66 MB of data downloaded during synchronization within 969 milliseconds  
Ticks EURUSD: history ticks synchronized from 2016.01.04 to 2016.09.02 | EURUSD tick history synchronized from 2016.04.01 to 2016.05.31  
Symbols USDCAD: symbol to be synchronized | USDCAD symbol synchronization  
Symbols USDCAD: symbol synchronized, 3384 bytes of symbol info received | symbol synchronized, 3384 bytes of data received  
History USDCAD: load 27 bytes of history data to synchronize in 0:00:00.094 | downloaded 27 bytes of history data within 94 milliseconds  
History USDCAD: history synchronized from 2013.01.01 to 2016.08.01 | USDCAD history synchronized from 2013.01.01 to 2016.08.01  
Ticks USDCAD: ticks synchronization started | starting USDCAD tick synchronization  
Ticks USDCAD: load 43.10 Mb of tick data to synchronize in 0:00:00.890 | 43.10 MB of data downloaded during synchronization within 890 milliseconds  
Ticks USDCAD: history ticks synchronized from 2016.04.01 to 2016.05.31 | USDCAD tick history synchronized from 2016.04.01 to 2016.05.31  
  
## Tick sequences

Tick sequences are generated before testing. The more ticks are used, the bigger delay before testing.

If you test on real ticks, correctness of a downloaded tick data relative to minute bars is checked. If the data is correct, the journal contains only one entry (for each symbol):

Ticks EURCAD : real ticks begin from 2016.04.01 00:00:00 | EURCAD real tick data are present from 2016.04.01 00:00:00  
---|---  
  
Otherwise, a detailed statistics is shown allowing users to evaluate the quality of the tick history.

Ticks EURUSD : real ticks begin from 2015.01.01 00:00:00 | EURUSD real tick data are present from 2015.01.01 00:00:00  
---|---  
Ticks EURUSD : 2015.01.01 00:00 - 2016.01.01 00:00 tick volumes not matched for 4 minute bars | tick volume has shown mismatch at 4 minute bars within 2015.01.01 00:00 - 2016.01.01 00:00  
Ticks EURUSD : 2015.01.01 00:00 - 2016.01.01 00:00 last prices absent for 16217 minute bars, bid prices used | no last prices detected for 16217 minute bars within 2015.01.01 00:00 - 2016.01.01 00:00, bid prices are to be used instead  
Ticks EURUSD : 2015.01.01 00:00 - 2016.01.01 00:00 last prices absent for 22 whole days, bars built by bid prices | no last prices detected for 22 full days within 2015.01.01 00:00 - 2016.01.01 00:00, bars have been generated using bid prices  
Ticks EURUSD : 2015.01.01 00:00 - 2016.01.01 00:00 last prices translation turned off for 881 minute bars, bid and last prices used | last price translation for 881 minute bars interrupted within 2015.01.01 00:00 - 2016.01.01 00:00, both last and bid prices are to be used instead  
  
Detailed statistics appears in the agent journal after the test:

Tester final balance 7905.30 USD | final balance comprised 7905.30 USD  
---|---  
Tester EURCAD,H1: 50056687 ticks, 6195 bars generated. Environment synchronized in 0:00:02.656. | generated 50056687 ticks and 6195 bars, environment synchronization performed for 0:00:02.656  
Test passed in 0:01:40.906 (including ticks preprocessing 0:00:27.047). | testing carried out for 0:01:40.906 (including ticks preparation which took 0:00:27.047)  
Tester EURCAD,H1: total time from login to stop testing 0:01:43.562 (including 0:00:07.329 for history data synchronization) | time from connecting to the agent up to the test completion - 0:01:43.562 (including history data synchronization that took 0:00:07.329)  
Tester 132757966 total ticks for all symbols | generated 132757966 ticks in total for all symbols  
Tester EURCAD: generate 50056687 ticks in 0:00:08.703, passed to tester 50056687 ticks | generated 50056687 ticks for EURCAD within 0:00:08.703, 50056687 ticks passed to the tester  
Tester EURUSD: generate 42615166 ticks in 0:00:09.235, passed to tester 42587228 ticks | generated 42615166 ticks for EURUSD within 0:00:09.235, 42587228 ticks passed to the tester  
Tester USDCAD: generate 40134644 ticks in 0:00:09.109, passed to tester 40114051 ticks | generated 40134644 ticks for USDCAD within 0:00:09.109, 40114051 ticks passed to the tester  
Tester 546 Mb memory used including 0.94 Mb of history data, 320 Mb of cached tick data (total memory for tick data 3135 Mb) | used 546 MB of memory, including 0.94 MB for history data and 320 MB for cache ticks (3135 MB used in total for tick data)  
Tester log file "E:\MetaTrader5\Tester\Agent-127.0.0.1-3000\logs\20160908.log" written | agent journal file saved at the specified path  
  
If only one symbol is tested, the journal displays total statistics instead of separate lines for each symbol:

Tester final balance 1199.73 USD | final balance is 1199.73 USD  
---|---  
Tester EURUSD,H1: 42668248 ticks, 6195 bars generated. Test passed in 0:00:41.360 (including ticks preprocessing 0:00:06.672). | generated 42668248 ticks and 6195 bars. Testing carried out for 0:00:41.360 (including ticks preparation which took 0:00:06.672)  
Tester 489 Mb memory used including 0.94 Mb of history data, 320 Mb of cached tick data (total memory for tick data 1023 Mb) | used 489 MB of memory, including 0.94 MB for history data and 320 MB for cache ticks (1023 MB used in total for tick data)  
Tester log file "E:\MetaTrader5\Tester\Agent-127.0.0.1-3000\logs\20160908.log" written | agent journal file saved at the specified path  
  
The minimum data exchange between the platform and the agent is performed at the synchronization stage during a repeated testing on the same history data. History cached in the agent memory is used. If the tick generation model remains unchanged, cached tick data is used as well. In this case, testing starts immediately:

Tester account info found | trading account data found  
---|---  
Network 1482 bytes of tester parameters loaded | downloaded 1482 bytes of testing parameters  
Tester initial deposit 1000.00 USD, leverage 1:100 | initial deposit before testing - 1 000 USD, leverage - 1:100  
Tester successfully initialized | testing initialized  
Network 1614 bytes of total initialization data received | total volume of the data obtained by the agent during initialization - 1614 bytes  
Tester Intel Core i7-3770 @ 3.40GHz, 16351 MB | configuration of the PC the agent is launched at  
History EURUSD,H1: history cached from 2014.01.01 23:00 | EURUSD H1 history cached starting from 2014.01.01 23:00  
Tester EURUSD,H1 (MetaQuotes-Demo): every tick generating | launched testing on all ticks (MetaQuotes-Demo server)  
Tester EURUSD,H1: testing of Experts\Tester\MultyPairCrossMA.ex5 from 2015.01.01 00:00 to 2016.01.01 00:00 started with inputs: | testing Moving Average EA from 2015.01.01 00:00 to 2016.01.01 00:00 is to be launched with the following inputs:  
Tester InpLots=0.10 Tester InpStopLoss=50 Tester InpTakeProfit=50 Tester InpTrailingStop=30 Tester InpFastMAPeriod=21 Tester InpSlowMAPeriod=34 | InpLots=0.10 InpStopLoss=50 InpTakeProfit=50 InpTrailingStop=30 InpFastMAPeriod=21 InpSlowMAPeriod=34  
History EURUSD,M5: history cached from 2014.01.01 23:00 | EURUSD M5 history cached starting from 2014.01.01 23:00  
History EURJPY,M5: history cached from 2014.01.01 23:00 | EURJPY M5 history cached starting from 2014.01.01 23:00  
History USDJPY,M5: history cached from 2014.01.01 23:00 | USDJPY M5 history cached starting from 2014.01.01 23:00  
  
## Testing completion

Stop out. If trading is unsuccessful, testing can be stopped by Stop Out:

Tester final balance 44.81 USD | final balance is 44.81 USD  
---|---  
Tester stop out occurred on 3% of testing interval | stop out occurred after passing 3% of the testing period  
  
Standard completion. Testing can be stopped earlier by calling the ExpertRemove function when a certain condition is fulfilled. This is followed by the following journal entries:

MACD Sample (EURUSD,H1) 2015.03.13 03:00:00 Testing stop. Balance is 299.29 | testing is stopped, the balance is 299.29  
---|---  
MACD Sample (EURUSD,H1) 2015.03.13 03:00:00 ExpertRemove() function called | ExpertRemove function has been called  
Tester removed itself within OnTick | EA has completed its work in the tick handler  
Tester final balance 299.29 USD | final balance is 299.29 USD  
Tester removed itself on 19% of testing interval | EA completed work after passing 3% of the testing period  
  
Memory error. Testing can be completed ahead of schedule due to a critical error. For example, constant memory re-allocations by the ArrayResize function can lead to excessive memory fragmentation which in turn may cause the memory block to be of insufficient size. The memory error is triggered as a result.

MemoryException 8192 Mb not available | memory block of 8192 MB is unavailable  
---|---  
MACD Sample (EURUSD,H1) 2015.01.02 09:00:15 cannot resize ExtDoubleArray4 from 536870912 to 1073741824 | at 2015.01.02 09:00:15, the EA failed to increase the ExtDoubleArray4 array size from 536870912 to 1073741824 bytes  
Tester memory error in OnTick | error occurred when handling memory in OnTick  
Tester stopped on 0% of testing interval | work complete after passing 3% of the testing period  
Tester not enough available memory, 37371 Mb used, 9178 Mb available, maximal available block is 4096 Mb | insufficient memory, total memory 37371 MB, available 9178 MB, maximum memory block size 4096 MB  
  
Array out of range. Exceeding the array range (i.e. array element index is equal or exceeds the number of array elements) is considered a critical error (indexing begins from zero).

MACD Sample (EURUSD,H1) 2015.01.06 18:42:59 array out of range in 'MACD Sample.mq5' (473,28) | array out of range in the MACD Sample.mq5 file (string 473, position 28)  
---|---  
Tester OnTick critical error | critical error in OnTick  
  
Zero divide. Zero divide is also considered a critical error.

MACD Sample (EURUSD,H1) 2015.01.06 18:42:59 zero divide in 'MACD Sample.mq5' (465,35) | zero divide in the MACD Sample.mq5 file (string 465, position 35)  
---|---  
Tester OnTick critical error | critical error in OnTick  
  
Initialization error. Testing stops without starting if the OnInit function in the program returns a code different from INIT_SUCCEEDED. For example, this feature can be used to manage input parameters.

MACD Sample (EURUSD,H1) 2015.01.01 00:00:00 Deinit reason is 8 | EA deinitialized at 2015.01.01 00:00:00  
---|---  
Tester tester stopped because OnInit failed | testing stopped due to OnInit error
