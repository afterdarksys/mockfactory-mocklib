# MockLib - MockFactory SDK Toolkit

Multi-language SDKs for interacting with MockFactory's cloud emulation platform.

## Supported Languages

- **Python** (`mocklib-python/`) - `pip install mocklib`
- **Node.js** (`mocklib-node/`) - `npm install @mockfactory/mocklib`
- **Go** (`mocklib-go/`) - `go get github.com/mockfactory/mocklib`
- **PHP** (`mocklib-php/`) - `composer require mockfactory/mocklib`
- **Shell** (`mocklib-shell/`) - `curl` + `jq` examples

## Quick Start

### Python
```python
from mocklib import MockFactory

mf = MockFactory(api_key="mf_...")
vpc = mf.vpc.create(cidr_block="10.0.0.0/16")
print(f"Created VPC: {vpc.id}")
```

### Node.js
```javascript
const MockFactory = require('@mockfactory/mocklib');

const mf = new MockFactory({ apiKey: 'mf_...' });
const vpc = await mf.vpc.create({ cidrBlock: '10.0.0.0/16' });
console.log(`Created VPC: ${vpc.id}`);
```

### Go
```go
import "github.com/mockfactory/mocklib"

client := mocklib.NewClient("mf_...")
vpc, _ := client.VPC.Create("10.0.0.0/16")
fmt.Printf("Created VPC: %s\n", vpc.ID)
```

### Shell
```bash
export MOCKFACTORY_API_KEY="mf_..."
source mocklib.sh

mocklib_vpc_create "10.0.0.0/16"
# Output: vpc-abc123
```

## API Endpoints

### Public API (Customer-Facing)
- `https://api.mockfactory.io/v1/*` - Rate limited, authenticated
- Used by all SDKs
- Pay-per-use billing

### Private API (Internal Only)
- `https://mockfactory.io/api/internal/*` - No rate limits
- Admin operations, metrics, system management
- Not exposed in SDKs

## Architecture

```
Customer App
    ↓
MockLib SDK (Python/Node/Go/PHP)
    ↓
Public API (https://api.mockfactory.io/v1)
    ↓
MockFactory Backend
    ↓
Real OCI Infrastructure
```

## Development

Each language SDK follows the same pattern:
1. **Client**: Handles authentication, HTTP requests
2. **Resources**: VPC, Lambda, DynamoDB, SQS, Storage
3. **Models**: Response objects with typed fields
4. **Errors**: Structured error handling

See individual language directories for details.
