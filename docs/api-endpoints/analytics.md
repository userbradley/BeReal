---
title: "API endpoint: Analytics"
---

| URL                                                                                               | Use                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `https://logs.browser-intake-datadoghq.com/api/v2/logs?ddsource=ios`                              | DataDog application usage metrics and RUM                                                                                                            |
| `https://api2.amplitude.com/`                                                                     | User journey tracking                                                                                                                                |
| `https://region1.app-measurement.com/a`                                                           | Firebase [See here for info](https://stackoverflow.com/questions/54461349/how-to-decrypt-firebase-requests-to-app-measurement-com/54463682#54463682) |
| `https://api.onesignal.com/apps/91b217c4-7ad8-4fd1-a01c-f4ed5b2a4711/ios_params.js?player_id=<>>` | Push messaging (Probably the notification going off)                                                                                                 |
| `https://fcmtoken.googleapis.com/register`                                                        | [Firebase Messaging](https://firebase.google.com/docs/cloud-messaging) (maybe also for push notifications, but authing?)                             |
| `https://firebaselogging-pa.googleapis.com/v1/firelog/legacy/batchlog`                            | Firebase Logging                                                                                                                                     |

## Requests and Responses

### `unspecified`

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
