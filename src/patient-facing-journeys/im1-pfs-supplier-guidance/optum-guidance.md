---
layout: default
title: Optum guidance
---

{% from "image-pop-out.njk" import imagePopOut %}

## High-level architecture

{{ imagePopOut('/assets/images/high_level_im1_auth.png' | url, 'IM1 Auth Architecture') }}

<div class="nhsuk-inset-text">
  <h3>MTLS certificates</p>
  <p>
    It is highly recommended that a certificate pair is generated explicitly to secure this connection in order to reduce the impact of a compromised certificate if used across multiple services.
  </p>
</div>

<div class="nhsuk-warning-callout">
  <h3 class="nhsuk-warning-callout__label">
    <span role="text">
      <span class="nhsuk-u-visually-hidden">Important: </span>
        Important
      </span>
  </h3>
  <p>
    IM1 PFS Auth provides a layer of authentication, verifying the NHS login access token provided in the request from the client application. Therefore, direct requests to the Optum IM1 PFS API implementation should be rejected, only requests that have a successful MTLS handshake having come through the IM1 PFS Auth proxy should be accepted.
  </p>
</div>

## Detailed Logical Architecture

{{ imagePopOut('/assets/images/optum_im1_auth_logical_architecture.png' | url, 'Optum IM1 Auth Logical Architecture') }}

## Open API Specification (OAS)

The API specification below pertains to the new IM1 PFS endpoint to be implemented by Optum (the interface identified by the blue star in the diagram above). It is the API endpoint that the IM1 PFS Auth API-M proxy will forward requests to.

### Key points to note

Whilst this endpoint supports cross-practice proxy access for IM1, it could also support the establishment of a session for both a standard logged-in user (i.e. user identifier and patient identifier are the same in the request). For proxy use cases, a request may have a user identifier and patient identifier (for a specific user and patient) OR just specify the user identifier to initiate a session and obtain details of all patients they can access service for.

This ultimately means that the endpoint will be able to support:

1. Create a session for a patient using an NHS login token. This is similar to the the existing `POST /sessions` endpoint, but in addition return the services the user can access, and any patients they can access services for
1. Create a session for a person with an online account but no patient record using an NHS login token. By prescribing a different patient to the user in the request, the response should contain the new session details and the services the user can access for the specified patient

#### [Download the Open API specification]({{ '/assets/specs/optum_im1_pfs_auth_oas_0.3.json'  | url }})
