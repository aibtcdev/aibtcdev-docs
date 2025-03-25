# Supabase API

The Supabase API provides access to data stored in the Supabase database. It offers endpoints for retrieving statistics and other information from the database.

## Base Path

All Supabase API endpoints are available under:
```
/supabase
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/stats` | Get statistics from the database |

## Response Format

All endpoints return responses in a standardized format:

### Success Response
```json
{
  "success": true,
  "data": {
    // The actual response data
  }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "id": "unique-error-id",
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      // Optional additional error details
    }
  }
}
```

## Get Statistics

Retrieves statistics from the Supabase database.

### Endpoint

```
GET /supabase/stats
```

### Example Requests

#### cURL

```bash
curl https://cache.aibtc.dev/supabase/stats
```

#### JavaScript

```javascript
async function getStats() {
  const response = await fetch(
    'https://cache.aibtc.dev/supabase/stats'
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getStats()
  .then(stats => {
    console.log('Statistics:', stats);
    console.log(`Total jobs: ${stats.total_jobs}`);
    console.log(`Main chat jobs: ${stats.main_chat_jobs}`);
    console.log(`Individual crew jobs: ${stats.individual_crew_jobs}`);
  })
  .catch(error => console.error('Error:', error));
```

#### Python

```python
import requests
import json

def get_stats():
    url = 'https://cache.aibtc.dev/supabase/stats'
    
    response = requests.get(url)
    response.raise_for_status()
    result = response.json()
    
    if result.get('success'):
        return result['data']
    else:
        error = result.get('error', {})
        raise Exception(f"API Error: {error.get('code')} - {error.get('message')}")

# Usage
try:
    stats = get_stats()
    print(f"Statistics as of {stats['timestamp']}:")
    print(f"Total jobs: {stats['total_jobs']}")
    print(f"Main chat jobs: {stats['main_chat_jobs']}")
    print(f"Individual crew jobs: {stats['individual_crew_jobs']}")
    print(f"Top profile Stacks addresses: {', '.join(stats['top_profile_stacks_addresses'])}")
    print(f"Top crew names: {', '.join(stats['top_crew_names'])}")
except Exception as e:
    print(f"Error: {e}")
```

### Example Response

```json
{
  "success": true,
  "data": {
    "timestamp": "2023-06-15T12:34:56.789Z",
    "total_jobs": 1500,
    "main_chat_jobs": 1000,
    "individual_crew_jobs": 500,
    "top_profile_stacks_addresses": [
      "SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF",
      "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA",
      "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM"
    ],
    "top_crew_names": [
      "Alpha Team",
      "Beta Squad",
      "Gamma Crew"
    ]
  }
}
```
