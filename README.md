# QA – API Testing Project

**Author:** ASENAI Shiberim
**Tool Used:** Postman  
**API Tested:** JSONPlaceholder (`https://jsonplaceholder.typicode.com`)  
**Date:** March 2026

---

## What Is This Project?

This is a API testing project where I tested a publicly available REST API called JSONPlaceholder. The goal was to simulate what a QA analyst would do on the job — sending real requests, validating responses, checking edge cases, and documenting anything unexpected along the way. Even though this project is minuscule, its a good refresher to have

I tested all four core HTTP methods: GET, POST, PUT, and DELETE. Nothing was just assumed to work — every endpoint was verified manually.

---

## Why JSONPlaceholder?

JSONPlaceholder is a free, open fake API that's widely used for testing and practice. It has no authentication requirements, which made it perfect for focusing purely on request/response validation without setup overhead.

---

## What I Tested

| # | Request Name | Method | Endpoint |
|---|-------------|--------|----------|
| 1 | All Posts | GET | `/posts` |
| 2 | Single Post | GET | `/posts/1` |
| 3 | Post Not Found | GET | `/posts/999` |
| 4 | Create Post | POST | `/posts` |
| 5 | Update Post | PUT | `/posts/10` |
| 6 | Delete Post | DELETE | `/posts/10` |

---

## Test Results

### 1. GET All Posts
- **Expected:** 200 OK, returns a list of all posts
- **Actual:** 200 OK, returned 100 posts in JSON format
- **Status:** Pass

---

### 2. GET Single Post
- **Expected:** 200 OK, returns one post with id, title, body, and userId fields
- **Actual:** 200 OK, all expected fields present
- **Status:** Pass

---

### 3. GET Post Not Found
- **Expected:** 404 Not Found — post ID 999 does not exist
- **Actual:** 404 Not Found
- **Status:** Pass

> **Note:** I also tested `/posts/1001` independently to check behavior beyond the dataset boundary. Also returned 404 as expected. 

---

### 4. POST Create Post
- **Expected:** 201 Created, returns the new post with a generated ID
- **Actual:** 201 Created — however the API ignored the custom `userId` and `id` values I sent and assigned its own
- **Status:** Pass with observation

> **Observation:** The API does not allow a clients to set their own `id` or `userId`. It overrides the values with server-generated ones. 

---

### 5. PUT Update Post
- **Expected:** 200 OK, returns the updated post
- **Actual:** 200 OK, title and body updated successfully
- **Status:** Pass

---

### 6. DELETE Post
- **Expected:** 200 OK, post is removed
- **Actual:** 200 OK returned — but a follow-up GET request confirmed the post still existed
- **Status:** ⚠️ Known Limitation

> **Observation:** The JSONPlaceholder simulates DELETE and returns a success response, but no data is actually removed. The same limitation applies to POST and PUT — changes are not persisted between requests. This is a known characteristic of mock APIs. No error but rather a limitaion issue.

---

## Key Findings Summary

| Finding | Type | Severity |
|---------|------|----------|
| API overrides client-submitted `id` and `userId` on POST | Observation | Low |
| Created posts are not retrievable after POST | Known Limitation | N/A |
| Deleted posts still return on follow-up GET | Known Limitation | N/A |

---

## What I Learned

Going through this project I got comfortable with the full CRUD cycle in Postman — not just sending requests but actually thinking about what the response *should* look like before hitting Send. The most valuable part was discovering the data persistence limitation on my own. It taught me that a 200 or 201 response doesn't automatically mean something worked end-to-end. Always verify with a follow-up request.

---

## Files in This Repo

- `README.md` — this file, full testing documentation
- `jsonplaceholder-api-tests.json` — exported Postman collection, import directly into Postman to run all requests

---

## How to Import the Postman Collection

1. Open Postman
2. Click **Import** in the top left
3. Select the `jsonplaceholder-api-tests.json` file
4. All 6 requests will load into a new collection ready to run

---

*This project is part of my QA portfolio. Built while completing a Software Development diploma at SAIT.*
