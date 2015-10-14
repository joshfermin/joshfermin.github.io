---
layout:     post
comments: 	true
title:      "Dive Music"
subtitle:   "Local Hack Day"
date:       2015-10-10 11:00:00
author:     "Josh Fermin"
header-img: "img/img1.jpg"
---

<h2 class="section-heading">Local Hack Day</h2>

<p><a href="https://localhackday.mlh.io/">Local hack day</a> is a day set up by MLH (Major League Hacking) where campuses/cities come together all over the world and set up their own hackathons. The focus of the hackathon was to create something that benefits the community.</p>

<p>So the idea I came up with was <a href="https://github.com/zhued/divemusic">divemusic</a>.</p>

<h2 class="section-heading">divemusic</h2>
<p>So, what is divemusic? Divemusic is primarily a map that shows you the top songs of each country. Our vision was to create a way for people to explore the trending, popular music from everywhere around the world.</p>

<p>Before we get into the nitty gritty, here is a demo!</p>
<a href="https://gfycat.com/ConsiderateLankyAvocet" align="center">
    <img src="http://giant.gfycat.com/ConsiderateLankyAvocet.gif">
</a>


<h2 class="section-heading">The Backend</h2>
<p>We used the soundcloud API to pull data from all around the world, this was a bit tricky since the only API calls we could use were to get particular users/tracks. So to get large amounts of data, we came up with an recursive algorithm that will get a users favorite tracks, and then from those tracks, get the users of those tracks and get their favorites, and repeating this process until a specified depth limit was reached.</p>

<p>And everytime a track was "taken" with the algorithm, we persisted it to our MongoDB (hosted by mongolabs) with the track id, user id, and most importantly geography info.</p>

<p>Here's the actual code if you wanna see how we did it:</p>

{% highlight javascript %}
function find_favorites(userid, counter, limit)
{
	counter += 1;

	if (counter >= limit) { 
		// if depth reached, exit
		db.DB_close();
		return; 
	};

	SC.get('/users/' + userid + '/favorites', function(err, fav) {
		if ( err ) {
			console.log(err);
		} else {
			for (var i = fav.length - 1; i >= 0; i--) {
				var q = new Object();
				q["track_id"]=fav[i].id;
				q["playback_count"]=fav[i].playback_count;
				// add track, user and geography info to db
		  		add_to_db(q, fav[i]);
			};
			// recurse through favorite tracks
			for (var i = fav.length - 1; i >= 0; i--) {
			  find_favorites(fav[i].user_id, counter, limit)
			};
		}
	});
}
{% endhighlight %}

<h2 class="section-heading">The Frontend</h2>
<p>So for the front end, we got stuck playing around with the connection of d3 and angular. We were scratching our heads trying to import a datamap library, and spent a good 3-4 hours trying to figure that out, until finally we changed the script to point to the online javascript and bam! Everything was working.</p>

<p>Now, all we had to do is set up routes for our express server to gather data from the MongoDB and send it over to the front end. So we set the following route to get the top 10 tracks of a given country (based on playback count):</p>

{% highlight javascript %}
// ***
// Gets track for a country
// ***
app.get('/toptracks/:country', function(req,res){
	var q = tracks.find({country:req.params.country}).sort({playback_count: -1}).limit(10);
	q.exec(function(err, tracks){
		if (err) throw err;
		res.status(200).send(tracks);
	})
});
{% endhighlight %}

<p>Then, all we had to do is hit this route from the front end and display it nicely and wala! We have divemusic!</p>