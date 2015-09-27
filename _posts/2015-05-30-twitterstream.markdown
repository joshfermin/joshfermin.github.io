---
layout:     post
comments: 	true
title:      "Twitterstream"
subtitle:   "Atlas Expo and Big Data"
date:       2015-05-30 16:00:00
author:     "Josh Fermin"
header-img: "img/earth3.png"
---

<h2 class="section-heading">What is Twitterstream?</h2>

<p>Twitterstream is basically heatmap that collects and analyzes tweet words and emojis. The analysis gauges the sentiment surrounding specific words occurring in many tweets across the United States. We streamed our tweets from the Twitter API and used Google's Geolocation to determine the location of the tweets. </p>

<a href="{{ site.baseurl }}/img/blog/twittermap.gif">
    <img src="{{ site.baseurl }}/img/blog/twittermap.gif">
</a>

<p>Here is an example of me using it under the topic of "nba". I filter the search by date and then enter a key word to search upon, in this case nba. This will then return to me a heatmap of all the tweets we have relating to nba and their sentiment (blue for good, red for bad).</p>

<h2 class="section-heading">The Architecture</h2>
<a href="{{ site.baseurl }}/img/blog/twitterstreamArchitecture.png">
    <img src="{{ site.baseurl }}/img/blog/twitterstreamArchitecture.png">
</a>
<!-- <p>
We started off with a model that goes as follows: A tweet collector module reads from a stream, writes to a local JSON file, and then uploads to our mongolabs database everyday. Oh how naïve we were. We quickly moved to the stream writing directly to the database, hindsight is 20-20 I guess.

We have data! Although we don’t need everything in the tweet, we only need a few attributes, and we need to add sentiment to it. Map-Reduce to the rescue! Or not… This was also stupid. It forced us to run batch jobs every so often to update our live data set. So we needed a way to make our application real-time, fast, and robust.

Kafka to the rescue, for real this time. This allowed us to cut out multiple reads and writes to the database. As new tweets came in, our consumers would clean the data and persist both a raw copy and a clean copy.

Okay, it looks like our backend data is working well! Or not… We were using kafka correctly, but we were not able to utilize the power that comes with it: clustering, replication, and fault tolerance. We were running the kafka instance on one node, with zero clustering.

Okay amazon SQS to the rescue FOR REAL this time. This was perfect. It would do the same thing as our kafka instance, but it would automatically cluster, replicate, and be fault tolerant. We feel confident about this.

Next was the front end. We decided to create a node.js server in order to create a database API that our frontend angular application could interact with. This was great at first, until we were requesting 100,000 tweets. Everything broke.

We decided that we would create API calls that would only load the tweets from the state that the user has clicked on. In addition it will only load 2000 tweets at a time. We used AJAX calls to achieve this.

We have this real time data, but we’re not showing it on the frontend. Nothing a little javascript magic can’t handle.

So that’s where the app is at now. Although we still have a lot we want to do.
</p> -->

<h2 class="section-heading">Improvements</h2>
1) Implement SOLR to improve search.

2) Make the front-end much prettier.

3) Get a better sentiment analysis.

4) Zoomable map.

Thanks for reading!



<blockquote>Note: I used reactjs to create the presentation. <a href="https://github.com/joshfermin/mongo_presentation">Here</a> is the github source if you want to see how I created it.</blockquote>


<h2 class="section-heading">ATLAS Expo</h2>
<img src="http://atlas.colorado.edu/wp-content/uploads/2015/04/Expo_800w_web_4-14-15_5.jpg">
