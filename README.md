# RSI versus SMA

This code is a custom indicator that calculates and plots the Relative Strength Index (RSI) and Simple Moving Average (SMA) on a chart. It is used to analyze market trends and make trading decisions.

## Indicator Initialization

The indicator initialization function is called `OnInit()`. In this function, we set up the indicator buffers and plots. The RSI and SMA buffers are defined as arrays:

```
double RSI_Buffer[];
double SMA_Buffer[];
```

We then set the indicator buffers using the `SetIndexBuffer` function:

```
SetIndexBuffer(0, RSI_Buffer);
SetIndexBuffer(1, SMA_Buffer);
```

Next, we create the indicator plots using the `PlotIndexSetDouble` and `PlotIndexSetString` functions. The `PLOT_EMPTY_VALUE` and `EMPTY_VALUE` constants are used to set the initial values of the plots:

```
PlotIndexSetDouble(0, PLOT_EMPTY_VALUE, EMPTY_VALUE);
PlotIndexSetDouble(1, PLOT_EMPTY_VALUE, EMPTY_VALUE);

PlotIndexSetString(0, PLOT_LABEL, 'RSI');
PlotIndexSetString(1, PLOT_LABEL, 'SMA');
```

The function returns `INIT_SUCCEEDED` to indicate that initialization was successful.

## Indicator Calculation

The indicator calculation function is called `OnCalculate()`. In this function, we calculate the RSI and SMA values.

First, we set the `ArraySetAsSeries` flag to `true` for the `close` array to ensure that the close prices are processed in reverse order:

```
ArraySetAsSeries(close, true);
```

We then calculate the RSI using the `iRSI` function and copy the calculated values to the `RSI_Buffer`:

```
int rsi_calculated = iRSI(Symbol(), PERIOD_CURRENT, 14, PRICE_CLOSE, prev_calculated);
ArrayCopy(RSI_Buffer, close, 0, prev_calculated, rates_total);
```

Next, we set the `ArraySetAsSeries` flag back to `false` for the `close` array to process the close prices in the normal order:

```
ArraySetAsSeries(close, false);
```

We calculate the SMA using the `iMA` function and copy the calculated values to the `SMA_Buffer`:

```
int sma_calculated = iMA(Symbol(), PERIOD_CURRENT, 20, 0, MODE_SMA, PRICE_CLOSE, prev_calculated);
ArrayCopy(SMA_Buffer, close, 0, prev_calculated, rates_total);
```

Finally, we return the total number of calculated bars.

## Product Description

The RSI versus SMA indicator combines the Relative Strength Index (RSI) and Simple Moving Average (SMA) to provide insights into market trends and potential trading opportunities. The RSI is a momentum oscillator that measures the speed and change of price movements, while the SMA is a trend-following indicator that smooths out price data.

By using this indicator, traders can identify overbought and oversold conditions in the market, as well as potential trend reversals. The RSI can indicate when a currency pair is overbought (above 70) or oversold (below 30), while the SMA can help confirm the direction of the trend.

This code is a sample implementation of the RSI versus SMA indicator and can be used as a reference for developing your own trading software. Please note that ForexRobotEasy is not the official developer of this product. To find the official developer and access detailed reviews and trading results, please visit [ForexRoboteasy.com](https://forexroboteasy.com/forex-robot-review/rsi-vs-sma-forex-software-unbiased-review-download-guide/).

For more information and to download the official version of this product, please refer to the MQL5 platform.
