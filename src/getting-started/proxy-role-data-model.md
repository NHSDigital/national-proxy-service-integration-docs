---
layout: default
title: Proxy role data model
---

{######## Declare imports #########}
{% from "image-pop-out.njk" import imagePopOut %}

## Logical national data model

The _target_ logical data model for a proxy role - as far as national services is concerned - is illustrated below.

{{ imagePopOut('/assets/images/logical_national_data_model.png' | url, 'Logical national data model') }}

## Logical local data model

The below logical data model describes the relationship between patient records, online accounts and permissions. This captures the expected conceptual entity relations that will be needed in a clinical system to support the set-up of proxy access.

{{ imagePopOut('/assets/images/logical_local_data_model.png' | url, 'Logical national data model') }}

<div class="nhsuk-inset-text">
  <p>A proxy will have a patient record if they are registered at the same practice as the patient.</p>
  <p>
    Where a proxy relationship exists for a patient and the proxy is registered t a different practice, it is expected that the proxy will have an online account and permissions and is associated with an NHS number of the proxy in order to ensure appropriate audit.
  </p>
</div>
