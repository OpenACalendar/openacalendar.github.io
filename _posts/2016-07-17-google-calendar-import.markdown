---
layout: post
title: Google Calendar ICS/ICAL Import - picking up changes
slug: google-calendar-import
created: 2016-07-17 10:45:00
---

Our calendar software offers data feeds that can be imported directly into Google Calendar, via a ICS/ICAL web feed. For this, we had to do some research to check how Google Calendar picks up on changes in events - if some detail of the event changes in your feed, you want Google Calendar to show the latest version.

To do this, [we used these 2 ical files](https://gist.github.com/jarofgreen/5147730ed99f1fe0f980a9600f6f5dad). The process is simple - put the first file on a web server somewhere. Import it to Google Calendar by selecting "Add to URL" in the menu next to other calendars. Wait until you are sure it's imported and you can see the events. Now go and put the contents of the second file at that same URL. Wait until it has been re-checked - this may take up to 14 hours, we have found. And here are the results.

### Test 1: only changing the start time

For our first test, the only thing that changes is the start time. `DTSTART;TZID=Europe/London:20160911T090000` becomes `DTSTART;TZID=Europe/London:20160911T110000`.

This change is **not** picked up by Google Calendar - the start time still shows as 9am. So this isn't enough.

### Test 2: OK, changing the start time and UID.

Ok, lets change the start time and the UID. `UID:event2@jmbtechnology.co.uk` becomes `UID:event2version2@jmbtechnology.co.uk`.

This time, Google Calendar does pick up the change - the start time now shows as 11am. However, changing the UID isn't great - other data may be tied to that. Lets keep looking.

### Test 3: change start time and sequence.

Ok, lets change the start time and the SEQUENCE from `SEQUENCE:1` to `SEQUENCE:2`.

Google calendar does pick up this change, and the UID stays the same. Great - but let's keep looking.

### Test 4: change start time and last modified.

We change the start time and the LAST-MODIFIED from `LAST-MODIFIED:20160714T074827Z` to `LAST-MODIFIED:20160715T0124827Z`. This change is not picked up by Google Calendar. Just to double check .....

### Test 5: change start time, sequence and last modified.

Ok, lets change the start time, the SEQUENCE from `SEQUENCE:1` to `SEQUENCE:2` and the LAST-MODIFIED from `LAST-MODIFIED:20160714T074827Z` to `LAST-MODIFIED:20160715T0124827Z`.

This change is picked up by Google Calendar.

### Conclusion

So if you have a ICS/ICAL web feed that you want to import to Google Calendar, and you want any changes in your event data to be picked up by Google Calendar make sure you update the SEQUENCE field.

The current version of our software doesn't handle this as well as it should do, and we will look into that.

Discuss this [on this GitHub issue](https://github.com/OpenACalendar/OpenACalendar-Web-Core/issues/176) or [our email list](/support.html). 
