# chat
This repository is realtime chat demo app with nuxt.js and socket.io.
The details are written on [Nuxt.js + Socket.ioでルームチャットアプリを作る ~ サーバーフレームワーク選べなくなっててつまずいた夏 - Qiita](https://qiita.com/at-946/items/590e618b041182b151ed).

## Build Setup

```bash
# build docker image
$ docker-compose build

# start docker container
$ docker-compose up
```

You can use the real-time chat application at `http://localhost:3000/chat/:room_id`.(e.g. `http://localhost:3000/chat/1`, `http://localhost:3000/chat/2`, etc.)

Users accessing the same room_id can exchange messages, but users accessing a different room_id can't exchange messages.
