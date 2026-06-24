# API Error Handling Guide

When integrating with the WeatherAPI, developers may encounter errors due to invalid requests, authentication failures, or server-side issues. This guide outlines the standard HTTP status codes, error codes, and the structure of error responses returned by our API.

## HTTP Status Codes

We use standard HTTP response codes to indicate the success or failure of an API request.

### 1. Client-Side Errors (4xx)

These status codes indicate that there was an issue with the request sent by the client (e.g., missing parameters, invalid key, or incorrect URL structure).

| HTTP Status | Error Name | Common Cause | How to Fix |
| --- | --- | --- | --- |
| 400 | Bad Request | The city name query parameter `q` is empty or invalid. | Verify that the `q` parameter is not empty and contains a valid location name. |
| 401 | Unauthorized | The API key parameter `key` is invalid or missing. | Check your dashboard to ensure you are passing the correct API key. |
| 403 | Forbidden | Your API key does not have access to this resource. | Upgrade your subscription plan or check your API key permissions. |
| 404 | Not Found | The requested endpoint does not exist. | Double-check the URL path for typos (e.g., `/v1/current.json`). |
| 429 | Too Many Requests | The API key has exceeded its monthly request limit. | Upgrade your subscription plan or implement local caching to reduce requests. |

### 2. Server-Side Errors (5xx)

These status codes indicate that something went wrong on the Weather API servers. The developer's request was correct, but the system is temporarily down.

| HTTP Status | Error Name | Common Cause | How to Fix |
| --- | --- | --- | --- |
| 500 | Internal Error | An unexpected error occurred on the weather server. | Retry the request after a few seconds. If the issue persists, contact support. |
| 503 | Service Unavailable | The server is temporarily offline for maintenance. | Wait a few minutes and try the request again. |

## Error Response Structure (JSON)

In the event of an error, the API returns a detailed error description in JSON format to help developers diagnose the issue.

JSON Error Example (HTTP 400 Bad Request)

```json
{
  "error": {
    "code": 1003,
    "message": "Parameter 'q' is missing.",
    "type": "invalid_request_error"
  }
}
```

## Response Fields

| Field Name | Type | Description |
| --- | --- | --- |
| error.code | Integer | Internal WeatherAPI unique error identifier. |
| error.message | String | A human-readable description of what went wrong. |
| error.type | String | Categorization of the error (e.g., `invalid_request_error` or `authentication_error`). |