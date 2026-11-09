# Modernization Plan: SupplyChain Worker Messaging Modernization

**Project**: SupplyChain Worker

---

## Technical Framework

- **Language**: Java 8
- **Framework**: Spring Boot 2.7.18
- **Build Tool**: Maven
- **Database**: None identified
- **Key Dependencies**: Spring AMQP (RabbitMQ), Lombok

---

## Overview

> This migration replaces the worker's RabbitMQ messaging dependency with Azure
> Service Bus. The application currently consumes order-created, inventory-alert,
> and approval-pending notifications from RabbitMQ. The modernized worker will:
>
> - Receive these notification messages through Azure Service Bus.
> - Preserve the existing message-processing responsibilities.
> - Use managed identity as the default Azure authentication approach.
>
> The work is scoped to the messaging migration and its verification; deployment
> and runtime upgrades are not included.

---

## Migration Impact Summary

| Application | Original | Azure target | Authentication | Comments |
|---|---|---|---|---|
| Worker | RabbitMQ | Azure Service Bus | Managed Identity | Three notification queues |

---

## Open Questions & Questionnaire

- [x] Q: Should infrastructure be provisioned? → A: No; focus on code migration.
- [x] Q: Should integration testing be included? → A: Yes; use mocked dependencies
  because no test infrastructure is provided.
- [x] Q: Should security/CVE remediation be included? → A: Yes; include the
  default dependency scan and remediation task.
- [x] Q: Which deployment target should be used? → A: No deployment; migration only.
