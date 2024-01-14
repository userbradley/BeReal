---
title: API Endpoints
---

We have been able to locate alot of the API endpoints by using a network wide SSL scanning proxy, however BeReal has introduces SSL pinning.

The endpoints are categorized as below

* [Content](content.md)
* [Analytics](analytics.md)
* [Feeds](feeds.md)
* [Moderation](moderation.md)
* [Messaging](messaging.md)
* [Helps](helps.md)
* [Person](person.md)
* [Relationships](relationships.md)
* [Search](search.md)
* [Core](content.md)
* [Spotify](spotify.md)

## Domain

All the API endpoints are against the domain:

```text
https://mobile.bereal.com/api/
```

!!! note "What about the API version"
    From what I can see, BeReal does not have different API versions

## Reading the documentation

When ever we mention an endpoint (say the Spotify one) it will be noted like below

```text
/music/spotify/login
```

You simply need to prepend the domain to it, so:

```text
https://mobile.bereal.com/api/music/spotify/login
```
