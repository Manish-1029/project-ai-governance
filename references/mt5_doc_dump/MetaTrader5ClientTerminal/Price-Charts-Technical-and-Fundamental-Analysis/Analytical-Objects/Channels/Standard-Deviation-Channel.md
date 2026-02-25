[🏠 Document Start](../../../README.md) / [Price Charts, Technical and Fundamental Analysis](../../README.md) / [Analytical Objects](../../Analytical-Objects.md) / [Channels](../Channels.md) / Standard Deviation Channel

[Previous](Equidistant-Channel.md) | [Next](Regression-Channel.md)

# Standard Deviation Channel

Standard Deviation Channel is built on base of Linear Regression Trend representing a usual [trendline](../Lines/Trendline.md) built between two points on the price chart using the method of least squares. As a result, this line proves to be the exact median line of the changing price. It can be considered as an equilibrium price line, and any deflection up or down indicates the superactivity of buyers or sellers respectively.

Standard Deviation Channel consists of two parallel lines, equidistant up and down from the Linear Regression Trend. The distance between frame of the channel and regression line equals to the value of the standard deviation of the close price from the regression line. All price changes take place within Standard Deviation Channel, where the lower frame works as support line, and the upper one does as resistance line. Prices usually exceed the channel frames for a short time. If they keep outside of the channel frames for a longer time than usually, it forecasts the possibility of trend turn.

## Drawing

To draw the channel, one should select this object and then click with the left mouse button in the chart. After that holding the mouse button one should draw the channel in the necessary direction and set its length. Additional parameters will be shown near the end point of the trendline of the channel: distance from the initial point along the time axis, distance from the initial point along the price axis.

![Standard Deviation Channel](images/stddev_channel.png)

## Controls

On the trend line of the channel linear regression there are three points that can be moved with the mouse. The first and the last points are used to change the channel length in different directions. The central point (moving point) is used to move a channel in the chart without changing its dimensions.

## Parameters

There are the following parameters of the standard deviation channel:

![Parameters](images/stddev_channel_parameters.png)

  * Date — coordinate on the time scale of the first point of the trend of the channel linear regression.
  * Date — coordinate on the time scale of the last point of the trend of the channel linear regression.
  * Ray Right — infinite duration of the channel to the right;
  * Ray Left — infinite duration of the channel to the left;
  * Fill — enable/disable color filling inside the channel;
  * Deviations — number of standard deviation values for building the channel borders.



Common parameters of object are described in a [separate section (#draw-settings)](../../Analytical-Objects.md#draw-settings).
