---
layout: post
title: Publishing to /group/photos/ without sufficient permissions - Facebook Bug
---

---

<i>Update : It is found that this issue was already <a href="http://philippeharewood.com/the-group-idphotos-endpoint-isnt-obeying-the-publish_actions-and-user_groups-permission-requirement/">reported by</a> Philippe Harewood and fixed by Facebook 
even before my report. This is just another example of how code changes must have caused the same vulnerability to reappear.</i>

---

#### Description


According to Facebook's Graph API documentation about <a href="https://developers.facebook.com/docs/graph-api/reference/v2.9/group/feed">publishing to groups</a> other than 'App and Games groups', `publish_actions` and either `user_managed_groups` or `user_groups` permissions are needed.

It was found possible to publish through the `photos` edge without setting `user_managed_groups` or `user_groups` scope, but only `publish_actions` in the access_token. 

#### Impact:

It posts an update to the attacker targeted group (ofcourse, victim should be a member of) EVEN if the user had only granted 'ONLY ME' privacy mode for posts while allowing the access token.

#### Reproduction:


1. Get an access_token for Graph API Explorer from a test account with `publish_actions` scope set.

2. Using Graph API Explorer, make a post on behalf of the user to the 'photos' edge of node {group-id}.

3. Use the POST field `url` and point it an image url.

4. Complete the request.

It returns an id and post_id after posting the update. Facebook fixed the vulnerability after it was reported to them.

{% highlight text %} 
Report sent : 02 Sep 2015 
Escalation : 22 Sep 2015 
Fix : Sometime after rewarding the bounty.
Bounty awarded : 04 May 2015 
{% endhighlight %}

Thanks for reading!

