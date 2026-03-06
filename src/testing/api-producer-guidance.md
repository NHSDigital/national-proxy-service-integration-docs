---
layout: default
title: API producer guidance
---

## Scope

Internal functional and non-functional testing of your service is outside the scope of this guidance. The below guidance is specifically orientated around the proxy use case and how to assure the [core requirements of enabling proxy access]({{ '/patient-facing-journeys/api-producer-guidance/#core-requirements' | url }}).

## Mocking access tokens

The API Management platform supports the mocking of both NHS login and CIS2 access tokens. The mock authorisation service also supports the generation of an access token for a proxy. This will enable you to generate access tokens to simulate the following scenarios:

- a user accessing services for themselves (NHS login, user-restricted)
- a user accessing services for a patient they care for (NHS login, user-restricted, delegated access)
- a clinical user accessing service (CIS2)

Detailed documentation for this can be found on their [Testing APIs with our mock authorisation service](https://digital.nhs.uk/developer/guides-and-documentation/security-and-authorisation/testing-apis-with-our-mock-authorisation-service#second-generation-service) page.

## Core test scenarios to assure

The below scenarios cover core behaviour of your API that you should ensure re tested for. This is not intended to be a complete list, and it is expected that your testing will involve a broader set of functional unit, component and integrations tests as needed.

| Scenario                                                                                                                | Expected outcome                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Any patient identifier in the URL route or query string matches the `sub` claim in the access token (if applicable).    | Request is successful                                                                                                                                                                                                                                    |
| Patient identifier in the URL route or query string does NOT match the `sub` claim in the access token (if applicable). | Request is rejected with a 401 response                                                                                                                                                                                                                  |
| Proxy's granted permissions are respected (if applicable).                                                              | The logged in user cannot perform operations that they don't have permission to perform on behalf of the patient                                                                                                                                         |
| Correct patient data is displayed                                                                                       | The selected patient's data is displayed rather than the logged in user's                                                                                                                                                                                |
| Correct patient record is updated when performing a transaction                                                         | When making a transactional request to GPC PFS, the update is applied to the correct record                                                                                                                                                              |
| Audit is correctly captured                                                                                             | When a request is made by proxy (delegated access) the clinical system correctly audits the fact that the action was completed by the logged in user on behalf of the patient i.e. captures both the user's NHS number (`act`) and the patient's (`sub`) |
| Assert correct behaviour of existing use cases                                                                          | APIs behaviour exhibits no regressions when using standard access token for the logged in user (patient access)                                                                                                                                          |
