---
title: MISP 2.4.88 released (aka Fuzzy hashing correlation, STIX 1.1 import and many API improvements)
date: 2018-02-21
layout: post
banner: /img/blog/misp-small.png
---

A new version of MISP [2.4.88](https://github.com/MISP/MISP/tree/v2.4.88) has been released including fuzzy hashing correlation (ssdeep), STIX 1.1 import functionality, various API improvements and many bug fixes

Fuzzy hashing (e.g ssdeep or tlsh) is a commonly used technique used to classify malware, binaries or even text. The MISP correlation engine has always been supporting a simple yet powerful matchinging algorithm to find similar attributes. After an training insightful session in Austria with Manfred Kaiser working at bmlv.gv.at and based on the previous work of [Brian Wallace](https://github.com/bwall) on ssdeep clustering, MISP 2.4.88 introduces the ability to correlate similar binaries (or just their values) using fuzzy hashing via ssdeep. In addition to the standard and advanced correlation algorithms (e.g. CDIR block matching) in MISP, fuzzy hashing correlation allows the matching of similarities among a set of binaries. The installation of the feature is described in the [README.install](https://github.com/MISP/MISP/blob/2.4/INSTALL/INSTALL.ubuntu1604.txt#L316) and don't forget to set the correlation threshold for ssdeep in MISP serverSetttings (e.g. MISP.ssdeep_correlation_threshold).

As of 2.4.88, MISP supports STIX 1.1.1 XML import from the user-interface similarly to how MISP JSON format data is used to create new events. We hope this will help users to import existing threat intelligence from other sources and benefit from the MISP standard format functionality. If you have any issues with import functionalities feel free to [send us sample STIX 1.1.1 files](/who/#contact).

The workflow for merging organisations has been improved to make it more intuitive for the administrators of the MISP instance.

The freetext import (the functionality to pass raw text to MISP and automatically detect indicators) API has been improved and it can now by used to return the raw parsing data instead of creating the attributes.

Keyboard shortcuts have been added application-wide in MISP to allow easier navigation for the analysts.

API to manage sharing groups has been updated and it's now extremely flexible to update sharing groups:

~~~
  - added functions to manage the additions/removals of objects from sharing groups
  - the following APIs are included:
    - /sharingGroups/addOrg/[sg_id]/[org_id]/[extend]
    - /sharingGroups/removeOrg/[sg_id]/[org_id]
    - /sharingGroups/addServer/[sg_id]/[server_id]/[all_orgs]
    - /sharingGroups/removeServer/[sg_id]/[server_id]

  - All parameters are optional and can instead be passed as JSON objects such as:

    {
      "org_uuid": "55f6ea5e-2c60-40e5-964f-47a8950d210f",
      "sg_id": "49",
      "extend": 1
    }

  - The API is extremely flexible with how to name objects, the following parameters are allowed:
    - Organisations:
      - org_id (The organisation's local instance ID)
      - org_uuid (The organisation's global UUID)
      - org_name (The organisation's identifier as known to the curent instance)
    - Server:
      - server_id (The server's local instance ID)
      - server_url (The URL of the server)
      - server_name (The local name of the server as assigned when adding the server)

  The sharing groups can also be addressed by ID or UUID.
~~~

[MISP modules](https://github.com/MISP/misp-modules) are now accessible from MISP API and allow MISP users to use the MISP modules from the API in addition to the user-interface.

Multiple bugs were also fixed and especially a security bug [CVE-2018-6926](https://cve.circl.lu/cve/CVE-2018-6926).

We would like to thank all the contributors who helped to fix bugs, contributed new features or support us to release this version.

MISP [galaxy](/galaxy.pdf), [objects](/objects.pdf) and [taxonomies](/taxonomies.pdf) were notably extended by many contributors. These are also included by default in MISP. Don't forget to do a `git submodule u
pdate` and update galaxies, objects and taxonomies via the UI.

MISP trainings are foreseen the 27/03 and 28/03 in Luxembourg including a full-day API and extension hands-on session. [For more information and registration](https://www.circl.lu/services/misp-training-materials/). We are also participating to the [Open Source Security Software Hackathon](https://hackathon.hack.lu/) which takes place the 26 March 2018 in Luxembourg.
