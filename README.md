# Kickstarter Analysis using Excel  
#### by Justin R. Papreck
---

## Overview
  In this analysis using Excel, a client is preparing to start a kickstarter campaign for a play, *Fever*, and wants to determine the ideal time and goal for the campaign. The dataset of over 4000 kickstarter campaigns is analyzed, looking at successful, canceled, and failed outcomes by month of initiation and initial fundraising goals set for campaigns associated with plays and theater. A total of 1369 Theater events were evaluated by month, and the subcategory plays, within theater events, evaluated 1047 kickstarter events. 
  
### Purpose
  The purpose of this analysis is to evaluate the best outcomes for future campaigns. By evaluating the timing of release, if there are months during the year that are significantly more successful or significantly less successful, more or fewer campaigns can be initiated during those times of year. Similarly, the goal set to raise in each campaign gives insight as to ranges that may be ideal. By looking at the percentages of successful compared to those that were canceled or failed, it can be determined which goal ranges will yield the best or worst results, to either pursue or avoid, respectively.

---
## Analysis and Challenges
### Analysis of Outcomes Based on Launch Date
  In analyzing the parent category of Theater events, which includes plays, television, music, documentaries, games, and other subcategories, the pattern of successful, failed, and canceled events were evaluated by the month of launch of the campaign. To sort the campaigns by year in a Pivot table, the YEAR() function was applied to the Date Created Conversion, which read the raw data for the launched_at column: 
  
 Drawing from Column J, "launched_at", which was represented as "1447174261", I applied the function
 ```
 =((J522/3600)/24)+DATE(1970, 1, 1)
 ```
  to convert this to a date in MM/DD/YYYY format. This was followed by the creation of another "Year" column, to which the forumula
  ```
  =YEAR(S522)
  ```
  was applied. From here, I created a pivot table filtering *Years, Parent Category*, and *Subcategory*, setting *outcomes* as the columns, *Date Created Conversion* to rows, and *Count of outcomes* as the values. This was made into a line graph, looking at the month of campaign and count of outcomes.  
  
![Theater_Outcomes_Pivot Table](https://user-images.githubusercontent.com/33167541/170137386-5728c02f-d7a2-47ea-92ac-9329b4c6780c.png)
  
  As can be seen in Figure 1, *Theater Oucomes Based on Launch Date"*, the months of January, February, March, April, August, September, and October had between 54 and 72 successful campaigns. The only month that had a significantly lower number of successful campaigns was December. December was the only month in the dataset that had nearly as many failed campaigns as successful campaigns. During May, June, and July the number of successful campaigns were 111, 100, and 87, respectively, while the number of failed campaigns remained between 31 and 52 throughtout the entire year. The number of canceled events was highest in January, with only 7 canceled. The rest of the year yielded 4 or fewer each month. 

![Theater_Outcomes_Based_vs_Launch](https://user-images.githubusercontent.com/33167541/170137427-93f8e69f-3e4a-484a-a4eb-db0cc0375aba.png)

  Based on these data, the best time of year to initiate campaigns is clearly starting in May and through the summer months. Launching a campaign in December should be avoided, as the number of successful cmapaigns drops below the number of failed and canceled campaigns, something that did not happen in any other month. 
  
  Because the following analysis only focuses on plays, a filter was added to the Theater Outcomes Based on Launch Date graph and is shown in Figure 2, *"Play Outcomes Based on Launch Date"*. There were no canceled events within the plays, but the pattern remains the same as with overall theater outcomes with the subtle difference that there were actually more failed theater events in December than successful events. 

![Play_Outcomes_Based_vs_Launch](https://user-images.githubusercontent.com/33167541/170137452-4233a548-3f97-483a-97ec-d0a8a8d2eb75.png)

### Analaysis of Outcomes Based on Goals
  To analyze the outcomes based on goals, the range of goals were separated into bins starting with campaigns under $1000, and then from $5000 onward in bins of $5000 up to $50,000. The goal, outcome, and subcategory were filtered to match the goal's bin, the correct outcome, and to ensure the data is only representing plays. 
  
 For the number of successful outcomes from $10,000 to $14,999, the code used was
 ```
 =COUNTIFS(Goal, ">= 10000", Goal, "<15000", Outcomes, "successful", Subcategory, "plays")
 ```
 Where "Goal" represents the column from the Kickstarted Sheet Goal column, "Outcomes" represents the outcomes column, and "Subcategory" represents the subcategory column. To calculate the total number of projects, 
 ``` 
 =SUM(B5:D5)
 ``` 
 was used in this column. To acquire the percentage of each outcome, the number of that outcome was divided by the total, 
 ```
 =B6/E6
 ```
 and then formatted as *Percentage*, from the Number representation table. 
  
  There were a broad range of goals set for each kickstarter campaign, from less than $1000 to greater than $50000, and it is not surprising that some of the ranges yielded more successes than failures as well as the converse. In Figure 3, *"Outcomes Based on Goal"*, the first thing of note is that there were no canceled play campaigns, so the line representing cancelations is simply zero throughout, which makes it much easier to interpret the successes versus unsuccessful campaigns. Up to the campaign goals of $15,000, there was a higher percentage of successful campaigns than failed campaigns, but this was declining as the dollar amount increased. From $20,000 to $30,000 the percentage of failed was substantially higher than that of the successful campaigns. Somewhere between $30,000 and $45,000, there was a drastic change, with a high percentage of successful campaigns, and then above $45,000 almost all of the campaigns failed. 
  
![Outcomes_vs_Goals](https://user-images.githubusercontent.com/33167541/170137473-63c9eb73-7bd2-4845-9a85-747933f13932.png)
  While this graphic representation suggests that there is a "sweet spot" somewhere between $30k and $45k, the representation can be misleading, because this represents only 9 projects total. Even more misleading is that 100% of campaigns at $45k failed, but this is true only because there was only 1 campaign with that goal compared to the 16 above $50k - still suggesting that the campaigns higher than $45k should be avoided.
  
### Challenges and Difficulties Encountered  
  The aspect of the project that I encountered to be difficult were in the formatting of the months in the Pivot Table - the default seemed to break the date into years and quarters, and was not completely intuitive as to how to extract years. After recreating the table a few times, it became clear. Another challenge was in the use of the COUNTIFS() function. In other programming I'm familiar with, using logicals doesn't typically use quotations around the logical statement, so Excel was giving an error message. After watching the Hint video, it became clear that the quotation marks were the issue I was encountering. 
  As far as interpreting the data - it is obvious that with the presentation of these graphs, the picture alone does not tell the story of what is happening, and the understanding of the numbers and the data at the individual points along with the graphs are necessary - something that the client will not want to look at, hence the need for this report. :smile:


---

## Results
- With regard to the start date, we can conclude that there is a much higher chance of launching successful campaigns between May and June, though there were still more successes than failures or cancelations during the other months of the year with the exception of December. The second conclusion made from this analysis was that December is the only month that should be completely avoided in launching a campaign as there were more unsuccessful campaigns than successful during that month.  

- Regarding the outcomes based on set goals, there are a lot of data supporting that campaigns under $15000 had a higher percentage of successful events. Additionally, there was a range between $30k and $45k that did yield more successes than failures. Some of the most extreme points on the graph are artifically inflated due to a lack of data points, which is seen in several of the bins greater than $15k, since these represent fewer than 10% of all campaigns launched. Some of this can be remedied by expanding the bins from $5,000 ranges to $10,000 from $20k onward, though that has issues of its own.  By increasing the number of smaller campaigns, there is a higher chance that the goals will be met, however the data aound $35k-$40k should not be ignored and further explored.

- One limitation of this particular dataset is that we are ignoring what countries the campaigns were launched in. There is the opportunity to really narrow down the potential places that the client will be considering launching the campaign, but it may be pointless if the play won't be available in that country, or even in the language spoken there. This will really impact the results if the plays recorded in the data in Italy  were in Italian as opposed to English, as the contributors to such a campaign will be greatly influences such as someone launching a kickstarter for a play in Italian to be launched in the United States will be less likely to be successful than a play in English. 
- Another limitation is the aforementioned number of collected data points with higher goals. It is not reliable to make conclusions based on 1 to 3 total projects in that goal range. By making larger bins in these ranges, it would be more reliable, though the standard error would also increase. 
- One of the limitations that I addressed in Figure 2 was the application of a filter for only plays, rather than looking at all theater categories. While this may be limiting, it's very unlikely that a kickstarter for a play is going to be successful in the crowds for Metal Concerts or Documentaries, and futher analysis would be needed to see if such correlations actually exist.

- One of the tabeles that I did create, Figure 2, just confirms that the relationship for the subset of Plays within Theater Outcomes shared the same relationship, so as not to make conclusions based on a larger dataset that isn't representative of the subset. A pie chart or histogram along-side the Outcomes Based on Goal would be helpful to see the number of campaigns within each bin, showing the client that the data at any given point will be more or less reliable. A box-plot would be useful to analyze whether any of the campaigns are potential outliers.  
