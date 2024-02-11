---
title: "API endpoint: messaging"
---


## Verified Endpoints

| URL                                                                             | Use                            |
|---------------------------------------------------------------------------------|--------------------------------|
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/SendMessage`             | POST message                   |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetMessages`             | GET message                    |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetConversationsById`    | GET message with the member id |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/CreateConversation`      | POST create a Groups 		   |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetConversationFeed`     | GET the conversation feed      |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetPendingInvites`       | GET the pending invitations    |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/ClearConversation`       | POST clear message feed        |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetSentInvites`          | GET invitations                |
| `https://ogma.bereal.team/media.upload.v1.MediaUploadService/CreateUploadUrls`  | POST upload a BeReal in chat   |
| `https://ogma.bereal.team/realtime.core.v1.RealTimeStreamService/Stream`        | GET new uploads                |
| `https://ogma.bereal.team/officialaccounts.feed.v1.FeedService/GetOAFanFeed`    | GET official accounts feed     |

## Chat images Storage Endpoint

| URL                                                                             | Use                            |
|---------------------------------------------------------------------------------|--------------------------------|
| `https://storage.googleapis.com/bereal-us-central1-chat-media/User_ID/ID.webp`  | GET chat images                |