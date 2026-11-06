# ws-gateway

A WebSocket gateway written in Go that handles the real-time side of an app so the main backend doesn't have to.

I've built real-time chat features a few times now, and each time I ended up rewriting the same pieces: tracking connections, grouping users into rooms, keeping multiple servers in sync, dealing with dropped connections. This project pulls all of that into one standalone service that any app can sit behind.

## How it's meant to work

Clients connect to the gateway over WebSockets and join rooms (a chat session, a team dashboard, whatever the app needs). When your backend wants to push something out, it makes a simple HTTP call to the gateway, and the gateway delivers it to everyone in that room. Your backend never has to hold a socket open.

Run more than one instance and they stay in sync through Redis, so it doesn't matter which server a client happens to be connected to.

## What I'm planning to build

- Connection handling with heartbeats to clean up dead connections
- Rooms and message routing (to a user, a room, or everyone)
- Pluggable JWT authentication
- An HTTP publish API for backend services
- Redis pub/sub so multiple instances can share the load
- Presence (who's online) and typing indicators
- Reconnection that catches clients up on messages they missed
- Rate limiting so one noisy client can't slow everyone down
- Metrics and load tests to see how far it scales
- A small TypeScript client for the browser side
- A Docker setup and examples to get running quickly

## Status

Early days. Starting with the core connection and room handling, then building outward from there.

## License

MIT
