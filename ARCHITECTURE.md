## Product Choice

**Product name:** Yandex Go  
**Link to the product's website:** https://go.yandex
**Short description:** Yandex Go is a ride-hailing and urban services aggregator that allows users to order taxis, delivery, and other city services from a single mobile application.

---

## Main components

![Yandex Go Component Diagram](/docs/diagrams/out/yandex-go/architecture-component/Component%20Diagram.svg)

[Component Diagram Code](/docs/diagrams/src/yandex-go/architecture-component.puml)

### Selected components

1. **Mobile Application** – client-side application used by customers to create ride requests, track drivers, and manage payments.

2. **API Gateway** – central entry point that receives requests from mobile apps and routes them to the appropriate backend services.

3. **Payment Service** – handles all payment-related operations such as charging customers, processing refunds, and storing transaction history.

4. **Maps and Routing Service** – responsible for calculating optimal routes, estimating travel time, and providing geolocation functionality.

5. **Database** – persistent storage that keeps information about users, orders, drivers, and completed trips.

---

## Data flow

![Yandex Go Sequence Diagram](/docs/diagrams/out/yandex-go/architecture-sequence/Sequence%20Diagram.svg)

[Sequence Diagram Code](/docs/diagrams/src/yandex-go/architecture-sequence.puml)

### Description of main flow

The main user interaction flow begins when the **Mobile Application** sends a ride request to the **API Gateway**.  
The gateway forwards this request to internal services such as **Maps and Routing** to calculate distance and price.  
After confirmation, the **Payment Service** verifies payment details and reserves funds.  
Finally, all confirmed data is stored in the **Database**, and the driver receives the order information.  
Throughout the process, components exchange data such as user location, trip parameters, pricing information, and payment status.

---

## Deployment

![Yandex Go Deployment Diagram](/docs/diagrams/out/yandex-go/architecture-deployment/Deployment%20Diagram.svg)

[Deployment Diagram Code](/docs/diagrams/src/yandex-go/architecture-deployment.puml)

### Deployment description

Client mobile applications are deployed on user smartphones.  
Backend services such as API Gateway, Payment, and Routing run in cloud infrastructure managed by Yandex.  
Databases are hosted on dedicated servers within the same cloud environment.  
External services like map providers and payment processors are integrated through secure network connections.

---

## Assumptions

- I assume the routing service continuously receives real-time traffic data to improve travel time estimations.
- I assume the payment service supports multiple external payment providers and implements secure tokenization of card data.

---

## Open questions

- How exactly is load balancing organized between regional data centers?
- What caching strategies are used to reduce the load on mapping and routing services during peak hours?
