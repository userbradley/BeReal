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
      "blockedAt": "2006-01-02T15:04:05-0700",
      "user": {
        "id": "string",
        "username": "string",
        "fullname": "string"
      }
    }
  ]
}
```

