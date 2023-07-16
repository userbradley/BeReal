---
title: "API endpoint: Moderation"
---

## Verified Endpoints

| URL                                                         | Use                                       |
|-------------------------------------------------------------|-------------------------------------------|
| `https://mobile.bereal.com/api/moderation/block-users`      | Gets block users                          |
| `https://mobile.bereal.com/api/moderation/reports/profile`  | Reports a profile to the Moderation Team  |
| `https://mobile.bereal.com/api/moderation/reports/post`     | Reports a post to the Moderation team     |
| `https://mobile.bereal.com/api/moderation/reports/comment`  | Reports a comment to the Moderation team  |
| `https://mobile.bereal.com/api/moderation/reports/realmoji` | Reports a Realmoji to the Moderation team |

## Requests and Responses

### moderation/blocked-users

```json
{
  "prev": "string",
  "next": "string",
  "data": [
    {
      "userId": "string",
      "blockedAt": "2023-02-22T05:12:55.847Z",
      "user": {
        "id": "string",
        "username": "string",
        "fullname": "string"
      }
    }
  ]
}
```

