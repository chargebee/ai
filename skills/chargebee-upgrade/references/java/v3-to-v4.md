# Java SDK Migration: V3 to V4
Applies to: com.chargebee:chargebee-java 3.x.x → 4.x.x
Minimum requirement: Java 11+

You are a migration assistant that converts Java code using the **Chargebee Java SDK V3** to **Chargebee Java SDK V4**. Apply the transformation rules below precisely. Preserve all business logic, comments, and code structure. Only change Chargebee SDK usage patterns.

## Migration Rules

### 1. Dependency Changes

**Maven (pom.xml):**
```xml
<!-- V3 - REMOVE -->
<dependency>
  <groupId>com.chargebee</groupId>
  <artifactId>chargebee-java</artifactId>
  <version>3.x.x</version>
</dependency>

<!-- V4 - ADD -->
<dependency>
  <groupId>com.chargebee</groupId>
  <artifactId>chargebee-java</artifactId>
  <version>4.4.0</version>
</dependency>
```

**Gradle (build.gradle):**
```groovy
// V3 - REMOVE
implementation 'com.chargebee:chargebee-java:3.x.x'

// V4 - ADD
implementation 'com.chargebee:chargebee-java:4.4.0'
```

**Note:** V4 requires Java 11 or later. If your project targets Java 8, you must upgrade your Java version first. V4 also uses Gson 2.13.2 (included transitively). If your project already uses Gson, ensure compatibility (minimum Gson 2.8.6 required).

---

### 2. Package / Import Changes

Replace all `com.chargebee` imports with `com.chargebee.v4` equivalents:

| V3 Import | V4 Import |
|-----------|-----------|
| `com.chargebee.Environment` | `com.chargebee.v4.client.ChargebeeClient` |
| `com.chargebee.Result` | *(replaced by typed response classes, see Rule 5)* |
| `com.chargebee.ListResult` | *(replaced by typed list response classes, see Rule 7)* |
| `com.chargebee.models.Customer` | `com.chargebee.v4.models.customer.Customer` |
| `com.chargebee.models.Subscription` | `com.chargebee.v4.models.subscription.Subscription` |
| `com.chargebee.models.Invoice` | `com.chargebee.v4.models.invoice.Invoice` |
| `com.chargebee.models.enums.*` | `com.chargebee.v4.models.<resource>.enums.*` |
| `com.chargebee.exceptions.APIException` | `com.chargebee.v4.exceptions.APIException` |
| `com.chargebee.exceptions.PaymentException` | `com.chargebee.v4.exceptions.PaymentException` |
| `com.chargebee.exceptions.InvalidRequestException` | `com.chargebee.v4.exceptions.InvalidRequestException` |
| `com.chargebee.exceptions.OperationFailedException` | `com.chargebee.v4.exceptions.OperationFailedException` |

**General rule:** `com.chargebee.models.{Resource}` becomes `com.chargebee.v4.models.{resource}.{Resource}` where the package name uses **camelCase** for multi-word resources (e.g., `differentialPrice`, `usageEvent`, `creditNote`, `itemPrice`, `hostedPage`, `attachedItem`, `itemFamily`). Single-word resources use lowercase (e.g., `customer`, `subscription`, `invoice`).

**New V4 imports you will need:**
```java
import com.chargebee.v4.client.ChargebeeClient;
import com.chargebee.v4.services.{Resource}Service;
import com.chargebee.v4.models.{resource}.params.{Resource}{Operation}Params;
import com.chargebee.v4.models.{resource}.responses.{Resource}{Operation}Response;
```

**IMPORTANT — Package casing examples:**
| V3 | V4 Package |
|----|------------|
| `com.chargebee.models.DifferentialPrice` | `com.chargebee.v4.models.differentialPrice.DifferentialPrice` |
| `com.chargebee.models.UsageEvent` | `com.chargebee.v4.models.usageEvent.UsageEvent` |
| `com.chargebee.models.CreditNote` | `com.chargebee.v4.models.creditNote.CreditNote` |
| `com.chargebee.models.ItemPrice` | `com.chargebee.v4.models.itemPrice.ItemPrice` |
| `com.chargebee.models.Customer` | `com.chargebee.v4.models.customer.Customer` |

---

### 3. Environment / Client Configuration

**V3 (static global singleton):**
```java
Environment.configure("acme", "cb_test_xxx");

// Optional: timeouts
Environment.defaultConfig().connectTimeout = 30000;
Environment.defaultConfig().readTimeout = 80000;
```

**V4 (immutable client instance):**
```java
ChargebeeClient client = ChargebeeClient.builder()
    .siteName("acme")
    .apiKey("cb_test_xxx")
    .build();

// With optional timeouts:
ChargebeeClient client = ChargebeeClient.builder()
    .siteName("acme")
    .apiKey("cb_test_xxx")
    .timeout(30000, 80000)
    .build();
```

**Important:** The V4 `ChargebeeClient` is immutable and thread-safe. Create it once and reuse it. It replaces the global `Environment.configure()` call. The client must be passed to where it is needed (dependency injection recommended) rather than relying on a static global.

**Retry configuration:**

V3:
```java
Environment.defaultConfig().updateRetryConfig(
    new com.chargebee.internal.RetryConfig(true, 3, 500,
        new java.util.HashSet<>(java.util.Arrays.asList(500)))
);
```

V4:
```java
ChargebeeClient client = ChargebeeClient.builder()
    .siteName("acme")
    .apiKey("cb_test_xxx")
    .retry(RetryConfig.builder()
        .enabled(true)
        .maxRetries(3)
        .baseDelayMs(500)
        .build())
    .build();
```

**Debug logging:**

V3:
```java
Environment.defaultConfig().updateEnableDebugLogging(true);
```

V4:
```java
ChargebeeClient client = ChargebeeClient.builder()
    .siteName("acme")
    .apiKey("cb_test_xxx")
    .debugLogging(true)
    .build();
```

---

### 4. API Operations (Create, Retrieve, Update, Delete, Actions)

The most significant change: V3 uses **static methods on resource classes** with a fluent builder ending in `.request()`. V4 uses **service objects** obtained from the client, with **typed Params builders** and **typed Response objects**.

#### Create

**V3:**
```java
Result result = Customer.create()
    .firstName("Ada")
    .lastName("Lovelace")
    .email("ada@example.com")
    .request();
Customer customer = result.customer();
```

**V4:**
```java
CustomerCreateResponse response = client.customers().create(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .lastName("Lovelace")
        .email("ada@example.com")
        .build()
);
Customer customer = response.getCustomer();
```

#### Retrieve

**V3:**
```java
Result result = Customer.retrieve("cust_123").request();
Customer customer = result.customer();
```

**V4:**
```java
CustomerRetrieveResponse response = client.customers().retrieve("cust_123");
Customer customer = response.getCustomer();
```

#### Update

**V3:**
```java
Result result = Customer.update("cust_123")
    .firstName("Jane")
    .email("jane@example.com")
    .request();
Customer customer = result.customer();
```

**V4:**
```java
CustomerUpdateResponse response = client.customers().update(
    "cust_123",
    CustomerUpdateParams.builder()
        .firstName("Jane")
        .email("jane@example.com")
        .build()
);
Customer customer = response.getCustomer();
```

#### Delete

**V3:**
```java
Result result = Customer.delete("cust_123").request();
Customer customer = result.customer();
```

**V4:**
```java
CustomerDeleteResponse response = client.customers().delete("cust_123");
Customer customer = response.getCustomer();
```

#### Resource Actions (e.g., merge, move, collect_payment)

**V3:**
```java
Result result = Customer.collectPayment("cust_123")
    .amount(1000)
    .request();
```

**V4:**
```java
CustomerCollectPaymentResponse response = client.customers().collectPayment(
    "cust_123",
    CustomerCollectPaymentParams.builder()
        .amount(1000)
        .build()
);
```

**Transformation pattern:**
| V3 Pattern | V4 Pattern |
|------------|------------|
| `{Resource}.{operation}(args).param1(v).param2(v).request()` | `client.{resources}().{operation}(args, {Resource}{Operation}Params.builder().param1(v).param2(v).build())` |
| `{Resource}.{operation}(id).request()` (no params) | `client.{resources}().{operation}(id)` |
| `result.{resource}()` | `response.get{Resource}()` |

**Service method naming:** The resource name on the client is **plural lowercase**: `client.customers()`, `client.subscriptions()`, `client.invoices()`, `client.coupons()`, etc.

---

### 5. Response Objects

**V3:** Uses generic `Result` for all operations. Extract resources via untyped accessor methods.
```java
Result result = Subscription.create().planId("basic").request();
Subscription sub = result.subscription();
Customer customer = result.customer(); // secondary resource from same response
```

**V4:** Each operation returns a **typed response class** with typed getters.
```java
SubscriptionCreateResponse response = client.subscriptions().create(
    SubscriptionCreateParams.builder().planId("basic").build()
);
Subscription sub = response.getSubscription();
Customer customer = response.getCustomer();
```

**Getter naming change:** V3 uses `result.customer()`, V4 uses `response.getCustomer()` (standard Java getter convention).

---

### 6. Model Property Accessors

**V3:** Uses short method names without `get` prefix:
```java
customer.id()
customer.firstName()
customer.email()
customer.createdAt()     // returns Timestamp
customer.autoCollection() // returns enum
```

**V4:** Uses standard Java getter convention with `get` prefix:
```java
customer.getId()
customer.getFirstName()
customer.getEmail()
customer.getCreatedAt()      // returns Long (unix timestamp)
customer.getAutoCollection() // returns enum
```

**Nested resources:**

V3:
```java
Customer.BillingAddress addr = customer.billingAddress();
String city = addr.city();
```

V4:
```java
Customer.BillingAddress addr = customer.getBillingAddress();
String city = addr.getCity();
```

---

### 7. List Operations & Filtering

**V3:**
```java
ListResult result = Customer.list()
    .limit(10)
    .offset("next_offset_value")
    .request();

for (ListResult.Entry entry : result) {
    Customer customer = entry.customer();
    System.out.println(customer.email());
}

String nextOffset = result.nextOffset();
```

**V4:**
```java
CustomerListResponse response = client.customers().list(
    CustomerListParams.builder()
        .limit(10)
        .offset("next_offset_value")
        .build()
);

for (Customer customer : response.getList()) {
    System.out.println(customer.getEmail());
}

String nextOffset = response.getNextOffset();
```

**Key differences:**
- V3 iterates over `ListResult.Entry` and calls `entry.customer()`. V4 iterates directly over the typed resource list via `response.getList()`.
- V3 uses `result.nextOffset()`. V4 uses `response.getNextOffset()`.

**Filters:**

V3:
```java
ListResult result = Customer.list()
    .limit(10)
    .stringFilterParam("email").startsWith("ada@")
    .timestampFilterParam("created_at").after(someTimestamp)
    .request();
```

V4:
```java
CustomerListResponse response = client.customers().list(
    CustomerListParams.builder()
        .limit(10)
        .email().startsWith("ada@")
        .createdAt().after(someTimestamp)
        .build()
);
```

**Filter change:** V3 uses generic `stringFilterParam("field_name")` / `timestampFilterParam("field_name")` etc. V4 uses **type-safe named methods** directly on the params builder (e.g., `.email()`, `.createdAt()`).

**Custom field filtering (V4 only):**
```java
CustomerListParams.builder()
    .customField("cf_plan_tier").stringFilter().in("gold", "platinum")
    .customField("cf_is_vip").booleanFilter().is(true)
    .build();
```

---

### 8. Idempotency Keys

**V3:**
```java
Result result = Customer.create()
    .firstName("Ada")
    .setIdempotencyKey("unique-key-123")
    .request();

boolean replayed = result.isIdempotencyReplayed();
```

**V4:**
```java
CustomerService scoped = client.customers().withOptions(
    RequestOptions.builder()
        .idempotencyKey("unique-key-123")
        .build()
);

CustomerCreateResponse response = scoped.create(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .build()
);
```

**Note:** In V4, idempotency keys are set via `RequestOptions` using `withOptions()` on the service, not on the request builder.

---

### 9. Custom Headers

**V3:**
```java
Result result = Customer.create()
    .firstName("Ada")
    .header("X-Custom-Header", "value")
    .request();
```

**V4:**
```java
CustomerService scoped = client.customers().withOptions(
    RequestOptions.builder()
        .header("X-Custom-Header", "value")
        .build()
);

CustomerCreateResponse response = scoped.create(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .build()
);
```

---

### 10. Per-Request Environment (V3) vs Per-Request Options (V4)

**V3:**
```java
Environment customEnv = new Environment("other-site", "other-api-key");
Result result = Customer.retrieve("cust_123").request(customEnv);
```

**V4:**
```java
// Create a separate client for a different site
ChargebeeClient otherClient = ChargebeeClient.builder()
    .siteName("other-site")
    .apiKey("other-api-key")
    .build();

CustomerRetrieveResponse response = otherClient.customers().retrieve("cust_123");
```

**For per-request timeout/retry overrides (V4 only):**
```java
CustomerService scoped = client.customers().withOptions(
    RequestOptions.builder()
        .connectTimeoutMs(15000)
        .readTimeoutMs(45000)
        .maxNetworkRetries(2)
        .build()
);
```

---

### 11. Exception Handling

**V3:**
```java
import com.chargebee.exceptions.APIException;
import com.chargebee.exceptions.PaymentException;
import com.chargebee.exceptions.InvalidRequestException;

try {
    Result result = Customer.create().email("bad").request();
} catch (PaymentException e) {
    System.err.println("Payment error: " + e.getMessage());
    System.err.println("Code: " + e.apiErrorCode);
    System.err.println("Param: " + e.param);
} catch (InvalidRequestException e) {
    System.err.println("Invalid request: " + e.getMessage());
    System.err.println("Param: " + e.param);
} catch (APIException e) {
    System.err.println("API error: " + e.getMessage());
    System.err.println("HTTP status: " + e.httpStatusCode);
}
```

**V4:**
```java
import com.chargebee.v4.exceptions.*;
import com.chargebee.v4.exceptions.codes.*;

try {
    CustomerCreateResponse response = client.customers().create(
        CustomerCreateParams.builder().email("bad").build()
    );
} catch (PaymentException e) {
    System.err.println("Payment error: " + e.getMessage());
    System.err.println("Code: " + e.getApiErrorCodeRaw());
    System.err.println("Param: " + e.getParam());
} catch (InvalidRequestException e) {
    System.err.println("Invalid request: " + e.getMessage());
    System.err.println("Param: " + e.getParam());

    // V4 strongly-typed error codes:
    ApiErrorCode errorCode = e.getApiErrorCode();
    if (errorCode instanceof BadRequestApiErrorCode) {
        BadRequestApiErrorCode code = (BadRequestApiErrorCode) errorCode;
        if (code == BadRequestApiErrorCode.DUPLICATE_ENTRY) {
            System.err.println("Duplicate!");
        }
    }
} catch (APIException e) {
    System.err.println("API error: " + e.getMessage());
    System.err.println("HTTP status: " + e.getStatusCode());
} catch (TransportException e) {
    // NEW in V4: network-level errors (DNS, timeout, etc.)
    System.err.println("Network error: " + e.getMessage());
}
```

**Key changes:**
| V3 | V4 |
|----|-----|
| `e.httpStatusCode` | `e.getStatusCode()` |
| `e.apiErrorCode` (String field) | `e.getApiErrorCode()` (typed enum) or `e.getApiErrorCodeRaw()` (String) |
| `e.param` (String field) | `e.getParam()` (method) or `e.getParams()` (List) |
| `e.type` (String field) | `e.getType()` (method) or `e.getErrorType()` (typed enum) |
| `e.jsonObj` (JSONObject field) | `e.getJsonResponse()` (String) |
| No transport exceptions | `TransportException`, `NetworkException`, `TimeoutException` |

---

### 12. HTTP Response Metadata

**V3:**
```java
Result result = Customer.create().firstName("Ada").request();
int httpCode = result.httpCode();
Map<String, List<String>> headers = result.getResponseHeaders();
```

**V4:**
Response objects extend `BaseResponse` which provides HTTP metadata:
```java
CustomerCreateResponse response = client.customers().create(params);
int httpCode = response.getHttpStatusCode();
Map<String, List<String>> headers = response.getResponseHeaders();
```

---

### 13. Nested Object Parameters

**V3:**
```java
Result result = Customer.create()
    .firstName("Ada")
    .billingAddressFirstName("Ada")
    .billingAddressLastName("Lovelace")
    .billingAddressLine1("50 Market St")
    .billingAddressCity("San Francisco")
    .billingAddressState("CA")
    .billingAddressZip("94105")
    .billingAddressCountry("US")
    .request();
```

**V4:**
```java
CustomerCreateResponse response = client.customers().create(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .billingAddress(
            CustomerCreateParams.BillingAddressParams.builder()
                .firstName("Ada")
                .lastName("Lovelace")
                .line1("50 Market St")
                .city("San Francisco")
                .state("CA")
                .zip("94105")
                .country("US")
                .build()
        )
        .build()
);
```

**Key change:** V3 uses flat `billingAddressCity()` style. V4 uses nested builder objects like `billingAddress(BillingAddressParams.builder()...build())`.

---

### 14. Enum Values

**V3:**
```java
import com.chargebee.models.enums.AutoCollection;

if (customer.autoCollection() == AutoCollection.ON) { ... }
```

**V4:**
```java
import com.chargebee.v4.models.customer.enums.AutoCollection;

if (customer.getAutoCollection() == AutoCollection.ON) { ... }
```

**Changes:** Package path changes from `com.chargebee.models.enums.*` to `com.chargebee.v4.models.{resource}.enums.*`. Enum values themselves remain the same.

---

### 15. Metadata / Custom Fields

**V3:**
```java
// Setting metadata (via JSON object)
Result result = Customer.create()
    .firstName("Ada")
    .request();
```

**V4:**
```java
// Setting metadata via builder
CustomerCreateResponse response = client.customers().create(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .metaData(Map.of("key", "value"))
        .build()
);

// Reading custom fields
Customer customer = response.getCustomer();
String customField = customer.getCustomField("cf_my_field");
Map<String, String> allCustomFields = customer.getCustomFields();
```

---

### 16. Async Operations (V4 Only - New Feature)

V4 introduces async support. Every service method has an `Async` variant returning `CompletableFuture`:

```java
// Async create
CompletableFuture<CustomerCreateResponse> future = client.customers().createAsync(
    CustomerCreateParams.builder()
        .firstName("Ada")
        .build()
);

future.thenAccept(response -> {
    System.out.println("Created: " + response.getCustomer().getId());
}).exceptionally(throwable -> {
    Throwable cause = throwable instanceof CompletionException
        ? throwable.getCause() : throwable;
    System.err.println("Error: " + cause.getMessage());
    return null;
});
```

This is optional — you do not need to convert to async during migration unless desired.

---

### 17. Client Cleanup (V4 Only)

V4's `ChargebeeClient` implements `AutoCloseable`. If using async operations, close the client when done to shut down the internal executor:

```java
// Using try-with-resources
try (ChargebeeClient client = ChargebeeClient.builder()
        .siteName("acme").apiKey("key").build()) {
    // ... use client ...
}

// Or manually
client.close();
```

---

## Quick Reference: Resource Name Mapping

The service accessor on the client uses **plural camelCase**:

| Resource Class | Client Accessor |
|---------------|----------------|
| `Customer` | `client.customers()` |
| `Subscription` | `client.subscriptions()` |
| `Invoice` | `client.invoices()` |
| `CreditNote` | `client.creditNotes()` |
| `Plan` | `client.plans()` |
| `Addon` | `client.addons()` |
| `Coupon` | `client.coupons()` |
| `PaymentSource` | `client.paymentSources()` |
| `HostedPage` | `client.hostedPages()` |
| `Event` | `client.events()` |
| `Order` | `client.orders()` |
| `Item` | `client.items()` |
| `ItemPrice` | `client.itemPrices()` |
| `AttachedItem` | `client.attachedItems()` |
| `ItemFamily` | `client.itemFamilies()` |

## Checklist

After migration, verify:
- [ ] All `com.chargebee` imports replaced with `com.chargebee.v4` equivalents
- [ ] `Environment.configure()` replaced with `ChargebeeClient.builder()...build()`
- [ ] All `{Resource}.{operation}().request()` calls replaced with `client.{resources}().{operation}(params)`
- [ ] All `result.{resource}()` calls replaced with `response.get{Resource}()`
- [ ] All model property accessors updated (`customer.email()` → `customer.getEmail()`)
- [ ] All `ListResult.Entry` iteration replaced with `response.getList()` iteration
- [ ] Exception field access updated to use getter methods
- [ ] Idempotency keys moved from `.setIdempotencyKey()` to `RequestOptions`
- [ ] Custom headers moved from `.header()` to `RequestOptions`
- [ ] Nested parameter methods flattened to nested builder objects
- [ ] Enum imports updated to resource-specific packages
- [ ] Build file updated with V4 dependency and Java 11+ target
- [ ] Code compiles and tests pass
