---
 layout: post
 title: Where are the Cheap Eats?
---


While watching the Cooking Channel, I saw a commercial for a show called [*Cheap Eats*](http://www.cookingchanneltv.com/shows/cheap-eats.html). I was intrigued and found myself on its website. Turns out, it is a lot like [*Diners, Drive-Ins and Dives*](http://www.foodnetwork.com/shows/diners-drive-ins-and-dives.html) where the host goes around to eat good food at restaurants around the country. The premise is that the host, Ali Khan, can only spend up to $35 in a particular city or metro area for breakfast, lunch, a snack, and dinner. Today we will visualize some of the aspects of the show.

The data
--------

I scraped the *Cheap Eats* [website](http://www.cookingchanneltv.com/shows/cheap-eats/cheap-eats-location-guide.page-1.html) to get the locations, food and cost for every episode. So far there are two seasons worth of episodes: seven in the first and thirteen in the second. A total of twenty episodes are currently available. Every episode features a meal from four different restaurants or food trucks in a single city or metro area.

Cities visited
--------------

Let's first take a look where Khan has gone. The seven first season locations are in orange and the thirteen second season locations are in blue.

{: .center}
![]({{ site.baseurl }}/files/cheap-eats/loc-map-1.png)

Unfortunately, Khan has not come to the west coast where I might be able to more easily check out the food/eatery appearing on the show. Nonetheless, there is quite the diversity to where he has been already, including Bozeman, Montana. There are also cities he has featured that are on my personal list of places to visit such as Charleston, Austin, and Boulder (to name a few).

It is interesting to note that he traveled much further in the first season: 8,128 mi vs. 5,515 mi. This becomes more obvious when you notice that most of season two was spent within a ~500 mi radius from Indianapolis. Despite this, the longest trip of the series occurs in season two, when Khan goes from Richmond to Bozeman (Ep. 10).

How cheap is cheap?
-------------------

We can also see how Khan has spent his money on the show. Below is a [violin plot](https://en.wikipedia.org/wiki/Violin_plot) of the cost of a meal versus the time of the meal. These sorts of plots are neat because they also show a measure of the probability density of the data. In this particular version, the black dots represent the actual cost for each meal so that you can see the density a little more clearly. Light green diamonds show the average for each type, while the three thin horizontal green lines show the quartiles. These plots are further divided among the two seasons.

{: .center}
![]({{ site.baseurl }}/files/cheap-eats/violin-cost-1.png)

There is a bit going on here so let's try to dissect this a little. One thing we can notice is that the most different shape between seasons seems to be Lunch. Not only has the average moved (upwards) but so has the standard deviation (downwards). A slightly different method to visualize this is to estimate the meal cost probability density. This can make the comparison between the two seasons easier to discern. That visualization is below where the panels are now the four different meals and the two curves are the two different seasons.

{: .center}
![]({{ site.baseurl }}/files/cheap-eats/pdf-cost-1.png)

It is much easier to see now that Lunch is not the same between the two seasons. One must keep in mind that the first season only has seven data points, with twenty data point in the second season, so these densities really are estimates. In addition to this, we can also apply a two-tailed t-test to compare the cost of a meal between seasons. In the table below is the p-value of each test for the four meal types. Recall a high p-value here suggests a similarity in the two distributions while a low p-value suggests the opposite. The scale of 'low' here is often at the 0.05 level (or 5%) often called the significance level *α*.

| Meal      |  p-value|
|:----------|--------:|
| Breakfast |    0.863|
| Lunch     |    0.290|
| Snack     |    0.975|
| Dinner    |    0.374|

For us then, we can see Lunch is the most dissimilar between seasons. The t-test also suggests that Snack is very similar between seasons. This type of test is not absolute though and should just be another measurement tool. By eye we see that this table makes sense with regards to the previous two plots.

Another way to divide the meal cost data is to look at it episode to episode. The plot below shows this with the top panel showing season one and the bottom panel showing season two.

{: .center}
![]({{ site.baseurl }}/files/cheap-eats/cost_vs_ep-1.png)

The spending per episode is clear here and there are some interesting weeks. I will highlight one here: episode eight of season two. Khan actually spends more on Breakfast than the other three meals while in Indianapolis. All four meals from this episode are listed in tabular form below. His Snack for the episode is also on the more expensive side; but I bet Key Lime Cheesecake is probably worth it!

| Restaurant       | Meal Time | Meal                    |  Cost \[$\]|  Season|  Episode|
|:-----------------|:----------|:------------------------|-----------:|-------:|--------:|
| Milktooth        | Breakfast | Sugar Pearl Waffles     |       10.00|       2|        8|
| Goose the Market | Lunch     | The Batali              |        8.35|       2|        8|
| Ezra’s Café      | Snack     | Key Lime Cheesecake     |        7.00|       2|        8|
| Tie Dye Grill    | Dinner    | Breaded Pork Tenderloin |        7.95|       2|        8|

Part of the premise of the show was of course to limit the total budget of four meals to $35. Let's take a look at how Khan actually did. The x-axis now plots both seasons together, while the y-axis remains the same (Meal Cost). The dotted red line is the budgeted $35 while the solid black line is the actual total per episode.

{: .center}
![]({{ site.baseurl }}/files/cheap-eats/cost_vs_ep_vs_total-1.png)

While Khan is generally able to stay under the limit, he does cross the threshold three times. He also hits $35 exactly on episode six of season two. But he is also able to stay under $30 twice. Overall, he does stick to the self-imposed limit pretty well, since his average per episode food cost is about $33. While that is quite a lot on an everyday per person basis, if this is thought of as a vacation/travel cost, it is actually quite reasonable.

To demonstrate that I think this can be a deal, below is a table of Dinners that are under $10 each. One can see there are six such meals he has ate on the show and the variety is pretty good. Dinner is obviously the most expensive meal to eat out on average, so keeping it cheap while maintaining good taste and flavor can be a steal and make a lot of financial sense.

| Restaurant          | Meal                                       |  Cost \[$\]| City         | State |  Season|  Episode|
|:--------------------|:-------------------------------------------|-----------:|:-------------|:------|-------:|--------:|
| Evangeline Café     | Maw Maw Chicken and Sausage Gumbo          |        8.99| Austin       | TX    |       1|        2|
| Pincho Factory      | Steak Pincho Bowl                          |        9.49| Coral Gables | FL    |       1|        4|
| Mama J’s            | Fried Catfish and Mac and Cheese           |        9.00| Richmond     | VA    |       2|        3|
| Tie Dye Grill       | Breaded Pork Tenderloin                    |        7.95| Indianapolis | IN    |       2|        8|
| Blackstone Meatball | Vegan Meatballs with Spicy Pork Ragu       |        8.00| Omaha        | NE    |       2|       11|
| Dalie’s Smokehouse  | Cranberry Cayenne Chicken with Baked Beans |        9.99| Valley Park  | MO    |       2|       13|

Of course, for any particular person there are many constraints, so mileage will always vary.

Parting thoughts
----------------

Since I have not actually been to any of the locations on the show, I cannot vouch for how the food actually tastes. But if we are to believe Khan's descriptions and portrayal of the food he is eating, the show should really be called *Cheap, but Good, Eats*. I hope to be able to update this post someday when I am able to visit a few of the places Khan has featured on the show and provide some commentary on the alternate show title.
