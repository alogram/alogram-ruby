# alogram_payrisk

AlogramPayRisk - the Ruby gem for the Alogram PayRisk Engine

Alogram PayRisk is an AI-native decision engine built for the speed and 
complexity of the modern commerce era. In a high-velocity world where 
AI-driven threats evolve in milliseconds, Alogram provides the real-time 
adaptability and forensic transparency needed to protect your ecosystem 
with total confidence. We solve the challenge of balancing frictionless 
growth with regulatory explainability, delivering instant, intelligent 
risk orchestration at enterprise scale.

---


## Licensing & Terms


Our client libraries and API specifications are open-source under the **Apache License 2.0** 
to ensure seamless integration into your tech stack.

Use of the Alogram PayRisk API service is proprietary and governed by our 
[Terms of Service](https://alogram.ai/#tos) and your specific **Enterprise Agreement**, 
if applicable.

To access the service, you must have:
*   A valid Alogram API Key.
*   An active subscription or signed Master Service Agreement.

Unauthorized use, including automated scraping or reverse engineering of the 
scoring engine, is strictly prohibited.


---


## Support & Traceability


Every Alogram API response includes a unique **`x-trace-id`** header. 
Please include this ID when contacting [packages@alogram.ai](mailto:packages@alogram.ai) 
regarding specific transactions or errors.


---


## Specification


The authoritative OpenAPI specification for this version is available for download:
**[Download openapi.yaml](https://developers.alogram.ai/openapi.yaml)** | **[Download openapi.json](https://developers.alogram.ai/openapi.json)**


---

### 🏎️ High Performance & Security
The Alogram Ruby SDK is built for enterprise-scale workloads:
*   **Async-Ready**: Built on `httpx` with native support for Fibers and Event Loops.
*   **Modern Protocols**: Native support for **HTTP/2** multiplexing and **TLS 1.3**.
*   **Connection Pooling**: Persistent session management for sub-millisecond connection reuse.
*   **Traceable**: Full support for `x-trace-id` and `x-idempotency-key` for forensic audit compliance.

---

## Installation

### Build a gem

To build the Ruby code into a gem:

```shell
gem build alogram_payrisk.gemspec
```

Then either install the gem locally:

```shell
gem install ./alogram_payrisk-0.2.9.gem
```

(for development, run `gem install --dev ./alogram_payrisk-0.2.9.gem` to install the development dependencies)

or publish the gem to a gem hosting service, e.g. [RubyGems](https://rubygems.org/).

Finally add this to the Gemfile:

    gem 'alogram_payrisk', '~> 0.2.9'

### Install from Git

If the Ruby gem is hosted at a git repository: https://github.com/alogram/alogram-ruby, then add the following in the Gemfile:

    gem 'alogram_payrisk', :git => 'https://github.com/alogram/alogram-ruby.git'

### Include the Ruby code directly

Include the Ruby code directly using `-I` as follows:

```shell
ruby -Ilib script.rb
```

## Getting Started

Please follow the [installation](#installation) procedure and then run the following code:

```ruby
# Load the gem
require 'alogram_payrisk'

# Setup authorization
AlogramPayRisk.configure do |config|
  # Configure API key authorization: ApiKey
  config.api_key['x-api-key'] = 'YOUR API KEY'
  # Uncomment the following line to set a prefix for the API key, e.g. 'Bearer' (defaults to nil)
  # config.api_key_prefix['x-api-key'] = 'Bearer'
  # Configure httpx session
  config.configure_session { |session| 'YOUR CONNECTION CONFIG PROC' }

  # Configure OAuth2 access token for authorization: oAuth2
  config.access_token = 'YOUR ACCESS TOKEN'
  # Configure a proc to get access tokens in lieu of the static access_token configuration
  config.access_token_getter = -> { 'YOUR TOKEN GETTER PROC' } 
  # Configure httpx session
  config.configure_session { |session| 'YOUR CONNECTION CONFIG PROC' }
end

api_instance = AlogramPayRisk::ForensicDataApi.new
tenant_id = 'tenant_id_example' # String | 
opts = {
  x_trace_id: 'x_trace_id_example', # String | Echoed or generated trace ID for tracking requests.
  x_idempotency_key: 'x_idempotency_key_example', # String | Unique Idempotency-Key sent in the GET request etc.
  start_time: 'start_time_example', # String | 
  end_time: 'end_time_example', # String | 
  page_size: 56, # Integer | 
  page_token: 'page_token_example' # String | 
}

begin
  #Query Historical Assessments
  result = api_instance.get_fraud_scores(tenant_id, opts)
  p result
rescue AlogramPayRisk::ApiError => e
  puts "Exception when calling ForensicDataApi->get_fraud_scores: #{e}"
end

```

## Documentation for API Endpoints

All URIs are relative to *https://api.alogram.ai*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*AlogramPayRisk::ForensicDataApi* | [**get_fraud_scores**](docs/ForensicDataApi.md#get_fraud_scores) | **GET** /v1/scores/{tenantId} | Query Historical Assessments
*AlogramPayRisk::RiskScoringApi* | [**risk_check**](docs/RiskScoringApi.md#risk_check) | **POST** /v1/risk/check | Assess Transaction Risk
*AlogramPayRisk::RoadmapPreviewApi* | [**account_risk_check**](docs/RoadmapPreviewApi.md#account_risk_check) | **POST** /v1/risk/account/check | Synchronous fraud decision for account/session events
*AlogramPayRisk::RoadmapPreviewApi* | [**kyc_risk_check**](docs/RoadmapPreviewApi.md#kyc_risk_check) | **POST** /v1/risk/kyc/check | Synchronous decision for KYC/identity verification
*AlogramPayRisk::SignalIntelligenceApi* | [**ingest_payment_event**](docs/SignalIntelligenceApi.md#ingest_payment_event) | **POST** /v1/events | Ingest Lifecycle Signals
*AlogramPayRisk::SignalIntelligenceApi* | [**ingest_signals**](docs/SignalIntelligenceApi.md#ingest_signals) | **POST** /v1/signals | Submit Behavioral Intelligence
*AlogramPayRisk::SystemApi* | [**health_check**](docs/SystemApi.md#health_check) | **GET** /v1/health | Health check for the service


## Documentation for Models

 - [AlogramPayRisk::Account](docs/Account.md)
 - [AlogramPayRisk::AccountCheckRequest](docs/AccountCheckRequest.md)
 - [AlogramPayRisk::AvsResultEnum](docs/AvsResultEnum.md)
 - [AlogramPayRisk::BankTransfer](docs/BankTransfer.md)
 - [AlogramPayRisk::Card](docs/Card.md)
 - [AlogramPayRisk::CardNetworkEnum](docs/CardNetworkEnum.md)
 - [AlogramPayRisk::CategorySignal](docs/CategorySignal.md)
 - [AlogramPayRisk::ChannelEnum](docs/ChannelEnum.md)
 - [AlogramPayRisk::CheckRequest](docs/CheckRequest.md)
 - [AlogramPayRisk::ConfidenceEnum](docs/ConfidenceEnum.md)
 - [AlogramPayRisk::Crypto](docs/Crypto.md)
 - [AlogramPayRisk::CvvResultEnum](docs/CvvResultEnum.md)
 - [AlogramPayRisk::DecisionResponse](docs/DecisionResponse.md)
 - [AlogramPayRisk::DeviceInfo](docs/DeviceInfo.md)
 - [AlogramPayRisk::DiscountCode](docs/DiscountCode.md)
 - [AlogramPayRisk::EntityIds](docs/EntityIds.md)
 - [AlogramPayRisk::EntryMethodEnum](docs/EntryMethodEnum.md)
 - [AlogramPayRisk::ExternalAssessment](docs/ExternalAssessment.md)
 - [AlogramPayRisk::FraudScore](docs/FraudScore.md)
 - [AlogramPayRisk::Identity](docs/Identity.md)
 - [AlogramPayRisk::Integrity](docs/Integrity.md)
 - [AlogramPayRisk::Interaction](docs/Interaction.md)
 - [AlogramPayRisk::InteractionTypeEnum](docs/InteractionTypeEnum.md)
 - [AlogramPayRisk::Invoice](docs/Invoice.md)
 - [AlogramPayRisk::IpInfo](docs/IpInfo.md)
 - [AlogramPayRisk::KycCheckRequest](docs/KycCheckRequest.md)
 - [AlogramPayRisk::KycPayload](docs/KycPayload.md)
 - [AlogramPayRisk::MerchantContext](docs/MerchantContext.md)
 - [AlogramPayRisk::OrderContext](docs/OrderContext.md)
 - [AlogramPayRisk::PayerTypeEnum](docs/PayerTypeEnum.md)
 - [AlogramPayRisk::PaymentAuthorizationOutcome](docs/PaymentAuthorizationOutcome.md)
 - [AlogramPayRisk::PaymentCaptureOutcome](docs/PaymentCaptureOutcome.md)
 - [AlogramPayRisk::PaymentCardTypeEnum](docs/PaymentCardTypeEnum.md)
 - [AlogramPayRisk::PaymentChargeback](docs/PaymentChargeback.md)
 - [AlogramPayRisk::PaymentChargebackOutcome](docs/PaymentChargebackOutcome.md)
 - [AlogramPayRisk::PaymentDisputeOutcome](docs/PaymentDisputeOutcome.md)
 - [AlogramPayRisk::PaymentEvent](docs/PaymentEvent.md)
 - [AlogramPayRisk::PaymentEventType](docs/PaymentEventType.md)
 - [AlogramPayRisk::PaymentMethod](docs/PaymentMethod.md)
 - [AlogramPayRisk::PaymentOutcome](docs/PaymentOutcome.md)
 - [AlogramPayRisk::PaymentRealtimeTypeEnum](docs/PaymentRealtimeTypeEnum.md)
 - [AlogramPayRisk::PaymentRefundOutcome](docs/PaymentRefundOutcome.md)
 - [AlogramPayRisk::PaymentWalletTypeEnum](docs/PaymentWalletTypeEnum.md)
 - [AlogramPayRisk::PostalAddress](docs/PostalAddress.md)
 - [AlogramPayRisk::Problem](docs/Problem.md)
 - [AlogramPayRisk::Purchase](docs/Purchase.md)
 - [AlogramPayRisk::PurchaseInitiatorEnum](docs/PurchaseInitiatorEnum.md)
 - [AlogramPayRisk::PurchaseSequenceEnum](docs/PurchaseSequenceEnum.md)
 - [AlogramPayRisk::PurchaseUsageEnum](docs/PurchaseUsageEnum.md)
 - [AlogramPayRisk::Realtime](docs/Realtime.md)
 - [AlogramPayRisk::ReasonDetail](docs/ReasonDetail.md)
 - [AlogramPayRisk::RiskBreakdown](docs/RiskBreakdown.md)
 - [AlogramPayRisk::RiskCategoryEnum](docs/RiskCategoryEnum.md)
 - [AlogramPayRisk::RiskLevelEnum](docs/RiskLevelEnum.md)
 - [AlogramPayRisk::ScaMethodEnum](docs/ScaMethodEnum.md)
 - [AlogramPayRisk::ScoreRecord](docs/ScoreRecord.md)
 - [AlogramPayRisk::ScoresSuccessResponse](docs/ScoresSuccessResponse.md)
 - [AlogramPayRisk::SignalsAccountVariant](docs/SignalsAccountVariant.md)
 - [AlogramPayRisk::SignalsInteractionVariant](docs/SignalsInteractionVariant.md)
 - [AlogramPayRisk::SignalsRequest](docs/SignalsRequest.md)
 - [AlogramPayRisk::StoredCredentialContext](docs/StoredCredentialContext.md)
 - [AlogramPayRisk::ThreeDSData](docs/ThreeDSData.md)
 - [AlogramPayRisk::Wallet](docs/Wallet.md)


## Documentation for Authorization


Authentication schemes defined for the API:
### ApiKey


- **Type**: API key
- **API key parameter name**: x-api-key
- **Location**: HTTP header

### oAuth2


- **Type**: OAuth
- **Flow**: accessCode
- **Authorization URL**: https://api.alogram.ai/oauth2/authorize
- **Scopes**: 
  - payrisk.read: Read fraud scores and decisions.
  - payrisk.write: Submit fraud checks, events, and signals.

