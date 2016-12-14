---
layout: post
title: "Getting Slack Tokens"
date: 2015-04-14
---
It is not straight forward to get a token with Slack. The expectation is that you write an OAuth client to get the token, but it is possible to get it manually. These are the steps I followed:

You should already have an account and a channel set up that you want to send error messages to.
<ol>
	<li>Create a new Slack App - <a href="https://api.slack.com/applications/new">https://api.slack.com/applications/new</a> which will give you a client_id and a client_secret which you need for step two. You will need to enter a redirect URI, which can be any page for this purpose.</li>
	<li>Got to <a href="https://slack.com/oauth/authorize?client_id=%5Bclient_id%5D&scope=chat:write:bot">https://slack.com/oauth/authorize?client_id=[client_id]&scope=chat:write:bot</a></li>
	<li>Authorise App on the page that is returned.</li>
	<li>From the URI copy the code that is returned.</li>
	<li>Go to <a href="https://slack.com/api/oauth.access?client_id=%5Bclient_id%5D&client_secret=%5Bclient_secret%5D&code=%5Bcode%5D">https://slack.com/api/oauth.access?client_id=[client_id]&client_secret=[client_secret]&code=[code]</a></li>
	<li>Your token is in the JSON that is displayed.</li>
</ol>
