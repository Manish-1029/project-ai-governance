[🏠 Document Start](../README.md) / [MQL5 Cloud Network](README.md) / Price Calculation

[Previous](How-to-Participate.md) | [Next](../Virtual-Hosting-for-247-Operation/README.md)

# Price Calculation

This section describes the formula of price calculation for providing and using the agents of the [MQL5 Cloud Network](README.md).

> All the financial operations connected with the MQL5 Cloud Network are performed through the internal payment system of [MQL5.community](https://www.mql5.com/ "MQL5.community"). You can view all the financial operations on the MQl5.community website in the profile of the user account used for working in the MQL5 Cloud Network.

Tester agent productivity and the time it spent for a task execution are taken into account when calculating payment amounts. Each tester agent has its productivity index - PR. The higher the CPU productivity, the higher this index and the more calculations an agent can perform per unit time.

Calculation of funds for executed calculations is arranged as follows. Payment for a tester agent having PR=100 is 0.08 USD per hour. One work unit is equal to one quantum that is equivalent to the work of an agent having PR=1 in 1 ms (1 millisecond). Therefore, the cost of one quantum is calculated as follows:

QuantPrice=0.08 USD/(100PR*3,600,000ms)=2.22222E-10 USD

The table below shows the calculations for the work of a single-core agent having PR=100 within 1 hour and 1 month.

Time range | QuantPrice, USD/(PR*ms) | Agent PR | Time, ms | Amount, USD  
---|---|---|---|---  
1 hour | 2.22222E-10 | 100 | 3,600,000 | 0.08  
1 month | 2.22222E-10 | 100 | 2,592,000,000 | 57.60  
  
In addition to the service cost, a fee is charged for the internet traffic transmitted to each agent for task execution. The transmitted data includes the file of the Expert Advisor being tested, its input parameters, environment settings, price data and other service information. The traffic cost is USD 0.00002 per megabyte.
