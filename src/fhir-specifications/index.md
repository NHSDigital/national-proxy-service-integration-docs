---
layout: default
title: FHIR specifications overview
---

{######## Declare imports #########}
{% from "image-pop-out.njk" import imagePopOut %}

This section provides an overview of how the National Proxy Service constructs FHIR resources and how integrating partners should interpret them.

All FHIR resources conform to the [UK Core FHIR standard](https://simplifier.net/hl7fhirukcorer4). This guide serves as a complementary reference to help interpret how those standards are applied within the context of the National Proxy Service.

## FHIR Resources

The National Proxy Service leverages the following FHIR resources:

| Resource type           | Description                                                                                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Consent`               | The primary representation of the proxy role, identifiers of the proxy and patient, the legal basis on which the role is founded and the current status |
| `QuestionnaireResponse` | Access request details captured from a user applying for proxy access or nominating a proxy.                                                            |
| `Patient`               | A patient pr or proxy's demographics                                                                                                                    |
| `RelatedPerson`         | A uni-directional real world relationship between two people.                                                                                           |

## Primary care data flow

{{ imagePopOut('/assets/images/primary_care_dataflow.png' | url, 'Primary care dataflow diagram') }}
