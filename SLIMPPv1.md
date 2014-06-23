
# SLIMPP

Simple, Light Instant Messaging and Presence Protocol


# Overview
 
SLIMPP is designed for Mobile IM, because XMPP is boring and burdensome. 


# Design Principle

1. Designed for Mobile and Iternat of Thing.

2. JSON over HTTP and MQTT.

3. Rapid integrate with web and mobile APP.


# Architecture

Simple, Light protocol design based on HTTP and MQTT.

Send and Push by two different channel:

1. SEND Channel(always HTTP)

    Client————SEND———>Server

2. PUSH Channel(HTTP poll, websocket or mqtt)

    Client<———PUSH———Server

3. Send and Receive

    Client———Send—-—>Server
      |                |
      |                |
      |<————Push———————|


# Addressing


    /domain/${domain}/node/${node}/client/${clientid}

    /domain/${domain}/room/${room}/

# Objects

## OID

OID(object id) identify a unique router endpoint, for example, an user, a room or a service.

## Presence

### Properties

Name            |Type   |Req    |Description
------------------------|-------|-------|------------
id              |string |true   |
from            |string |true   | presence from
type            |string |true   | online | offline | subscribe | subscribed | unsubscribe | unsubscribed
show            |string |true   | away | chat | dnd 
status          |string |true   |
vcard           |object |false  |

### JSON Object

    {
        "id": 'jack',
        "from": "jack",
        "type": "online",
        "show": "online",
        "status": "I am online",
        "status_time": "10:55",
        "vcard": {}
    }


## Message

### Properties 

Name            |Type   |Req    |Description
------------------------|-------|-------|------------
id              |string |true   |
thread          |string |true   |
type            |string |true   | chat, grpchat
body            |string |true   |
timestamp       |long   |true   |

### JSON Object


    {
        'id' : 'ahhaahkakkda',
        ‘headers’: {
            ‘content-type”: ‘docfile’,
        },
        'type' : 'chat',
        ‘thread’ : ‘threadid’,
        ‘body’ : “blablabla…”,
        ‘timestamp’ : 1938294828
    }

    content-type: "text" / "image" / "audio" / "video" /


## Buddy

### Properties 

Name            |Type   |Req    |Description
------------------------|-------|-------|------------
id              |string |true   |
name            |string |true   |
nick            |string |true   |
group           |string |true  
avatar          |string |true 


### JSON Object

    {
        'id' : 'ahhaahkakkda',
        'name' : 'jack',
        'nick' : 'Jack',
        'group' : 'friend',
        'avatar' : 'http://gravatar.com/kakdakddj28dj.png'
    }
    

## Room

### Properties 

### Properties 

Name            |Type   |Req    |Description
------------------------|-------|-------|------------
id              |string |true   |
name            |string |true   |
nick            |string |true   |
group           |string |true  
avatar          |string |true 

### JSON Object

    {
        'id' : 'ahhaahkakkda',
        'name' : 'room',
        'nick' : 'Room1',
        'group' : 'RD',
        'avatar' : 'http://gravatar.com/kakdakddj28dj.png'
    }

## Client

### Properties 

Name            |Type   |Req    |Description
----------------|-------|-------|------------
type            |string |true   | web/mac/windows/linux/android/ios
appid           |string |true   |
deviceid        |string |true   |
clientid        |string |true   |
ticket          |string |true   |

### JSON Object
    
    {
        'appid': 'livehub.io',
        'deviceid': 'android-2922',
        'clientid': 'livehub-android-akakkdk',
        'ticket': 'uuidticket'
    }
        



# Design

## Authentication

### Login

    POST /app/login

    POST /slimpp/v1/login

### Logout
    
    POST /app/login

    GET or POST /slimpp/v1/login

## Presence Management

### Online

    POST /slimpp/v1/presences/online

### Show

    POST /slimpp/v1/presences/show


### Offline

    POST /slimpp/v1/presences/offline

## Send Message

    POST /slimpp/v1/messages/

## Send Status

    POST /slimpp/v1/statuses/

## Attachments

Files, Images, Video and Audio


    POST /slimpp/v1/attachements/（发送文件、图片、视频）

    POST /slimpp/v1/upload/ (上传文件、图片、语音、视频)

## Buddy Management

### GET Buddies(上线时读取buddies)

    GET /slim/v1/buddies

    {
        buddies: []
    }


### Add Buddies

    POST /slimpp/v1/buddies/

    buddy name
    buddy group


### Update Buddies

    PUT /slimpp/v1/buddies/${id}/

### Delete Buddies

    DELETE /slimpp/v1/buddies/${id}

### BLOCK Buddies

    POST /slimpp/v1/buddies/${id}/block

### Unblock Buddies

    POST /slimpp/v1/buddies/${id}/unblock


## Room Management


### Room Type

1. persistent

2. temporary

### GET Rooms

    GET /slimpp/v1/rooms

### Create Room

    POST /slimpp/v1/rooms/

    TODO: paramters

### Get Members

    GET /slimpp/v1/rooms/${room}/members/

### Invite Members

    POST /slimpp/v1/room/${room}/members/

### Join Room

    POST /slimpp/v1/rooms/${room}/join

### Leave Room

    POST /slimpp/v1/rooms/${room}/leave

### Block Room

    POST /slimpp/v1/rooms/${room}/block

### Unblock Room

    POST /slimpp/v1/rooms/{$room/unblock



# Message Router

## Send

## Push

## PubSub

    User OID:

    /domain/abc.com/node/1

    /domain/def.com/node/1

    Room OID:

    /domain/abc.com/room/1

    /domain/def.com/room/1

## Topic

route message and statues with pub sub.

publish to /domain/${domain}/${class}/${id}

## Rate Limit

Rate limit requests from clients to protect the health of the service and maintain high service quality for other clients. You can use a token bucket algorithm to quantify request limits.

Return the remaining number of request tokens with each request in the RateLimit-Remaining response header. 

http://en.wikipedia.org/wiki/Token_bucket



# Implementation

PHP + Erlang


# Author

slimpp.io


# Referrence

WhatsApp

XMPP
