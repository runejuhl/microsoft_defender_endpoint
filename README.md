`atea.service.microsoft_defender_endpoint`
=========

Ansible role for deploying, onboarding and configuring Microsoft Defender for
Endpoint for Linux.

Requirements
------------

This role requires an onboarding script (containing a JSON blob), or the JSON
file itself.

If using the onboarding script you can simply edit the script to print the JSON
blob as text (to avoid any escape sequences due to the text being embedded in
Python), or change the `destfile` path and remove any lines referencing `sudo`
before running the script.

Role Variables
--------------

The only required variable is `microsoft_mde_onboarding_blob`. See "Example
Playbook" for an example.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Minimal configuration:

``` yaml
---
- become: true
  hosts: all
  roles:
    - role: atea.service.microsoft_defender_endpoint
      vars:
        microsoft_mde_onboarding_blob:
          "onboardingInfo": "{\"body\":\"{\\\"previousOrgIds\\\":[],\\\"orgId\\\":\\\"..."
```

Extended configuration with custom configuration:

``` yaml
---
- become: true
  hosts: all
  roles:
    - role: atea.service.microsoft_defender_endpoint
      vars:
        microsoft_mde_config_custom:
          antivirusEngine:
            enforcementLevel: 'passive'
            enableFileHashComputation: true
          cloudService:
            cloudBlockLevel: 'zero_tolerance'
            automaticSampleSubmissionConsent: 'none'

        microsoft_mde_onboarding_blob:
          "onboardingInfo": "{\"body\":\"{\\\"previousOrgIds\\\":[],\\\"orgId\\\":\\\"..."
```

Note that all possible configuration variables (according to the [Microsoft Defender
for Endpoint for Linux documentation](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/linux-preferences)) have been documented in the role. See the complete role documentation with the following command:

``` sh
ansible-doc -t role atea.service.microsoft_defender_endpoint
```

License
-------

GNU Affero General Public License v3.0 or later

Author Information
------------------

Created in scenic Scandinavia by Atea Open Source.
