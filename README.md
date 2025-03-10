# ZerePy

## bAIbysitter Plugin

We developed a plugin to seamlessly integrate Zerepy with Baibysitter not just for the hackathon, but with the goal of making Baibysitter a security tool that helps Zerepy agents conduct safer transactions

### JSON Agent Configuration

```json
{
    "name": "sonic",
    "network": "testnet",
    "baibysitter": {
        "enabled": true,
        "name": "BaibySitter",
        "api_url": "http://localhost:8000"
    }
}
```

---

## Baibysitter Middlewares in ZerePy

The integration uses two main middlewares:

### 1. `BaibysitterMiddleware` (Base)

**File:** `baibysitter_middleware.py`

```python
from abc import ABC
from config import BaibysitterConfig

class BaibysitterMiddleware(ABC):
    def __init__(self, config: BaibysitterConfig):
        self.config = config
        self.name = config.name or self.__class__.__name__
```

#### **Abstract base class that:**
- Handles Baibysitter's basic configuration.
- Defines the transaction validation flow.
- Provides abstract methods for specific validation.

---

### 2. `SonicMiddleware` (Implementation)

**File:** `sonic_middleware.py`

```python
from typing import List, Any, Dict
from baibysitter_middleware import BaibysitterMiddleware

class SonicMiddleware(BaibysitterMiddleware):
    def should_validate_action(self, action_name: str) -> bool:
        return action_name in ["transfer", "swap"]
    
    def _extract_transaction_data(self, action_name: str, params: List[Any]) -> Dict[str, Any]:
        # Specific implementation for Sonic transactions
        pass
```

#### **Specific implementation that:**
- Validates transfer and swap actions.
- Extracts and formats transaction data for Baibysitter.
- Manages integration with Sonic-specific contracts.

---

### **How the Middlewares Work**
Both middlewares work together to validate transactions **before execution**, ensuring the integrity and security of operations.





---

<img width="856" alt="Image" src="https://github.com/user-attachments/assets/63f3a763-4ca2-44ae-8029-2d481119fb76" />
