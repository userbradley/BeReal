# BeReal
<img src="https://upload.wikimedia.org/wikipedia/commons/8/89/Logo-BeReal.png" width="90" alt="Bereal Application">

This Repo contains all the endpoints that I was able to find from my Network wide SSL inspecting proxy.

<!-- TOC -->
* [BeReal](#bereal)
  * [Api Domain](#api-domain)
  * [Endpoints](#endpoints)
    * [Metric Collection](#metric-collection)
    * [BeReal Application Specific requests](#bereal-application-specific-requests)
      * [Storage](#storage-)
      * [Feeds](#feeds)
      * [Relationships](#relationships)
      * [Search](#search)
      * [Settings](#settings)
      * [Person](#person)
      * [Posting a photo](#posting-a-photo)
      * [Legal schmooz](#legal-schmooz)
      * [Help Section](#help-section)
  * [Domains](#domains)
  * [Application workflows](#application-workflows)
    * [Get Usernames](#get-usernames)
    * [feeds/friends-v1](#feedsfriends-v1)
    * [feeds/discovery](#feedsdiscovery)
    * [feeds/memories/video](#feedsmemoriesvideo)
    * [feeds/memories](#feedsmemories)
    * [api/terms](#apiterms)
    * [api/relationships/suggestions](#apirelationshipssuggestions)
    * [api/relationships/friends](#apirelationshipsfriends)
    * [relationships/friend-requests](#relationshipsfriend-requests)
    * [relationships/friend-requests/received](#relationshipsfriend-requestsreceived)
    * [relationships/friend-requests/sent](#relationshipsfriend-requestssent)
    * [api/person/profiles/<uid>](#apipersonprofilesuid)
    * [sendCaptureInProgressPush](#sendcaptureinprogresspush)
    * [Firebase push](#firebase-push)
    * [content/post](#contentpost)
    * [Metric Collection](#metric-collection-1)
  * [Stargazers over time](#stargazers-over-time)
<!-- TOC -->

## Api Domain

The current domain for the BeReal api is

```
https://mobile.bereal.com/api/
```

Any reference to something like `/feeds/` assumes you just go `https://mobile.bereal.com/api/feeds/`

## Endpoints

The below contains an overview of the endpoints. 

### Metric Collection

| URL                                                                                               | Use                                                                                                                      | Request type    |
|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-----------------|
| `https://logs.browser-intake-datadoghq.com/api/v2/logs?ddsource=ios`                              | Application usage metrics                                                                                                | `POST HTTP/2.0` |
| `https://api2.amplitude.com/`                                                                     | User journey tracking                                                                                                    | `POST HTTP/2.0` |
| `https://region1.app-measurement.com/a`                                                           | Firebase (I'm like 80% sure)                                                                                             | `POST HTTP/2.0` |
| `https://api.onesignal.com/apps/91b217c4-7ad8-4fd1-a01c-f4ed5b2a4711/ios_params.js?player_id=<>>` | Push messaging (Probably the notification going off)                                                                     | `GET HTTP/2.0`  |
| `https://fcmtoken.googleapis.com/register`                                                        | [Firebase Messaging](https://firebase.google.com/docs/cloud-messaging) (maybe also for push notifications, but authing?) | `POST HTTP/2.0` |
| `https://firebaselogging-pa.googleapis.com/v1/firelog/legacy/batchlog`                            | Firebase Logging                                                                                                         | `POST HTTP/2.0` |

### BeReal Application Specific requests


#### Storage 
| URL                                                          | Use                                                                                                    | Request type   |
|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|----------------|
| `https://storage.bere.al/Photos/<uid>`                       | Where the user generated images are stored, backed by a [GCS Bucket](https://cloud.google.com/storage) | `GET HTTP/2.0` |
| `https://bereal-us-central1-memories.storage.googleapis.com` | Memories 2022 recap video storage                                                                      | `GET HTTP/2.0` |
                                                                                                                                                                                      
  
#### Feeds


| URL                                                            | Use                                              | Request type   |
|----------------------------------------------------------------|--------------------------------------------------|----------------|
| `https://mobile.bereal.com/api/feeds/discovery?limit=<number>` | Feed of `discover` page - Limited by number(int) | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/memories?limit=<number>`  | Your memories                                    | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/memories/video`           | Not sure, perhaps a future feature?              | `GET HTTP/2.0` |
| `https://mobile.bereal.com/api/feeds/friends-v1`               | Loads all the images that you're friends with    | `GET HTTP/2.0` |

#### Relationships


| URL                                                                    | Use                                                           | Request type    |
|------------------------------------------------------------------------|---------------------------------------------------------------|-----------------|
| `https://mobile.bereal.com/api/relationships/contacts`                 | Sends a hashed list of phone numbers to work out who you know | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/relationships/friends`                  | List of friends you                                           | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/friend-requests`          | Makes a friend                                                | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/relationships/friend-requests/sent`     | List of friend requests                                       | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/friend-requests/received` | List of friend requests                                       | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/relationships/suggestions`              | Users you _may know_                                          | `GET HTTP/2.0`  |

#### Search

| URL                                            | Use                                                   | Request type   |
|------------------------------------------------|-------------------------------------------------------|----------------|
| `https://mobile.bereal.com/api/search/profile` | Searches based on full name or partial name of a user | `GET HTTP/2.0` |

#### Settings

| URL                                                        | Use                                                               | Request type    |
|------------------------------------------------------------|-------------------------------------------------------------------|-----------------|
| `https://mobile.bereal.com/api/settings`                   | Retrieves settings for the app, both global and user              | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/settings/notification-push` | Gets user preferences on push notifications                       | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/api/parental-consent-request`   | Creates a request for parental consent if user is under 13 in EEZ | `POST HTTP/2.0` |


#### Person


| URL                                                                         | Use                                                                                                         | Request type              |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------|
| `https://us-central1-alexisbarreyat-bereal.cloudfunctions.net/getUserNames` | Gets usernames for public users it seems. Was only called when I opened the _discover_ page                 | `POST HTTP/2.0`           |
| `https://mobile.bereal.com/api/person/realmojis/upload-url`                 | Gets [GCS Signed URL](https://cloud.google.com/storage/docs/access-control/signed-urls) for realmoji upload | `GET HTTP/2.0`            |
| `https://mobile.bereal.com/api/person/me`                                   | Gets info about your account                                                                                | `GET HTTP/2.0`            |
| `https://mobile.bereal.com/api/person/profile`                              | Updates and gets info about you!                                                                            | `POST/PATCH/GET HTTP/2.0` |
| `https://mobile.bereal.com/api/person/me/username`                          | Updates your username                                                                                       | `PATCH HTTP/2.0`          |


#### Posting a photo


| URL                                                                                      | Use                                                                                                    | Request type    |
|------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-----------------|
| `https://us-central1-alexisbarreyat-bereal.cloudfunctions.net/sendCaptureInProgressPush` | Letting BeReal know you're taking a photo                                                              | `POST HTTP/2.0` |
| `https://firebasestorage.googleapis.com/v0/b/storage.bere.al/o/`                         | Uploads the photo to Firebase from what I can see                                                      | `POST HTTP/2.0` |
| `https://mobile.bereal.com/api/content/post`                                             | Finalizing the post, attaching location and retakes                                                    | `POST HTTP/2.0` |
| `https://mobile.bereal.com/content/posts/upload-url`                                     | Gets [GCS Signed URL](https://cloud.google.com/storage/docs/access-control/signed-urls) for uploads    | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/posts/me`                                             | Gets your post                                                                                         | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/posts/caption`                                        | Creates a caption on your post                                                                         | `POST HTTP/2.0` |
| `https://mobile.bereal.com/content/posts/visibility`                                     | Updates the visibility of a BeReal                                                                     | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/comments`                                             | Gets comments and creates them                                                                         | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/realmojis`                                            | Gets a list of realmojis                                                                               | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/realmojis/upload-url`                                 | Gets [GCS Signed URL](https://cloud.google.com/storage/docs/access-control/signed-urls) for Real Mojis | `GET HTTP/2.0`  |
| `https://mobile.bereal.com/content/screenshots`                                          | Updates when you screenshot a post                                                                     | `POST HTTP/2.0` |
| `https://mobile.bereal.com/content/screenshots/me`                                       | Gets list of users who screenshot?                                                                     | `GET HTTP/2.0`  |


#### Legal schmooz
| URL                                           | Use                                             | Request type   |
|-----------------------------------------------|-------------------------------------------------|----------------|
| `https://mobile.bereal.com/api/terms/privacy` | What Terms and conditions the user has accepted | `GET HTTP/2.0` |

#### Help Section
| URL                                                                     | Use                                                                                            | Request type   |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|----------------|
| `https://berealapp.zendesk.com/api/private/mobile_sdk/settings/id.json` | Where the user send message to the help service   [Bereal use Zendesk](https://www.zendesk.fr) | `GET HTTP/2.0` |
| `https://berealapp.zendesk.com/attachments/token/ID/?name=ID.jpeg`      | Where the user Photo is stored (help message)                                                  | `GET HTTP/2.0` |
                  
                                                                                                                                                                                      
  
## Domains

Below contains the _top level_ domains that BeReal uses

| Domain           | Use cases                                                              |
|------------------|------------------------------------------------------------------------|
| `bereal.team`    | Seems to be _Back Office_ stuff and cloud infrastructure               |
| `bere.al`        | Seems to be public facing domains like their website, and jobs posting |
| `bereal.com`     | More back office tools                                                 |
| `bereal.network` | CND and off cloud Networking systems                                   |



### Subdomains

Below is all the subdomains we have been able to find


| URL                           | Use                                                                                    |
|-------------------------------|----------------------------------------------------------------------------------------|
| `status.bereal.team`          | Simple text based status page of services                                              |
| `tools.bereal.team`           | Probably internal tooling                                                              |
| `auth.bereal.team`            | _assuming_ to be authentication services                                               |
| `doc.bereal.team`             | Probably a custom URL for google docs  (Protected by IAP)                              |
| `dev.argocd.bereal.team`      | Development [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) deployment             |
| `webhooks.bereal.team`        | Most likely incoming webhooks to the BeReal systems                                    |
| `status.bereal.team`          | Text based status page                                                                 |
| `tools.bereal.team`           | Internal tooling                                                                       |
| `dev.mobile.bereal.team`      | Not sure                                                                               |
| `dev.webhooks.bereal.team`    | *DEV* Development webhooks                                                             |
| `grafana.bereal.team`         | Grafana system, dashboards and alerting                                                |
| `dev.doc.bereal.team`         | *DEV* Most likely internal Documentation                                               |
| `dev.grafana.bereal.team`     | *DEV* Grafana system, dashboards and alerting                                          |
| `kiali.bereal.team`           | [Istio Service mesh console](https://kiali.io)                                         |
| `bereal.team    `             | Apex Domain                                                                            |
| `dev.tools.bereal.team`       | *DEV* Internal Tooling                                                                 |
| `mobile.bereal.team`          |                                                                                        |
| `dev.status.bereal.team`      | *DEV* Status page                                                                      |
| `argocd.bereal.team`          | [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) Deployment                         |
| `auth.bereal.team`            | Authentication systems                                                                 |
| `doc.bereal.team`             | Most likely internal Documentation                                                     |
| `dev.auth.bereal.team`        | *DEV* Authentication systems                                                           |
| `dev.notific.bereal.team`     | *DEV* Misspell   notification system                                                   |
| `bere.al`                     | Website                                                                                |
| `storage2.bere.al`            | GCS Storage                                                                            |
| `app.bere.al`                 | Website too                                                                            |
| `test.bere.al`                | Test website                                                                           |
| `www.bere.al`                 | Website                                                                                |
| `intra.bere.al`               | BeReal Ambassadors site (now Deprecated)                                               |
| `jobs.bere.al`                | BeReal job postings                                                                    |
| `storage.bere.al`             | GCS Storage                                                                            |
| `backup.bere.al`              | Backup GCS Storage                                                                     |
| `sandbox-storage2.bere.al`    | Storage Sandbox                                                                        |
| `sandbox-storage.bere.al`     | Storage Sandbox                                                                        |
| `dev.kiali.bereal.com`        | *DEV* Istio Service mesh console](https://kiali.io)                                    |
| `prod.dashboard.bereal.com`   | Probably Grafana                                                                       |
| `mobile.bereal.com`           | Not sure                                                                               |
| `api-fasterstore.bereal.com`  | _probably_ Ecommerce management platform [Faster Stores](https://www.fasterstores.com) |
| `dev.mobile.bereal.com`       | Not sure                                                                               |
| `bereal.com`                  | Website                                                                                |
| `dev.grafana.bereal.com`      | *DEV* Grafana system, dashboards and alerting                                          |
| `webhooks.bereal.com`         | Most likely incoming webhooks to the BeReal systems                                    |
| `push.bereal.com`             |                                                                                        |
| `prod.fasterstore.bereal.com` | _probably_ Ecommerce management platform [Faster Stores](https://www.fasterstores.com) |
| `prod.kiali.bereal.com`       | Production [Istio Service mesh console](https://kiali.io)                              |
| `gke-test.bereal.com`         | Probably testing GKE                                                                   |
| `test.fasterstore.bereal.com` | _probably_ Ecommerce management platform [Faster Stores](https://www.fasterstores.com) |
| `dev.tools.bereal.com`        | *DEV* Internal tooling                                                                 |
| `all.argocd.bereal.com`       | [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) Deployment                         |
| `dev.push.bereal.com`         | Not sure                                                                               |
| `api.bereal.com`              | BeReal API Endpoint                                                                    |
| `dev.function.bereal.com`     | Probably cloud function domain                                                         |
| `dev.notification.bereal.com` | Probably Notification dev platform                                                     |
| `notification.bereal.com`     |                                                                                        |
| `function.bereal.com`         | Probably cloud function domain                                                         |
| `auth.bereal.com`             | Internal Authentication I would think                                                  |
| `dev.auth.bereal.com`         | *DEV*                  Internal Authentication I would think                           |
| `test.graphapi.bereal.com`    | Graph-api testing                                                                      |
| `notif.bereal.com`            | Probably notification infrastructure                                                   |
| `dev.traefik.bereal.com`      | [Traefik](https://doc.traefik.io/traefik/) Proxy for GKE                               |
| `cdn-eu.bereal.com`           | EU CND                                                                                 |
| `dev.argocd.bereal.com`       | Dev   [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) Deployment                   |
| `help.bereal.com`             | Help Pages                                                                             |
| `grafana.bereal.com`          | Grafana                                                                                |
| `dev.webhooks.bereal.com`     | Dev incoming webhooks to BeReal                                                        |
| `api-dev.bereal.com`          | Dev API                                                                                |
| `dev.graphapi.bereal.com`     | Dev Graph-api                                                                          |
| `argocd.bereal.com`           | [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) Deployment                         |
| `tools.bereal.com`            | Internal tooling (now Deprecated)                                                      |
| `jobs.bereal.com`             | Job postings                                                                           |
| `cdn.eu.bereal.com`           | EU CDN                                                                                 |
| `bereal.network`              | Seems to be their out of cloud Network services domain                                 |
| `cdn.bereal.network`          | New CDN running on `MCI Communications Services, Inc. d/b/a Verizon Business`          |
| `dev-cdn.bereal.network`      | Development CDN running on `MCI Communications Services, Inc. d/b/a Verizon Business`  |

---

## Application workflows



### Get Usernames

This seems to be the endpoint that gets called when you load the _Discover_ page (eg: people that are not your _direct_ friends)
Post to URL

_Requires Authentication_
```json
{
    "data": {
        "uids": [
            "a5wIW3KgmnTiS6QXph0IiY3lEAb2"
        ]
    }
}
```

Response (Authenticated)
```json
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
```json
{
    "error": {
        "message": "You must be authenticated.",
        "status": "UNAUTHENTICATED"
    }
}
```

### feeds/friends-v1
When the app opens, it makes a call to `api/feed/friends-v1`

Below is an example, with PII removed. 
```json
{
  "userPosts": {
    "user": {
      "id": "[REDACTED]",
      "username": "[REDACTED]",
      "profilePicture": {
        "url": "https://cdn.bereal.network/Photos/[REDACTED]/profile/[REDACTED]",
        "width": 999,
        "height": 999
      }
    },
    "region": "us-central",
    "momentId": "L1O8S_Tbph2fpEeuoSWcv",
    "posts": [
      {
        "id": "-PGe3UUH4wsDg0ttqc7G-",
        "visibility": ["friends"],
        "primary": {
          "url": "https://cdn.bereal.network/Photos/[REDACTED]/post/[REDACTED]",
          "width": 2000,
          "height": 1500
        },
        "secondary": {
          "url": "https://cdn.bereal.network/Photos/[REDACTED]/post/[REDACTED]",
          "width": 2000,
          "height": 1500
        },
        "caption": "I love my tortilla blanky 🥰",
        "retakeCounter": 0,
        "lateInSeconds": 16110,
        "isLate": true,
        "isMain": true,
        "realMojis": [
          {
            "id": "Jn8tDy3wwwJ197BHr7lJs",
            "user": {
              "id": "[REDACTED]",
              "username": "[REDACTED]",
              "profilePicture": {
                "url": "https://cdn.bereal.network/Photos/[REDACTED]/profile/[REDACTED]",
                "width": 1000,
                "height": 1000
              }
            },
            "media": {
              "url": "https://cdn.bereal.network/Photos/[REDACTED]/realmoji/[REDACTED]",
              "width": 500,
              "height": 500
            },
            "type": "up",
            "emoji": "👍",
            "isInstant": false,
            "postedAt": "2023-07-14T02:47:15.850Z"
          }
        ],
        "comments": [],
        "unblurCount": 0,
        "takenAt": "2023-07-14T02:46:26.520Z",
        "creationDate": "2023-07-14T02:46:26.657Z",
        "updatedAt": "2023-07-14T02:46:26.657Z"
      }
    ]
  },
  "friendsPosts": [
    {
      "user": {
        "id": "[REDACTED]",
        "username": "[REDACTED]",
        "profilePicture": {
          "url": "https://cdn.bereal.network/Photos/[REDACTED]/profile/[REDACTED]",
          "width": 1000,
          "height": 1000
        }
      },
      "momentId": "L1O8S_Tbph2fpEeuoSWcv",
      "region": "us-central",
      "moment": {
        "id": "L1O8S_Tbph2fpEeuoSWcv",
        "region": "us-central"
      },
      "posts": [
        {
          "id": "HLAxwJatn4OZFmLieuM8N",
          "primary": {
            "url": "https://cdn.bereal.network/Photos/[REDACTED]/post/[REDACTED]",
            "width": 1500,
            "height": 2000
          },
          "secondary": {
            "url": "https://cdn.bereal.network/Photos/[REDACTED]/post/[REDACTED]",
            "width": 1500,
            "height": 2000
          },
          "location": {
            "latitude": [REDACTED],
            "longitude": [REDACTED]
          },
          "retakeCounter": 1,
          "lateInSeconds": 0,
          "isLate": false,
          "isMain": true,
          "takenAt": "2023-07-13T22:16:41.468Z",
          "realMojis": [
            {
              "id": "qPIyfQuWbdr1Ma4bwDE1N",
              "user": {
                "id": "[REDACTED]",
                "username": "[REDACTED]",
                "profilePicture": {
                  "url": "https://cdn.bereal.network/Photos/[REDACTED]/profile/[REDACTED]",
                  "width": 1000,
                  "height": 1000
                }
              },
              "media": {
                "url": "https://cdn.bereal.network/Photos/[REDACTED]/realmoji/[REDACTED]",
                "width": 500,
                "height": 500
              },
              "type": "up",
              "emoji": "👍",
              "isInstant": false,
              "postedAt": "2023-07-14T02:47:15.850Z"
            }
          ],
          "comments": [],
          "unblurCount": 0,
          "takenAt": "2023-07-14T02:46:26.520Z",
          "creationDate": "2023-07-14T02:46:26.657Z",
          "updatedAt": "2023-07-14T02:46:26.657Z"
        }
      ]
    }
  ]
}

```

### feeds/discovery

This is the `Discovery` page, where you can see people that are not your friends.

You can see an example response from the API by looking at the [public.json](public.json)

### feeds/memories/video

2021 and 2022 memories recaps video

```json
{
    "status": "unavailable",
    "url": null
}
```

### feeds/memories

This shows all your memories

```json
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

```json
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

```json
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

```json
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

```json
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

```json
{
    "data": [],
    "next": null
}
```

### relationships/friend-requests/sent

Shows a list of friend requests the user (me) has sent to other users, as well as the status of the request

```json

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

```json
{
    "data": {
        "photoURL": "Photos/<me>/profile/<me>-1655905537-profile-picture.jpg",
        "topic": "<me>",
        "userName": "<me>"
    }
}
```

Response 

```json
{
    "result": "projects/alexisbarreyat-bereal/messages/7517087177659076139"
}
```

### Firebase push

Request 

```json
{
    "cacheControl": "public,max-age=172800",
    "contentType": "image/jpeg",
    "metadata": {
        "type": "bereal"
    },
    "name": "Photos/<me>/bereal/7c44d6e8-086b-4a18-b8b4-d3785f58cda8-1660122851.jpg"
}
```

```json
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

```json
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

```json
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
### Metric Collection
```
{
        "_dd": {
            "device": {
                "architecture": "arm64e"
            }
        },
        "date": "2023-05-22T17:39:51.607Z",
        "ddtags": "env:prod,version:1.1.2",
        "logger.name": "AlexisBarreyat.BeReal",
        "logger.thread_name": "main",
        "logger.version": "1.17.0",
        "message": "[UploadPostWorker] restarting upload",
        "network.client.available_interfaces": [
            "cellular"
        ],
        "network.client.is_constrained": false,
        "network.client.is_expensive": true,
        "network.client.reachability": "yes",
        "network.client.sim_carrier.allows_voip": true,
        "network.client.sim_carrier.iso_country": "--",
        "network.client.sim_carrier.name": "--",
        "network.client.sim_carrier.technology": "LTE",
        "network.client.supports_ipv4": true,
        "network.client.supports_ipv6": true,
        "service": "AlexisBarreyat.BeReal",
        "status": "info",
        "usr.id": "ID",
        "usr.region": "europe-west",
        "version": "1.1.2",
        "version.build": "9854"
    },


```


## Stargazers over time

[![Stargazers over time](https://starchart.cc/userbradley/BeReal.svg)](https://starchart.cc/userbradley/BeReal)
