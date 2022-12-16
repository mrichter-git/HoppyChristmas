# Hoppy Christmas! A guide to christmas beers

## Abstract:
Being a small brewery, we would like to conduct a study on beer trendiness to optimize our production with respect to time. We analyse seasonal trends in beer consumption to know when to release a new one. On top of this we analyse the evolution over time of multiple beer's consumption in order to have the minimum amount of remaining storage after sales. Our goals would be to understand what makes a beer trendy and be able to predict how the beer’s success evolves throughout the year. With this, we could know how much beer to produce at a certain time. In particular, we would like to produce a holiday season beer. To do so we will focus our analyses on the winter season. We would like to know what the typical characteristics of a Christmas beer are and how much people will consume it relatively to other beers.

## Research questions:
* Can we find successful beers during a certain season?
* If yes, what makes a trendy christmas beer? 
  * What characterises them ? Is there a specific flavor which is more appreciated in winter, or does it even have influence in that regard ?
  * Can we find key words, describing what would make a beer successful on winter days e.g. the feeling of warmness it provides ?
  * Are there confounding factors ?
* Can we extend the analysis we made for the Christmas beers to the other ones ?
 
## Methods

### Preprocessing

The data are already quite clean for this dataset: a large portion of data wrangling was already done for us. Also, we do not consider the _./ratings.txt.gz_ files in the BeerAdvocate and RateBeer folders, as they are an unclean version of the _./reviews.txt.gz_ files. 
Firstly, some beers do not provide enough data to be taken into account in our processing. Thus, we filter for beers that have been reviewed for more than two years, and which already have enough feedbacks. The threshold for that is decided based on the distribution of the number of reviews per beer.

To ease the access and the opening speed, we store those data as a pickle file (_.pkl_).

### Feature extraction

Then, by analysing review density of different beers types (e.g. IPA, American Pale Wheat Ale) as a proxy for beer popularity, we select a subset of beers that show a strong seasonnal trend as shown [here](https://towardsdatascience.com/finding-seasonal-trends-in-time-series-data-with-python-ce10c37aa861), in particular for the winter months.

We can typically see how certain events influence a beeer's popularity (St. Patrick's day or Christmas / New Year's Eve for example) :
<p align="middle">
 <img src="images/irish_stout_popularity.jpeg" width="300"/>
 <img src="images/winter_warmer_popularity.jpeg" width="300"/>
</p>


To further study those particular beers, we will take a look at the average grades to analyze how appreciated those popular beers are, along with the feeling experienced by the reviewers, and perform a comparison between the metrics of the seasonal beers and the non-seasonal ones.


### Lexical differences between all beers and winter related beers

 <p align="middle">
  <img src="images/wordmap.jpeg" width="300" />
  <img src="images/winter_wordmap.jpeg" width="300" /> 
</p>

Based on the lexic used to review winter beers, we would like to extract the key features and words describing what makes a beer a successful one during winter period. Should any Natural Language Processing be required, we will conduct a sentiment analysis on these reviews using the _NLTK_ library. This will provide us with the needed tools to investigate how much the user appreciated it.


## Tasks repartition

Data story

| Names                | Tasks |
|-----------------|-------|
| Louis Gounot    | Data story, Features extraction |
| Hugo Delesalle  | Preprocessing, Data visualization |
| Baudouin Bosc   | Sentiment analysis, Data visualization|
| Michael Richter | Seasonal trend analysis, Data story |

## Proposed timeline

19.11 &#8594; 02.12 :
 * Preprocessing
 * Seasonal trend analysis


02.12 &#8594; 16.12 : 
 * Sentiment analysis
 * Start of data story:
   * website creation
   * global structure
 * Features extraction


16.12 &#8594; 21.12 :

  * Data visualization
  * Data story : 
     * write story and connect dots
     * embed graphics

21.12 &#8594; 23.12 - 23h50 :

   * Draw conclusions
   * Clean up code

23.12 - 23h51 &#8594; 23.12 - 23h59 :

  * git commit
  * git push
  * Taste beers
