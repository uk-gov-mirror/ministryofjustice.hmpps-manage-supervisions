# 3. Build in Typescript

Date: 2021-03-15

## Status

Accepted

## Context

HMPPS is converging on a [combination of Node.js and Kotlin](https://structurizr.com/share/56937/decisions#%2FRefer%20and%20monitor%20an%20intervention:1).

## Decision

The application will be built in Node.js using Typescript, and will be based on the [HMPPS Typescript template application](https://github.com/ministryofjustice/hmpps-template-typescript).

## Consequences

Many library and pipeline choices are already made by default in the template app. If these need to change, we will issue further ADRs where appropriate.

Business logic may be extracted in future (see ADR 2), and may be
reimplemented in another language such as Kotlin. Software design should
maintain separation of business and UI logic.
