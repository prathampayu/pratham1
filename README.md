# Detailed Report of Work Completed at PayU

**Name:** Pratham Ghorpade  
**Role:** Engineering Intern  
**Team:** Engineering Team  
**Organization:** PayU  
**Reporting period:** From the beginning of the internship work up to **13 November 2026**

---

## Introduction

During my internship at PayU, I worked primarily on the EMI and affordability ecosystem. The work covered domain understanding, EMI Service integration testing, ACS Simulator-based testing, load and capacity testing, SQL-based analysis, monitoring and alerting, payment integrations, and the design of internal AI-assisted investigation systems.

The work involved understanding the complete lifecycle of an EMI transaction:

1. Merchant and product configuration.
2. EMI eligibility and pre-eligibility.
3. Lender and banking-system interaction.
4. Payment gateway routing.
5. Authentication and authorization.
6. Transaction processing and status updates.
7. Reconciliation and final transaction outcome.
8. Monitoring, alerting, troubleshooting, and operational support.

The work progressed from learning the PayU business and technical ecosystem to designing and documenting practical implementations for testing, analysis, monitoring, and automation.

Where a query or architecture was designed but its production deployment or execution was not independently confirmed, it is identified as a design, query pattern, or implementation proposal rather than a confirmed production deployment.

---

# 1. Type of Training Undergone and Objectives

## 1.1 PayU organization and payment-domain training

The initial training focused on understanding PayU’s business and technical environment.

I learned how PayU’s payment systems connect:

- Merchants
- KAMs
- Product teams
- Payment and integration teams
- Banks and lenders
- Payment gateways
- Banking Operations
- Technical support teams
- Engineering and Tech On-Call teams

I also learned that EMI is not an isolated feature. It depends on several services and configuration layers working together. A problem in merchant configuration, lender eligibility, gateway routing, API communication, authentication, or reconciliation can affect the complete customer journey.

### Objectives

The objectives of this training were to:

- Understand PayU’s role in the online payment ecosystem.
- Understand how PayU supports merchants and banking or lending partners.
- Learn the major EMI products and transaction flows.
- Understand how the Engineering Team supports business and operational teams.
- Learn how technical issues are converted into business impact.
- Understand the difference between payment-performance problems and configuration or onboarding problems.

---

## 1.2 EMI product and affordability training

The work covered the following EMI and affordability products:

- Credit Card EMI
- UPI Credit Card EMI
- Debit Card EMI
- Cardless EMI
- BNPL
- LazyPay EMI and LazyPay BNPL flows

The training focused on understanding:

- EMI eligibility
- Pre-eligibility
- Lender selection
- Merchant and lender mappings
- Payment gateway routing
- Customer authentication
- Order creation
- OTP validation
- Order confirmation
- Status inquiry
- Final transaction status
- Reconciliation and refund-related statuses

### Objectives

The objectives were to:

1. Understand the end-to-end EMI journey.
2. Understand where eligibility decisions are made.
3. Identify the role of lenders and payment gateways.
4. Understand how failures are represented in APIs and transaction data.
5. Learn how to investigate an EMI issue from both technical and business perspectives.

---

## 1.3 EMI Service and ACS Simulator training

A major part of the work involved the **EMI Service** and **ACSSimulator**.

The ACS Simulator was used as a controlled test dependency to simulate external lender, affordability, or authentication-system behavior. This allowed EMI flows to be tested without depending entirely on live lender or banking systems.

The work focused particularly on:

- EMI Service interaction with ACSSimulator.
- Pre-eligibility request and response behavior.
- LazyPay EMI scenarios.
- LazyPay BNPL scenarios.
- Eligible and ineligible responses.
- Failure and error-response scenarios.
- Request and response mapping.
- Validation of expected LazyPay workflow behavior.

### Objectives

The objectives of the ACS Simulator training were to:

- Understand how the EMI Service communicates with an external affordability or lender-like system.
- Learn how simulator responses affect the next stage of the EMI flow.
- Test different eligibility and failure scenarios.
- Validate that requests are constructed correctly.
- Validate that responses are interpreted correctly.
- Confirm that LazyPay-related flows follow the expected BNPL workflow.
- Isolate whether an issue is caused by the EMI Service, simulator behavior, request mapping, response mapping, or configuration.
- Safely test integration behavior without exposing live traffic to uncontrolled experiments.

This training gave me practical exposure to integration testing and helped me understand how external dependencies can be represented in a controlled test environment.

---

## 1.4 Load and capacity-testing training

Another important area was capacity and load testing of the EMI Service.

The work involved understanding how the EMI Service behaves under sustained traffic and how its deployment on EKS can be evaluated.

The tools and concepts covered included:

- k6
- Locust
- Kubernetes
- Amazon EKS
- Virtual users
- Request-rate control
- Worker configuration
- Synchronous and asynchronous traffic
- CPU and memory utilization
- Service scalability
- Throughput and latency
- Error-rate monitoring
- Isolation of test traffic from live production traffic

### Objectives

The objectives were to:

- Measure EMI Service performance under controlled load.
- Understand the service’s capacity and scaling behavior.
- Identify bottlenecks in the application or infrastructure.
- Test both synchronous and asynchronous or bulk traffic.
- Validate behavior at a fixed request rate.
- Monitor service health during load testing.
- Keep performance testing isolated from live customer traffic.
- Produce console-based test results that can be reviewed easily.

The preferred load-test design was a self-contained k6 script that:

- Uses a fixed **250 requests per second**.
- Does not use staged load profiles.
- Accepts VU count, duration, and worker count as command-line parameters.
- Sends approximately **70% asynchronous or bulk traffic**.
- Sends approximately **30% synchronous traffic**.
- Prints performance results directly in the console.

Locust was also considered for distributed or worker-based test execution and for scenarios where a more flexible Python-based load model is useful.

---

## 1.5 SQL, Redshift, and data-analysis training

I received practical training in converting business requirements into SQL queries.

The work involved Redshift and materialized views related to:

- Transactions
- Payment types
- Merchant-payment mappings
- Payment gateways
- Gateway parameters
- Pre-eligibility
- Processed files
- EMI performance

### Objectives

The objectives were to:

- Write read-only queries for business analysis.
- Understand PayU’s reporting data structures.
- Calculate transaction volume and success rate.
- Join transaction data with lender and gateway metadata.
- Analyze merchant and lender performance.
- Extract structured values from JSON fields.
- Create queries suitable for Grafana dashboards and alerts.
- Use consistent and explainable metric definitions.

---

## 1.6 Monitoring, dashboards, and alerting training

I also learned how PayU’s business and technical systems are monitored using Grafana, OpenSearch, PromQL, and Redshift.

This training covered:

- Grafana time-series panels
- Grafana Stat panels
- Unified alert rules
- OpenSearch and Lucene queries
- Prometheus metrics
- Kubernetes pod-level monitoring
- Business alerts
- API latency alerts
- File-processing alerts
- SFTP failure alerts
- Escalation to Tech On-Call, KAM, Product, or Banking Operations

### Objectives

The objectives were to:

- Detect technical incidents early.
- Monitor business performance continuously.
- Identify affected merchants, lenders, or gateways.
- Build actionable rather than generic alerts.
- Ensure notifications display calculated values clearly.
- Route issues to the correct responsible team.

---

## 1.7 AI agent and automation training

I also gained experience in designing AI-based internal support and investigation systems.

The work included:

- Intent classification
- Skill routing
- Database analysis
- OpenSearch investigation
- Documentation lookup
- Planner-executor workflows
- Result verification
- Caching and idempotency
- Redis task management
- FastAPI A2A interfaces
- Structured responses
- Evidence-based troubleshooting

The main focus was the EMI KAM Agent, which is intended to support:

- KAMs
- Product teams
- PS teams
- Integration teams
- Internal operations and engineering teams

### Objectives

The objectives were to:

- Build an EMI-focused support and investigation capability.
- Use the correct source for each question.
- Keep database and log access read-only.
- Avoid exposing secrets and customer PII.
- Explain what happened, why it happened, and what should happen next.
- Ask for missing information instead of making unsupported assumptions.

---

# 2. Technical Knowledge Gained

## 2.1 End-to-end EMI Service understanding

I gained an understanding of how the EMI Service participates in the larger payment journey.

The service may interact with:

- Merchant systems
- Pre-eligibility systems
- Lender or banking systems
- Authentication and OTP systems
- Payment gateways
- Order-processing systems
- Status and reconciliation systems

I learned that an EMI transaction can fail at different stages, including:

- Merchant configuration
- Eligibility
- Customer or card eligibility
- Lender risk checks
- OTP or authentication
- Order creation
- Authorization
- Gateway routing
- Lender response
- Reconciliation

This helped me understand why transaction debugging must be based on the exact stage at which a failure occurred.

---

## 2.2 ACSSimulator integration knowledge

Through the ACS Simulator work, I learned how external dependencies can be simulated during integration testing.

Important technical concepts included:

- Simulator-driven request and response flows.
- Controlled external-service behavior.
- Pre-eligibility response handling.
- Eligible and ineligible test cases.
- Error and failure simulation.
- Response-field mapping.
- Dependency isolation.
- Workflow validation.
- End-to-end integration testing.

I also learned that a simulator should not only return a successful response. It should support different behavior patterns so that the application can be tested for:

- Successful eligibility.
- Failed eligibility.
- Invalid or incomplete input.
- External-service errors.
- Timeout or unavailable-dependency behavior.
- Unexpected response values.
- LazyPay-specific BNPL outcomes.

The simulator must also follow the expected business workflow. For LazyPay BNPL, it is not sufficient to test an isolated API response; the sequence of the BNPL journey and the relationship between the EMI Service and the simulator must also be validated.

---

## 2.3 Load testing and performance engineering

I gained knowledge of how to design controlled performance tests for the EMI Service.

### Traffic model

The preferred traffic model uses:

- Fixed rate: **250 requests per second**
- Asynchronous or bulk traffic: **70%**
- Synchronous traffic: **30%**
- Configurable VU count
- Configurable test duration
- Configurable worker count
- No staged ramp-up or ramp-down profile

This model makes test results easier to compare because the request rate remains constant.

### Key metrics

The performance tests are intended to measure:

- Requests per second
- Average response time
- Median response time
- P90 and P95 latency
- Maximum latency
- Error rate
- Timeout rate
- Successful request count
- Failed request count
- Throughput by request type
- Service saturation
- CPU utilization
- Memory utilization
- Pod scaling behavior

### Test isolation

A major learning was that production load testing must remain isolated from live customer traffic.

This means that performance tests should use:

- A controlled environment.
- Test-specific identifiers.
- Simulator-backed external dependencies.
- Clearly separated test traffic.
- Monitoring that distinguishes test traffic from real traffic.
- No uncontrolled requests against live lender or customer flows.

---

## 2.4 k6 and Locust knowledge

### k6

The k6 design focused on a single self-contained script that:

- Can be run from the command line.
- Accepts runtime parameters.
- Maintains a fixed request rate.
- Supports synchronous and asynchronous traffic distribution.
- Prints summary results in the terminal.
- Does not require a staged load profile.

The expected parameterization includes:

- Number of virtual users.
- Test duration.
- Number of workers.

### Locust

Locust was considered for:

- Distributed test execution.
- Worker-based load generation.
- Python-based scenario definition.
- More complex user workflows.
- Flexible request sequencing.
- Integration with EKS-based testing infrastructure.

The use of both tools provided an understanding of the difference between:

- A compact, rate-controlled k6 test.
- A more flexible, distributed Locust test.

---

## 2.5 Kubernetes and EKS knowledge

I gained knowledge of monitoring and testing services deployed on Amazon EKS.

This included understanding:

- Pods
- Containers
- Replica scaling
- Worker distribution
- Resource requests
- CPU utilization
- Memory utilization
- Service-level throughput
- Pod-level performance
- Failure behavior under load

For infrastructure monitoring, CPU utilization was defined as container CPU usage divided by requested CPU cores. Memory utilization was defined as memory used divided by allocated memory.

This allows each pod’s utilization to be evaluated rather than showing only an overall service average.

---

## 2.6 EMI transaction and success-rate analysis

I learned how to define and analyze EMI success rates.

The analysis considers:

- Total transactions
- Eligible attempts
- Successful transactions
- Failed transactions
- Bounced transactions
- Dropped transactions
- User-cancelled transactions

The work also covered the importance of clearly defining:

- Numerator
- Denominator
- Included statuses
- Excluded statuses
- Time range
- Merchant or lender scope
- Aggregation period

For some Grafana patterns, success statuses included:

- `captured`
- `pending`
- `auth`
- `cancelled`
- `autoRefund`

For North Star business analysis, successful outcomes and failed-to-success reconciliation were treated separately from user-cancelled transactions.

I learned that two success-rate queries cannot be compared directly unless their:

- Status definitions
- Denominators
- Filters
- Time ranges
- Aggregations
- Merchant and lender scopes

are the same.

---

## 2.7 Redshift and materialized views

The work used or referenced PayU-related materialized views such as:

- `data_dumps.payubiz_payu_transaction_mv`
- `data_dumps.payubiz_payu_payment_type_mv`
- `data_dumps.payubiz_payu_merchant_payment_type_mv`
- `data_dumps.payubiz_payu_paymentgateway_mv`
- `data_dumps.payubiz_payu_paymentgateway_param_mv`
- `data_dumps.treasury_aggregated_pre_eligibility_data_mv`
- `data_dumps.treasury_aggregated_emi_processed_file_mv`

I learned how to:

- Join transactions with payment-type mappings.
- Map lender codes to bank names.
- Identify inactive payment types.
- Identify inactive merchant mappings.
- Check gateway-level activation.
- Analyze payment gateway parameters.
- Filter by transaction timestamp.
- Build rolling and monthly metrics.
- Build Grafana-compatible queries.

---

## 2.8 Pre-eligibility JSON analysis

Pre-eligibility responses contain dynamic lender and offer information in JSON format.

The work involved defining methods to:

- Parse `response_data`.
- Extract dynamic lender keys.
- Identify eligibility status.
- Extract error codes.
- Extract error reasons.
- Extract journey types.
- Group responses by merchant and lender.
- Count TRUE and FALSE outcomes.
- Analyze lender-specific and tenure-specific results.
- Avoid hardcoding one lender or one merchant.

The planned dashboard requirements included filters for:

- Merchant ID
- Amount
- Response time
- Requesting API
- Grafana time picker

A key technical learning was that JSON paths and journey-type extraction must be validated using actual returned records. A query that executes successfully is not necessarily semantically correct if the extracted field is empty or does not match the expected business values.

---

## 2.9 EMI integration and routing analysis

I learned how multiple configuration layers determine whether an EMI integration is active and how it is routed.

The analysis included:

- Payment-type status.
- Merchant-payment-type status.
- Payment gateway status.
- Lender-to-gateway mapping.
- Gateway parameters.
- PIH-related configuration.
- Merchant activation.
- Direct lender or gateway routing.

The PIH classification considered:

- `flowtype` parameters.
- `posturl` parameters.
- Legacy `integrationType = 'O'`.
- Special classification of PG `281` as the EMI MS base PG.

This helped define classifications such as:

- PIH-capable PG.
- Non-PIH direct PG.
- EMI MS base PG.
- Inactive lender integration.
- Fully active lender integration.

---

## 2.10 Grafana, OpenSearch, and PromQL

I gained practical knowledge of three important observability areas.

### Grafana

The work covered:

- Time-series dashboards.
- Stat queries.
- Business metrics.
- Bank-wise EMI reporting.
- Lender-wise reporting.
- Monthly reporting.
- File-processing metrics.
- Alert rules.
- Time-picker filtering.
- Merchant selectors.
- Query variables.

### OpenSearch

OpenSearch was used for transaction and API investigation, including:

- Lender API latency.
- Request and response behavior.
- Service-chain analysis.
- Error patterns.
- Lender-specific visualization.
- Lucene filtering.

### PromQL

PromQL work included infrastructure metrics such as:

- CPU usage by pod.
- CPU usage relative to requested cores.
- Memory utilization.
- Unhealthy pod counts.
- Namespace-scoped queries for `emi-service`.

---

## 2.11 AI agent architecture

I gained knowledge of designing an agent that uses specialized tools for different questions.

The EMI KAM Agent was structured around five main skills:

1. North Star database analysis.
2. OpenSearch transaction debugging.
3. EMI FAQ.
4. EMI integration guidance.
5. Configuration and onboarding guidance.

The agent is intended to:

- Understand simple English and Hinglish.
- Identify whether a question is about a merchant, PayU ID, lender, or configuration.
- Ask for a Merchant ID or Merchant Key where necessary.
- Use Redshift for aggregate analysis.
- Use OpenSearch for transaction-specific investigation.
- Use documentation for conceptual questions.
- Avoid unsupported conclusions.
- Provide a business-friendly next action.

---

## 2.12 Production agent execution architecture

The related agent architecture included:

- Streamlit reference implementation.
- FastAPI A2A sidecar.
- Redis task state.
- JSON-RPC methods.
- REST work and status endpoints.
- Server-sent event progress streaming.
- Intent routing.
- Skill dispatch.
- Planner and executor.
- Database and log tools.
- Intent verification.
- Result caching.
- Idempotency.
- Per-session locking.
- Controlled observer remediation.
- Result storage.
- Evaluation and feedback scoring.

The architecture separates:

- Reference UI behavior.
- Production API behavior.
- Lightweight scaffolding.
- Shared execution logic.

This was important for understanding how an AI support system can move from a prototype to a reliable internal service.

---

## 2.13 CodeGraph and offline knowledge systems

I also gained knowledge of two proposed knowledge-layer approaches.

### EMI CodeGraph

The proposed EMI CodeGraph includes:

- Offline source parsing.
- Tree-sitter.
- Structured extraction.
- SQLite with FTS5.
- Graph relationships.
- Protobuf fast-path lookups.
- GitLab CI builds.
- Artifact validation.
- Read-only query access.

### Nexus-style architecture

The broader architecture includes:

- Neo4j graph storage.
- Qdrant or Weaviate vector storage.
- Offline code parsing.
- AST analysis.
- Call graphs.
- Git history.
- Embeddings.
- Shared indexed knowledge for agents.

The key learning was how to move expensive repository analysis away from the live agent request path and provide bounded, source-referenced answers through pre-indexed artifacts.

---

## 2.14 Debugging and reliability

A structured four-phase agent-debugging process was defined:

1. Capture the failure state.
2. Diagnose the likely cause.
3. Take the smallest contained recovery action.
4. Produce a human-readable report.

The process is intended for:

- Repeated tool failures.
- Context overflow.
- Incorrect routing.
- Service connection failures.
- Missing files.
- Stale repository state.
- Timeout or quota problems.
- Tests that remain unsuccessful after a claimed fix.

This helped establish an evidence-based approach to debugging rather than relying on repeated retries or assumptions.

---

# 3. Understanding of the Organization

## 3.1 PayU’s interconnected payment ecosystem

The work provided an understanding that PayU operates a highly interconnected payment and affordability platform.

An EMI transaction may involve:

- Merchant systems.
- PayU transaction services.
- EMI Service.
- Lender systems.
- Banking partners.
- Payment gateways.
- Authentication services.
- Pre-eligibility systems.
- Reconciliation systems.
- Monitoring and alerting systems.

This means that a customer-facing problem may not originate in the same service where it becomes visible.

For example:

- An eligibility issue may be caused by lender rules.
- A missing EMI option may be caused by merchant configuration.
- A gateway failure may appear as a payment authorization failure.
- A simulator mismatch may look like an EMI Service defect.
- A file-sharing failure may be caused by SFTP credentials or external connectivity.

---

## 3.2 Understanding of cross-functional responsibilities

### KAMs

KAMs require:

- Merchant-level performance analysis.
- Clear explanations of business impact.
- Lender and bank-level drill-downs.
- Recommended next actions.
- Information that can be shared with merchants or internal teams.

### Product and PS teams

These teams help with:

- Product behavior.
- Merchant onboarding.
- EMI journey expectations.
- Product-specific integration requirements.
- Lender and banking workflows.

### Integration and Banking Operations

These teams handle or support:

- Lender activation.
- Payment-type configuration.
- Gateway mappings.
- Merchant integration.
- File-sharing processes.
- SFTP issues.
- Bank coordination.

### Engineering and Tech On-Call

These teams are responsible for:

- EMI Service health.
- API performance.
- Transaction failures.
- Service incidents.
- Load and capacity issues.
- Production alerts.
- Corrective technical action.

The work showed that technical analysis becomes useful only when it identifies both the likely cause and the team responsible for the next action.

---

## 3.3 Importance of simulator-based testing

The ACS Simulator work showed how PayU can safely test external integrations without directly depending on live lender systems.

This provides benefits such as:

- Reproducible test conditions.
- Controlled positive and negative responses.
- Safer integration testing.
- Faster debugging.
- Reduced dependency on partner availability.
- Better validation of request and response contracts.
- Ability to test unusual or failure conditions.

It also showed that simulator behavior must represent the business workflow accurately. A technically valid response is not sufficient if it does not occur at the correct stage or does not match the expected LazyPay BNPL flow.

---

## 3.4 Importance of controlled performance testing

The load-testing work showed how service performance must be evaluated without affecting live customer traffic.

This requires:

- Isolated environments.
- Controlled traffic.
- Simulated dependencies.
- Clear traffic distribution.
- Stable request rates.
- Infrastructure monitoring.
- Test-specific identification.
- Careful interpretation of results.

This is especially important for a payment service because uncontrolled load can affect real merchants, customers, lenders, or downstream systems.

---

## 3.5 Business monitoring and technical monitoring

I learned that PayU requires two separate but connected monitoring perspectives.

### Technical monitoring

This includes:

- API latency.
- Error rates.
- Service failures.
- Pod health.
- CPU and memory utilization.
- SFTP failures.
- File-processing failures.
- Dependency failures.

### Business monitoring

This includes:

- EMI success rate.
- Transaction volume.
- EMI GMV.
- Active merchant count.
- Pre-eligibility volume.
- Lender performance.
- Bank-wise performance.
- BIN eligibility errors.

A service may be technically available but still have a serious business problem. Therefore, technical and business dashboards must be designed separately and connected during investigation.

---

## 3.6 Evidence and data governance

Another organizational learning was the importance of evidence-based analysis.

The work emphasized:

- Using Redshift for aggregate metrics.
- Using OpenSearch for transaction-specific debugging.
- Using configuration data for routing and integration analysis.
- Using documentation for conceptual questions.
- Keeping data access read-only.
- Avoiding PII and secrets.
- Clearly identifying uncertain or unverified conclusions.
- Requesting missing inputs instead of inventing data.

---

# 4. Progress of Work and Implementation Done

## 4.1 Phase 1: Domain onboarding and system understanding

The first phase involved understanding:

- PayU’s business model.
- Payment and EMI products.
- Merchant and lender relationships.
- Payment gateway behavior.
- Eligibility and pre-eligibility.
- Transaction status handling.
- Operations and support roles.

This formed the base for the later technical work.

---

## 4.2 Phase 2: EMI Service and ACSSimulator integration work

The second phase focused on the EMI Service and its interaction with ACSSimulator.

The work included:

- Understanding the integration boundary between EMI Service and the simulator.
- Reviewing how requests are sent to the simulated dependency.
- Understanding how responses are mapped into the EMI flow.
- Testing pre-eligibility scenarios.
- Testing eligible and ineligible responses.
- Considering failure and error scenarios.
- Validating expected LazyPay EMI and BNPL behavior.
- Checking whether simulator behavior supports downstream flow execution.
- Separating service-side issues from simulator-side or configuration-side issues.

The ACS Simulator made it possible to test integration behavior in a controlled environment instead of depending entirely on live lender or banking services.

### Implementation outcome

The integration and test scenarios were defined around the EMI Service and simulator workflow. The work established the expected testing approach and behavior to validate.

The available records do not independently confirm the completion status of every individual simulator test case. Therefore, the final project report should classify individual scenarios separately as:

- Completed.
- In progress.
- Blocked.
- Pending validation.

---

## 4.3 Phase 3: LazyPay EMI and BNPL pre-eligibility testing

The work also covered LazyPay-related scenarios.

The testing focus included:

- Pre-eligibility request behavior.
- Eligibility and non-eligibility responses.
- BNPL-specific flow expectations.
- External dependency simulation.
- Response interpretation.
- Error handling.
- Validation of the next step after pre-eligibility.

An important learning was that LazyPay BNPL behavior must be validated as a complete workflow rather than as an isolated API call.

The integration must be checked for:

- Correct request structure.
- Correct customer or transaction context.
- Correct simulated response.
- Correct interpretation by EMI Service.
- Correct continuation to the next step.
- Correct handling of failures.

---

## 4.4 Phase 4: EMI Service load and capacity testing

The fourth phase covered performance testing for the EMI Service deployed on EKS.

### Test design

The preferred design included:

- A self-contained k6 test.
- Fixed request rate of **250 requests per second**.
- No staged load profile.
- Configurable VU count.
- Configurable duration.
- Configurable worker count.
- Approximately 70% asynchronous or bulk requests.
- Approximately 30% synchronous requests.
- Console output containing the test results.

Locust was also considered for worker-based or distributed test execution.

### Performance areas evaluated

The load-testing work was designed to evaluate:

- Throughput.
- Response latency.
- Percentile latency.
- Error rate.
- Timeouts.
- Synchronous request behavior.
- Asynchronous or bulk request behavior.
- Pod utilization.
- Scaling behavior.
- Application bottlenecks.
- Dependency behavior.
- Stability over the test duration.

### Infrastructure monitoring

During load tests, the relevant infrastructure metrics included:

- CPU usage by pod.
- CPU usage relative to requested CPU.
- Memory usage.
- Number of healthy and unhealthy pods.
- Replica behavior.
- Service availability.
- Request error rate.

### Implementation outcome

The load-test requirements and traffic model were defined for execution using k6 and Locust. The design was intended to support repeatable and comparable tests.

The test setup must remain isolated from live customer traffic. Any final performance figures should only be reported after the relevant test has been executed and its output captured.

---

## 4.5 Phase 5: EMI performance analysis framework

A structured North Star analysis framework was defined for EMI performance investigations.

The framework includes:

- Merchant ID or Merchant Key as the required merchant identifier.
- Last-month analysis when no period is specified.
- Previous two-month average as the default comparison.
- Total transaction volume.
- Eligible EMI attempts.
- Success, failed, bounced, dropped, and user-cancelled buckets.
- Field 9 error analysis.
- Lender and issuer analysis.
- Payment gateway analysis.
- BIN analysis.
- Configuration analysis.
- One or two anonymized sample transactions when appropriate.
- Business-friendly next actions.

The framework also separates:

- Payment-performance analysis.
- Transaction debugging.
- Configuration and onboarding analysis.
- Lender or banking escalation.

---

## 4.6 Phase 6: SQL and Redshift query development

Query patterns were developed or documented for:

- EMI success rate.
- Lender-specific success rate.
- Bank-wise Credit Card EMI performance.
- Payment gateway performance.
- Monthly EMI reporting.
- Monthly EMI and BNPL GMV.
- Transaction volume.
- Merchant counts.
- Pre-eligibility outcomes.
- BIN eligibility failures.
- Inactive EMI integrations.
- Fully active lender integrations.
- PIH-capable gateways.
- Processed-file counts.

Important data sources included the PayU transaction, payment-type, gateway, merchant mapping, pre-eligibility, and processed-file materialized views.

The work also documented query limitations such as:

- Differences in success-rate definitions.
- Differences in denominator logic.
- Time-window differences.
- Merchant-wide versus lender-specific scope.
- Query execution and validation requirements.
- Dynamic JSON extraction concerns.

---

## 4.7 Phase 7: Pre-eligibility dashboard work

The pre-eligibility dashboard was designed around:

`data_dumps.treasury_aggregated_pre_eligibility_data_mv`

The intended analysis includes:

- All-merchants and all-lenders reporting.
- Merchant-to-lender grouping.
- TRUE and FALSE eligibility counts.
- Dynamic lender extraction.
- Journey-type analysis.
- Tenure-level analysis.
- Response-time analysis.
- Requesting-API analysis.
- Amount filtering.
- Grafana time-picker filtering.
- Merchant-ID selection.

The dashboard requirement was to avoid hardcoding:

- A single merchant.
- A single lender.
- A fixed date range.
- A fixed amount range.

The user-reported all-lender query worked without the journey-type predicate, while one reported test returned no data after the journey-type condition was added. This means the extracted journey-type values and filter behavior require direct validation against the active dataset.

---

## 4.8 Phase 8: EMI integration and routing inventory

The integration-analysis work covered:

- Inactive payment types.
- Inactive merchant mappings.
- Fully active lender mappings.
- Gateway activation.
- PIH parameter identification.
- Legacy PIH configuration.
- EMI MS base PG classification.
- Direct non-PIH gateway classification.

The work used configuration relationships across payment-type, merchant-payment-type, gateway, and gateway-parameter views.

This created reusable query patterns for identifying configuration gaps that may affect:

- EMI visibility.
- Lender availability.
- Payment routing.
- Merchant onboarding.
- Payment initiation.
- Payment gateway selection.

---

## 4.9 Phase 9: Grafana dashboards and business alerts

A broad set of dashboard and alert requirements was documented.

### EMI performance alerts

These included:

- Low EMI success rate.
- Extremely low EMI success rate.
- Low EMI GMV.
- Extremely low EMI GMV.
- Low EMI transaction volume.
- EMI transacting merchant count drop.
- Pre-eligibility hit drop.
- BIN eligibility failure increase.
- Lender-specific low success rate.
- Bank-specific Credit Card EMI success-rate issues.
- Monthly EMI success-rate reporting.

### Lender API monitoring

The lender API scope included flows for:

- HDFC DC EMI.
- LazyPay BNPL.
- Bajaj.
- LPEMI.
- Axio.
- ZestMoney.

The APIs included:

- Pre-eligibility.
- Create order.
- Validate OTP.
- Order confirmation.
- Status inquiry.
- Initiate transaction.
- Initiate OTP.
- Customer status.
- Eligibility.
- Inquiry.

### File and SFTP monitoring

The processed-file work used:

`data_dumps.treasury_aggregated_emi_processed_file_mv`

The requirements included:

- Daily file counts.
- Asia/Kolkata reporting-day boundaries.
- `createdBy = -1` subset analysis.
- Missing or failed file identification.
- Non-null error reasons.
- SFTP connection failure detection.
- Invalid user or password errors.
- Alerts routed to the relevant banking-product SPOC or operations team.

These alert and dashboard definitions are documented requirements and query patterns. The available records do not independently confirm that every dashboard panel, alert rule, or notification route has been activated in production.

---

## 4.10 Phase 10: Infrastructure monitoring

Infrastructure monitoring requirements were defined specifically for the EMI Service namespace.

The monitoring covered:

- CPU utilization by pod.
- CPU usage divided by requested CPU cores.
- Memory utilization based on used versus allocated memory.
- Unhealthy pod count.
- Namespace-specific PromQL.
- Container-level filtering.
- Pod-level visualization.
- Resource saturation during load tests.

This infrastructure view complements business monitoring by showing whether performance problems are related to:

- CPU saturation.
- Memory pressure.
- Insufficient replicas.
- Pod instability.
- Application-level errors.
- Dependency latency.

---

## 4.11 Phase 11: EMI KAM Agent work

The EMI KAM Agent was defined as a focused internal assistant for EMI investigation and support.

Its intended users include:

- KAMs.
- Product teams.
- PS teams.
- Integration teams.
- Internal engineering teams.

The five main skills are:

1. North Star database analysis.
2. OpenSearch transaction debugging.
3. EMI FAQ.
4. EMI integration guidance.
5. Configuration and onboarding guidance.

The agent is intended to support:

- Credit Card EMI.
- UPI Credit Card EMI.
- Debit Card EMI.
- Cardless EMI.
- BNPL.

Standalone UPI and unrelated non-EMI payment questions are outside the intended scope.

The agent should:

- Use simple English and Hinglish.
- Request Merchant ID or Merchant Key where required.
- Use PayU ID for transaction debugging.
- Use Redshift for aggregate analysis.
- Use OpenSearch for transaction-specific analysis.
- Protect customer data.
- Provide deterministic answers.
- Explain root cause and next action.
- Clearly state uncertainty when evidence is missing.

---

## 4.12 Phase 12: UPI and production agent architecture

The related production-style agent architecture included:

- Streamlit reference implementation.
- FastAPI A2A sidecar.
- Redis task state.
- JSON-RPC and REST work endpoints.
- Task status polling.
- SSE progress streaming.
- Intent routing.
- Skill dispatch.
- Harness selection.
- Planner and executor.
- Database and log investigation.
- Documentation search.
- Intent verification.
- Result caching.
- Idempotency.
- Per-session locking.
- Controlled remediation.
- Result storage.
- Evaluation scoring.

The architecture also distinguished:

- Rich reference application.
- Production sidecar.
- Thin scaffold implementation.
- Shared execution engine.

This work helped define how an internal AI support system could be organized for reliability and controlled evidence usage.

---

## 4.13 Phase 13: CodeGraph and knowledge-layer design

A proposed EMI microservice CodeGraph was designed to move code and configuration analysis outside the live request path.

The proposed process included:

1. GitLab CI triggering the build.
2. Selecting approved repositories and source paths.
3. Parsing code with Tree-sitter.
4. Using regex fallback for supported structures.
5. Extracting structured facts.
6. Enriching the graph with GitLab information.
7. Validating generated artifacts.
8. Publishing SQLite and Protobuf outputs.

The planned outputs were:

- SQLite with FTS5 for full-text search and graph relationships.
- Protobuf for fast exact-key lookups.

A comparison was also made with a broader Nexus-style architecture based on:

- Neo4j.
- Qdrant or Weaviate.
- Offline source indexing.
- Call graphs.
- Git history.
- Embeddings.

The design records do not independently confirm that the full CodeGraph artifact, query CLI, or runtime integration has been deployed.

---

## 4.14 Phase 14: Agent introspection and debugging process

A reusable debugging workflow was documented for agent and engineering failures.

### Phase 1: Capture failure state

Record:

- Error message.
- Stack trace if available.
- Last successful action.
- Last failed action.
- Goal in progress.
- Environment assumptions.
- Branch and filesystem state.
- Repeated patterns.

### Phase 2: Diagnose

Classify the issue as:

- Logic-related.
- State-related.
- Environment-related.
- Policy-related.
- Service-related.
- Data-related.

### Phase 3: Contained recovery

Take the smallest safe action, such as:

- Checking actual filesystem state.
- Narrowing the task to one file or test.
- Stopping repeated retries.
- Reducing low-signal context.
- Verifying service health.
- Testing one discriminating hypothesis.

### Phase 4: Report

Provide:

- Root-cause hypothesis.
- Recovery action.
- Evidence.
- Result.
- Risk.
- Follow-up.
- Preventive improvement.

---

# Overall Work Status

| Work area | Progress |
|---|---|
| PayU and EMI domain onboarding | Completed as practical training |
| EMI Service understanding | Completed and applied to integration analysis |
| ACSSimulator integration work | Covered through controlled EMI and LazyPay testing scenarios |
| LazyPay EMI and BNPL testing | Workflow and pre-eligibility scenarios defined and analyzed |
| k6 load-test design | Defined around fixed 250 RPS, configurable execution, and console reporting |
| Locust load-test approach | Considered for worker-based and distributed execution |
| EKS capacity and infrastructure monitoring | Defined for pod-level and service-level analysis |
| EMI North Star analysis framework | Defined and documented |
| Redshift and SQL query patterns | Developed and documented |
| Pre-eligibility dashboard requirements | Defined with dynamic lender and merchant support |
| EMI integration inventory | Defined using payment-type, merchant, gateway, and parameter views |
| PIH and non-PIH classification | Query logic defined |
| Grafana business monitoring | Requirements and query patterns documented |
| OpenSearch lender API monitoring | Scope and visualization requirements documented |
| Processed-file and SFTP monitoring | Requirements and query patterns documented |
| EMI KAM Agent | Scope and skills defined |
| UPI agent architecture | Detailed execution architecture documented |
| CodeGraph and knowledge indexing | Proposed architecture defined |
| Agent introspection debugging | Four-phase process defined |
| Production deployment of all described work | Not independently verified |
| Execution of every load test and simulator scenario | Individual completion status requires test evidence |
| Activation of every dashboard and alert | Not independently verified |

---

# Key Outcomes of the Internship Work

The major outcomes of the work were:

1. Developed a strong understanding of PayU’s EMI and affordability ecosystem.
2. Learned how the EMI Service interacts with external dependencies such as ACSSimulator.
3. Gained experience with LazyPay EMI and BNPL pre-eligibility testing.
4. Defined controlled integration-testing scenarios for eligible, ineligible, and failure responses.
5. Designed a fixed-rate load-testing approach for the EMI Service.
6. Defined a 250 RPS test model with 70% asynchronous and 30% synchronous traffic.
7. Learned how to evaluate EMI Service capacity on EKS.
8. Developed SQL patterns for EMI performance, eligibility, integration, and monitoring.
9. Defined Grafana and OpenSearch monitoring requirements.
10. Learned how to separate technical monitoring from business monitoring.
11. Defined a structured North Star analysis skill for EMI investigations.
12. Designed the scope and skills of the EMI KAM Agent.
13. Studied production agent architecture, Redis task handling, A2A interfaces, and evidence-based routing.
14. Designed an offline CodeGraph and knowledge-indexing approach.
15. Created a structured methodology for debugging agent failures and engineering issues.

---

# Conclusion

My work at PayU progressed from foundational learning to practical analysis, testing, monitoring, and automation design.

The most important practical areas were:

- EMI Service and ACSSimulator integration.
- LazyPay EMI and BNPL workflow testing.
- Pre-eligibility analysis.
- EMI Service load and capacity testing.
- Redshift-based transaction and business analysis.
- Grafana, OpenSearch, and infrastructure monitoring.
- EMI integration and gateway-routing analysis.
- EMI KAM Agent design.
- CodeGraph and offline knowledge-layer architecture.
- Evidence-based engineering and agent debugging.

Together, these activities provided exposure to both sides of engineering work at PayU:

- **Building and testing services**, including simulator-based integration and load testing.
- **Operating and investigating services**, including dashboards, alerts, SQL analysis, logs, agent workflows, and incident diagnosis.

The work created a foundation for further implementation and validation. The main areas requiring final confirmation are the execution results of individual ACS Simulator scenarios, completed load-test runs, active production dashboards, deployed alert rules, and runtime deployment of the proposed agent and CodeGraph components.
