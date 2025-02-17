---
title: MISP 2.4.85 released (aka feeds and warning-lists improvement and more)
date: 2017-12-22
layout: post
banner: /img/blog/misp-small.png
---

A new version of MISP [2.4.85](https://github.com/MISP/MISP/tree/v2.4.85) has been released including improvements to the feed ingestion performance, warning-list handling and many bug fixes.

Warning-lists can now be used for filtering out import when using the API via /attributes/add either pass the url param `/enforceWarninglist:1` or set the `"enforceWarninglist":1` key on individual attributes to be checked.

Warning-lists performance is improved especially on the ingestion, the deletion of the warning-lists can be done from the UI and very large warning-lists are now properly updated even on MySQL instances configured with conservative maximum packet sizes.

Feed quick sync is now part of MISP allowing the calling of attributes using the precalculated hashes without having to parse the complete feed. We strongly recommend
feed providers to use the [latest feed generator](https://github.com/MISP/PyMISP/commit/195cd6d7fc305ac6628ed8f2ff762b3f69a9b6ca) in PyMISP to benefit from the quick sync.

Tags can now be restricted to a single user (in addition to the existing restrictions per organisation). This can help to
support analyst workflows where a certain type of user can tag or classify in an organisation.

Auth keys of users can now be reset from the command line by using `/var/www/MISP/app/Console/cake Authkey [email@of.user]`.

Improvement and cleanup in the event index:

- removed threat level and analysis from the index as they're eclipsed by the taxonomies for most use-cases
- changed the behaviour when users click on org logoes (redirect to filtered index)

Various UI improvements to clean up the interface for the analysts, including changes such as the collapse of attributes with highly correlating events:

![collapse of correlation](/img/blog/collapse.png "{class='img-responsive'}")

The advanced sighting view on objects is now properly working.

New attribute types were introduced in MISP in order to improve the support of new or improved objects:

- x509-fingerprint-sha256 - to support the updated [x509 object](/objects.html#_x509)
- x509-fingerprint-md5 - to support the updated [x509 object](/objects.html#_x509)
- stix2-pattern - to a new [stix2-pattern object](/objects.html#_stix2_pattern)
- whois-registrant-org - to support the updated [whois object](/objects.html#_whois)

The STIX 2.0 export had undergone significant improvements to support the full mapping between the MISP and STIX 2.0 standards.
If a mapping is not supported in the STIX 2.0 standard, we also export custom objects to allow organisations to still receive
These often crucial pieces of MISP information  in the STIX export. The basic logic for STIX 2.0 import has been implemented for it to make it's debut in
the next release.

Many bug fixes and improvement were introduced in this version.

The full change log is available [here](https://www.misp.software/Changelog.txt). [PyMISP change log](https://www.misp.software/PyMISP-Changelog.txt) is also available.

PyMISP has been also updated, boasting a more clever approach to timestamp handling while updating MISP JSON files. The PyMISP documentation has been updated [PDF](https://media.readthedocs.org/pdf/pymisp/latest/pymisp.pdf).

MISP [galaxy](/galaxy.pdf), [objects](/objects.pdf) and [taxonomies](/taxonomies.pdf) were notably extended by many contributors. These are also included by default in MISP. Don't forget to do a `git submodule update` and update galaxies, objects and taxonomies via the UI.

New MISP trainings are foreseen the 17/01 and 18/01 in Luxembourg including a full-day API and extension hands-on session. [For more information and registration](https://www.circl.lu/services/misp-training-materials/). We have also many other trainings and events foreseen in 2018, [for more information](/events/)

