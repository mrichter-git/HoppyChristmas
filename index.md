 
As a small brewery, it's important to stay up to date on the latest trends in the beer industry. One way to do this is by analyzing reviews from websites like BeerAdvocate and RateBeers, where beer enthusiasts share their thoughts on different types of beers. Our brewery is curious to know what makes a beer trendy at a certain period of the year and if it will be trendy the following years. In particular, we are interested in finding out which types of beers would be best suited for a winter beer release and more specifically for a Christmas beer release. We would also like to understand what goes into making such a beer: what are the most desired features and typical characteristics of a winter beer? Finally, the brewery seeks to discover how much this new perfect Christmas beer will be consumed relatively to other beers.

# Which beers are seasonal ?
The first step to grasping what makes a good christmas beer is to actually find some christmas beers. As a starting hypothesis, we assumed that the temporal density of reviews of a beer is a good proxy for it's popularity: a beer that is reviewed a lot around Christmas and nearly not during summer is considered to be a Christmas beer. Based on this, beers were grouped by their type (IPA, Stout, Belgian ...) and the reviews of each day were counted. From this, we obtained some beers with particular trends:

We can typically see how certain events influence a beer's popularity (St. Patrick's day for the irish stout and Christmas / New Year's Eve for the Winter Warmer) :
<p align="middle">
 <img src="images/irish_stout_popularity.jpeg" width="400"/>
 <img src="images/winter_warmer_popularity.jpeg" width="400"/>
</p>

> Maybe also a steady beer e.g. IPA
> Talk about why this can tell us which beers have seasonality
 
In order to really select the beer that were the most seasonal, we gave the seasonality a rating. By decomposing the review count per day, we could isolate the trend of the beer, it's seasonality score and how much our model was off. Through this analysis, some beer types were found to display strong seasonal trendiness. The *Irish Stout* is a great example. We expect it to be mainly consumed around St. Patrick's day (17 March). 

{% include irish_stout_decompose.html %}

As we can see from the graph above, the review density peak lies exactly in March each year. By separating the overall popularity (Trend) from a periodic signal (Seasonality), The peaks in popularity are even more visible. Even a beer that had a very successful couple of years will be picked up by this decomposition.

The same decomposition is also valid on individual beers, given that they have enough reviews. Here we look at the *Délirium Noël*. As the name suggests, the expected popularity peak is around Christmas.

{% include delirium_seasonal_decomp.html %}

Again, we see what was expected: a peak around December. Since this beer is probably only available around Christmas, this result is not surprising. Nonetheless, the cause of the popularity surge doesn't matter. If the beer is available all year or if it is only available at Christmas, it remains a holiday season beer. Therefore the hypothesis of using a beer review density as popularity stands.   

> Insert bar plot with seasonality
> a
> a
> Allow to interact with it, maybe give a description of the beers when clicked on

# Of these seasonal beers, which ones are good?
Once the beers that display a trend around december are selected, we want to know which ones are overall appreciated. Relying solely on the rating isn't enough: some people give strict ratings but very positive written reviews and vice-versa. To remedy to this issue, natural language processing (NLP) methods were used. We could then qualify the reviews based on if they were considered positive or negative. By simply counting how much a word appears in the reviews, we can find the most prevalent words to describe categories of beers. First of all, the overall most used words to describe beers were found. To be able to capture the most common words for the winter beers, the most common words overall were removed.

> insert word cloud with positive vs negative words
> Talk a bit about the words that came out and what it intuitively has to do with positive/negative beers

By using the Winter beers selected by the seasonality analysis, we get these most occurring words

> insert word cloud with positive vs negative words for winter beers
> Talk a bit about the words that came out and what it intuitively has to do with winter beers, maybe compare with the same set of graphs for summer beers

# How to make a good winter beer?
Now that we know which beers are popular in winter and that we know which of these beers have received a good review, we can extract features from these reviews. These features can be properties of the beer such as flavour notes, color or even the bottle itself. This consists of finding the adjectives attached to each feature that we are trying to study. Since we are studying a subset of the reviews of positive reviews trendy in december, the adjectives attaches are expected to describe a positive trait of the beer. We choose to take the 5 features that appear the most often. Then for each feature, we extract again the 5 most recurrent words that describe this features. By normalizing these values to get a percentage of occurrence, the most important characteristics and their most important attributes can be plotted:

For winter time, we get:
{% include winterfile.html %}

We also wanted to know if a characteristics of a good winter beer are also required to make a good summer beer. To do so, the same analysis done to winter beers was also done for summer beers giving:
{% include summerfile.html %}


> Talk about interesting features and most occurring ones

# Conclusion
In light of all the previous findings, beers have a seasonality and they have typical characteristics depending on the season. Certain beers have common features such as the body, the head or the carbonation of the beer. But value features will differ depending on the season. But our first question was to understand what makes a typical christmas beer. Obviously, christmas beers are beers that are consumed during the winter season with typical characteristics such as white foam, dark colors, and not too much carbonation. We can see that there are quite some differences with sumer beers which have characteristics like golden colors, high level of carbonation. 

# Hoppy Christmas and a happy brew year!

<div class="background_beer">
  <h3>Little reminder : if you want to taste a beer :</h3>

  <p align="middle">
    <img src="images/satellite.jpg" width=auto />
  </p>
</div>

<!---
# RENDU 2

## Proposed method of analysis
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


## Beer seasonality analysis
To be able to select a subset of seasonal beers, a trend analysis was conducted. To do so...


## Review sentiment analysis and feature extraction
Once the season beers have been selected, it's important to know which ones are good and which are bad. To do so, we check with the beers that have a good rating and test for positive text reviews. From this it's possible to extract the characteristic

## Regroup, answer the question of title

## Conclude



### Little reminder : if you want to taste a beer :

 <p align="middle">
  <img src="images/satellite.jpg" width="300" />
</p>

### tests

{% include summerfile.html %}
{% include winterfile.html %}
-->
