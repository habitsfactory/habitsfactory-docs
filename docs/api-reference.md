# API Reference

Habits Factory exposes a RESTful API built with Django REST Framework. This document covers all available endpoints.

## Base URL

```
Development: http://localhost:8000/api/
Production:  https://api.habitsfactory.io/api/
```

## Authentication

Authentication details will be documented once the auth system is finalized. Currently, the API supports:

- Session-based authentication (development)
- Token-based authentication (planned)

## Response Format

All responses follow a consistent JSON structure:

### Success Response

```json
{
  "id": 1,
  "name": "Morning Exercise",
  "category": 2,
  "created_at": "2024-01-15T08:30:00Z"
}
```

### List Response

```json
{
  "count": 25,
  "next": "http://localhost:8000/api/habits/?page=2",
  "previous": null,
  "results": [
    { "id": 1, "name": "Morning Exercise", ... },
    { "id": 2, "name": "Read 30 minutes", ... }
  ]
}
```

### Error Response

```json
{
  "detail": "Not found.",
  "code": "not_found"
}
```

## Endpoints

### Categories

#### List Categories

```http
GET /api/categories/
```

Returns all habit categories.

**Response**

```json
[
  {
    "id": 1,
    "name": "Health",
    "color": "#4CAF50",
    "created_at": "2024-01-01T00:00:00Z"
  },
  {
    "id": 2,
    "name": "Productivity",
    "color": "#2196F3",
    "created_at": "2024-01-01T00:00:00Z"
  }
]
```

#### Create Category

```http
POST /api/categories/
```

**Request Body**

```json
{
  "name": "Learning",
  "color": "#9C27B0"
}
```

**Response** `201 Created`

```json
{
  "id": 3,
  "name": "Learning",
  "color": "#9C27B0",
  "created_at": "2024-01-15T10:30:00Z"
}
```

#### Get Category

```http
GET /api/categories/{id}/
```

#### Update Category

```http
PUT /api/categories/{id}/
PATCH /api/categories/{id}/
```

#### Delete Category

```http
DELETE /api/categories/{id}/
```

---

### Habits

#### List Habits

```http
GET /api/habits/
```

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `category` | integer | Filter by category ID |
| `is_active` | boolean | Filter by active status |
| `ordering` | string | Sort by field (e.g., `name`, `-created_at`) |

**Response**

```json
{
  "count": 10,
  "results": [
    {
      "id": 1,
      "name": "Morning Exercise",
      "description": "30 minutes of cardio or strength training",
      "category": {
        "id": 1,
        "name": "Health",
        "color": "#4CAF50"
      },
      "is_active": true,
      "created_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Create Habit

```http
POST /api/habits/
```

**Request Body**

```json
{
  "name": "Read 30 minutes",
  "description": "Read non-fiction books",
  "category": 2,
  "is_active": true
}
```

#### Get Habit

```http
GET /api/habits/{id}/
```

#### Update Habit

```http
PUT /api/habits/{id}/
PATCH /api/habits/{id}/
```

#### Delete Habit

```http
DELETE /api/habits/{id}/
```

---

### Habit Entries

Habit entries track daily completions.

#### List Entries

```http
GET /api/entries/
```

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `habit` | integer | Filter by habit ID |
| `date` | string | Filter by date (YYYY-MM-DD) |
| `date_from` | string | Filter entries from date |
| `date_to` | string | Filter entries until date |
| `completed` | boolean | Filter by completion status |

**Response**

```json
{
  "count": 30,
  "results": [
    {
      "id": 1,
      "habit": 1,
      "date": "2024-01-15",
      "completed": true,
      "value": 1,
      "notes": "Great morning workout!"
    }
  ]
}
```

#### Create Entry

```http
POST /api/entries/
```

**Request Body**

```json
{
  "habit": 1,
  "date": "2024-01-15",
  "completed": true,
  "value": 45,
  "notes": "Extended session today"
}
```

#### Bulk Create/Update

```http
POST /api/entries/bulk/
```

Create or update multiple entries at once.

**Request Body**

```json
{
  "entries": [
    { "habit": 1, "date": "2024-01-15", "completed": true },
    { "habit": 2, "date": "2024-01-15", "completed": false },
    { "habit": 3, "date": "2024-01-15", "completed": true, "value": 8 }
  ]
}
```

#### Get Entry

```http
GET /api/entries/{id}/
```

#### Update Entry

```http
PUT /api/entries/{id}/
PATCH /api/entries/{id}/
```

#### Delete Entry

```http
DELETE /api/entries/{id}/
```

---

### Statistics

#### Habit Statistics

```http
GET /api/habits/{id}/stats/
```

Returns statistics for a specific habit.

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `period` | string | `week`, `month`, `year`, `all` |

**Response**

```json
{
  "habit_id": 1,
  "period": "month",
  "completion_rate": 0.85,
  "current_streak": 7,
  "longest_streak": 21,
  "total_completions": 26,
  "average_value": 32.5
}
```

#### Weekly Summary

```http
GET /api/stats/weekly/
```

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `date` | string | Week containing this date (default: current week) |

**Response**

```json
{
  "week_start": "2024-01-08",
  "week_end": "2024-01-14",
  "overall_completion_rate": 0.72,
  "habits": [
    {
      "id": 1,
      "name": "Morning Exercise",
      "completions": 5,
      "completion_rate": 0.71
    }
  ],
  "by_category": [
    {
      "category": "Health",
      "completion_rate": 0.80
    }
  ]
}
```

#### Yearly Summary

```http
GET /api/stats/yearly/
```

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `year` | integer | Year to summarize (default: current year) |

---

### Correlations

#### Get Correlations

```http
GET /api/correlations/
```

Returns correlation analysis between habits.

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `min_strength` | string | Minimum strength: `very_weak`, `weak`, `moderate`, `strong`, `very_strong` |
| `algorithm` | string | `pearson`, `spearman`, `dtw`, or `all` |

**Response**

```json
{
  "correlations": [
    {
      "habit_a": {
        "id": 1,
        "name": "Morning Exercise"
      },
      "habit_b": {
        "id": 3,
        "name": "Healthy Eating"
      },
      "pearson": 0.72,
      "spearman": 0.68,
      "dtw": 0.25,
      "strength": "strong",
      "direction": "positive"
    }
  ],
  "computed_at": "2024-01-15T12:00:00Z",
  "data_points": 45
}
```

---

### Data Export

#### Export to CSV

```http
GET /api/export/csv/
```

**Query Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| `habits` | string | Comma-separated habit IDs (optional) |
| `date_from` | string | Start date |
| `date_to` | string | End date |

**Response**

Returns a CSV file download.

```csv
date,habit_id,habit_name,completed,value,notes
2024-01-15,1,Morning Exercise,true,1,
2024-01-15,2,Read 30 minutes,true,45,Finished chapter 5
```

---

## Error Codes

| Status Code | Description |
|-------------|-------------|
| `200` | Success |
| `201` | Created |
| `204` | No Content (successful deletion) |
| `400` | Bad Request (validation error) |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not Found |
| `500` | Internal Server Error |

## Rate Limiting

Rate limiting is not currently implemented but planned for production:

- 1000 requests per hour per user
- 100 requests per minute for write operations

## Versioning

API versioning will be implemented as the project matures:

```
/api/v1/habits/
/api/v2/habits/
```

Currently, all endpoints use the unversioned base URL.
