---
layout: post
title: "The EQS-Lidl Podium Conspiracy Theory"
date: 2016-07-06
excerpt: "A joke about cycling statistics taken too far. GIS analysis was involved."
tags: [cycling, data]
feature: https://i.imgur.com/QKwj011.png?1
comments: true
---

*A joke between friends taken too far. I did this analysis and write-up during the 2016 Tour de France and posted it to [the pro-cycling subreddit](https://www.reddit.com/r/peloton/) where, at the time, it became one of the top 10 posts in the community's history.* 

**Introduction**

Sport fans are superstitious. It’s a fact of nature. That’s why we wear our special socks on race day and always sit in the same spot at the bar. We also come to believe that certain teams or athletes are cursed, like Sagan, GvA, or Sep Vanmarcke always finishing second, Richie Porte inevitably suffering a mechanical just outside the 3km mark, or the Rainbow Jersey tanking a rider’s career.

So yesterday, while reading through the Race Thread comments, I ran across [/u/Sappert’s interesting theory](https://www.reddit.com/r/peloton/comments/4r7vqq/predictions_thread_tour_de_france_stage_4_saumur/d4za2go/) that Etixx Quickstep riders are only successful when there’s a Lidl near the finish. For those of you who aren’t aware, Lidl is a German Supermarket company that has stores all around Europe and became a main EQS sponsor for the 2016 season.

“Hmm… what an interesting theory,” I thought to myself. “I wonder how much truth it holds?” This of course meant that I had to investigate. Could Lidls near the finish be a predictor for an EQS podium finish? I had to find out.

**Methods**

This question required two pieces of data: (1) European Lidl locations, and (2) Finish locations and results for 2016 UCI World Tour. I obtained (1) from Open Street Map, and (2) from Wikipedia. For the latter, I had to manually look up the name and coordinates of the finishing town for all WT races and check to see if an EQS rider had finished in the top 3. Probably not the most efficient way to go about doing it, but hey, it worked. Couple notes: threw out two stages that were cancelled because of snow, one TTT (even though EQS finished on the podium, I didn’t think it counted), and also the Tour Down Under (because non-Euro races don’t matter… Aussies are asleep, right?).

I then counted how many Lidl’s were in each finishing city. I did this in ArcGIS by creating buffers of various sizes around city centers and totaling the number of supermarkets within them. I eventually settled on a 10km buffer around the city center, because European cities are small and that seemed like a reasonable, arbitrary distance to pick. You can see all this in this map, and find the underlying data for [races here](https://drive.google.com/file/d/0B0RSlki1E4zOMUpBdzFIeS1fbnM/view?usp=drive_open) and [Lidls here](https://drive.google.com/open?id=0B0RSlki1E4zOeXlpV2hFQjlEN3M).

<figure>
	<a href="http://i.imgur.com/qUMMqoq.jpg"><img src="http://i.imgur.com/qUMMqoq.jpg?1"></a>
	<figcaption>Map of Lidls and EQS Podium Finishes.</figcaption>
</figure>

With the data compiled, I loaded it up into R for some statistical testing. Since I limited myself to only counting podium finishes, I opted for a simple binomial logistic regression. I had to play around with the data, seeing how different distances, countries, dates, and # of Lidl’s affected the results. Eventually, I decided to limit myself to only races in Italy and France, even though it meant throwing out many of the team’s wins in Switzerland, Belgium, and Spain. I justified it to myself because Italy and France have hosted the Tour and Giro so far this year, and Grand Tours (and Roubaix) are the only races that matter in cycling. And in the end, I discovered that…

**Conclusion**

Every additional Lidl within 10km of the finish line* increases the log odds of an EQS rider finishing on the podium by ~53.3% ! *For races ending in France or Italy

As reference, there were 47 races in France and Italy in 2016. EQS finished on the podium in 16 of those, or 34% of races. This means that for every additional Lidl near the race finish, the probability that an EQS rider finishes on the podium goes up, at a statistically “good enough” p-value of 0.08. Model output here, and graph here.

<figure class="half">
    <a href="http://i.imgur.com/EEPpCWD.png"><img src="http://i.imgur.com/EEPpCWD.png"></a>
	<a href="http://i.imgur.com/KCoGMMZ.jpg"><img src="http://i.imgur.com/KCoGMMZ.jpg"></a>
	<figcaption>Lidls within distance of EQS Podium Finish Probability Model.</figcaption>
</figure>

There’s more work that could be done in researching this, like breaking it out into a more complex relationship of highest placed EQS rider (as opposed to just a podium finish), including GC standings, mapping out the whole race route and counting how many Lidl’s are passed during the day, or seeing how other teams fare. Probably easy to do is to also just look at actual wins vs. just podiums. Maybe I’ll do this later. But for now, I’m convinced that having a Lidl nearby is crucial for an EQS podium.

Just look at today’s stage. Dan Martin was the highest placed EQS rider, barely missing out on the podium. There were no Lidl’s in Le Lioran. Coincidence? [The science speaks for itself!](https://www.youtube.com/watch?v=7tzfl1wTemM)

