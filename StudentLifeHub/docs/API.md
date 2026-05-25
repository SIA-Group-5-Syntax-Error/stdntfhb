# API Documentation

## Table of Contents

1. Book Search
2. Announcements List
3. Get Announcement by ID
4. Create Announcement
5. Update Announcement
6. Delete Announcement
7. Dictionary Search
8. List Tasks
9. Create Task
10. Update Task
11. Delete Task
12. Authentication
13. Status Codes

---

# Base URL

```text
http://127.0.0.1:8000
```

---

# 1. Book Search

## Endpoint

```http
GET /api/books/search
```

## Description

Search books by title.

---

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| title | string | Yes | Book title to search |

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "service": "book-search-api",
  "results": [
    {
      "id": 1,
      "title": "Introduction to Algorithms",
      "author": "Thomas H. Cormen",
      "isbn": "0262033844",
      "published_at": "2009-07-31",
      "created_at": "2024-01-01T12:00:00Z",
      "updated_at": "2024-01-02T12:00:00Z"
    }
  ]
}
```

---

## Error Response

### Status Code

```text
422 Unprocessable Entity
```

### Response Body

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "title": [
      "The title field is required."
    ]
  }
}
```

---

# 2. Announcements List

## Endpoint

```http
GET /api/announcements
```

## Description

Retrieve a list of announcements proxied from the upstream announcement service.

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "status": "success",
  "data": [
    {
      "title": "Campus Orientation",
      "date": "2025-08-14 09:00",
      "content": "Orientation for new students will be held in the main auditorium."
    },
    {
      "title": "Library Hours Changed",
      "date": "2025-09-01 08:30",
      "content": "Library opening hours updated for the fall semester."
    }
  ]
}
```

---

## Error Response

### Status Code

```text
502 Bad Gateway
```

### Response Body

```json
{
  "error": "Could not load announcements."
}
```

---

# 3. Get Announcement by ID

## Endpoint

```http
GET /api/announcements/{id}
```

## Description

Retrieve a specific announcement by ID.

---

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | integer | Yes | Announcement ID |

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "id": "123",
  "title": "Student Council Meeting",
  "description": "Monthly meeting in Conference Room B",
  "date": 1712001600
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "message": "Announcement not found"
}
```

---

# 4. Create Announcement

## Endpoint

```http
POST /api/announcements
```

## Description

Create a new announcement.

---

## Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

---

## Request Body

```json
{
  "title": "New Event",
  "content": "Event details here"
}
```

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "id": "456",
  "title": "New Event",
  "content": "Event details here",
  "date": 1712100000
}
```

---

## Error Response

### Status Code

```text
422 Unprocessable Entity
```

### Response Body

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "title": [
      "The title field is required."
    ]
  }
}
```

---

# 5. Update Announcement

## Endpoint

```http
PUT /api/announcements/{id}
```

## Description

Update an existing announcement.

---

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | integer | Yes | Announcement ID |

---

## Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

---

## Request Body

```json
{
  "title": "Updated Title",
  "content": "Updated content"
}
```

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "id": "123",
  "title": "Updated Title",
  "content": "Updated content",
  "date": 1712001600
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "message": "Announcement not found"
}
```

---

# 6. Delete Announcement

## Endpoint

```http
DELETE /api/announcements/{id}
```

## Description

Delete an announcement.

---

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | integer | Yes | Announcement ID |

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "message": "Announcement deleted"
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "message": "Announcement not found"
}
```

---

# 7. Dictionary Search

## Endpoint

```http
GET /api/dictionary/search
```

## Description

Lookup a word using the external dictionary API.

---

## Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| word | string | Yes | Word to search |

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "status": "success",
  "word": "hello",
  "definition": "Used to express a greeting."
}
```

---

## Error Response

### Status Code

```text
400 Bad Request
```

### Response Body

```json
{
  "status": "error",
  "message": "No word provided"
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "status": "error",
  "message": "Word not found"
}
```

---

# 8. List Tasks

## Endpoint

```http
GET /api/tasks
```

## Description

Retrieve all tasks from the configured task service.

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
[
  {
    "id": "1",
    "title": "Buy groceries",
    "status": "pending"
  },
  {
    "id": "2",
    "title": "Finish assignment",
    "status": "completed"
  }
]
```

---

## Error Response

### Status Code

```text
502 Bad Gateway
```

### Response Body

```json
{
  "message": "Upstream task service unavailable"
}
```

---

# 9. Create Task

## Endpoint

```http
POST /api/tasks
```

## Description

Create a new task.

---

## Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

---

## Request Body

```json
{
  "title": "Buy groceries",
  "completed": false
}
```

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "message": "Task added successfully",
  "data": {
    "id": "101",
    "title": "Buy groceries",
    "status": "pending"
  }
}
```

---

## Error Response

### Status Code

```text
422 Unprocessable Entity
```

### Response Body

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "title": [
      "The title field is required."
    ]
  }
}
```

---

# 10. Update Task

## Endpoint

```http
PUT /api/tasks/{id}
```

## Description

Update a task status.

---

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | integer | Yes | Task ID |

---

## Request Headers

| Header | Value |
|---|---|
| Content-Type | application/json |

---

## Request Body

```json
{
  "status": "completed"
}
```

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "message": "Task updated successfully",
  "data": {
    "id": "101",
    "title": "Buy groceries",
    "status": "completed"
  }
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "message": "Task not found"
}
```

---

# 11. Delete Task

## Endpoint

```http
DELETE /api/tasks/{id}
```

## Description

Delete a task.

---

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| id | integer | Yes | Task ID |

---

## Success Response

### Status Code

```text
200 OK
```

### Response Body

```json
{
  "message": "Task deleted successfully"
}
```

---

## Error Response

### Status Code

```text
404 Not Found
```

### Response Body

```json
{
  "message": "Task not found"
}
```

---

# Authentication

No authentication is required for these endpoints.

---

# Status Codes

| Status Code | Description |
|---|---|
| 200 OK | Successful request |
| 400 Bad Request | Missing or invalid request parameter |
| 404 Not Found | Resource not found |
| 422 Unprocessable Entity | Validation failed |
| 502 Bad Gateway | Upstream service unavailable |

---

# Postman Collection

```text
postman_collection.json
```