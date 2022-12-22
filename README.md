
## BeReal How it works ?

<!-- PROJECT LOGO -->
<br />
<div align="center">
 
    <img src="https://bere.al/images/logos/bereal-twitter.png" alt="Logo" width="80" height="80">
 


## API Endpoints

### Metric Collection

| URL                                                                                               | Use                                                                                                                     | Request type    |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|-----------------|
| `https://logs.browser-intake-datadoghq.com/api/v2/logs?ddsource=ios`                              | Application usage metrics                                                                                               | `POST HTTP/2.0` |
| `https://api2.amplitude.com/`                                                                     | User journey tracking                                                                                                   | `POST HTTP/2.0` |
| `https://region1.app-measurement.com/a`                                                           | Firebase (I'm like 80% sure)                                                                                            | `POST HTTP/2.0` |
| `https://api.onesignal.com/apps/91b217c4-7ad8-4fd1-a01c-f4ed5b2a4711/ios_params.js?player_id=<>>` | Push messaging (Probably the notification going off)                                                                    | `GET HTTP/2.0`  | 
| `https://fcmtoken.googleapis.com/register`                                                        | [Fibebase Messging](https://firebase.google.com/docs/cloud-messaging) (maybe also for push notifications, but authing?) | `POST HTTP/2.0` |
| `https://firebaselogging-pa.googleapis.com/v1/firelog/legacy/batchlog`                            | Firebase Logging                                                                                                        | `POST HTTP/2.0` |

### BeReal Application Specific requests

#### Storage
| URL                                    | Use                                                                                                                     | Request type    |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------|-----------------|
| `https://storage.bere.al/Photos/<uid>` | Where the user generated images are stored, backed by a [GCS Bucket](https://cloud.google.com/storage)                  | `GET HTTP/2.0`  |

#### Posting a photo
| URL                                                                                      | Use                                                 | Request type    |
|------------------------------------------------------------------------------------------|-----------------------------------------------------|-----------------|
| `https://us-central1-alexisbarreyat-bereal.cloudfunctions.net/sendCaptureInProgressPush` | Letting Bereal know you're taking a photo           | `POST HTTP/2.0` |
| `https://firebasestorage.googleapis.com/v0/b/storage.bere.al/o/`                         | Uploads the photo to Firebase from what I can see   | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/content/post`                                             | Finalizing the post, attaching location and retakes | `POST HTTP/2.0` |

#### Feeds
| URL                                                            | Use                                              | Request type   |
|----------------------------------------------------------------|--------------------------------------------------|----------------|
| `https://mobile.bereal.com/api/feeds/memories?limit=<number>`  | Your memories                                    | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/memories/video`           | Not sure, perhaps a future feature?              | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/friends`                  | Loads all the images that you're friends with    | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/discovery?limit=<number>` | Feed of `discover` page - Limited by number(int) | `GET HTTP/2.0` |

#### Relationships
| URL                                                                                               | Use                                                                                                                     | Request type    |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|-----------------|
| `https://mobile.bereal.com/api/relationships/friends`                                             | List of friends you have                                                                                                | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/friend-requests`                                     | Makes a friend request                                                                                                  | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/relationships/friend-requests/sent`                                | List of friend requests sent                                                                                            | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/friend-requests/received`                            | List of friend requests received                                                                                        | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/suggestions`                                         | Users you _may know_                                                                                                    | `GET HTTP/2.0`  |

#### Person
| URL                                                                         | Use                                                                                         | Request type    |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|-----------------|
| `https://us-central1-alexisbarreyat-bereal.cloudfunctions.net/getUserNames` | Gets usernames for public users it seems. Was only called when I opened the _discover_ page | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/person/profiles/<uid>`                       | Shows information about the user by ID                                                      | `GET HTTP/2.0`  |


#### Legal schmooz
| URL                                                                                               | Use                                                                                                                     | Request type    |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|-----------------|
| `https://mobile.bereal.com/api/terms`                                                             | What Terms and conditions the user has accepted                                                                         | `GET HTTP/2.0`  |



#### Other
| URL                   | Use                                                       |
|-----------------------|-----------------------------------------------------------|
| `status.bereal.team`  | Simple text based status page of services                 |
| `tools.bereal.team`   | Probably internal tooling                                 | 
| `auth.bereal.team`    | _assuming_ to be authentication services                  | 
| `doc.bereal.team`     | Probably a custom URL for google docs  (Protected by IAP) | 
| `webhooks.bereal.com` | push data from user (app) to serveur (database)           | 


---





### Get Usernames

This seems to be the endpoint that gets called when you load the _discover_ page (eg: people that are not your _direct_ friends)
Post to URL

_Requires Authentication_
```text
{
    "data": {
        "uids": [
            "a5wIW3KgmnTiS6QXph0IiY3lEAb2"
        ]
    }
}
```

Response (Authenticated)
```text
{
    "result": [
        {
            "name": "Liv",
            "photoURL": "Photos/a5wIW3KgmnTiS6QXph0IiY3lEAb2/profile/a5wIW3KgmnTiS6QXph0IiY3lEAb2-1657273844-profile-picture.jpg",
            "uid": "a5wIW3KgmnTiS6QXph0IiY3lEAb2",
            "userName": "liv_lutner"
        }
    ]
}
```
Response (Un-authenticated)
```text
{
    "error": {
        "message": "You must be authenticated.",
        "status": "UNAUTHENTICATED"
    }
}
```

### feeds/friends
When the app opens, it makes a call to `api/feed/friends`

Below is an example, with PII removed. 
```text
[
  {
    "id": "<>>",
    "notificationID": "<>>",
    "ownerID": "<>>",
    "userName": "<>>",
    "user": {
      "id": "<>",
      "username": "<>"
    },
    "mediaType": "late",
    "region": "us-central",
    "bucket": "storage.bere.al",
    "photoURL": "https://storage.bere.al/Photos/<>/bereal/f822aa7a-3b0c-495f-b5bd-a4250a465083-1659997174.jpg",
    "imageWidth": 1500,
    "imageHeight": 2000,
    "secondaryPhotoURL": "https://storage.bere.al/Photos/<>/bereal/f822aa7a-3b0c-495f-b5bd-a4250a465083-1659997174-secondary.jpg",
    "secondaryImageHeight": 2000,
    "secondaryImageWidth": 1500,
    "members": [
      "<>"
    ],
    "lateInSeconds": 67,
    "isPublic": false,
    "location": {
      "_latitude": <>,
      "_longitude": -<>
    },
    "retakeCounter": 0,
    "creationDate": {
      "_seconds": 1659997238,
      "_nanoseconds": 684000000
    },
    "updatedAt": 1660002563356,
    "takenAt": {
      "_seconds": 1659997174,
      "_nanoseconds": 0
    },
    "comment": [],
    "realMojis": [
      {
        "id": "-j-<>>",
        "uid": "<>>",
        "userName": "<>>",
        "user": {
          "id": "<>>",
          "username": "<>>",
          "profilePicture": {
            "height": 1000,
            "width": 1000,
            "url": "https://storage.bere.al/cdn-cgi/image/width=200,height=200/Photos/<>/profile/<>-1658600169-profile-picture.jpg"
          }
        },
        "emoji": "😍",
        "type": "heartEyes",
        "uri": "https://storage.bere.al/Photos/<>/realmoji/<>-realmoji-heartEyes-1659046828.jpg",
        "date": {
          "_seconds": 1660002563,
          "_nanoseconds": 350000000
        }
      }
    ],
    "screenshots": [],
    "screenshotsV2": []
  },
]
```

### feeds/discovery

This is the `Discovery` page, where you can see people that are not your friends.

You can see an example response from the API by looking at the [public.json](public.json)

## feeds/memories/video

2021 memories recaps video

```text
{
    "status": "unavailable",
    "url": null
}
```

### feeds/memories

This shows all your memories

```text
        {
            "id": "RPe9OfuPIOscE9LPxoRpX",
            "thumbnail": {
                "url": "https://storage.bere.al/cdn-cgi/image/height=130/Photos/<>/bereal/3cc9ad9d-<>-4199-9987-e3dc145<>45-1659976930.jpg",
                "width": 98,
                "height": 130
            },
            "primary": {
                "url": "https://storage.bere.al/Photos/<>/bereal/3cc9ad9d-<>-4199-9987-e3dc145<>45-1659976930.jpg",
                "width": 1500,
                "height": 2000
            },
            "secondary": {
                "url": "https://storage.bere.al/Photos/<>/bereal/3cc9ad9d-<>-4199-9987-e3dc145<>45-1659976930-secondary.jpg",
                "width": 1500,
                "height": 2000
            },
            "isLate": true,
            "memoryDay": "2022-08-08"
        },

```
### api/terms

Shows what terms and conditions the user has accepted
```
{
    "data": [
        {
            "code": "gps",
            "status": "ACCEPTED",
            "signedAt": "2022-06-20T13:21:07.850Z",
            "termUrl": "https://bere.al",
            "version": "1"
        },
        {
            "code": "memories",
            "status": "ACCEPTED",
            "signedAt": "2022-06-20T13:20:39.727Z",
            "termUrl": "https://bere.al",
            "version": "1"
        },
        {
            "code": "terms",
            "status": "ACCEPTED",
            "signedAt": "2022-06-20T13:20:39.726Z",
            "termUrl": "https://bere.al/en/terms",
            "version": "1"
        },
        {
            "code": "privacy",
            "status": "ACCEPTED",
            "signedAt": "2022-06-20T13:20:39.727Z",
            "termUrl": "https://bere.al/en/privacy",
            "version": "1"
        },
        {
            "code": "fof",
            "status": "UNKNOWN",
            "termUrl": "https://bere.al",
            "version": "1"
        }
    ]
}
```

### api/relationships/suggestions
This API returns a list of account that you _may or may not know_ (This is worked out server side based on syncing contacts)

```text
        {
            "fullname": "Mya <>",
            "id": "<>",
            "mutualFriends": 3,
            "profilePicture": {
                "height": 500,
                "url": "https://storage.bere.al/Photos/<>/profile/<>-1651416654-profile-picture.jpg",
                "width": 500
            },
            "username": "<>"
        },
```

### api/relationships/friends

This API gives a list of users you are friends with

```text
{
            "fullname": "<>",
            "id": "<>",
            "profilePicture": {
                "height": 500,
                "url": "https://storage.bere.al/Photos/<>/profile/<>-1651432152-profile-picture.jpg",
                "width": 500
            },
            "status": "accepted",
            "username": "<>"
        },
```

### relationships/friend-requests

Post request to make a friend request

```text
{
    "fullname": "Erin <>>",
    "id": "<>",
    "mutualFriends": 2,
    "profilePicture": {
        "height": 500,
        "url": "https://storage.bere.al/Photos/<>/profile/<>-1655582465-profile-picture.jpg",
        "width": 500
    },
    "status": "sent",
    "updatedAt": "2022-08-09T00:41:43.375Z",
    "username": "<>>"
}
```

### relationships/friend-requests/received

Shows a list of friend requests the user (me) has received

As I have no pending requests, this is what it shows. I would assume it would show the fields `profilePicture` and `UserName`

```text
{
    "data": [],
    "next": null
}
```

### relationships/friend-requests/sent

Shows a list of friend requests the user (me) has sent to other users, as well as the status of the request

```text

{
    "data": [
        {
            "fullname": "Erin <>",
            "id": "<>>",
            "mutualFriends": 2,
            "profilePicture": {
                "height": 500,
                "url": "https://storage.bere.al/Photos/<>>/profile/<>-1655582465-profile-picture.jpg",
                "width": 500
            },
            "status": "sent",
            "updatedAt": "2022-08-09T00:41:43.375Z",
            "username": "<>>"
        }
    ],
    "next": null
}
```

### api/person/profiles/<uid>
This API returns information about the user, but their UID (Unique ID)

```
{
    "createdAt": "2022-05-01T20:34:24.741Z",
    "fullname": "<>",
    "id": "<>",
    "profilePicture": {
        "height": 500,
        "url": "https://storage.bere.al/Photos/<>/profile/<>-1651578666-profile-picture.jpg",
        "width": 500
    },
    "relationship": {
        "commonFriends": {
            "sample": [
                {
                    "fullname": "<>",
                    "id": "<>",
                    "profilePicture": {
                        "height": 500,
                        "url": "https://storage.bere.al/Photos/<>/profile/<>-1651432152-profile-picture.jpg",
                        "width": 500
                    },
                    "username": "<>"
                },
                {
                    "fullname": "Courtney",
                    "id": "<>",
                    "profilePicture": {
                        "height": 500,
                        "url": "https://storage.bere.al/Photos/<>/profile/<>-1648163954-profile-picture.jpg",
                        "width": 500
                    },
                    "username": "<>"
                }
            ],
            "total": 2
        },
        "friendedAt": null,
        "status": null
    },
    "username": "<>"
}
```

### sendCaptureInProgressPush

This is a cloud function that seems to push a message to pubsub on the BeReal side

What it sends:

```text
{
    "data": {
        "photoURL": "Photos/<me>/profile/<me>-1655905537-profile-picture.jpg",
        "topic": "<me>",
        "userName": "<me>"
    }
}
```

Response 

```text
{
    "result": "projects/alexisbarreyat-bereal/messages/7517087177659076139"
}
```

### Firebase push

Request 

```text
{
    "cacheControl": "public,max-age=172800",
    "contentType": "image/jpeg",
    "metadata": {
        "type": "bereal"
    },
    "name": "Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851.jpg"
}
```

```text
{
    "bucket": "storage.bere.al",
    "cacheControl": "public,max-age=172800",
    "contentDisposition": "inline; filename*=utf-8''7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851-secondary.jpg",
    "contentEncoding": "identity",
    "contentType": "image/jpeg",
    "crc32c": "rfGb7g==",
    "downloadTokens": "551a5e87-a995-47dc-a108-13668abdecfa",
    "etag": "CLzws8n3u/kCEAE=",
    "generation": "1660122857011260",
    "md5Hash": "f/wNKCMBarI56uGxAOX6jg==",
    "metadata": {
        "type": "bereal"
    },
    "metageneration": "1",
    "name": "Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851-secondary.jpg",
    "size": "563242",
    "storageClass": "MULTI_REGIONAL",
    "timeCreated": "2022-08-10T09:14:17.082Z",
    "updated": "2022-08-10T09:14:17.082Z"
}
```

### content/post

This is the API endpoint bereal posts to when it's finalizing the post

Request 

```text
{
    "backCamera": {
        "bucket": "storage.bere.al",
        "height": 2000,
        "path": "Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851.jpg",
        "width": 1500
    },
    "frontCamera": {
        "bucket": "storage.bere.al",
        "height": 2000,
        "path": "Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851-secondary.jpg",
        "width": 1500
    },
    "isLate": true,
    "isPublic": false,
    "location": {
        "latitude": <>>,
        "longitude": <>>
    },
    "retakeCounter": 4,
    "takenAt": "2022-08-10T09:14:11Z"
}
```

Response

```text
{
    "caption": null,
    "comments": {
        "sample": [],
        "total": 0
    },
    "createdAt": "2022-08-10T09:14:17.603Z",
    "id": "<>-YKzhel",
    "isLate": true,
    "lateInSeconds": 1425,
    "location": {
        "latitude": <>,
        "longitude": <>
    },
    "moment": {
        "id": "dr6O-8wHaE4xRgnxLpY9M",
        "region": "europe-west"
    },
    "primary": {
        "height": 2000,
        "url": "https://storage.bere.al/Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851.jpg",
        "width": 1500
    },
    "realmojis": {
        "sample": [],
        "total": 0
    },
    "retakeCounter": 4,
    "screenshots": {
        "sample": [],
        "total": 0
    },
    "secondary": {
        "height": 2000,
        "url": "https://storage.bere.al/Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851-secondary.jpg",
        "width": 1500
    },
    "takenAt": "2022-08-10T09:14:11.000Z",
    "user": {
        "id": "<me>",
        "profilePicture": {
            "height": 1000,
            "url": "https://storage.bere.al/Photos/<me>/profile/<me>-1655905537-profile-picture.jpg",
            "width": 1000
        },
        "username": "<>"
    },
    "visibility": [
        "friends"
    ]
}
```



## Stargazers over time

[![Stargazers over time](https://starchart.cc/userbradley/BeReal.svg)](https://starchart.cc/userbradley/BeReal)
