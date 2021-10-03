

# Asterisk External Media Sample

This package demonstrates how to use the ARI External Media feature to transcribe
the audio from a bridge using the Google Speech APIs. 

## Installation

#### Prerequisites
* A functional Asterisk 16.6.0+ installation.
* A conference bridge or phone configured.
* Node.JS version 10 or greater.
* Google Speech API credentials set in environment variable GOOGLE_APPLICATION_CREDENTIALS.  
See https://cloud.google.com/speech-to-text/docs/ for more information.

```
;For CentOS 7 User
yum install -y  unzip
curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
sudo yum install -y nodejs

cd /root/asterisk-external-media-master
npm install -g
ari-transcriber --help

;; 구글 STT 인증
export GOOGLE_APPLICATION_CREDENTIALS=makecallio-4dfc1194b038.json

;; W/ Asteirsk
;; ARI 이용한 클라이언트 (구글SST와 연결되는 TCP소켓,  Nodejs 기반)
ari-transcriber --format=slin16 'Local/1002' --listenServer=127.0.0.1:6600 --ariServerUrl=bcs.makecall.io:8089 --ariUser=olssoo --ariPassword=015500 --speechLang=ko-KR --speakerDiarization true

;; 외부미디어 (ari-transcriber가 운영되는 서버) 
https://bcs.makecall.io:8089/ari/channels/externalMedia?app=olssoo-app&external_host=127.0.0.1%3A6600&encapsulation=rtp&transport=udp&connection_type=client&format=slin16&direction=both&api_key=olssoo:015500

;; Without Asterisk
;; ARI 이용한 클라이언트 (구글SST와 연결되는 TCP소켓,  Nodejs 기반)
ari-transcriber --format=slin16 'Local/1002' --listenServer=0.0.0.0:6600 --ariServerUrl=bcs.makecall.io:8089 --ariUser=olssoo --ariPassword=015500 --speechLang=ko-KR --speakerDiarization true

;; 외부미디어 (ari-transcriber가 운영되는 서버) 
https://bcs.makecall.io:8089/ari/channels/externalMedia?app=olssoo-app&external_host=172.31.0.100%3A6600&encapsulation=rtp&transport=udp&connection_type=client&format=slin16&direction=both&api_key=olssoo:015500

```




```
;구글 인증 파일
;makecallio-4dfc1194b038.json

{
  "type": "service_account",
  "project_id": "makecallio",
  "private_key_id": "4dfc1194b038af1610f48e7710dc93a696068bc8",
  "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCnB+l0tPHWZ2De\nxrK+TnFQNLyBnDN/8HQqeaAIt9EP1G85uS3W+Zut2fZi/fH8KKVfTXU768rMOSJr\nRX1PEuoOjohi6onKsJmM94vNmQbdGHHi3M/B5DPuTiJC92zX12MyZM0eA4rhUfly\nLACOhdYqNLlKZ3FmLVj7Qrfc6OiHx5kr2cpCQ6mOjLh52ZCfQo+p30dniwMPAr9W\n+uiOUVZNsmHPBpWFRd8MTBDPLnOMzOblvH+sX47/BiWOjQ5QqPfblqYRea/xqkuf\nqcQX9zRxQXqY324uVkE/FZtZwTl+EhBZi0GzM6giNqu+BUY4WWiVqO977R305kme\nz19CpteDAgMBAAECggEAPYP38oALiyuirRlfzh/ksqXhgRiOjQF5PwVxL5THPb2+\nwvMU01Y1hDdAe1/MZdJwaWOFGC70jvdB2mEKz/sG0Zqj105KtigJPTYUOoGv2fC9\nTNCHAYEysQL8sk4eu3V7dp1SP8oNNYOzy10yTUs0P3IQhbsINBniahM91PHAZfS/\n3Upxk+JHemYUt6y5WJVMSubRLtNyCGvp2n0G1djTEPJYzJ9nOjZscZkuQwPo+SXw\nfDneQSV4UxczG0vHbeSZBtqxUMzpc3EjBOmoM+nZkXRPDIrZiBEL0ubfjXzvvlm6\nzxA3Rzp+7bQUs9PKOvjjIWXUyU8NJI+ChLQ3dKMAWQKBgQDXpA93egMl4nOYretY\n5V+daCg7dcdajPrfvzgKsvsDXk/IIWqAsnPeraJGEKTKD7triCHNlGMc0qDV+p1u\najUDjaUb2NJzjsTKqVKFXsnpwIFvxLHs7GV51Tbci5NhIhw5KPAvmjsppb5i+STH\nhYBh5+m2x8gekaUlif+pkRQvmwKBgQDGStEFzaAp73a1QiuxG254AYDIoTUvShlJ\nPl9JGU7xYAUn42ncpVKjiZtlNSr5W+c21hgJTd/jgxzqSDPhHIoqM3vRfZ5ca0Tv\nS1J/WNgg2blJOOLUhghOE9m+s2dKvYMvMAWqhvX6jUJ1Q32AABvBOwuJmMbNncNC\nO5y30l+aOQKBgDqzPkKXxCOb8TuunFImnlCK+ei1tv6/QcuGkgrXjdzs32rrLcK6\n0S/ctD++aB1ZCvvKoukDa7d83qtg/VoBL004Uamy7Bbo1kkUrpH/q5cmABYcxRJp\nh3YSxExk8kmOr4Af1MIgidpcc+cdSxXFEZ2VM9m9qIwpuXruhdny1DvhAoGAVL4U\npk5CbKmSKdSlp4L5qv+5cgSzHgqk09B8GFlgi3dlvK5Lx6g/sPRWHOKkAv1rytuk\nWhWV4T1fViCVS1dPFMn72IO+8fBF/Z5LG3F0rFVgAhL1na3KTtPc8srpEd/7+Gal\nhUM4TGOiS0sUj2d8dRAu1hccnzMVB3FCgKy/fsECgYA0zLs+GeF+OIU/xhyTXCNt\nq6s3QbOV1dg8fQiPooa8YiVqAe43RjGA4LmqW+zh5IRye0/YqPlWuPuY/+lw0mA2\nqRoJdnsFC0uIQFebKzdUgP5fxVd2Sl5krloV5twVD41NIYcbKwjixCIT+hi2rVbC\nBDTkt+7f7Ay6BgHGFbgIcg==\n-----END PRIVATE KEY-----\n",
  "client_email": "793164633643-compute@developer.gserviceaccount.com",
  "client_id": "104853134327062216473",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/793164633643-compute%40developer.gserviceaccount.com"
}
```


Run `npm install` from the top of the source tree.
This will install the required npm packages including `node-ari-client` and `@google-cloud/speech`.
You can then run the transcriber as `bin/ari-transcriber`.  If you add the `-g`
option to `npm install` to install system wide, you can just run `ari-transcriber`. 

## Usage

```
$ ari-transcriber --help
ari-transcriber [options] <dialstring>

Start the transcription server

Positionals:
  dialstring  Extension to dial such as "Local/1234"

Incoming Audio Server
  --format, -f        Asterisk format/codec                                         [string] [choices: "ulaw", "slin16"] [default: "ulaw"]
  --listenServer, -l  Address and port on which to listen for audio from Asterisk                     [string] [default: "127.0.0.1:9999"]

Speech
  --speechModel         Google Speech API model                  [string] [choices: "phone_call", "video", "default"] [default: "default"]
  --speechLang          BCP-47 Language code.  en-US, fr-CA, etc.                  [string] [choices: "en-US", "fr-CA"] [default: "en-US"]
  --speakerDiarization  Outputs words associated to speaker index to the console.                               [boolean] [default: false]

ARI
  --ariServerUrl, -a  The URL for the Asterisk instance                                        [string] [default: "http://127.0.0.1:8088"]
  --ariUser, -u       The user configured in ari.conf                                                       [string] [default: "asterisk"]
  --ariPassword, -p   The password for the user configured in ari.conf                                      [string] [default: "asterisk"]

Transcription WebSocket
  --sslCert  WebSocket secure server (wss) certificate. If omitted, a non-secures (ws) websocket server will be created           [string]
  --sslKey   WebSocket secure server key. Must be supplied if sslCert is ssplied                                                  [string]
  --wssPort  WebSocket server port.  If omitted, no websocket server will be started                                              [number]

Options:
  --version          Show version number                                                                                         [boolean]
  --help             Show help                                                                                                   [boolean]
  --audioOutput, -o  A file into which the raw audio from Asterisk can be written                                                 [string]

Examples:
  ari-transcriber --format=slin16 --sslCert=/etc/letsencrypt/live/myserver/fullchain.pem
  --sslKey=/etc/letsencrypt/live/myserver/privkey.pem --wssPort=39990 --speakerDiarization 'Local/1234'
```

The ari-transcriber performs several tasks:
* Creates an ari-client instance
* Creates a WebSocket server from which the live transcription can be accessed
* Starts an audio server to receive the audio from Asterisk
* Creates an instance of Google Speech Provider that takes the audio from the server, transcribes it, and sends the transcription out the websocket
* Uses the ARI instance to:
  * Create a mixing bridge
  * Create a Local channel which dials the conference bridge to be monitored
  * Place the local channel into the mixing bridge
  * Create an External Media channel that directs the audio to the audio server
  * Place the External Media channel into the mixing bridge

Why the Local channel and bridge?  To keep the sample as simple as possible,
it's assumes that a conference bridge is already available.  Since that
bridge wouldn't be controlled by ARI/Stasis, we can't just add the External
Media channel directly to it.  Instead we have to create a Local channel that _dials_
the conference bridge, then bridge _that_ channel with the External Media
channel.  If you were ading External Media capabilities to your own application,
chances are that your app would already control the participant bridge and you
wouldn't need the Local channel and mixing bridge.

## Try It!

You don't need the WebSocket transcription server to try this.
Just a phone to call.

```
$ export GOOGLE_APPLICATION_CREDENTIALS=<path to Google API credentials>
$ ari-transcriber --format=slin16 'Local/1234'
```

