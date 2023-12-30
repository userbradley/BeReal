---
title: "API endpoint: Analytics"
---

| URL                                                      | Use                                              |
|----------------------------------------------------------|--------------------------------------------------|
| `https://mobile.bereal.com/api/feeds/memories/video`     | Lists your years recap Video                     |
| `https://mobile.bereal.com/api/feeds/memories`           | Lists all your memories                          |
| `https://mobile.bereal.com/api/feeds/memories-v1`        | _assuming_ this is the new memories endpoint     |
| `https://mobile.bereal.com/api/feeds/people`             | Gets all the people                              |
| `https://mobile.bereal.com/api/feeds/friends-of-friends` | Gets the friends of Friends feed                 |
| `https://mobile.bereal.com/api/feeds/user-stats`         | Returns user status for the logged in user (you) |
| `https://mobile.bereal.com/api/feeds/friends-v1`         | Loads all the images that you're friends with    |

## Requests and Responses


### feeds/memories

```json
{
  "prev": "string",
  "next": "string",
  "data": [
    {
      "id": "string",
      "thumbnail": {
        "url": "string",
        "width": 0,
        "height": 0
      },
      "primary": {
        "url": "string",
        "width": 0,
        "height": 0
      },
      "secondary": {
        "url": "string",
        "width": 0,
        "height": 0
      },
      "isLate": true,
      "memoryDay": "string",
      "location": {
        "latitude": 0,
        "longitude": 0
      }
    }
  ],
  "memoriesSynchronized": true
}
```

### feeds/memories-v1

```json
{
    "prev": "string",
    "next": "string",
    "data": [
    {
        "memoryDay": "string",
        "momentId": "string",
        "mainPostMemoryId": "string",
        "mainPostThumbnail": {
            "url": "string",
            "width": 0,
            "height": 0
        },
        "mainPostPrimaryMedia": {
            "url": "string",
            "width": 0,
            "height": 0
        },
        "mainPostSecondaryMedia": {
            "url": "string",
            "width": 0,
            "height": 0
        },
        "isLate": true,
        "numPostsForMoment": 0
    }
],
    "memoriesSynchronized": true
}
```
### feeds/people

```json
{
  "prev": "string",
  "next": "string",
  "data": [
    {
      "user": [
        {
          "id": "string",
          "username": "string",
          "profilePicture": {
            "url": "string",
            "width": 0,
            "height": 0
          }
        }
      ],
      "moment": {
        "id": "string",
        "region": "europe-west"
      },
      "isBirthday": true,
      "posts": [
        {
          "id": "string",
          "primary": {
            "url": "string",
            "width": 0,
            "height": 0,
            "blurHash": "string"
          },
          "secondary": {
            "url": "string",
            "width": 0,
            "height": 0,
            "blurHash": "string"
          },
          "realmoji": {
            "id": "string",
            "user": {
              "id": "string",
              "username": "string",
              "profilePicture": {
                "url": "string",
                "width": 0,
                "height": 0
              }
            },
            "media": {
              "url": "string",
              "width": 0,
              "height": 0
            },
            "emoji": "👍",
            "type": "string",
            "isInstant": true,
            "postedAt": "2006-01-02T15:04:05-0700"
          },
          "music": {
            "isrc": "<>",
            "track": "string",
            "artist": "string",
            "artwork": "https://i.scdn.co/image/<>",
            "preview": "https://p.scdn.co/mp3-preview/<>",
            "openUrl": "https://open.spotify.com/track/<>",
            "visibility": "public",
            "provider": "spotify",
            "providerId": "string",
            "audioType": "track"
          },
          "caption": "string",
          "location": {
            "latitude": 0,
            "longitude": 0
          },
          "retakeCounter": 0,
          "takenAt": "2006-01-02T15:04:05-0700",
          "lateInSeconds": 0,
          "isLate": true,
          "isMain": true,
          "creationDate": "2006-01-02T15:04:05-0700",
          "updatedAt": "2006-01-02T15:04:05-0700",
          "realMojiSamples": [
            {
              "id": "string",
              "user": {
                "id": "string",
                "username": "string",
                "profilePicture": {
                  "url": "string",
                  "width": 0,
                  "height": 0
                }
              },
              "media": {
                "url": "string",
                "width": 0,
                "height": 0
              },
              "emoji": "👍",
              "type": "string",
              "isInstant": true,
              "postedAt": "2006-01-02T15:04:05-0700"
            }
          ]
        }
      ]
    }
  ]
}
```

### feeds/friends-of-friends

```json
{
  "prev": "string",
  "next": "string",
  "data": [
    {
      "id": "string",
      "user": {
        "id": "string",
        "username": "string",
        "profilePicture": {
          "url": "string",
          "width": 0,
          "height": 0
        },
        "relationship": {
          "status": "pending",
          "commonFriends": [
            {
              "id": "string",
              "username": "string",
              "fullname": "string",
              "profilePicture": {
                "url": "string",
                "width": 0,
                "height": 0
              }
            }
          ]
        }
      },
      "moment": {
        "id": "string",
        "region": "europe-west"
      },
      "primary": {
        "url": "string",
        "width": 0,
        "height": 0,
        "blurHash": "string"
      },
      "secondary": {
        "url": "string",
        "width": 0,
        "height": 0,
        "blurHash": "string"
      },
      "location": {
        "latitude": 0,
        "longitude": 0
      },
      "caption": "string",
      "takenAt": "2006-01-02T15:04:05-0700",
      "postedAt": "2006-01-02T15:04:05-0700",
      "lateInSeconds": 0,
      "realmojis": {
        "total": 0,
        "self": {
          "id": "string",
          "user": {
            "id": "string",
            "username": "string"
          },
          "media": {
            "url": "string",
            "width": 0,
            "height": 0
          },
          "emoji": "👍",
          "isInstant": true,
          "postedAt": "2006-01-02T15:04:05-0700"
        },
        "sample": [
          {
            "id": "string",
            "user": {
              "id": "string",
              "username": "string"
            },
            "media": {
              "url": "string",
              "width": 0,
              "height": 0
            },
            "emoji": "👍",
            "isInstant": true,
            "postedAt": "2006-01-02T15:04:05-0700"
          }
        ]
      }
    }
  ]
}
```

### feeds/friends-v1

```json
{
  "userPosts": {
    "user": {
      "id": "string",
      "username": "string",
      "profilePicture": {
        "url": "string",
        "width": 0,
        "height": 0
      }
    },
    "momentId": "string",
    "region": "europe-west",
    "isBirthday": true,
    "posts": [
      {
        "id": "string",
        "primary": {
          "url": "string",
          "width": 0,
          "height": 0,
          "blurHash": "string"
        },
        "secondary": {
          "url": "string",
          "width": 0,
          "height": 0,
          "blurHash": "string"
        },
        "location": {
          "latitude": 0,
          "longitude": 0
        },
        "realMojis": [
          {
            "id": "string",
            "user": {
              "id": "string",
              "username": "string",
              "profilePicture": {
                "url": "string",
                "width": 0,
                "height": 0
              }
            },
            "media": {
              "url": "string",
              "width": 0,
              "height": 0
            },
            "emoji": "👍",
            "type": "string",
            "isInstant": true,
            "postedAt": "2006-01-02T15:04:05-0700"
          }
        ],
        "comments": [
          {
            "id": "string",
            "user": [
              {
                "id": "string",
                "username": "string",
                "profilePicture": {
                  "url": "string",
                  "width": 0,
                  "height": 0
                }
              }
            ],
            "content": "string",
            "postedAt": "2006-01-02T15:04:05-0700"
          }
        ],
        "caption": "string",
        "retakeCounter": 0,
        "takenAt": "2006-01-02T15:04:05-0700",
        "music": {
          "isrc": "<>",
          "track": "string",
          "artist": "string",
          "artwork": "https://i.scdn.co/image/<>",
          "preview": "https://p.scdn.co/mp3-preview/<>",
          "openUrl": "https://open.spotify.com/track/<>",
          "visibility": "public",
          "provider": "spotify",
          "providerId": "string",
          "audioType": "track"
        },
        "lateInSeconds": 0,
        "isLate": true,
        "isMain": true,
        "creationDate": "2006-01-02T15:04:05-0700",
        "updatedAt": "2006-01-02T15:04:05-0700",
        "screenshots": [
          {
            "id": "string",
            "user": {
              "id": "string",
              "username": "string",
              "profilePicture": {
                "url": "string",
                "width": 0,
                "height": 0
              }
            },
            "snappedAt": "2006-01-02T15:04:05-0700"
          }
        ],
        "visibility": [
          "friends"
        ],
        "stats": {
          "realMojisCounters": {
            "sum": 0,
            "percentages": [
              "string"
            ]
          }
        },
        "realMojiSamples": [
          {
            "id": "string",
            "user": {
              "id": "string",
              "username": "string",
              "profilePicture": {
                "url": "string",
                "width": 0,
                "height": 0
              }
            },
            "media": {
              "url": "string",
              "width": 0,
              "height": 0
            },
            "emoji": "👍",
            "type": "string",
            "isInstant": true,
            "postedAt": "2006-01-02T15:04:05-0700"
          }
        ],
        "unblurCount": 0
      }
    ]
  },
  "friendsPosts": [
    {
      "user": [
        {
          "id": "string",
          "username": "string",
          "profilePicture": {
            "url": "string",
            "width": 0,
            "height": 0
          }
        }
      ],
      "momentId": "string",
      "region": "europe-west",
      "isBirthday": false,
      "posts": [
        {
          "id": "string",
          "primary": {
            "url": "string",
            "width": 0,
            "height": 0,
            "blurHash": "string"
          },
          "secondary": {
            "url": "string",
            "width": 0,
            "height": 0,
            "blurHash": "string"
          },
          "location": {
            "latitude": 0,
            "longitude": 0
          },
          "realMojis": [
            {
              "id": "string",
              "user": {
                "id": "string",
                "username": "string",
                "profilePicture": {
                  "url": "string",
                  "width": 0,
                  "height": 0
                }
              },
              "media": {
                "url": "string",
                "width": 0,
                "height": 0
              },
              "emoji": "👍",
              "type": "string",
              "isInstant": true,
              "postedAt": "2006-01-02T15:04:05-0700"
            }
          ],
          "comments": [
            {
              "id": "string",
              "user": [
                {
                  "id": "string",
                  "username": "string",
                  "profilePicture": {
                    "url": "string",
                    "width": 0,
                    "height": 0
                  }
                }
              ],
              "content": "string",
              "postedAt": "2006-01-02T15:04:05-0700"
            }
          ],
          "caption": "string",
          "retakeCounter": 0,
          "takenAt": "2006-01-02T15:04:05-0700",
          "music": {
            "isrc": "<>",
            "track": "string",
            "artist": "string",
            "artwork": "https://i.scdn.co/image/<>",
            "preview": "https://p.scdn.co/mp3-preview/1<>",
            "openUrl": "https://open.spotify.com/track/<>",
            "visibility": "public",
            "provider": "spotify",
            "providerId": "string",
            "audioType": "track"
          },
          "lateInSeconds": 0,
          "isLate": true,
          "isMain": true,
          "creationDate": "2006-01-02T15:04:05-0700",
          "updatedAt": "2006-01-02T15:04:05-0700"
        }
      ]
    }
  ],
  "remainingPosts": 0,
  "maxPostsPerMoment": 0,
  "unblur": {
    "userId": "string",
    "fullname": "string",
    "username": "string",
    "profileURL": "string",
    "createdAt": "2006-01-02T15:04:05-0700"
  }
}
```
