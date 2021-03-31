# 7. Write data to Delius synchronously

Date: 2021-03-31

## Status

Accepted

## Context

In order to preserve continuity of service, and data integrity, when actions are taken in our application, we need to reflect those actions in nDelius. This is so that if a case can no longer be handled by our applicaiton, the user can go to nDelius to continue the process without needing to re-enter information.

Additionally, current reporting is based on nDelius, so by storing our data in nDelius we can ensure that no data is lost from existing reports.

There are two possible modes in which our application could store data in remote systems.

1. Synchronous, or blocking. The application writes data to the remote system immediately, and reports the result back to the user. This choice is relevant when validation from the remote system is required, or during early stages of development when data needs are not yet fully settled. However, as the remote system is integral to the process, it will be slower, and may cause the new service to be seen as being slower than the remote system it is replacing.

1. Asynchronous, or non-blocking. This is more of an event-oriented process, where feedback from the remote system is not required. Data is stored locally to the service, and other systems are informed of changes by the [publication of domain events](https://structurizr.com/share/56937/decisions#%2FRefer%20and%20monitor%20an%20intervention:2) as used by other HMPPS services. This could be implemented via HMPPS-wide event streams, locally to the application with the use of a background worker for processing asynchronous writes, or both. This is faster for the user, but depends on robust data validation in our service.

Our service does not own any data at this point; is it not the primary repository for the information it processes.

## Decision

We will start by using all remote systems (via the Community and other APIs) in a purely synchronous mode, both for reading and writing. This is in order that we can rely on validation in nDelius in the early stages of development, and notify the user of errors.

## Consequences

Because all data will be stored and retrieved synchronously, service-local data storage is not yet required.

This approach will be slower for the user, and may lead to a perception that our service is less performant than nDelius.

We acknowledge that this introduces technical debt in the form of strong coupling between our service and the remote services it relies upon.

The service should expect to move to asynchronous writes where possible in future, when the service has stabilised. This may be driven by:

* Performance optimisation, based on accurate profiling
* The need to inform other services of change events
* Repayment of technical debt incurred as noted above
* Deprecation of or changes to remote APIs
* The service becoming the canonical owner of data it processes

Note that service-local data storage and event broadcast may be required before asynchronous writes; there may be a point when the service is writing synchronously both to its own data storage and to remote APIs, and informing other services via events.

There may always be a need for synchronous writes; we do not assume that in future all writing to remote APIs will be asynchronous.
