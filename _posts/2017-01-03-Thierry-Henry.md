---
 layout: post
 title: Thierry Henry's Premier League Career
---


Let's take a look back at part of the storied history of [Thierry Henry](https://en.wikipedia.org/wiki/Thierry_Henry). A former footballer, the French striker has plied his trade at a few clubs over his two decade career. His most extensive spell was at Arsenal Football Club from 1999 to 2007 (with a small stint in 2012) and it was there that he truly made his name. Further biographical details will be spared since they are readily available elsewhere. However it should be noted that Henry stands as one of my favorite players of all-time. His playing for Arsenal, my favorite club, has much to do with that I imagine.

This post is simply a look at the Premier League stats Henry compiled. It should be noted that he played in multiple competitions each year he played for Arsenal (as do most top-level European clubs): the domestic league, European tournaments, and domestic tournaments. This post, for now, will focus exclusively on the domestic league. The reason is just to keep things simple.

Getting data
------------

I got all this data from the sports website, [Statbunker](https://www.statbunker.com/). Using the `rvest` package in R, I scraped the match page for [Henry](https://www.statbunker.com/players/SeasonMatches?player_id=12&comps_type=EPL&dates=-1&comps_id=-1). After some massaging, I got a full breakdown of all Premier League matches Henry ever played in including match results and his personal stats for the match. I initially did not realize it but his per match assist numbers are not quite correct. I cross-referenced as best I could with other sources. While I could show that some of the assist numbers are not right, I could not show what the true numbers are. For that reason, I will not show any assist numbers. It is unfortunate, but it must be done.

The viz
-------

Let's first just take a look at how many matches Henry played, per season.

{: .center}
![]({{ site.baseurl }}/files/henry/starts_subs_season-1.png)

The total matches played is in italics above the bars while the red and gold colors separate matches where he subbed or started. The number inside the bars then represent the numbers of each sub or start (where space is available). Summing all the seasons up we see he made a total of 258 Premier League appearances for Arsenal. The first few things to note is the peak in the middle and the rather small bar at the left end. The peak in the middle shows 37 matches played with none coming off the bunch, unlike other years. It should be noted there are only 38 matches in the league. This means he started in all matches but one in each of those two seasons. The other outlier is t he 2011/2012 season where Henry was actually loaned back to Arsenal for a period of matches in the winter. Here it is clear he was brought back solely to be a spark off the bench. We can see this a bit more clearly if we get the average minutes played in a match, again per season. For our purposes, a soccer match only lasts 90 minutes.

{: .center}
![]({{ site.baseurl }}/files/henry/ave_min_season-1.png)

So Henry was only played around 25 minutes a match in that loan spell from 2012. Taking a look at the other end of the spectrum (at the beginning of his career), we see that he did not average close to a full match. Of the 26 matches started in his first season, 1999/2000, he only completed 13 of them. This is often the case with younger players as they tend to be withdrawn for other players to close out the match

Next, we can look at the critical stat: goals. If his assist numbers were accurate, I would also discuss them here but as I said before, that is not the case so I will not display those stats. Additionally, there does not seem to be more expansive stats per match that I can find such as passes, chances created, etc. But we will look at goals, the things that directly lead to wins (and draws). First, we look at his goals on a per match basis.

{: .center}
![]({{ site.baseurl }}/files/henry/goals_per_match-1.png)

One can see that Henry had 134 appearances with no goals, meaning he registered a goal in about 48% of his matches. His 175 goals were then spread out over the remaining 124 matches. Put another way, he averaged 0.68 goals a match. Transforming these numbers again, he scored a goal every 121 minutes. His goal ratio is actually one of the [best](https://www.premierleague.com/gallery/111326) the Premier League has ever seen. We can also see how well Arsenal performed when he actually did or did not score those goals.

{: .center}
![]({{ site.baseurl }}/files/henry/goals_vs_result-1.png)

This plot shows how many goals Henry had for each match result. As can be expected, a goal correlates rather strongly with a win or draw. Henry clearly had a good goal scoring record. So let's see how he scored over the seasons he was with Arsenal.

{: .center}
![]({{ site.baseurl }}/files/henry/goals_by_season-1.png)

Henry scored quite consistently, having averaged over 20 goals a season (excluding his loan spell). This is further evident in his winning the [Premier League Golden Boot](https://en.wikipedia.org/wiki/Premier_League_Golden_Boot#Winners) (given to the player with the most goals) a record four times. He did this in four out of five seasons from 2001/02 to 2005/06.

### Against all teams

So far, I have looked at his per match and per season stats. But another interesting way to slice the data is to look at it against each club Henry has ever played against. Note that the Premier League has 20 teams with the promotion/relegation system so that Henry has actually faced off against 35 teams. Let's first tackle how Henry has faired against each club, in terms of results.

{: .center}
![]({{ site.baseurl }}/files/henry/results_by_team-1.png)

The distributions of the wins, draws and losses are interesting to see. The red bars indicate losses so reading the graph, Henry lost most often to Manchester United (six matches). In fact United are the only team he holds a losing record against. He is even against a few teams, like Bolton, and holds winning records against all other teams, including Liverpool who he lost to five times in the Premier League. It should be noted he never lost to Tottenham, Arsenal's chief rival.

Turning attention to the final few plots, I take a look at his goals against each team and how often he actually played against them. In both sets of plots, you'll see a few teams highlighted in red: Chelsea, Liverpool, Manchester United, and Tottenham. The first three teams along with Arsenal composed the ["Big Four"](https://en.wikipedia.org/wiki/Premier_League#.22Big_Four.22_dominance_.282000s.29) teams of the Premier League. Alongside Tottenham then, these four teams were Arsenal's main rivals during Henry's time.

First, we can see how many matches and the average minutes played per match are per team. This helps transform the previous plot by adding up all the results to see the total matches Henry has played in. The average minutes per match helps give a sense of how much he actually played. In other words, an average around 90 minutes meant he generally started and did not get substituted off, while a lower average means he was more likely to have been substituted off.

{: .center}
![]({{ site.baseurl }}/files/henry/results_vs_opp-1.png)

Knowing this now, we can see how many goals he scored against every team. Here the absolute goals scored is the left panel, the average per 90 minutes is the center panel, and the average per match is the right panel. The latter two will of course look quite similar since Henry tended to play the full match. But displaying the averages in both these forms is good because it does help dingtuiush the instances when he did not play the full ninety minutes.

{: .center}
![]({{ site.baseurl }}/files/henry/goals_vs_opp-1.png)

His play against the major rivals is not bad; he averaged at least a half goal per match. In fact he averaged that mark against 26 of the 35 teams he played. Flipping back and forth between the last two plots you can extract some interesting info. For example, Henry tended to play score a lot against Birmingham City and Portsmouth, averaging at least 1.0 goal a match aginst both. On the opposite end of the spectrum, Henry averaged less than 0.4 goals a match against Bolton and Everton.

Conclusions
-----------

Theirry Henry stands as one of the greatest strikers of his generation and leaves behind a rich and revered legacy in England. Given his Premier League match data, I took a look at his stats during his stay at Arsenal. I plotted his matches played, match results, and goals scored. I primarily sliced these according to season or opponent. His per match assist counts were not quite correct so I omitted them entirely. I hope to have better, more accurate stats in the future. Should this be the case, this post will be updated accordingly.
