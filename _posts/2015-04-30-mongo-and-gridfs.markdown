---
layout:     post
comments: 	true
title:      "Mongo Sharding and GridFS"
subtitle:   "Data Engineering."
date:       2015-04-30 16:00:00
author:     "Josh Fermin"
header-img: "img/post-bg-08.jpg"
---

<h2 class="section-heading">Mongo Sharding and GridFS</h2>
<p>A couple of days ago I gave a talk in my data engineering class about Mongo and how I was using it in combination with GridFS for my work. If you want to dive into the slides here they are: <a href="http://joshfermin.me/mongo_presentation/#/">Mongo Presentation</a>. To navigate through the presentation, use the arrow keys, or simply press the spacebar to go to the next page.</p>

<p>I have been using Mongo Sharding in conjunction with GridFS to create a new database for all the APKs and Files our team uses to scan for malware. We need to transfer all these files to this new db, because the old way of storage is a huge RAID of hard disks and it is starting to fail more and more often. This new database consists of seven 10 TB shards combining to a total of 70TB.</p>

<p>What I covered in the presentation: 
<ul>
	<li><b>What is sharding?</b>
		<ul>
		<li>Why do we need sharding?</li>
		<li>How sharding works in terms of MongoDB</li>
		</ul>
	</li>
	<li><b>Mongo Sharding Tutorial</b>
		<ul>
		<li>Config Server</li>
		<li>Mongos - Routing server</li>
		<li>Creating DBs and Shards</li>
		<li>How to shard on DB/Collection level</li>
		</ul>
	</li>
	<li><b>GridFS</b>
		<ul>
		<li>How GridFS stores Files</li>
		<li>GridFS Implementation</li>
		<li>Example: C# Driver</li>
		</ul>
	</li>
	<li><b>Resources</b>
		<ul>
		<li><a href="http://docs.mongodb.org/manual/tutorial/deploy-shard-cluster/">Deploying a Sharded Cluster in Mongo</a></li>
		<li><a href="http://docs.mongodb.org/master/MongoDB-sharding-guide.pdf">MongoDB Sharding Guide</a></li>
		</ul>
	</li>



</ul>
</p>

<blockquote>Note: I used reactjs to create the presentation. <a href="https://github.com/joshfermin/mongo_presentation">Here</a> is the github source if you want to see how I created it.</blockquote>
