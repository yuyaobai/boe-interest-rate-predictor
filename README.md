# About this Project  
  
This project is part of the LSE's [DS202W Data Science for Social Scientists](https://lse-dsi.github.io/DS202/2024-2025/winter-term/) course.  

The following is taken from the project's instructions:  
In this part, we'll have a closer look at the setting of Bank of England interest rates! It is the single most important interest rate in the UK and has a wide ranging impact on the economy as a whole. Set too high and the economic activity grinds to halt, unemployment rates increase and the risk of recession/depression increases; set too low and the economy overheats and inflation rates climb too high (risk of walking or even galloping inflation). If you want to learn more about interest rates, you can visit the [Bank of England's page](https://www.bankofengland.co.uk/monetary-policy/the-interest-rate-bank-rate).

The Bank of England sets the interest rates periodically and relies on a number of indicators to do so. For the purpose of this exercise, you'll place yourself in the shoes of a financial analyst and try to predict based on quarterly indicators (i.e indicators in the three months up to the rate setting meeting) whether the interest rates will go up, down or stay the same.

The economic indicators we're looking at are as follows:


<table border="2" class="dataframe">
<colgroup>
  <col style="width: 20%;">
  <col style="width: 60%;">
  <col style="width: 20%;">
</colgroup>
<thead>
<tr>
  <th><span data-qmd="Indicator"></span></th>
  <th><span data-qmd="Meaning"></span></th>
  <th><span data-qmd="Source"></span></th>
</tr>
</thead>
<tbody>
<tr>
<td>
Consumer Confidence Index (CCI)
</td>
<td> <quote>The Consumer confidence index (CCI) is a standardised confidence indicator providing an indication of future developments of households’ consumption and saving.<br/> The index is based upon answers regarding household’s expected financial situation, their sentiment about 
the general economic situation, unemployment and capability of savings. <br/>
An indicator above 100 signals a boost in the consumers’ confidence towards the future economic situation, as a consequence of which they 
are less prone to save, and more inclined to spend money on major purchases in the next 12 months.<br/> Values below 100 indicate a pessimistic attitude towards future developments in the economy, possibly resulting in a tendency to save more and consume less.<br/>
This indicator is measured as an amplitude adjusted index, long-term average = 100. </quote> 
</td>
<td>
[OECD](https://www.oecd.org/en/data/indicators/consumer-confidence-index-cci.html?oecdcontrol-cf46a27224-var1=GBR&oecdcontrol-b2a0dbca4d-var3=1997-01&oecdcontrol-b2a0dbca4d-var4=2024-12)
</td>
</tr>
<tr>
<td>
Consumer Prices Index<br/> including owner occupiers' <br/>housing costs (monthly estimates)
</td>
<td> <quote>CPIH is the most comprehensive measure of inflation. <br/>It extends CPI (consumer price index) to include a measure of the costs associated with owning, maintaining and living in one's own home, known as owner occupiers' housing costs (OOH), along with council tax</quote>
</td>
<td>[UK's Office for National Statistics](https://www.ons.gov.uk/economy/inflationandpriceindices/timeseries/l59c/mm23)</td>
</tr>
<tr>
<td>
GDP (monthly estimates)
</td>
<td>
The GDP is the standard measure of the value added created through the production of goods and services in a country during a certain period.
</td>
<td>
[UK's Office for National Statistics](https://www.ons.gov.uk/economy/grossdomesticproductgdp/datasets/gdpmonthlyestimateuktimeseriesdataset)
</td>
</tr>
<tr>
<td>
Exchange rates
</td>
<td>
We track GBP to EUR and GBP to USD monthly exchange rates
</td>
<td>
[Bank of England](https://www.bankofengland.co.uk/boeapps/database/fromshowcolumns.asp?Travel=NIxIRxSUx&FromSeries=1&ToSeries=50&DAT=RNG&FD=1&FM=Dec&FY=1974&TD=31&TM=Jan&TY=2025&FNY=&CSVF=TT&html.x=46&html.y=35&C=1D1&C=IN3&Filter=N)
</td>
</tr>
<tr>
<td>
10-year gilt yields
</td>
<td>
A 10-year gilt yield refers to the return (or interest rate) that investors receive when they buy a 10-year UK government bond (gilt) and hold it to maturity. It represents the annualized yield that an investor would earn over the bond’s life.
<br/>
Let's break things down further:
<br/><br/>
Government Bonds (or gilts) are issued by the UK government to borrow money. A 10-year gilt means the bond matures in 10 years. The yield is the effective return an investor gets from holding the bond. It’s influenced by:
<ul>
<li> The bond's fixed coupon rate (interest payments).</li>
<li> The market price of the bond (yields move inversely to prices).</li> 
</ul>

Why do gilt yields matter?
<br/>

It’s a key indicator of market expectations for economic growth and inflation.

Rising yields suggest higher borrowing costs and possibly higher interest rates.
Falling yields suggest lower interest rates and a preference for safer assets.

*Example:*

If the UK 10-year gilt yield is 4%, it means that, on average, investors demand a 4% annual return over the next 10 years for lending money to the UK government.
If the yield rises to 5%, it means investors require a higher return (possibly due to inflation fears or expectations of higher interest rates).
</td>
<td>
[Federal Reserve Bank of St-Louis](https://fred.stlouisfed.org/series/IRLTLT01GBM156N#)
</td>
</tr>
<tr>
<td>
Unemployment rate <br/>(aged 16 and over, seasonally adjusted): %
</td>
<td>
<quote>Unemployment measures people without a job who have been actively seeking work within the last four weeks and are available to start work within the next two weeks.<br/> The unemployment rate is not the proportion of the total population who are unemployed. <br/>It is the proportion of the economically active population (people in work and those seeking and available to work) who are unemployed.
</quote>
</td>
<td>
[UK's Office for National Statistics](https://www.ons.gov.uk/employmentandlabourmarket/peoplenotinwork/unemployment/timeseries/mgsx/lms/)
</td>
</tr>
</tbody>
</table>

<br/>

These indicators are contained in a first separate dataset (the economic indicators dataset that you can download below) and are recorded for every month from 01/01/1997 to 01/11/2024.

Aside from these indicators, you have a second (separate) dataset (obtained from the [Bank of England](https://www.bankofengland.co.uk/boeapps/database/Bank-Rate.asp)) the records the Bank Rates i.e base interest rates set by the Bank from 06/05/1997 to 06/02/2025 (it also contains a variable `rate_change` that indicates whether the interest rate went down (value -1), went up (value 1) or stayed the same (value 0) compared to the previous rate setting event).

# 📋 Your Tasks
1. Before you do any classification, you'll need to do a bit of data processing:
   
   - Download the Bank of England interest rates dataset and load it into a dataframe called `df`. Carefully inspect the dataset and check that rate setting events occur every once in a while. 
   - Now download the economic indicators dataset into another dataframe: your task is to assign to each row of `df` values of economic indicators from the last quarter i.e the average of each indicator for the last three months up to the date of the rate setting event. For e.g, if the rate setting event is on 06/05/1997, you will to average data for GDP for May 1997, April 1997 and March 1997 and do the same separately for the other indicators i.e exchange rates, 10-year gilt yield, unemployment rates, CPIH and CCI.

2. Create a baseline logistic regression model:
   
   - Split your data in training and test set (70% of the years for training set - be careful with the ordering!)
   - Use whatever metric you feel is most apt for this task to evaluate your model's performance. Explain why you chose this metric.
   - Explain what the regression coefficients mean in the context of this problem.

3. Now is your time to shine once again ! Come up with your own feature selection, feature engineering and/or model selection strategy and try to get a better model performance than you had before.
Don't forget to validate your results using the appropriate resampling techniques!
<br/> Whatever you do, this is what we expect from you:

   - Show us your code and your model.

   - Explain your choices (of feature engineering, model selection or resampling strategy)

   - Evaluate your model's performance. If you created a new model, compare it to the baseline model. If you performed a more robust resampling, compare it to the single train-test split you did in the previous question.
