---
title: Network
description: Network
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "network"
  - "coding"
comments: true
---
## Hypertext Markup Language (HTML)

- A text-based approach to describe how content contained within an HTML file is structured.

---

## Hypertext Transfer Protocol (HTTP)

- It enables communications between clients and servers.
- It works as a request-response protocol between a client and server.

### Anatomy of an HTTP request

- An HTTP request must have the following:
  - An HTTP method (like `GET`)
  - A host URL (like `https://api.spotify.com/`)
  - An endpoint path (like `v1/artists/{id}/related-artists`)
  - Optional:
    - Body
    - Headers
    - Query strings
    - HTTP version

### Anatomy of an HTTP response

- A response must have the following:
  - Protocol version (like `HTTP/1.1`)
  - Status code (like  `200`)
  - Status text (`OK`)
  - Headers
  - Optional:
    - Body

### HTTP methods

- `POST`, `PUT`, `PATCH`, and `DELETE` can change data on the server.

#### 1. `GET`

- It requests data from a specified resource.
- Query string (name/value pairs) is sent in the URL of a `GET` request.
- It reads or retrieves a resource.
- A successful `GET` returns a response containing the information you requested.

- In a weather app, `GET` retrieves the current weather for a specific city.

#### 2. `POST`

- It creates a new resource.
- It requires a body in which you define the data of the entity to be created.
- A successful `POST` request would be a `200` response code.

- In a weather app, `POST` adds weather data about a new city.

- `POST`ing multiple times would create multiple separate orders.

#### 3. `PUT`

- It updates the entire resource with data that is passed in the body payload.
- If no resource matches the request, it will create a new resource.

- In a weather app, `PUT` updates all weather data about a specific city.

- Multiple PUT requests will update the same existing order.

#### 4. `HEAD`

- It is like `GET` without the response body.

#### 5. `DELETE`

- It deletes the specified resource.

- In a weather app, `DELETE` deletes a city we no longer wanted to track for some reason.

#### 6. `PATCH`

- It modifies a part of a resource.
- You only need to pass in the data that you want to update.

- In a weather app, `PATCH` updates the rainfall for a specified day in a specified city.

#### 7. `OPTIONS`

- It describes the communication options for the target resource.

#### 8. `CONNECT`

- It starts a two-way communication (a tunnel) with the requested resource.

#### 9. `TRACE`

- It performs a message loop-back test that tests the path for the target resource (useful for debugging purposes).

---

## Secure Shell (SSH)

- A network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.

---

## Transmission Control Protocol (TCP)

- TCP and IP are the basic rules that define the Internet.
- TCP is a standard that defines how to establish and maintain a network conversation by which applications can exchange data.
  - It determines how to break application data into packets that networks can deliver.
  - It sends packets to and accepts packets from, the network layer.
  - It manages flow control.
  - It acknowledges all packets that arrive.
  - It handles the retransmission of dropped packets, as it's meant to provide error-free data transmission.

---

## User Datagram Protocol (UDP)

- It reduces latency and jitter by not reordering packets or retransmitting missing data.
- It discards invalid data packets.
