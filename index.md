 
As a small brewery, it's important to stay up to date on the latest trends in the beer industry. One way to do this is by analyzing reviews from websites like BeerAdvocate and RateBeers, where beer enthusiasts share their thoughts on different types of beers. Our brewery is curious to know what makes a beer trendy at a certain period of the year and if it will be trendy the following years. In particular, we are interested in finding out which types of beers would be best suited for a winter beer release and more specifically for a Christmas beer release. We would also like to understand what goes into making such a beer: what are the most desired features and typical characteristics of a winter beer?

Our approach can be separated in three parts that we will explore sequentially during this data-story. Firstly, we seek to find seasonal beers by analyzing the temporal density of the reviews. Then we assess which beers are positively reviewed. Moreover we focus on deconstructing the reviews to grasp the key characteristics, such as flavour or color. Finally, we examine what positive attributes each characteristic has, e.g. a nutty attribute for the flavor characteristic. After all these steps, we could find what makes the best data-driven Christmas beer.

# Which beers are seasonal ?
The first step to grasping what makes a good christmas beer is to actually find some christmas beers. As a starting hypothesis, we assumed that the temporal density of reviews of a beer is a good proxy for it's popularity: a beer that is reviewed a lot around Christmas and nearly not during summer is considered to be a Christmas beer. Based on this, beers were grouped by their type (IPA, Stout, Belgian ...) and the reviews of each day were counted. By simply plotting this through time, we can't extract much meaningful information.

<p align="middle">
 <img src="images/reviews_time.jpg" width=auto/>
</p>

However, in the optic of reducing the effect of the yearly increase in popularity, we can sum the reviews per day of the year over it's whole lifespan. With this we start to observe a trend that is exhibited for some beers such as stouts. They are more popular in march because of St. Patrick's day. Still it is quite challenging to uncover quantitative information from these values.

<p align="middle">
 <img src="images/grouped_reviews.jpg" width=auto/>
</p>
 
In order to really select the beer that were the most seasonal, we gave the seasonality a rating. By decomposing the review count per day, we could isolate the trend of the beer, it's seasonality score and how much our model was off. Through this analysis, some beer types were found to display strong seasonal trendiness. The *Irish Stout* is a great example. We expect it to be mainly consumed around St. Patrick's day (17 March). 

{% include irish_stout_decompose.html %}

As we can see from the graph above, the review density peak lies exactly in March each year. By separating the overall popularity (Trend) from a periodic signal (Seasonality), The peaks in popularity are even more visible. Even a beer that had a very successful couple of years will be picked up by this decomposition.

The same decomposition is also valid on individual beers, given that they have enough reviews. Here we look at the *Délirium Noël*. As the name suggests, the expected popularity peak is around Christmas.

{% include delirium_seasonal_decomp.html %}

Again, we see what was expected: a peak around December. Since this beer is probably only available around Christmas, this result is not surprising. Nonetheless, the cause of the popularity surge doesn't matter. If the beer is available all year or if it is only available at Christmas, it remains a holiday season beer. Therefore the hypothesis of using a beer review density as popularity stands.   

Knowing this, we could do the decomposition for every beer type on the websites RateBeer and BeerAdvocate to find the beers with the highest seasonality. For Christmas, we looked at the beers that had a high seasonality coefficient value in the winter months and we obtained the following beers: 
<p align="middle">
 <img src="images/winter_bar.jpg" width=auto/>
</p>

The beers found correspond to our expectations with most having a reference to Christmas or to Winter in their titles.
By looking at the beers that have their seasonality peak in summer, we can also find some summer beers:
<p align="middle">
 <img src="images/summer_bar.jpg" width=auto/>
</p>

# Of these seasonal beers, which ones are good?
Once the beers that display a trend around december are selected, we want to know which ones are overall appreciated. Relying solely on the rating isn't enough: some people give strict ratings but very positive written reviews and vice-versa. To remedy to this issue, natural language processing (NLP) methods were used. We could then qualify the reviews based on if they were considered positive or negative. By simply counting how much a word appears in the reviews, we can find the most prevalent words to describe categories of beers. First of all, the overall most used words to describe beers were found. To be able to capture the most common words for the winter beers, the most common words overall were removed.

<p align="middle">
 <img src="images/all_WC.jpg" height = "400" style="margin: 0px 0px 5px 5px;"  />
 <img src="images/winter_WC.jpg" height = "400" style="margin: 0px 0px 5px 5px;" />
 <img src="images/summer_WC.jpg" height = "400" style="margin: 0px 0px 5px 5px;" />
</p>

On the image on the left, we can find the most common words used to describe the beers of the dataset. Not surprisingly, some words like *"beer"* or *"flavour"* appear very often in the reviews. Therefore, once removed, we should obtain a good idea of the winter beer words in the middle and the summer beer words on the right. In the winter beers, we find a lot of words that describe the beer characteristics and aren't very useful, such as *"taste"* or *"aroma"*. Nonetheless, we get some interesting attributes that appear like *"spice"*, *"Fruits"* or *"Cinnamon"*. The same idea can be done for the summer beers. Some interesting words are *"banana"*, *"citrus"* or again *"spice"*.

# What makes a good winter beer?
Now that we know which beers are popular in winter and that we know which of these beers have received a good review, we can extract features from these reviews. These features can be properties of the beer such as flavour notes, color or even the bottle itself. This consists of finding the adjectives attached to each feature that we are trying to study. Since we are studying a subset of the reviews of positive reviews trendy in december, the adjectives attaches are expected to describe a positive trait of the beer. We choose to take the 5 features that appear the most often. Then for each feature, we extract again the 5 most recurrent words that describe this features. By normalizing these values to get a percentage of occurrence, the most important characteristics and their most important attributes can be plotted:

For winter time, we get:
{% include winterfilewoslider.html %}
{% include winterfile.html %}

We also wanted to know if a characteristics of a good winter beer are also required to make a good summer beer. To do so, the same analysis done to winter beers was also done for summer beers giving:
{% include summerfilewoslider.html %}
{% include summerfile.html %}

<h4>Definitions:</h4>
Head
: The head of a beer refers to the foam that forms at the top of a glass of beer when it is poured. The head is made up of small bubbles of carbon dioxide and is usually creamy or white in color. The head of a beer is an important part of the overall appearance of the beer and can affect the flavor and mouthfeel of the beer when it is consumed.

Color
: The color of a beer is determined by the types and amounts of grains, hops, and other ingredients used in the brewing process, as well as the method of brewing and fermentation. Beers can range in color from pale straw or yellow, to amber, red, brown, or black.

Carbonation
: Carbonation in beer refers to the presence of dissolved carbon dioxide gas in the liquid. Carbon dioxide is a natural byproduct of the fermentation process that occurs during the production of beer. The level of carbonation in a beer can affect its flavor, aroma, and mouthfeel.

Lacing
: Beer lacing refers to the pattern of foam or head that forms on the inside of a glass of beer as it is consumed. As a person drinks a beer, the foam on the surface of the liquid will leave behind a series of rings or streaks on the inside of the glass. Beer lacing is often considered a desirable quality in a beer, as it can be an indication of the beer's freshness and quality.

Body
: The body of a beer refers to the fullness, thickness, or mouthfeel of the liquid when it is consumed. The body of a beer can range from light and thin, to full and rich. The body of a beer is influenced by a variety of factors, including the types and amounts of grains and hops used in the brewing process, the method of brewing and fermentation, and the level of carbonation.


# How can we make the perfect Christmas beer?
With this, we can start to answer the initial question: How do we make this perfect christmas beer? Intuitively, it is possible to choose some Christmassy attributes. One would assume a cinnamon flavoured beer would suit a Christmas beer. By looking at the word clouds, these intuitions can be confirmed or not. But giving Christmassy tastes to the beer won't always make it popular. To know what the most popular beer attributes are, we need to look at the radar plots. We see that some of the attributes are shared between winter and summer beers, but we can nonetheless define a good christmas beer.  

<div class="containerwin">
  <div class="textboxwin">
    <p><b>The best Winter Beer</b></p>
    <p>Head: White </p>
    <p>Color: Brown </p>
    <p>Carbonation: Medium </p>
    <p>Lacing: Nice/Good </p>
    <p>Body: Medium </p>

  </div>
  <div class="borderboxwin">
    <div class="glasswin"> 
      <div class="innerwin">
        {% for i in (1..8) %}
          <div class="bubble"></div>
        {% endfor %}
      </div>
    </div>
  </div>
</div>

The same applies for a good summer beer:

<div class="container">
  <div class="textbox">
    <p><b>The best Summer Beer</b></p>
    <p>Head: White </p>
    <p>Color: Golden/Yellow </p>
    <p>Carbonation: High </p>
    <p>Lacing: Nice/Good </p>
    <p>Body: Medium </p>

</div>
  <div class="borderbox">
    <div class="glass"> 
      <div class="inner">
        {% for i in (1..36) %}
          <div class="bubble"></div>
        {% endfor %}
      </div>
    </div>
  </div>
</div>

While it also depends on glass cleanliness, a good lacing is more likely for a beer with higher ABV (alcohol content) and a richer body. Further, a richer body is more prone to happen when the carbonation of the beer is lower. Body also has an influence on the color of the beer. In fact, all of these characteristics are confounded. Even while knowing the best characteristics for the perfect winter beer, brewing is an art that is hard to master. A lot of trial and error goes into getting to the perfect Christmas beer. Nonetheless, knowing what to aim for while doing these trials is the first part of the process.

# Conclusion
In light of all the previous findings, some beers are seasonal and have typical characteristics depending on the season. Certain beers have common features such as the body, the head or the carbonation of the beer. But value features will differ depending on the season. But our first question was to understand what makes a typical christmas beer. Obviously, christmas beers are beers that are consumed during the winter season with typical characteristics such as white foam, dark colors, and not too much carbonation. We can see that there are quite some differences with summer beers which have characteristics like golden colors, high level of carbonation. 

We found however that knowing what beer to make is only the first part of the analysis. As each characteristic depend on each other, experience in beer making is still necessary to brew the perfect beer. But by knowing the direction in which to go, an outline of a recipe can be given:

> Grains: To achieve a brown color, you will want to use darker-colored grains such as caramel malt, chocolate malt, or black malt. These grains will also contribute to the body and flavor of the beer. You can also use lighter-colored grains such as pale malt or pilsner malt to balance the color and provide a crisp, refreshing flavor.
>
> Hops: Hops can contribute to the aroma and flavor of the beer, as well as the level of bitterness. Choose hops that will complement the flavor and aroma of the darker grains and contribute to the overall balance of the beer.
>
> Fermentation: The level of carbonation in the finished beer will be determined by the amount of carbon dioxide produced during fermentation. To achieve a medium level of carbonation, you will want to carefully control the fermentation process to produce the desired amount of carbon dioxide.
>
> Head retention: The appearance and stability of the head on the beer will be influenced by the types and amounts of proteins and sugars in the wort, as well as the pouring technique. To achieve a white head with good lacing, you will want to pay attention to these factors and adjust as needed.

# Hoppy Christmas and happy brew year!

<div class="background_beer">
  <h3>If you are looking for us, we'll be increasing our experience in beers:</h3>

  <p align="middle">
    <img src="images/satellite.jpg" width=auto style="padding: 0px 40px 0px 40px;" />
  </p>
</div>

