[🏠 Document Start](../README.md) / [Algorithmic Trading, Trading Robots](README.md) / Optimization Types

[Previous](Journal-of-Testing.md) | [Next](Real-and-Generated-Ticks.md)

<a id="optimization-types"></a>
# Optimization Types (#optimization-types)

Two optimization types are available in the tester. You can select the appropriate one on the [Settings (#settings)](Strategy-Optimization.md#settings) tab of the Strategy Tester.

<a id="slow-complete-algorithm"></a>
## Slow Complete Algorithm (#slow-complete-algorithm)

In this mode, optimization runs are performed for all possible combinations of values of input variables selected on the [appropriate tab (#inputs)](Strategy-Optimization.md#inputs).

This method is the most precise one. However, running the Expert Advisor with all possible combinations takes much time.

<a id="fast-genetic-algorithm"></a>
## Fast Genetic Algorithm (#fast-genetic-algorithm)

This type of optimization is based on the genetic algorithm of search for the best values of input parameters. This type is much faster than the first one and is almost of the same quality. The slow complete optimization that would take several years can be performed within several hours using the genetic algorithm.

Each individual has a specific set of genes which corresponds to the set of their parameters. Genetic optimization is based on the constant selection of the most "adapted" parameters (values that give the best result). In the general form, the algorithm can be represented the following way:

  * From the total number of all possible combinations of parameters, two populations (sets) are selected by a random sample;
  * Both sets are tested and the one with the best results (according to the optimization criterion) is left;
  * The set members are randomly crossed with one another, undergoing random mutations and inversions of parameters;
  * The descendants are sorted out by the best results, and crossing repeats;
  * Sorting and crossing operations are repeated as long as there is improvement of results (the best result among descendants is better than the best one among the parents). If the optimization criterion values are not improved during several crossings (generations), the optimization process is completed.



<a id="number-of-test-runs"></a>
### Number of Test Runs (#number-of-test-runs)

During the genetic optimization, the number of test runs is much lower, which provides quickness of optimization. After the start of the genetic optimization, an estimated number of test runs is displayed on the [Settings (#settings)](Strategy-Testing.md#settings) tab. It is calculated by the following formula:

Population size * (Unconditional number of generations + Number of generations for convergence estimation)

where:

  * Population size is calculated based on the number of possible combinations of optimization parameters, may range from 64 to 256;
  * Unconditional number of generations may range from 15 to 31. It is defined by the presence of optimization criterion improvement. 15 generations are tested in all optimizations. If a generation within the range between 15 and 31 does not have any improvement of the optimization criterion, an additional test of the next generations is started for convergence estimation.
  * Number of generations for convergence estimation is calculated as one third of the unconditional number of generations. If the unconditional number of generation is 18 (the 17-th generation has shown the best result and there are no improvements shown by the 18-th generation) then another 5 generations are tested: the 18-th generation has not shown any improvement, and for the estimation of convergence we need 18/3 = 6 generations without improvements of the optimization criterion. If there are no improvements shown by the specified number of generations, optimization is stopped.



  * If the total number of optimization steps exceeds 1,000,000 in a 32-bit system or 100,000,000 in a 64-bit system, the genetic optimization mode starts automatically.
  * During the [genetic optimization](Optimization-Types.md), intermediate results are saved in cache after the calculation of each generation (in a file platform_data_folder/tester/cache/*.gen). Thus the optimization process can be interrupted at any time. Even if the process of genetic optimization is interrupted as a result of an external factor (for example, power failure), the optimization will be automatically continued from the last calculated generation at the next start. The genetic optimization cache is stored until the [optimization settings (#settings)](Strategy-Optimization.md#settings) are changed or the optimization process is completed.
  * At a regular optimization stop (when you press the [Stop button (#settings)](Strategy-Optimization.md#settings)) all the previously calculated runs are saved. When the optimization process is resumed, it continues from the last calculated run.

  
---  
  
<a id="criterion"></a>
### Optimization Criterion (#criterion)

An optimization criterion is a certain factor, which value defines the quality of a tested set of parameters. The higher the value of the optimization criterion, the better the testing result with the given set of parameters. Such a factor can be selected in a field to the right of "Optimization" on the [Settings (#settings)](Strategy-Optimization.md#settings) tab.

> The optimization criterion is required only for the genetic algorithm.

The following optimization criteria are available:

  * Balance max — the highest value of the balance.
  * Profit Factor max — the highest value of the [profit factor (#profit-factor)](Testing-Report.md#profit-factor).
  * Expected Payoff max — the highest value of the [expected payoff (#expected-payoff)](Testing-Report.md#expected-payoff).
  * Drawdown min — in this case, the [relative drawdown of balance (#drawdown)](Testing-Report.md#drawdown) in percentage terms is taken into account.
  * Recovery Factor max — the highest value of the [recovery factor (#recovery-factor)](Testing-Report.md#recovery-factor).
  * Sharpe Ratio max — the highest value of the [Sharpe ratio (#sharpe-ratio)](Testing-Report.md#sharpe-ratio).
  * Custom max — the optimization criterion here is the value of the OnTester() function in the Expert Advisor. This parameter allows using any custom value for the optimization of Expert Advisors.



Another option is to use "Complex Criterion max". This is an integral and complex measure of a test pass quality. It measures multiple parameters:

  * Number of Deals
  * Drawdown
  * Recovery Factor
  * Expected Payoff
  * Sharpe Ratio



By using this criterion, you can see that the highest value of one parameter (for example the profit) is not always the best option in terms of the complex analysis. The complex criterion gradually selects the best passes: firstly, by the number of deals, then by the Expected Payoff, Recovery Factor, and so on. The new option allows reception of the best optimization passes according to all parameters. Furthermore, you can select the optimal pass based on the desired parameter, such as the highest profit.

<a id="all-symbols-selected-in-market-watch"></a>
## All Symbols Selected in Market Watch (#all-symbols-selected-in-market-watch)

Unlike the above described optimization types, this one allows to test an Expert Advisor with the same [input parameters (#inputs)](Strategy-Optimization.md#inputs), but with different symbols. Only the [main symbol of testing (#settings)](Strategy-Optimization.md#settings) is changed in each pass, i.e. the symbol of chart the EA would be attached to.

Optimization is performed only for symbols that are currently chosen in the [Market Watch](../Trading-Operations/Market-Watch.md). So you can manage optimization by adjusting the set of selected symbols. 

  * Please note that downloading of necessary price data from the server may take a long time. However, the slowdown of optimization as a result of data downloading occurs only during the first launch for a symbol, next time only the missing data is downloaded.
  * The current values of [input parameters (#inputs)](Strategy-Optimization.md#inputs) specified in the "Value" field are used for the optimization by symbols.


  * [MQL5 Cloud Network (#cloud)](Strategy-Optimization.md#cloud) is not supported for this type of optimization.

  
---
