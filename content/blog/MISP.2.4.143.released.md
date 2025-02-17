---
title: MISP 2.4.143 released (10 year anniversary edition)
date: 2021-05-15
layout: post
banner: /img/blog/misp-sea.png
---

# MISP 2.4.143 released

MISP 2.4.143 released including a new audit subsystem, various quality of life improvements and bug fixes.

# 10 year anniversary

[MISP has, as of the 15th of May, turned 10,](https://twitter.com/MISPProject/status/1393141380369821697) to celebrate the occasion we have a celebratory MISP logo acting as a temporary replacement of the usual one for the duration of this release.

It has been a long road since Christophe Vandeplas released the initial version of CyDefsig (later renamed to MISP) in 2011. We would hereby like to thank all contributors and supporters for making MISP what it is today. Looking back at how the tooling and the communities evolved over the decade, we can see how threats and threat intelligence has changed and evolved over the years, molding the platform in the process. Here's to at least another 10 years of active sharing and bringing communities together!

# New audit system

Thanks to @JakubOnderka, we now have a whole new audit system, storing relevant audit logs in a more concise yet easily machine-parsable way (all changes will be logged as JSON objects). This feature is disabled by default and needs to be enabled in the server settings, though keep in mind that it will not convert existing entries. Especially for new instances, we highly recommend switching to the new system!

# Event republish-alert flood protection

As our communities grow and we all build our own internal tooling for processing data in MISP, the more likely it is to run into some slightly frustrating issues. One such issue we've encountered recently came from a tool that seems to have regularly (and frequently!) modified certain events and republished them consecutively. This in itself is not an issue, however, it can generate a lot of noise in terms of alert emails. We have now added a protective measure to counter this, make sure you have a look at the appropriate settings to create lockout timers for alerts that can be issued for a single event.

# Improvements

- Event report hints autocomplete while typing in the Markdown has been improved
- Server rules element improved
- MISP modules results now point to the original object itself

# MISP Modules

Two new MISP modules were introduced:

- cof2misp module to allow the import of Passive DNS in [JSON COF Format](https://tools.ietf.org/id/draft-dulaunoy-dnsop-passive-dns-cof-08.html) into MISP
- An improved [onyphe module](https://github.com/MISP/misp-modules/blob/main/misp_modules/modules/expansion/onyphe.py) to do expansion in MISP with full MISP object support

# Acknowledgement

We would like to thank all the [contributors](/contributors), reporters and users who have helped us in the past months to improve MISP and information sharing at large. This release includes multiple updates in [misp-objects](/objects.html), [misp-taxonomies](/taxonomies.html) and [misp-galaxy](/galaxy.html)
.

As always, a detailed and [complete changelog is available](/Changelog.txt) with all the fixes, changes and improvements.

