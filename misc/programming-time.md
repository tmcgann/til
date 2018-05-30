# Programming Time

Fairly comprehensive piece on time by Zach Holman: https://zachholman.com/talk/utc-is-enough-for-everyone-right

Got some good links to things to consider when handling time in programs...

## Time Zones

There's actually a timezone database, sometimes referred to as the tz database or Olson database. It keeps track of all the world's timezones, which is important since they can change randomly at any moment. The database also contains a list of rules related to each time zone.

- Info on tz database: https://en.wikipedia.org/wiki/Tz_database
- List of time zones: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
- The actual database files: https://www.iana.org/time-zones

## Storing Time

If you're going to store time, the best way to do it is usually with two data points:

1. The actual time stored as an ISO 8601 string in UTC time
    - RFC 3339 is a subset of ISO 8601. It's simplified and more strict (time zone required)
2. The relative timezone as a fully qualified name (stored as a string) as seen in the official tz database
    - Allows you to calculate relative time on clients
    - Time zone names are standard so lots of libraries will recognize them (e.g. America/Los Angeles)

## Time in the Browser

The Intl namespace is helpful for translating times: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl

The time element is super helpful for displaying time in an accessible way. For example:

```html
<time title="May 28, 2018, 3:47 PM PST" datetime="2018-05-28T15:47:57-08:00">six minutes ago</time>
```

These JavaScript libraries are good to use:

- moment.js → the standard, does everything JS date/time library
- date-fns → a new take on moment.js
- github/time-elements → Web component extension to the <time> element. Also includes auto-updating timestamps, as well as some locale help.

## Recurring Events

Often an app will need some kind of calendar widget and a way to schedule recurring events. RFC 5545 specifies standardized temporal expressions for recurring events. AWESOME!

The spec defines RRULES or "recurrence rules". Every Tuesday looks like this:

```
FREQ=WEEKLY;BYDAY=TU;INTERVAL=1
```

Isn't that amazing?! Lesson re-learned: Don't reinvent the wheel.

Martin Fowler also wrote a white paper on this: https://martinfowler.com/apsupp/recurring.pdf
