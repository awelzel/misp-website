---
title: MISP 2.4.119 released (aka the quality of life release)
layout: post
banner: /img/blog/119-1.png
date: 2019-12-04
---

# MISP 2.4.119 released

A new version of MISP ([2.4.119](https://github.com/MISP/MISP/tree/v2.4.119)) has been released, including several functionalities that should make the operation of a MISP instance more convenient.

# Vulnerability CVE-2019-19379 has been fixed

In app/Controller/TagsController.php in MISP 2.4.118, users can bypass intended restrictions on tagging data. The vulnerability has been fixed in 2.4.119 and assigned the following [CVE-2019-19379](https://cve.circl.lu/cve/CVE-2019-19379). We strongly recommend to update to this version. Thanks to Christophe Vandeplas for the reporting.

# Database diagnostics

There is a new sub-system in the diagnostics tool that will compare the current state of your MISP database to the reference db schema, highlighting potential issues / divergences. Keep in mind, not all issues are necessarily cause for concern, but generally it is recommended to fix the issues that are deemed critical. If you have doubts about why your DB looks different from what is expected, feel free to open up a github issue and we'll try to point you in the right direction.

On top of flagging diverging traits of your DB compared to the reference, the system also allows users to generate SQL queries that would rectify the potential issues. Please make sure that you back your database up before running the suggested queries and keep in mind that altering existing tables with high volumes of data can temporarily double the disk space requirements of the given table along with taking a long amount of time (especially true for large log, correlation and sighting tables).

# Improved timestamp filtering in MISP

attribute_timestamp flag added to attributes/restSearch. Now 4 different timestamp filters exist in MISP and can be used. An explanation of the 4 timestamp filters:

- timestamp: Filters on attribute AND event timestamp
- event_timestamp: Filters on event timestamp
- attribute_timestamp: Filters on attribute timestamp
- publish_timestamp: Filters on event.publish_timestamp

# API deprecation

The preparations for MISPs large refactor are well underway, this time we've added a new system that will start tracking deprecated endpoints in MISP and warning users of their state. The new system has the following functionalities:

- an internal list of deprecated endpoints is maintained
- any query against these endpoints increments a counter in redis
- if the deprecation is a confirmed hard deprecation, the user is warned via response headers (API) or flash messages (UI)
- for soft deprecations, we are collecting the information (locally on the instance only, it is up to the administrators to share the outcome with us on demand, outside of MISP, nothing is sent back automatically) on certain endpoints that we might consider deprecating based on usage. We are monitoring our instances to see if there's an interest to keep these features around - if you would like to submit your community's usage of these endpoints, reach out to us!

To view the results of the collection, just navigate to the diagnostics page.

# Export API refactor

All of the deprecated export APIs (such as /events/hids export, /events/stix or /events/xml) have been refactored and are using restSearch under the hood now. Nothing should change from a user perspective except for a size-able gain in peformance thanks to all of the restSearch optimisations.

If you do notice some of your legacy scripts misbehaving, please open a github issue and describe what went wrong.

# Sighting synchronisation

Sightings are now synchronising much more reliably, with a new sighting push setting being added to the server connection and a new publish sighting button being available for users with sighting rights on the event view.

# misp-modules version 2.4.119

MISP modules have been improved and many new modules were added in [expansion](http://misp.github.io/misp-modules/expansion/), [export](http://misp.github.io/misp-modules/export_mod/) and [import](http://misp.github.io/misp-modules/import_mod/). Don't forget to update the modules to benefit from the improvements and new features.

# Acknowledgement

We would like to thank all the [contributors](/contributors), reporters and users who have helped us in the past months to improve MISP and information sharing at large.

As always, a detailed and [complete changelog is available](/Changelog.txt) with all the fixes, changes and improvements.

