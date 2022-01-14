# Impact on Inflation due to Covid for US & Canada
# Members: Amandeep Kaur, Hira Binth Naseer , Nedal Mahanweh , Matthew Phan
# Fintech Bootcamp @ UFT

## Message 
Define the core message or hypothesis of the project.
The purpose of this project is to determine and analyze Covid 19 statistics and find correlation with the inflation of
the headline consumer index for US and Canada 
Quantitative analysis methods from Python and Pandas shall be in use for assessing various data sets regarding different Canada and the US with the Headline Consumer index of each country. 

## Requirements
The purpose of this project is to demonstrate data exploration, cleanup , data analysis based on certain questions,
and to engage in visualization using the libraries: PyViz, Panel, PlotExpress, and Hvplot. An additional library is also required
and we chose the library Pygal for additional visualization (bar charts)

Each question & Answer

## Approach
The coding actions include reading and cleaning csv data, visualization, plotting using hvplot, seaborn, plotly, panel, pyviz and pygal
Our team gathered covid cases easily from (https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data9)
We had covid info from World Bank
Our US information was collected into a CSV file and cleaned (https://www.rateinflation.com/inflation-rate/usa-historical-inflation-rate/)
We noticed that there was lacking 2022 data and some missing 2021 data, so we decided to not do any 2022 analysis
fill in 2021 data from another source. First was to clean the covid cases csv file, and collapse / aggregate Canada and US 
by monthly for analysis. Then Inflation rates for 2021 were cleaned by removing the years before 2019. 
We used help from this source : https://www.pluralsight.com/guides/building-visualizations-with-pygal 

The refined and constructed information shall yield the average covid cases per month, rolling standard standard deviations, averages
and a mean.
 
   Questions: 
   Is there a correlation between rise in covid cases and the headline consumer index for the US and Canada?
   (heatmap, parrallel coordinates, twin plot, plotly)   
   What is the mean of the inflation of canada and us?
   Is there correlation between US and Canada inflation?
   What is the average covid cases per month for USA and Canada?
   What is the STD of each data set? What will it look like plotted? Can these be plotted in a proper scale?
   Twin Plot reference : https://cmdlinetips.com/2019/10/how-to-make-a-plot-with-two-different-y-axis-in-python-with-matplotlib/
   What will inflation and cases look like plotted?
   What does total covid cases and inflation rate look like on a aggregate chart?
   
   During our analysis for this question, we discovered that there is correlation between US inflation and covid cases, and Canada inflation
   and Canada covid cases, however we  also tested to see if there was correlation between US Inflation and Canada inflation which concluded
   to a judgement where there is no relation. This gave us the opportunity to explore further into specific inflation sectors and we intuitively
   decided to examine the Food and Shelter sectors. The Heatmap gives a positive result (high number close to 1) between Food, Shelter, And inflation
   for both countries individually. 
   
  
These questions were asked because of the noticeable price increases the past few years of many categories including consumer, food, and real estate prices.

## Code Snippets & Outputs
```
skel code
# create figure and axis objects with subplots()
std_plot=US_data.rolling(window=7).std()

fig_std,ax_std=plt.subplots()
ax_std.plot(years_months_df["Month & Year"], std_plot["Inflation_US"], marker="o")
ax_std.set_xlabel("Month & Year")
```
![US Inflation STD & Covid Cases STD](/images/2_seperate_axes_1_plot_twinx_.jpg)

```
ax2_std=ax_std.twinx()
# make a plot with different y-axis using second axis object
ax2_std.plot(years_months_df["Month & Year"], std_plot["Covid_Cases_US"],color="blue",marker="d")
ax2_std.set_ylabel("Covid Cases US STD",color="blue",fontsize=14)
plt.show()
# save the plot as a file
fig_std.savefig('2_seperate_axes_1_plot_twinx_std.jpg',
            format='jpeg',
            dpi=100,
            bbox_inches='tight')
```
![US Inflation STD & Covid Cases STD Proper Scaled](/images/2_seperate_axes_1_plot_twinx_std.jpg)
```
# Line chart for US covid cases 
create_line_chart(avg_covid_cases["Covid_Cases_US"],
                  title="Average covid cases for USA ",
                 ylabel="AVG covid cases for US", xlabel="year",color="blue")
# Line chart for CANADA COVID CASES
create_line_chart(avg_covid_cases["Covid_Cases_CA"],
                  title="Average Covid Cases for Canada ",
                 ylabel="avg covid cases for Canada ", xlabel="year",color="orange")
                 

```
![Average Cases both US & Canada Seperate](/images/avg%20covide%20cases%20for%20CA%20and%20US.png)

```

# creating object
bar_chart = pygal.Bar()
bar_chart = pygal.HorizontalBar()
# adding range of months from 1 to 12
#bar_chart.x_labels = map(str, range(1,12))
for index,row in combined_df.iterrows():
    #a.append(row["Inflation_US"])
    b.append(row["Covid_Cases_US"])
    c.append(row["Covid_Cases_CA"])
    #d.append(row["Inflation_CA"])
```
![Summary Bar Plot Pygal](/images/bar%20plot%20pygal.png)

```
# Plot data using parallel_coordinates plot
px.parallel_coordinates(correlation)
```
![Correlation Plotly Parallel Coordinates](/images/correlation%20%20for%20combined%20df%202%20.png)
```
## use  heatmap to plot the correlation 
sns.heatmap(correlation) 
```
![Heatmap Correlation Summary](/images/correlation%20%20for%20combined%20df.png)

```
#plotting heatmap based on correlation
sns.heatmap(correlation)
```
![Food, Shelter, Inflation Correlation Canada Heatmap](/images/correlation%201.png)

```
#finding a correlation between covid cases and inflation rate of food and shelter in US
correlation = us_df.corr()
correlation
```
![Food, Shelter, Inflation Correlation US](/images/correlation%20for%20US.png)

```
covid_db.hvplot()
```
![US & Canada Hvplot cases](/images/covid_cases%20in%20CA%20and%20US%20for%20period%20.png)

```
inflation_rate.rolling(window=7).mean().plot(figsize=(20,7))
```
![Rolling Mean For Inflation Canada / US](/images/rolling%20.mean%20for%20combined%20df.png)

```
US_data.rolling(window=7).std().plot(figsize=(10,5), title= "7 day rolling standard deviation for inflation rate and covid cases of Canada")
```
![Rolling STD 7 Day Canada Inflation & Cases](/images/rolling%20std%20for%20CA.png)

```
# create figure and axis objects with subplots()
fig,ax=plt.subplots()
ax.plot(years_months_df["Month & Year"], combined_df["Inflation_US"], marker="o")
ax.set_xlabel("Month & Year")
ax.set_ylabel("Inflation")
```
![Twin Plot US Inflation / Cases (unscaled)](/images/Twin%20Plot%20for%20Inflation%20&%20US%20Cases%20for%20Combined%20DataFram.png)

```
 #create figure and axis objects with subplots()
fig,ax = plt.subplots()
# make a plot
ax.plot(years_months_df["Month & Year"], combined_df["Inflation_US"], marker="o")
# set x-axis label
ax.set_xlabel("Month & Year",fontsize=14)
# set y-axis label
ax.set_ylabel("Inflation US",color="red",fontsize=14)
# twin object for two different y-axis on the sample plot
ax2=ax.twinx()
```
![Twin Plot US Inflation / Cases (proper scale)](/images/twin%20plot.png)
