# Documentation gaps

The below is a list of docs that have currently not been created / completed, but this repo should be treated as living documentation and added to as n when a need arises to support integrators

## Unfinished

`/patient-facing-journeys/nhs-app-guidance`

- General overview of how to enable proxy journeys in the nhs app, the capabilities that are in place (i.e. listing who the use can manage service for, profile switching etc.) DONE
- Explanation of the Auth package and how it can be leveraged to deal with token exchange so product teams can focus on delivering the user journey (DEPENDENT ON AUTH PACKAGE BEING BUILT in NHS App)

---

`/clinical-workflows/migrating-roles/`

- How suppliers should identify records to migrate. Mandatory requirements such as both parties needing to have an NHS number
- Call out guidance on NOT migrating proxies without an NHS number (Care home use case and cross-practice proxy's set up with fake patient records)
- Assurance process to test the migration in PTL environment
- Steps to follow for migration & cut-over
- Any technical guidance to inform what a created role MUST have to supplement the FHIR spec

## New

`testing` section pages

- user data for test cases
- other supporting docs to aid testing and assurance of our endpoints (without duplicating what's on our catalogue pages)

---

`fhir-specifications` section pages

Here we want any documentation that isn't obvious through our spec's alone.

Consider documentation approach akin to health checks docs (although avoid duplicating what should already be evident in the API spec):

https://nhsdigital.github.io/digital-health-checks-public/fhir-bundle-descriptions/overview/

- Consent - status code -> status code reason mapping (which status code reasons are valid for which status')
