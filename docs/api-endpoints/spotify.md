---
title: "API endpoint: spotify"
---


## Verified Endpoints

| URL                                                                             | Use                            |
|---------------------------------------------------------------------------------|--------------------------------|
| `https://mobile.bereal.com/api/music/spotify/login`                             | GET login information          |
| `https://mobile.bereal.com/api/music/spotify/token`                             | GET login token                |

```
https://accounts.spotify.com/authorize?response_type
=code&client_id=ID&scope=user-read-currently-playing&redirect_uri
=https%3A%2F%2Fmobile.bereal.com%2Fapi%2Fmusic%2Fspotify%2Ftoken&state=TOKEN

response_type: code
client_id:     CLIENT_ID
scope:         user-read-currently-playing
redirect_uri:  https://mobile.bereal.com/api/music/spotify/token
state:         STATE_ID
```
