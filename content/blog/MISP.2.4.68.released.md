---
title: MISP 2.4.68 released
date: 2017-03-08
layout: post
banner: /img/blog/misp-small.png
---

A new version of MISP [2.4.68](https://github.com/MISP/MISP/tree/v2.4.68) has been released including multiple bug fixes and improvements.

Improvements and features added:

- Enable sync permissions for read-only accounts.
- Upload org logo can now be performed via the org edit/view interface.
- An option to disable cached export has been added for low disk space servers.

Blacklisting of deleted events is now enabled by default. This feature existed before but was not enabled by default. This feature allows MISP users to
ensure that deleted events never propagate back to their instance. The blacklist can easily be managed from the MISP interface. As this
feature is a default behaviour that a large majority of the MISP community needs, we have decided to enable this feature by default starting from version 2.4.68.

Many bugs were fixed in this release, including a specific speed improvement in the event deletion process.

For the ongoing work on [misp-objects](https://github.com/MISP/misp-objects), a new float type has been added to support additional composite objects.
We welcome contributions to the misp-objects' design and any ideas helping us to ensure that a consistent set of objects are ready for the next release.

The full change log is available [here](https://www.misp.software/Changelog.txt).

Don't hesitate to [open an issue](https://github.com/MISP/MISP/issues) if you have any feedback, found a bug or want to propose new features.
