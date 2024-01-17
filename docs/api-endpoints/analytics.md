---
title: "API endpoint: Analytics"
---

| URL                                                                                               | Use                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `https://logs.browser-intake-datadoghq.com/api/v2/logs?ddsource=ios`                              | DataDog application usage metrics and RUM                                                                                                            |
| `https://api2.amplitude.com/`                                                                     | User journey tracking                                                                                                                                |
| `https://api.lab.amplitude.com/sdk/v2/vardata?v=0`                                                | 2023 recap video analytics                                                                                                                           |
| `https://region1.app-measurement.com/a`                                                           | Firebase [See here for info](https://stackoverflow.com/questions/54461349/how-to-decrypt-firebase-requests-to-app-measurement-com/54463682#54463682) |
| `https://api.onesignal.com/apps/91b217c4-7ad8-4fd1-a01c-f4ed5b2a4711/ios_params.js?player_id=<>>` | Push messaging (Probably the notification going off)                                                                                                 |
| `https://fcmtoken.googleapis.com/register`                                                        | [Firebase Messaging](https://firebase.google.com/docs/cloud-messaging) (maybe also for push notifications, but authing?)                             |
| `https://firebaselogging-pa.googleapis.com/v1/firelog/legacy/batchlog`                            | Firebase Logging                                                                                                                                     |

## Requests and Responses

### `2023 recap video analytics`

```
{
    "campaign-memoriesrecap2023": {
        "key": "off",
        "metadata": {
            "default": true
        }
    },
    "delhi-tagging-rollout-countries": {
        "key": "on",
        "value": "on"
    },
    "friend-recommendations-m2-ios": {
        "key": "active-weighted",
        "metadata": {
            "experimentKey": "exp-2"
        },
        "payload": {
            "fr-backend-variant": "active",
            "fr-card-reshow": 10,
            "fr-friend-threshold": 30,
            "fr-recco-count": 5
        },
        "value": "active-weighted"
    },
    "ios-cairo-streaks": {
        "key": "off",
        "metadata": {
            "default": true
        }
    },
    "ios-chat-forwarding": {
        "key": "treatment",
        "metadata": {
            "experimentKey": "exp-1"
        },
        "value": "treatment"
    },
    "ios-onboarding-revamp": {
        "key": "new-flow",
        "metadata": {
            "experimentKey": "exp-2"
        },
        "payload": {
            "notif": "old",
            "order": "new"
        },
        "value": "new-flow"
    },
    "ios-pinned-memories": {
        "key": "treatment",
        "metadata": {
            "experimentKey": "exp-1"
        },
        "value": "treatment"
    },
    "ios-sharing-cell": {
        "key": "share-and-clean",
        "metadata": {
            "experimentKey": "exp-2"
        },
        "payload": {
            "clean-cell": true,
            "external-sharing": true
        },
        "value": "share-and-clean"
    },
    "ios-tagging": {
        "key": "treatment",
        "metadata": {
            "experimentKey": "exp-1"
        },
        "value": "treatment"
    },
    "ios-tagging-resharing": {
        "key": "off",
        "metadata": {
            "default": true
        }
    },
    "ios-upload-perf-improvements": {
        "key": "treatment",
        "metadata": {
            "experimentKey": "exp-2"
        },
        "value": "treatment"
    },
    "memories-entry-points-ios": {
        "key": "navbar",
        "metadata": {
            "experimentKey": "exp-1"
        },
        "value": "navbar"
    },
    "sunset-survey-card": {
        "key": "off",
        "metadata": {
            "default": true
        }
    },
    "sunset-survey-card-prospect-cta": {
        "key": "off",
        "metadata": {
            "default": true
        }
    },
    "tagging-country-flag": {
        "key": "on",
        "value": "on"
    }
}
```

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
    {
        "_dd": {
            "device": {
                "architecture": "arm64e"
            }
        },
        "date": "2024-01-02T17:00:47.708Z",
        "ddtags": "env:prod,version:1.21.2",
        "error.kind": "HTTPError",
        "error.message": "HTTPError {httpCode=none, category=network, cocoa=-1200, description='An SSL error has occurred and a secure connection to the server cannot be made.'}",
        "error.stack": "HTTPError {httpCode=none, category=network, cocoa=-1200, description='An SSL error has occurred and a secure connection to the server cannot be made.'}",
        "logger.name": "AlexisBarreyat.BeReal",
        "logger.thread_name": "background",
        "logger.version": "1.23.0",
        "message": "[BAK] request : [GET] https://mobile.bereal.com/api/bereal/moments/last/europe-west ❌ \n error: HTTPError {httpCode=none, category=network, cocoa=-1200, description='An SSL error has occurred and a secure connection to the server cannot be made.'}",
        "network.client.available_interfaces": [
            "wifi",
            "cellular"
        ],
        "network.client.is_constrained": false,
        "network.client.is_expensive": false,
        "network.client.reachability": "yes",
        "network.client.sim_carrier.allows_voip": true,
        "network.client.sim_carrier.iso_country": "--",
        "network.client.sim_carrier.name": "--",
        "network.client.sim_carrier.technology": "LTE",
        "network.client.supports_ipv4": true,
        "network.client.supports_ipv6": true,
        "service": "AlexisBarreyat.BeReal",
        "status": "error",
        "usr.id": "ID",
        "usr.region": {
            "value": "europe-west"
        },
        "version": "1.21.2",
        "version.build": "14123"
    }
```
