# Alogram PayRisk Ruby SDK

[![Gem Version](https://badge.fury.io/rb/alogram_payrisk.svg)](https://badge.fury.io/rb/alogram_payrisk)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

The official Ruby client for the **Alogram PayRisk Engine**. 

Alogram is an AI-native risk orchestration platform built for high-velocity commerce. This SDK provides sub-millisecond risk scoring, behavioral intelligence ingestion, and forensic transparency for enterprise ecosystems.

### 🏎️ High-Performance Networking
Built for scale, this SDK features:
*   **HTTP/2 Native**: Multiplexed connections for low-latency parallel scoring.
*   **Asynchronous I/O**: Built on `httpx` for non-blocking integration into modern Ruby apps (Fibers/Async).
*   **TLS 1.3**: The highest standard of transit security for sensitive transaction data.
*   **Spec-compliant**: Automatically kept in sync with the Alogram OpenAPI 3.0.4 specification.

---

## 📦 Installation

Add this line to your application's `Gemfile`:

```ruby
gem 'alogram_payrisk', '~> 0.3.2'
```

And then execute:
```bash
bundle install
```

---

## 🚀 Quick Start (The "Full Circle" Lifecycle)

Alogram is designed for a three-step risk lifecycle: **Score -> Ingest -> Query.**

### 1. Configure the Client
```ruby
require 'alogram_payrisk'

AlogramPayRisk.configure do |config|
  config.api_key['x-api-key'] = 'sk_live_your_key'
  # For local development against the emulator:
  # config.host = 'localhost:8080'
  # config.scheme = 'http'
end

api = AlogramPayRisk::RiskScoringApi.new
```

### 2. Request a Risk Decision
Call Alogram *before* you charge the customer to get a real-time decision.

```ruby
request = AlogramPayRisk::CheckRequest.new({
  entities: {
    tenant_id: "your_tenant_id",
    session_id: "sid_550e8400",
    client_id: "cid_998234"
  },
  purchase: {
    amount: 99.99,
    currency: "USD",
    payment_method: {
      type: "card",
      bin: "411111",
      card_network: "visa"
    }
  }
})

begin
  # Decision is returned in < 100ms
  decision = api.risk_check("idk_unique_key_123", request)
  
  if decision.decision == 'approve'
    puts "✅ Transaction approved (Score: #{decision.decision_score})"
    # Proceed with payment...
  else
    puts "❌ Transaction declined: #{decision.reason_codes}"
  end
rescue AlogramPayRisk::ApiError => e
  puts "Error: #{e.code} - #{e.response_body}"
end
```

### 3. Ingest Lifecycle Events
Once the payment is processed, notify Alogram of the outcome to improve your AI model's accuracy.

```ruby
events_api = AlogramPayRisk::SignalIntelligenceApi.new

event = AlogramPayRisk::PaymentEvent.new({
  event_type: 'authorization',
  payment_intent_id: decision.payment_intent_id,
  outcome: { 
    status: 'success', 
    processor_response_code: '00' 
  }
})

events_api.ingest_payment_event("idk_event_123", event)
```

---

## 🧪 Local Development & Testing

We provide a **Local Emulator** to let you test without network access or production keys.

1.  **Start the Emulator**:
    ```bash
    docker run -p 8080:8080 us-docker.pkg.dev/alogram-public/sdk/payrisk-emulator:0.3.2
    ```
2.  **Point the SDK to Localhost**:
    ```ruby
    AlogramPayRisk.configure do |config|
      config.scheme = 'http'
      config.host = 'localhost:8080'
      config.api_key['x-api-key'] = 'test' # Accepts any string
    end
    ```

---

## 🛡️ Error Handling

| Status | Meaning | Action |
| :--- | :--- | :--- |
| `401` | Unauthorized | Check your `x-api-key` configuration. |
| `422` | Validation Error | Ensure IDs follow the required patterns (e.g., `sid_`, `idk_`). |
| `429` | Rate Limited | Implement an exponential backoff. |
| `5xx` | Alogram Downtime | Fallback to a default 'approve' to avoid conversion loss. |

---

## ⚖️ License

Apache License 2.0. See [LICENSE](LICENSE) for details.
