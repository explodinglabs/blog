---
layout: post
title: ZeroMQ Request/Reply in C
permalink: /c/zeromq/request-reply
---
* TOC
{:toc}

## Server

The server should handle incoming JSON-RPC requests on port 5000.

Install the [czmq](https://github.com/zeromq/czmq) library.

Write a server script, `server.c`:

```c
#include <czmq.h>

int main(void) {
    // Connect
    zsock_t *responder = zsock_new_rep("tcp://*:5000");
    // Recv
    char *string = zstr_recv(responder);
    puts(string);
    zstr_free(&string);
    // Send
    zstr_send(responder, "Pong");
    // Disconnect
    zsock_destroy(&responder);
    return 0;
}
```

Build and start the server:

```sh
$ gcc -lczmq server.c -o server
$ ./server
```

## Client

Write client script:

```c
#include <czmq.h>

int main(void) {
    // Connect
    zsock_t *requester = zsock_new_req("tcp://127.0.0.1:5000");
    // Send
    zstr_send(requester, "Ping");
    // Recv
    char *string = zstr_recv(requester);
    puts(string);
    zstr_free(&string);
    // Disconnect
    zsock_destroy(&requester);
    return 0;
}
```

Build and run:

```sh
$ gcc -lczmq client.c -o client
$ ./client
Pong
```
