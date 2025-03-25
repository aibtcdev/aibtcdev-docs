# STX City API

The STX City API provides access to token data from the STX.city platform. It offers information about tokens on the Stacks blockchain, including their metrics, social links, and other details.

## Base Path

All STX City API endpoints are available under:
```
/stx-city
```

## Available Endpoints

| Endpoint | Description |
|----------|-------------|
| `/tokens/tradable-full-details-tokens` | Get details about tradable tokens |

## Response Format

All endpoints return responses in a standardized format:

### Success Response
```json
{
  "success": true,
  "data": {
    // The actual response data from STX.city
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

## Get Tradable Tokens

Retrieves details about tradable tokens on the Stacks blockchain.

### Endpoint

```
GET /stx-city/tokens/tradable-full-details-tokens
```

### Example Requests

#### cURL

```bash
curl https://cache.aibtc.dev/stx-city/tokens/tradable-full-details-tokens
```

#### JavaScript

```javascript
async function getTradableTokens() {
  const response = await fetch(
    'https://cache.aibtc.dev/stx-city/tokens/tradable-full-details-tokens'
  );
  
  const result = await response.json();
  
  if (result.success) {
    return result.data;
  } else {
    throw new Error(`API Error: ${result.error.code} - ${result.error.message}`);
  }
}

// Usage
getTradableTokens()
  .then(tokens => {
    console.log(`Found ${tokens.length} tradable tokens`);
    // Display the top 5 tokens by price
    const topTokens = tokens
      .sort((a, b) => b.metrics.price_usd - a.metrics.price_usd)
      .slice(0, 5);
    console.log('Top tokens by price:', topTokens.map(t => t.name));
  })
  .catch(error => console.error('Error:', error));
```

#### Python

```python
import requests
import json

def get_tradable_tokens():
    url = 'https://cache.aibtc.dev/stx-city/tokens/tradable-full-details-tokens'
    
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
    tokens = get_tradable_tokens()
    print(f"Found {len(tokens)} tradable tokens")
    
    # Display the top 5 tokens by liquidity
    top_tokens = sorted(tokens, key=lambda x: x['metrics']['liquidity_usd'], reverse=True)[:5]
    for token in top_tokens:
        print(f"{token['name']} ({token['symbol']}): ${token['metrics']['price_usd']:.4f} - Liquidity: ${token['metrics']['liquidity_usd']:.2f}")
except Exception as e:
    print(f"Error: {e}")
```

### Example Response Structure

The response contains an array of token objects with the following structure:

```json
{
  "success": true,
  "data": [
    {
      "contract_id": "SP2QEZ06AGJ3RKJPBV14SY1V5BBFNAW33D96YPGZF.token-name",
      "symbol": "TKN",
      "name": "Token Name",
      "decimals": 6,
      "total_supply": "1000000000000",
      "circulating_supply": "500000000000",
      "image_url": "https://example.com/token.png",
      "header_image_url": "https://example.com/header.png",
      "metrics": {
        "price_usd": 0.12345,
        "holder_count": 1500,
        "swap_count": 3200,
        "transfer_count": 8500,
        "liquidity_usd": 250000
      },
      "amms": ["alex-launchpool"],
      "description": "Description of the token and its purpose",
      "homepage": "https://token-website.com",
      "telegram": "https://t.me/token_group",
      "xlink": "https://x.com/token_account",
      "discord": "https://discord.gg/token",
      "verified": true,
      "socials": [
        {
          "platform": "twitter",
          "value": "https://x.com/token_account"
        },
        {
          "platform": "discord",
          "value": "https://discord.gg/token"
        }
      ]
    },
    // ... more tokens
  ]
}
```
