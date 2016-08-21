---
layout: post
title: Web App Future Requirements
slug: future-requirements
created: 2016-08-21 09:00:00
---

I've been thinking about the future direction of the project, and what that means for the hosting requirements for it. 

One path is to try to make it as easy to host as possible; for example by supporting both MySQL and Postgres. While this has obvious benefits in making it easier for others to pick up, it also makes it more complex and means it will require more testing. Also in a quest to support many different environments you end up supporting a simpler set of features and avoiding using the latest more advanced features - or in the worst case, rewriting those features.

So while having a more demanding set of hosting requirements isn't great, it does mean simpler code that can take advantage of all the latest features, with simpler testing.

Ideally we would go with the former (easy to host). But given the resources available to this project, I've concluded that the latter path is the better way to go (more demanding requirements). Maybe this will change in the future if the resources available to the project change, but for now this is the plan.

So here are things that will probably happen in the future:

<strong>PHP 7 required.</strong> We would have to hike the minimum required PHP version to 5.6 soon anyway, as the latest versions of some of the libraries we use are only available for that. However, it makes sense to jump to PHP 7. This isn't so much because of any particular feature in PHP 7 (although Scalar type declarations and Return type declarations look great!) but beacuse of the increased performance available in PHP 7. While technically we could still support PHP 5.6 in that case, that does increase the amount of testing required - so we may just say PHP 7. The latest Ubuntu LTS (Xenial, 16.04) comes with PHP 7, and while it's not in the mainstream Debian stable yet there are reasonable options for backporting.

(The latest Ubuntu LTS also has the advantage of coming with versions of Apache and Nginx that both support HTTP2 - another performance win!)

<strong>Postgres 9.4 required.</strong> We want to take advantage of the JSON and JSONB column types, only available from 9.2 and 9.4 respectively. Debian Jessie comes with 9.4, Ubuntu LTS comes with 9.5.

<strong>Postgis required.</strong> If we say this, we can use functions like searching for points a set distance from the user natively in the database. Both Debian and Ubuntu come with this in packaging, and popular services like Amazon AWS RDS support this.

<strong>Optionally, Some kind of No-SQL DB or platform as a caching layer.</strong> We've been looking at the performance of some of the DB queries recently, and listing events is actually painful. Because our data structure is normalised (as it should be!), listing events involves so many joins and a few sub queries. While we could probably improve what we have a bit it will always be complex, and having a fully populated data set in a cache with no joins required should be a fast solution.

<strong>If your using this new optional caching layer, a messaging que moves from the current optional requirement to a compulsory one.</strong> Otherwise, when you edit an event it would take ages for the cache to update. This is actually currently true but currently the cache only contains minor things like the count of future events in a group or area. When the cache starts to contain actual event listings, stale data will be much more noticeable and problematic!

Lastly, <strong>when will any of this happen?</strong> Not for a while. We will probably do one more big release (v1.7.0) with the same requirements we have now. The big releases after that will probably start to creep up the requirements.

We hope this doesn't cause problems for people, but given the resources available and the large amount of work to do this seems wise. Comments welcome directly or on the email list, as always!

