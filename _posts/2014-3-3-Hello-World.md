---
layout: post
title: Blog Post 1: First Week thoughts + Project Benson
---

## First Week at Metis

My first week at the Metis data science bootcamp in Chicago is in the books, so I thought I would reflect on it briefly. The material for week one was largely review, with an emphasis on working with and understanding the theory of the python language. We were introduced to several useful libraries and python packages including matplotlib, pandas, and numpy. Additionally, we worked with using git for version control. I found the pace to be quick, but manageable, and certainly feel that my familiarity with the basic Data Science toolkit has improved tremendously in just 4 days. 

I have also enjoyed getting to know my classmates and instructors over the first week. There is quite a variety in backgrounds, but everyone is very capable and we all seem to be more or less on the same level with respect to experience. I'm definitely excited about working with this group over the next few months.

##Project Benson

Our first project began on day one and was completed by Friday afternoon. Project benson involved some exploratory data analysis for a hypothetical philanthropic organization looking to optimize recruitment efforts for an event based on New York City MTA subway passenger data. The rest of this post will be dedicated to a breakdown of my team's project approach, and the link to our final report can be found [placeholder.] (www.google.com)

###Problem and Initial Approach
Women Tech Women Yes (WTWY), a non-profit group dedicated to increasing female representation in tech fields, has an upcoming fundraising Gala. The tickets to the event are free, but WTWY wants to target individuals who are likely to join the organization and contribute financially. They would like to leverage MTA subway turnstile data to determine how best to optimize their recruitment resources outside selected subway stations in New York City.

After examining some of the available [data](http://web.mta.info/developers/turnstile.html), our team elected to pursue the acquisition of additional data that would provide more detail on demographics in an effort to stress "quality over quantity" with respect to targeting recruits. We determined that, given the vast scale of the turnstile data, it would be appropriate to first narrow our scope by including additional data sources, namely, demographic information on New York City residents from the US Census.

###Assumptions

The team began with some assumptions, as the information available in the hypothetical problem scenario was rather vague. First, and most importantly, we assume the target individual to be a female working in a tech industry specifically. Second, we assume users of public transport will use subway stations closest to their place of residence. Numerous other minor assumptions were made, and those will be touched on where appropriate.

###Census Data

The census data provided insight into the residential areas, broken down into "tracts", with the highest concentration of women working in "computer, engineering, and science occupations". We looked at this data graphically, and determined a selection of subway stops nearest these tracts to focus on. 

###MTA Data

We elected to use 4 weeks worth of MTA data, roughly 779 thousand data points, from the month of May 2016. This was because the Gala was described as being held in early summer, and thus it seemed prudent to examine an amount of data that would provide a good approximation of commuter patterns for that specific time period.

The MTA data was rather messy, particularly with regard to the turnstile counts, with some stations data affected by the counter resetting or randomly reversing direction and counting in reverse. We developed two arbitrary cleaning methods to address these issues. The first flagged rows with a "Machine Reset" variable for instances where the count differed drastically between successive rows. The second was to filter for any negative values and any values where the count in any 4 hour period exceeded 6000 users. This number was chosen arbitrarily under the assumption that a reasonable upper limit on the capacity of a stile would be roughly 1 user per 2 seconds for a period of four hours.

###Bringing it all together

After cross referencing our results from the investigations of both datasets, we derived a list of the top 5 subway stops to recommend to WTWY for where they should concentrate their recruitment efforts. The list was a weighted ranking sum.

###Additional Ideas Not Pursued due to Time Constraints

We had initially planned to pursue a detailed analysis on the daily fluctuations in subway traffic with respect to time in order to determine the optimum time of day to focus recruitment efforts, however we ultimately ran out of time and were unable to pursue it. We would nonetheless recommend WTWY concentrate their efforts in the evenings during the weekdays, from roughly 4 pm to 8pm, given that it is safe to assume that subway traffic flow roughly correlates with peak commuter hours.

Additionally, as is the case with most projects involving data analysis, some further tidying up of the data may have been helpful.

Finally, while we are confident with the results we obtained from the analysis of census data, we would have liked to include additional demographic information, namely income level and age, to further refine our target group.

###Por Conclure

Project Benson was a fantastic opportunity to get our hands dirty with some real data. It highlighted the usefulness and versatility of the pandas and matplotlib libraries, the importance of using git/github when collaborating on a project, and forced our team to think quantitatively as well as make some subjective decisions. I am pleased with our work and look forward to future projects as I continue to learn the ins and outs of data science.

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.