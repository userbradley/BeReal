---
title: "API endpoint: Content"
---

## Verified Endpoints

| URL                                                          | Use                                                                                                                                                                             |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `https://mobile.bereal.com/api/content/comments`             | Gets comments and creates them                                                                                                                                                  |
| `https://mobile.bereal.com/api/content/posts/upload-url`     | Retrieves the [Signed URL](https://cloud.google.com/cdn/docs/using-signed-urls#:~:text=A%20signed%20URL%20is%20a,specific%20actions%20on%20a%20resource.) to the uploaded Image |
| `https://mobile.bereal.com/api/content/posts`                | Finalizes image upload, sends front and back camera and storage location for images                                                                                             |
| `https://mobile.bereal.com/api/content/posts/me`             | Gets your post                                                                                                                                                                  |
| `https://mobile.bereal.com/api/content/posts/caption`        | Creates a caption on your post                                                                                                                                                  |
| `https://mobile.bereal.com/api/content/posts/visibility`     | Updates the visibility of a BeReal                                                                                                                                              |
| `https://mobile.bereal.com/api/content/realmojis`            | Gets a list of realmojis                                                                                                                                                        |
| `https://mobile.bereal.com/api/content/realmojis/upload-url` | Gets [GCS Signed URL](https://cloud.google.com/storage/docs/access-control/signed-urls) for Real Mojis                                                                          |
| `https://mobile.bereal.com/api/content/realmojis/instant`    | Puts an instant RealMoji on a post                                                                                                                                              |
| `https://mobile.bereal.com/api/content/screenshots`          | Updates when you screenshot a post                                                                                                                                              |
| `https://mobile.bereal.com/api/content/screenshots/me`       | Gets list of users who screenshot?                                                                                                                                              |
| `https://mobile.bereal.com/api/content/unblurs`              | Gets the unblurs and ubnlurs a users post and how many they can unblur                                                                                                          |



## moments


## Verified Endpoints

| URL                                                             | Use                                                                                                                                                                             
|-----------------------------------------------------------------|-------------------------------------------|
| `https://mobile.bereal.com/api/bereal/moments/last/europe-west` | Gets last (eu) Bereal notification time   |  
 
Response

```json
{
		"id": {
			"NywegFScSAG83Fg4rugyI",
		    "startDate":"2024-01-14T10:37:05.108Z",
			"endDate":"2024-01-14T10:39:05.108Z",
			"region":"europe-west",
			"timezone":"Europe/Paris",
			"localTime":"11:37",
			"localDate":"2024-01-14"
}
```                                                                                                 

## Unverified Endpoints

!!! note "We don't know if these endpoints still exist or are used"
    Because of the whole SSL pinning thing, we have no clue

| URL                                                                                      | Use                                                                                                    |
|------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| `https://us-central1-alexisbarreyat-bereal.cloudfunctions.net/sendCaptureInProgressPush` | Letting BeReal know you're taking a photo                                                              |
| `https://firebasestorage.googleapis.com/v0/b/storage.bere.al/o/`                         | Uploads the photo to Firebase from what I can see                                                      |

## Requests and Responses

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
        "latitude": <>,
        "longitude": <>
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
    "createdAt": "2006-01-02T15:04:05-0700",
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
    "takenAt": "2006-01-02T15:04:05-0700",
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
