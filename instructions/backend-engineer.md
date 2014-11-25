# Backend Engineer Challenge

*Please make your repository accessible by @pierrevalade, @jeremylv, @joeydong and @pierre-elie.*

## Google Calendar Data Proxy

Build a NodeJS app that transforms data from the [Google Calendar API](https://developers.google.com/google-apps/calendar/concepts) into a specific format. This app should also handle the OAuth authentication flow. **Do not use the [google-api-nodejs-client](https://github.com/google/google-api-nodejs-client)**.

### Routes

#### Authentication

Authenticate the user using [Google's Web Server OAuth Flow](https://developers.google.com/accounts/docs/OAuth2#webserver). The following routes should be implemented in your app.

##### `/authenticate`

The first url the user is directed to. This should redirect the user to Google's OAuth login page.

##### `/authenticate/callback`

The callback from Google's OAuth login page. This should respond with an access token for use in the later routes.


#### Calendars

##### `/calendars?accessToken=<accessToken>`

List the user's calendars given an access token. The response data should follow this format:

```
[{
  id: "joey@sunrise.am",
  title: "Joey's Calendar",
  color: "42d692",
  writable: true,
  selected: true,
  timezone: 'America/New_York'
}]
```

#### Events

##### `/calendars/<calendarID>/events?accessToken=<accessToken>`

List *all* events for calendar with `calendarID` given an access token. The response data should follow this format:

```
[{
  id: "p3ab9j6or3ib9k6gojcba16cq48b9m8d2j2cpm8l1kcda36k",
  status: "confirmed",
  title: "Lunch at Chipotle",
  start: {
    dateTime: "2014-07-25T12:00:00-04:00",
    timezone: "America/New_York"
  },
  end: {
    dateTime: "2014-07-25T10:15:00-04:00",
    timezone: "America/New_York"
  },
  location: 'Chipotle - 568 Broadway',
  attendees: [{
    name: "Pierre-Elie Fauche",
    emails: [
      "pe@sunrise.am"
    ],
    self: false,
    rsvpStatus: "attending"
  }],
  organizer: {
    name: "Joey Dong",
    emails: [
    "joey@sunrise.am"
    ],
    self: true
  },
  editable: true,
  recurrence: 'FREQ=WEEKLY'
}]
```

### Some Libraries to Consider

- [Express JS](https://github.com/visionmedia/express)
- [Node Request](https://github.com/mikeal/request)
- [Async JS](https://github.com/caolan/async)
- [Mocha](https://github.com/visionmedia/mocha)

## Bonus: Log formatting library

This second challenge is **optional**. It can be included with your Google Calendar proxy code if you decide to give it a try.
Organize your library as you see fit but it should expose a function accepting the following input as parameter and return the following output.

### Input

Array of raw log strings
```js
[
  'HTTP Request',
  'HTTP Request URL http://example.com',
  'HTTP Request Headers Authorization: Bearer oauth-token',
  'HTTP Request Headers Accept: application/json',
  'HTTP Request Timeout 25s',
  'Response time: 500ms',
  'Response length: 85KB',
  'Parsing event [id:1] No title',
  'Parsing event [id:1] 3 attendees',
  'Parsing event [id:2] Title: "Lunch"',
  'Parsing event [id:2] 0 attendees'
]
```

### Output

Structured, grouped logs into a single string (new lines are not *displayed* here).
The logs have been organized into sections based on prefix, with proper indentation.
```
HTTPRequest
  URL http://example.com
  Headers
    Authorization: Bearer oauth-token
    Accept: application/json
  Timeout 25s
Response
  time: 500ms
  length: 85KB
Parsing event [id:1]
  No title
  3 attendees
Parsing event [id:2]
  Title: "Lunch"
  0 attendees
```

Of course this set of input/output is just an example of the expected behavior of your lib.

## Side notes

Keep in mind what we will compare your work with: our own production Google proxy.
While we are not asking for a full production-ready proxy, we’d like to see that your code has that potential:
- clean
- flexible
- extensible
- maintainable
- great error/exception handling & reporting
