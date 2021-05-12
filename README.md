# Voodfy API example

This is a bare-bones example of a Voodfy API REST API.

# REST API

The REST API to the example app is described below.

## Authenticate

### Request

`POST /v1/auth/`

    curl -v -i -H 'Accept: application/json' -H "Origin: https://portal.voodfy.com" -H "Content-Type: application/json" --data-raw '{"email":"demo@voodfy.com","password":"demovoodfy54321"}' https://api-1.voodfy.com/v1/auth

### Response
    HTTP/2 200
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    {"code":200,"msg":"ok","count":0,"next":"","previous":"","result":{"user":{"active":true,"email":"foo@foo.com","firstName":"bar","id":"5f1e012dbbc82e26fc9e11c1","is_staff":false,"is_superuser":false,"lastName":"barrrrr","notifications":false,"token":"token"}}}

## Get videos 

### Request

`GET /v1/me`

    curl -v 'https://api-1.voodfy.com/v1/me?page=1&size=9' -H 'accept: application/json, text/plain, */*' -H 'Authorization: Token <token>'

### Response

    HTTP/2 200
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    {"code":200,"msg":"ok","count":0,"next":"","previous":"","result":{"videos":[]}}

## Get a specific video

### Request

`GET /v1/videos/:id`

    curl -i -H 'Accept: application/json' -H "Content-Type: application/json" -H 'authorization: Token <token>' https://api-1.voodfy.com/v1/videos/:id

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 36

    {
      "code": 200,
      "msg": "ok",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "video": {
        "access": "",
        "cid": "<cid>",
        "createdAt": "<createdAt>",
        "description": "",
        "duration": <duration>,
        "id": "<id>",
        "ipfs": "<ipfs>",
        "kind": "video",
        "poster": "<poster>",
        "size": <size>,
        "tags": "",
        "thumbnailPreview": {
          "numColumns": 0,
          "numThumbs": 0,
          "thumbHeight": 73,
          "thumbWidth": 126,
          "timeInterval": 5,
          "url": "<thumbs_preview>"
        },
        "title": "<title>",
        "tracker": "<tracker>"
        }
      }
    }

## Get video player playlist

### Request

`GET /v1/videos/:id/player?playerType=chrome&origin=localhost`

    curl -i -H 'Accept: application/json' -H "Authorization: Token <token>" https://api-1.voodfy.com/v1/videos/:id/player?playerType=chrome&origin=localhost`

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    {
      "code": 200,
      "msg": "ok",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "video": {
          "access": "",
          "cid": "<cid>",
          "cors": [],
          "description": "",
          "duration": <duration>,
          "embed": {
            "autoPlay": false,
            "cors": [],
            "encrypted": false,
            "loop": false,
            "muted": false,
            "p2p": false,
            "password": "",
            "passwordProtected": false,
            "playAndPause": true,
            "qualityLevel": true,
            "speedRate": false,
            "subtitles": false,
            "timeline": true,
            "urlTokenized": false,
            "volume": true
          },
          "encrypted": false,
          "id": "<id>",
          "ipfs": "<ipfs>",
          "kind": "video",
          "passwordProtected": false,
          "playlist": {
            "name": "DASH",
            "quality": "ultra",
            "url": "<playlist>",
            "version": 0
          },
          "poster": "<poster>",
          "tags": "",
          "thumbnailPreview": {
            "numColumns": 0,
            "numThumbs": 0,
            "thumbHeight": 73,
            "thumbWidth": 126,
            "timeInterval": 5,
            "url": "<url>"
          },
          "title": "<title>",
          "tracker": "<tracker>",
          "urlTokenized": false
        }
      }
    }

## Add live stream

### Request

`POST /v1/transmissions`

    curl --request POST--header 'Authorization: Token <token>' --header 'Content-Type: application/json' --data '{"title": "title", "description": "description", "poster": "poster"}' https://publish.voodfy.com/v1/transmissions

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    {
      "code": 1076,
      "msg": "Transmission created",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "transmission": {
          "id": "609a91d4e64d1ec8e4e0c3c8",
          "kind": "transmission",
          "playlist": {
            "name": "",
            "quality": "",
            "url": "https://stream-2.voodfy.com/hls/voodfy+1272d3a570b0064e77e3a73bb30f5280/index.m3u8",
            "version": 0
          },
          "rtmpURL": "rtmp://localhost/live",
          "srtURL": "srt://live:7000?streamid=localhost",
          "streamKey": "voodfy+1272d3a570b0064e77e3a73bb30f5280"
        }
      }
    }

## Get live stream

### Request

`GET /v1/transmissions/:id`

    curl --request GET --url http://localhost:8083/v1/transmissions/609a8d83e64d1e868f7b60bb --header 'Authorization: Token <token>'

### Response

    {
      "code": 1076,
      "msg": "ok",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "transmission": {
          "id": "609a91d4e64d1ec8e4e0c3c8",
          "kind": "transmission",
          "playlist": {
            "name": "",
            "quality": "",
            "url": "https://stream-2.voodfy.com/hls/voodfy+1272d3a570b0064e77e3a73bb30f5280/index.m3u8",
            "version": 0
          },
          "rtmpURL": "rtmp://localhost/live",
          "srtURL": "srt://live:7000?streamid=localhost",
          "streamKey": "voodfy+1272d3a570b0064e77e3a73bb30f5280"
        }
      }
    }

## Get live streams

### Request

`GET /v1/transmissions`

    curl --request GET --url http://localhost:8083/v1/transmissions --header 'Authorization: Token <token>'

### Response

    {
      "code": 1076,
      "msg": "ok",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "transmissions": [{
          "id": "609a91d4e64d1ec8e4e0c3c8",
          "kind": "transmission",
          "playlist": {
            "name": "",
            "quality": "",
            "url": "https://stream-2.voodfy.com/hls/voodfy+1272d3a570b0064e77e3a73bb30f5280/index.m3u8",
            "version": 0
          },
          "rtmpURL": "rtmp://localhost/live",
          "srtURL": "srt://live:7000?streamid=localhost",
          "streamKey": "voodfy+1272d3a570b0064e77e3a73bb30f5280"
        }]
      }
    }

## Update live stream

### Request

`PATCH /v1/transmissions/:id`

    curl --request PATCH --header 'Authorization: Token <token>' --header 'Content-Type: application/json' --data '{"title": "title", "description": "description", "poster": "poster"}' https://publish.voodfy.com/v1/transmissions/:id

### Response

    HTTP/1.1 200 OK
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    {
      "code": 200,
      "msg": "ok",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {
        "transmission": {
          "id": "609a91d4e64d1ec8e4e0c3c8",
          "kind": "transmission",
          "playlist": {
            "name": "",
            "quality": "",
            "url": "https://stream-2.voodfy.com/hls/voodfy+1272d3a570b0064e77e3a73bb30f5280/index.m3u8",
            "version": 0
          },
          "rtmpURL": "rtmp://localhost/live",
          "srtURL": "srt://live:7000?streamid=localhost",
          "streamKey": "voodfy+1272d3a570b0064e77e3a73bb30f5280"
        }
      }
    }

## DELETE live stream

### Request

`DELETE /v1/transmissions/:id`

    curl --request DELETE --header 'Authorization: Token <token>' --header 'Content-Type: application/json' https://publish.voodfy.com/v1/transmissions/:id 

### Response

    {
      "code": 1083,
      "msg": "Transmission deleted",
      "count": 0,
      "next": "",
      "previous": "",
      "result": {}
    }

## Add video with CID

### Request

`POST /v1/videos-cid`

    curl -v -i -H 'Accept: application/json' -H "Origin: https://portal.voodfy.com" -H "Content-Type: application/json" --data-raw '{"cid": "<cid>"}' https://publish.voodfy.com/v1/videos-cid

### Response
    HTTP/2 200
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    {"code":200,"msg":"ok","count":0,"next":"","previous":"","result": {"resource": {
      "file_id": "",
      "filename": "<cid>",
      "folder": "<folder>",
      "id": "<id>",
      "state": 0,
      "tasks": null,
      "tracker": "<tracker>",
      "type": "Video"
    },
    "status": "adding..."}}

## Get resource status

### Request

`GET /v1/resources/:resource_id/status`

    curl --request GET --url https://publish.voodfy.com/v1/resources/:resource_id/status --header 'Accept: text/event-stream' --header 'Connection: keep-alive' --header 'Origin: https://beta.voodfy.com' --header 'Referer: https://beta.voodfy.com/' --header 'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:77.0) Gecko/20100101 Firefox/77.0'

### Response
    HTTP/2 200
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    event:message
    data:FINISHED

## Get video by resource id

### Request

`GET /v1/videos?resource=<resource_id>

    curl --request GET --url https://api-1.voodfy.com/v1/videos?resource=<resource_id> --header 'Origin: https://beta.voodfy.com' --header 'Referer: https://beta.voodfy.com/' --header 'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:77.0) Gecko/20100101 Firefox/77.0'

### Response
    HTTP/2 200
    Date: Thu, 24 Feb 2011 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    {
      "code": 200,
      "msg": "ok",
      "count": 1,
      "next": "",
      "previous": "",
      "result": {
        "videos": [
          {
            "access": "",
            "cid": "<cid>",
            "createdAt": "2021-05-12 23:28:36",
            "description": "",
            "duration": 0,
            "id": "<cid>",
            "ipfs": "<ipfs>",
            "kind": "video",
            "poster": "<poster>",
            "size": 0,
            "tags": "",
            "thumbnailPreview": {
              "numColumns": 83,
              "numThumbs": 166,
              "thumbHeight": 73,
              "thumbWidth": 126,
              "timeInterval": 5,
              "url": "<thumbs_preview>"
            },
            "title": "<title>",
            "tracker": "<tracker>"
          }
        ]
      }
    }
