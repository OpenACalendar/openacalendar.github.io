---
layout: post
title: Web app version 1.5.4 released; Security fix
slug: webapp-version-1-5-4
created: 2015-12-23 19:30:00
---

Version 1.5.4 is released! Details of the changes [are here](http://ican.openacalendar.org/webapp/release/1.5.4.html).

To upgrade, [follow these instructions](http://docs.openacalendar.org/en/v1.5.x/serveradministrators/core/upgrading.html).

This contains 2 major things;

Firstly a security issue. Sorry. Any user that otherwise has edit rights can edit any curated list in some screens only. There is a simple one line fix, and disabling the Curated List feature gets around this. [More details are here.](https://github.com/OpenACalendar/OpenACalendar-Web-Core/issues/515)

(BTW did you know we have a private mailing list for security discussions before they are made public? If you run our software ask to be added to it.)

Secondly, we are starting to move away from making graphics from Font Awesome to using it directly. This should mean much smoother graphics on high density screens, but may change how the site looks in some very old browsers. This work will not finish until v1.6.0 is released, but we have put a lot in this release. (The old CSS rules and graphics will stay available in the v1.5.x branch to make sure other code still works.)

We are now starting on work for v1.6.0 - stay tuned for more details!
