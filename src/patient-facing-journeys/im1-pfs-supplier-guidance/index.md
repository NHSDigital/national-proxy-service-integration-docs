---
layout: default
title: IM1 PFS supplier guidance
---

{% from "image-pop-out.njk" import imagePopOut %}

## Background

Proxy's (parents and carers) cannot currently access digital health services for Patients who are registered at a different GP practice in an auditable way via the NHS app. This means that an estimated 2.65 million carers are unable to access services on behalf of the people they care for.

Historically there have been local processes in GP practices that have lead to:

- Unsafe workarounds: GP practices create "unofficial accounts" for Proxy's. These accounts are not linked to an NHS number, are not traceable, and fall outside normal safeguarding/management processes.
- Inconsistent processes: Proxy relationships are created in silos, leading to inconsistent checks, and a lack of visibility across different care settings.

### Constraint

The reason that this is the case is that IM1 interfaces (how the NHS app interacts with primary care services offered by EMIS/Optum and TPP) only allow patients to access services at their own GP practice. Credentials are supplier-specific and without an NHS number for the proxy the NHS App cannot support cross-practice proxy access.

There is also no integrated means for GPs to contact another GP practice to carry out safeguarding checks when granting or managing access over time. This introduces further risk and potential delays to the setup of access.

### Current architecture

{{ imagePopOut('/assets/images/current_im1_architecture.png' | url, 'Current IM1 Architecture') }}

## Enabling cross-practice proxy access

The proxy programme have set out to solve this but in a way that does not affect existing IM1 interfaces i.e. minimising the impact on suppliers and patient-facing applications.

The key enabler being an new IM1 PFS Auth service that suppliers and patient facing apps integrate with. This will perform two key functions

1. Authenticate users using NHS login tokens (replacing the need for IM1 proprietary credentials)
1. Act as forward proxy, determining which supplier system to forward the request to (based on the patient's ODS code)

### Pre-requisites

It is expected that the NHS app will be able to generate a proxy access token; [read more about this here]({{ '/patient-facing-journeys/enable-proxy-access-to-services' }}).

In addition to the changes in the NHS app, the implementation approach relies on the following pre-requisites being met in the GP system:

- The proxy role MUST have been created in the GPIT system and local permissions granted.
- There MUST always be a patient record for the patient held in their GP practice’s GPIT system​.
- There MAY be a patient record for the proxy if they are also under the care of the same GP practice​.
- There MUST always be an online account in the GPIT system for the proxy​ and the online account MUST be bound to an NHS number​ (if an online account doesn't exist, it should be created at the point of creating the proxy role​). If the proxy is not under the care of the same GP practice as the patient then an online
  account should be created; noting that there will not be patient record for the proxy​.
- There MAY be an online account for the patient if they have online access for themselves, but this is not
  required for them to be supported by a proxy​.
- The proxy role in the national proxy service (VRS) MUST have been created, and is `active`​

This broadly aligns with the following data local data model:

{{ imagePopOut('/assets/images/logical_local_data_model.png' | url, 'Logical local data model') }}

The below diagram illustrates the logical architecture at a high level. The key thing to point out is that this approach enables a session to be established at the patient's GP practice securely without the logged-in user needing to be a registered patient, and no changes are required to existing IM1 interfaces.

{{ imagePopOut('/assets/images/high_level_im1_auth.png' | url, 'IM1 Auth Architecture') }}

## Supplier-specific guidance

- [Optum (EMIS) Guidance]({{ '/patient-facing-journeys/im1-pfs-supplier-guidance/optum-guidance' | url }})
- [TPP Guidance]({{ '/patient-facing-journeys/im1-pfs-supplier-guidance/tpp-guidance' | url }})
