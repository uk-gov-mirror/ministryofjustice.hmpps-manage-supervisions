# 2. Build a Monolith

Date: 2021-03-15

## Status

Accepted

## Context

HMPPS general policy on microservice development is to [separate user and business interfaces by default](https://structurizr.com/share/56937/decisions#%2FRefer%20and%20monitor%20an%20intervention:1). This is adopted in order to build microservices with bounded contexts, and to
provide business logic APIs from the start.

The above ADR mentions some consequences that are directly relevant to this project, in particular "Contracts between the UI and the service components will take a while to stabilise, creating churn in the beginning."

## Decision

We will initially build the "Manage a Sentence in the Community" product as a single server-side application.
The same application will be responsible for user interface, database storage, and communication to external APIs. This
is in contravention of the above HMPPS default, but is appropriate in this case.

We will do this because monolithic applications are quicker to get started with and iterate. A two-tier architecture
does not confer any advantages at this early stage of development, and adds complexity to the iterative process of an
early-stage application.

For our product, which is aimed at a pilot at this point, we believe that this is a premature optimisation.

## Consequences

At some point it may be appropriate to split the application into a two-tier architecture that adds a business-level API or
database storage that can be reused by other clients. That change will be documented in an ADR that supercedes this one.

The internal software design of the application must take care to separate UI and business logic, to take into account that
in future the business logic may need to be exposed via an API or reimplemented in Kotlin.
