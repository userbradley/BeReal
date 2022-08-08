## API Endpoints

| URL                                                                  | Use                                           | Request type    | Example request              | 
|----------------------------------------------------------------------|-----------------------------------------------|-----------------|------------------------------|
| `https://logs.browser-intake-datadoghq.com/api/v2/logs?ddsource=ios` | Application usage metrics                     | `post http/2.0` | See Datadog                  |
| `https://mobile.bereal.com/api/feeds/friends`                        | Loads all the images that you're friends with | `Get HTTP/2.0`  | See `Friends`                |
| `https://mobile.bereal.com/api/terms`                                | Not sure yet                                  | `GET HTTP/2.0`  | <>                           |
| `https://mobile.bereal.com/api/feeds/memories?limit=14` | Your memories | `GET HTTP/2.0   |                              |
| `https://mobile.bereal.com/api/feeds/memories/video`  | Not sure, perhaps a future feature? | `GET HTTP/2.0`  |                              |
| `https://api2.amplitude.com/` | User journy tracking | `POST HTTP/2.0 | See  [Amplitude](#amplitude) |


### Datadog 

```text
    {
        "date": "2022-08-08T16:46:01.257Z",
        "ddtags": "env:Production",
        "logger.name": "AlexisBarreyat.BeReal",
        "logger.thread_name": "main",
        "logger.version": "1.10.0",
        "message": "[ImageService]: Fix dirty URL : Photos/<>>/realmoji/<>>-realmoji-surprised-1655905571.jpg",
        "moment.creationDate": 681669021.766,
        "moment.deleveryDate": 681669032.805382,
        "moment.id": "<>>",
        "moment.region": "europe-west",
        "network.client.available_interfaces": [
            "wifi",
            "cellular"
        ],
        "network.client.is_constrained": false,
        "network.client.is_expensive": false,
        "network.client.reachability": "yes",
        "network.client.sim_carrier.allows_voip": true,
        "network.client.sim_carrier.iso_country": "gb",
        "network.client.sim_carrier.name": "EE",
        "network.client.sim_carrier.technology": "LTE",
        "network.client.supports_ipv4": true,
        "network.client.supports_ipv6": false,
        "service": "AlexisBarreyat.BeReal",
        "status": "debug",
        "usr.creationDate": 677424039.6040001,
        "usr.deviceUID": "<>>",
        "usr.id": "<>>",
        "usr.language": "en",
        "usr.region": "europe-west",
        "usr.username": "<>>",
        "version": "0.22.4"
    },
```

### Amplitude

```text
v:           3
client:      <>
e:           [{"session_id":<>>,"user_properties":{"$set":{"terms_gps":"ACCEPTED"}},"language":"English","event_type":"$identify","sequence_number":3130,"user_id":"<>>","country":"United Kingdom","api_properties":{"ios_idfv":"<>>"},"device_id":"<>>","event_properties":{},"uuid":"<>>","device_manufacturer":"Apple","version_name":"0.22.4","library":{"name":"amplitude-ios","version":"8.10.0"},"os_name":"ios","platform":"iOS","event_id":968,"carrier":"EE","timestamp":1659977451643,"groups":{},"os_version":"15.5","device_model":"iPhone13,2","group_properties":{}},{"session_id":<>>,"user_properties":{"$set":{"terms_memories":"ACCEPTED"}},"language":"English","event_type":"$identify","sequence_number":3131,"user_id":"<>>","country":"United Kingdom","api_properties":{"ios_idfv":"<>>"},"device_id":"<>>","event_properties":{},"uuid":"<>>","device_manufacturer":"Apple","version_name":"0.22.4","library":{"name":"amplitude-ios","version":"8.10.0"},"os_name":"ios","platform":"iOS","event_id":969,"carrier":"EE","timestamp":1659977451674,"groups":{},"os_version":"15.5","device_model":"iPhone13,2","group_properties":{}},{"session_id":<>>,"user_properties":{"$set":{"terms_unknown":"UNKNOWN"}},"language":"English","event_type":"$identify","sequence_number":3132,"user_id":"<>","country":"United Kingdom","api_properties":{"ios_idfv":"<>"},"device_id":"<>","event_properties":{},"uuid":"<>","device_manufacturer":"Apple","version_name":"0.22.4","library":{"name":"amplitude-ios","version":"8.10.0"},"os_name":"ios","platform":"iOS","event_id":970,"carrier":"EE","timestamp":1659977451694,"groups":{},"os_version":"15.5","device_model":"iPhone13,2","group_properties":{}},{"session_id":<>,"user_properties":{},"language":"English","event_type":"Viewed Home","sequence_number":3133,"user_id":"<>","country":"United Kingdom","api_properties":{"ios_idfv":"<>"},"device_id":"<>","event_properties":{},"uuid":"<>","device_manufacturer":"Apple","version_name":"0.22.4","library":{"name":"amplitude-ios","version":"8.10.0"},"os_name":"ios","platform":"iOS","event_id":2156,"carrier":"EE","timestamp":1659977451654,"groups":{},"os_version":"15.5","device_model":"iPhone13,2","group_properties":{}},{"session_id":<>,"user_properties":{"$set":{"memoriesVideoStatus":"unavailable"}},"language":"English","event_type":"$identify","sequence_number":3134,"user_id":"<>","country":"United Kingdom","api_properties":{"ios_idfv":"<>"},"device_id":"<>","event_properties":{},"uuid":"<>","device_manufacturer":"Apple","version_name":"0.22.4","library":{"name":"amplitude-ios","version":"8.10.0"},"os_name":"ios","platform":"iOS","event_id":971,"carrier":"EE","timestamp":1659977451710,"groups":{},"os_version":"15.5","device_model":"iPhone13,2","group_properties":{}}]
upload_time: 1659977453096
checksum:    <>
```
