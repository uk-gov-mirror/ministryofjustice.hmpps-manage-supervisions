# 4. Define release environments

Date: 2021-03-15

## Status

Accepted

## Context

In order to predicatably release our code, it needs testing both by itself, and with other systems. Related systems include:

* nDelius / Community API
* OASys / Assessments API

In future, integration testing with other HMPPS services will also be required.

## Decision

We will manage releases using four environments, which are the same as used by nDelius and the Community API.

1. **Test**: used during development.
2. **Stage**: used for integration and user testing of new features within the team.
3. **Pre-prod**: used for testing of releases with live data, before they go live.
4. **Prod**: used by users, with real data.

In our test environment, we will connect to the test environment of the Community API, and so forth.

## Consequences

If upstream environments change, we will need to change with them in order to continue using matching datasets.

Other services may use different environments, and we will have to choose the correspondence on a case-by-case basis if we need to connect to them.
