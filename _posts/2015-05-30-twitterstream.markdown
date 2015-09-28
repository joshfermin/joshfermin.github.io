---
layout:     post
comments: 	true
title:      "Twitterstream"
subtitle:   "Atlas Expo and Big Data"
date:       2015-05-30 16:00:00
author:     "Josh Fermin"
header-img: "img/earth3.png"
---

<h2 class="section-heading">What is <a href="https://github.com/CUBigDataClass/tweetstream">Twitterstream</a>?</h2>

<p><a href="https://github.com/CUBigDataClass/tweetstream">Twitterstream</a> is a searchable heatmap that collects and analyzes the sentiment of tweets in the United States. The sentiment analysis takes in account not only the tweet text but the emojis as well. </p>

<a href="{{ site.baseurl }}/img/blog/twittermap.gif">
    <img src="{{ site.baseurl }}/img/blog/twittermap.gif">
</a>

<p>Here is an example of me using it under the topic of "nba". I filter the search by date and then enter a key word to search upon, in this case nba. This will then return to me a heatmap of all the tweets we have relating to nba and their sentiment (blue for good, red for bad).</p>

<h2 class="section-heading">The Architecture</h2>
<a href="{{ site.baseurl }}/img/blog/twitterstreamArchitecture.png">
    <img src="{{ site.baseurl }}/img/blog/twitterstreamArchitecture.png">
</a>
<p>
Here's where the fun stuff really comes in. Over the course of the semester we built, destroyed, and rebuilt our backend architecture multiple times.
</p>
<br> 

<h3>First Draft - Batch Jobs</h3>
<p>
First of, we started with a model that goes as follows: A tweet collector module reads from a stream, writes to a local JSON file, and then uploads to our mongolabs database everyday. This was clearly not sustainable, as there were so many moving parts just to get data from the Twitter API. 
</p>
<p>
But we went with it for a few weeks and began doing analysis on the data. We didn't need the whole tweet, we only needed a few things and then add sentiment to the tweet text itself. So we chose Map Reduce! Turns out... this was also a bad decision. Doing it this way forced us to run two batch jobs (one for the JSON file to the mongolabs database, and another for the map reduce). 
<p>
At this point we were manually running batch jobs and started to look at other alternatives. Time to rebuild!
</p>
<br> 

<h3>Second Draft - Kafka</h3>
<p>
We completely scrapped our first draft and instead put Kafka in its place. It allowed multiple reads and writes to the db. As new tweets came in, the consumers of the topic would then perform the sentiment analysis and filter out all the info we didn't need, and then write this output to a db. 
</p>
<p>
And the best part? It did this all in one step. Except for one problem, we were using kafka correctly, but it was way more than what we needed. We did not utilize any of the great things that come with kafka (clustering, replication, and fault tolerance) since we were running it on one node.
</p>
<br> 

<h3>Final Draft - Amazon SQS</h3>
<p>
So finally we went to the twitter engineers and they suggested to us Amazon SQS. This was exactly what we needed. It would do the same thing as our kafka instance, but it would implement all the clustering, replication, and fault tolerance for us.
</p>
<br> 

<h3>The Front End</h3>
<p>
Finally was the implementation of the front end. We created a node.js server that would serve as an API to our database which could return data to our front end. This data was then thrown into d3.js to make the heatmap. We started to run into issues when we needed to send 100,000s of tweets to the front end. 
</p>
<p>
To fix this, we added limits to the API calls and decided to display only the 10 most recent tweets (and subsequent tweets as they came in from Amazon SQS) until the user performed a search. We used AJAX calls to speed up the process of all of these.
</p>
<p>
And that's everything we did over the course of the semester!
</p>


<h2 class="section-heading">Improvements</h2>
<p>
	<ul>
		<li>Implement SOLR to improve search.</li>
		<li>Get a better sentiment analysis.</li>
		<li>Zoomable map and improve front end.</li>
	</ul>	
</p>

<!-- <h2 class="section-heading">The Team</h2> -->

<h2 class="section-heading">Atlas Expo</h2>
<p>We later presented this at the Atlas Expo along with the other projects from many other classes. Check out more <a href="http://atlas.colorado.edu/atlas-technology-expo-spring-2015/">here</a>!</p>
<img src="http://atlas.colorado.edu/wp-content/uploads/2015/04/Expo_800w_web_4-14-15_5.jpg">
