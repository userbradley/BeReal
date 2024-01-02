---
title: "API endpoint: messaging"
---


## Verified Endpoints

| URL                                                                          | Use                            |
|------------------------------------------------------------------------------|--------------------------------|
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/SendMessage`          | POST message                   |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetMessages`          | GET message                    |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetConversationsById` | GET message with the member id |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetConversationFeed`  | GET the conversation Feed      |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetPendingInvites`    | GET the pending invitations    |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/ClearConversation`    | POST clear message Feed        |
| `https://ogma.bereal.team/chat.core.v1.ChatCoreService/GetSentInvites`       | GET invitations                |

### `Send a message`

```
gRPC message 0 (compressed False)
[message]    1                               
[message]    1.1                             
[message]    1.1.1                           
[string]     1.1.1.1  “ID”
[message]    1.2                             
[uint32]     1.2.1    1                      
[string]     1.2.2    this is a message

```
