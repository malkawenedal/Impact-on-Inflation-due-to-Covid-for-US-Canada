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
   It has been observed that the Covid cases in US have more effect on the US Shelter inflation variable in comparison to covid cases in 
   Canada. Heat maps and these were chosen as a more deteremined visualization of showing correlation between specific shelters
   that have inflated during covid times
   
   Is there correlation between US and Canada inflation?.
   There is a direct correlation between inflation and Covid cases. A spike is observed in Q4 
   of 2020 following to Q1 of 2021 (this may be representing the second WAVE OF Covid).
   During our data exploration where we used the consumer headline index of inflation in general, there was correlation but not as strong
   with correlation between us and canada 

   What is the average covid cases per month for USA and Canada?
   Even though the population of US is exponentially larger than Canada, the average cases in both countries have raised at almost an equivalent rate as 
   observed by the line graphs 

   What is the STD of each data set? What will it look like plotted? Can these be plotted in a proper scale?
   the standard deviation chart is not properly scaled and due to time constraints this is the initial chart this other chart here is what it could look like but it has a 
   reverse index and without time constraint it could be fixed it looks different than the twin plots earlier but showing deviation the meeting points are still similar and show 
   different times of different waves 
   Twin Plot reference : https://cmdlinetips.com/2019/10/how-to-make-a-plot-with-two-different-y-axis-in-python-with-matplotlib/
   What will inflation and cases look like plotted?
   What does total covid cases and inflation rate look like on a aggregate chart?
   
   During our analysis for this question, we discovered that there is correlation between US inflation and covid cases, and Canada inflation
   and Canada covid cases, however we  also tested to see if there was correlation between US Inflation and Canada inflation which concluded
   to a judgement where there is no relation. This gave us the opportunity to explore further into specific inflation sectors and we intuitively
   decided to examine the Food and Shelter sectors. The Heatmap gives a positive result (high number close to 1) between Food, Shelter, And inflation
   for both countries individually. 
   The purpose of this project is to determine and analyse Covid 19 
statistics and final correlation with the inflation of the consumer index 
for US and Canada.
•Quantitative analysis methods from Python, Pandas & other data 
visualization libraries used for assessing various data sets and determine 
the correlation between inflation & covid cases
Covid cases dataset – the data was extracted for the 
two countries only from the 
global_time_series_data_set. It was cleaned to check for 
null values and renaming the columns.
•Inflation dataset – the data was extracted from World 
Bank for US and from statcan website for Canada. The 
extremely detailed dataset was extracted to display 
only the consumer price index. For further analysis; food 
& shelter component of the inflation was pulled, 
renamed and merged with the covid dataset using 
pandas.
  
These questions were asked because of the noticeable price increases the past few years of many categories including consumer, food, and real estate prices.

## Code Snippets & Outputs

There are 4 Jupyter Notebooks for this project:
File 1: US& CA inflation and covid cases analysis.ipynb
This file loads and cleans the csv files US&CA Dataset.csv , covid19_confirmed_cases_US_CA.csv , food_shelter_CA_US.csv, into Pandas Dataframes. Column names
are renamed for organization, nulls are checked to be sure there aren't too many, and data types are checked to see the data sets are matching for plotting and analysis.

Then Hvplot is used for visualizing covid cases for US & Canada
```
covid_db.hvplot()
```
![US & Canada Hvplot cases](/images/covid_Us_cases.png)
![US & Canada Hvplot cases](/images/covid_cases_ca.png)

```
# create figure and axis objects with subplots()
std_plot=US_data.rolling(window=7).std()

fig_std,ax_std=plt.subplots()
ax_std.plot(years_months_df["Month & Year"], std_plot["Inflation_US"], marker="o")
ax_std.set_xlabel("Month & Year")
```
![US Inflation STD & Covid Cases STD](/images/2_seperate_axes_1_plot_twinx_.jpg)
![Canada Inflation STD & Covid Cases STD](/images/ca_twin.png)
```
# Create panels to structure the layout of the dashboard
geo_column = pn.Column(
    "## Total number of COVID Cses in US & Canada", covid_db.hvplot(),
    px.parallel_categories(
    combined_df,
    dimensions=["Inflation_CA","Covid_Cases_CA"],
    color="Inflation_CA",
),
    #  Plot  US data  in combined Dataframe using parallel_categories plot
px.parallel_categories(
    combined_df,
    dimensions=["Inflation_US","Covid_Cases_US"],
    color="Inflation_US",
)
)
```
![Dashboard](/images/dashboard_1.png)

![Food & Shelter US](/images/bokeh_plot-2.png)

![Food & Shelter Canada](/images/bokeh_plot.png)
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
![Average Cases both US & Canada Seperate](/images/avgs.png)

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
