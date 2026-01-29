# Chat

Public endpoint for reading chat messages. No authentication required. Posting or deleting messages requires authentication and is not documented in this reference.

---

## GET /api/chat/messages

Get chat messages for a token (cursor-based pagination).

**Query parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `token` | string (required) | Token contract address (0x + 40 hex chars). Must pass validation (e.g. validateAddress). |
| `limit` | integer (1–200) | Max number of messages to return (optional, default: 50) |
| `beforeId` | string (MongoDB ObjectId) | If provided, returns messages older than this message ID (for “load more” / previous page) |

**Response:** `data` (array of message objects with e.g. `id`, `user`, `token`, `message`, `reply_to`, `timestamp`, `editedAt`, `username`, `avatar`), `hasMore`, optional `nextCursor`. Messages are returned oldest-to-newest in the array; when `beforeId` is used, they are the ones immediately older than that message.
