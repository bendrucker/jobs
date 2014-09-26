# Backend Engineer Challenge

*Please make your repository accessible by @pierrevalade, @jeremylv, @joeydong and @pierre-elie.*

**Google Calendar Data Proxy**

Build a NodeJS app that transforms data from the [Google Calendar API](https://developers.google.com/google-apps/calendar/concepts) into a specific format. This app should also handle the OAuth authentication flow. **Do not use the [google-api-nodejs-client](https://github.com/google/google-api-nodejs-client)**.

## Routes

### Authentication

Authenticate the user using [Google's Web Server OAuth Flow](https://developers.google.com/accounts/docs/OAuth2#webserver). The following routes should be implemented in your app.

#### `/authenticate`

The first url the user is directed to. This should redirect the user to Google's OAuth login page.

#### `/authenticate/callback`

The callback from Google's OAuth login page. This should respond with an access token for use in the later routes.


### Calendars

#### `/calendars?accessToken=<accessToken>`

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

### Events

#### `/calendars/<calendarID>/events?accessToken=<accessToken>`

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

## Some Libraries to Consider

### [Express JS](https://github.com/visionmedia/express)

### [Node Request](https://github.com/mikeal/request)

### [Async JS](https://github.com/caolan/async)

### [Mocha](https://github.com/visionmedia/mocha)
