---
title: MISP 2.4.117 released (aka the the pre-conference season release)
date: 2019-10-11
layout: post
banner: /img/blog/decay.png
---

# MISP 2.4.117 released

A new version of MISP ([2.4.117](https://github.com/MISP/MISP/tree/v2.4.117)) has been release including major performance improvements in MISP and PyMISP, publish filter emails, throttling restSearch (very useful when you want to limit some users using the API of your MISP instance) and many more improvements.

## New feature publish filters

As port of the cyber-exchange programme, one of the participants - Armins Palms - gave us a great idea for an improvement that has been long overdue. Users now have the possibility to create filter rules for the publish alert e-mails. One of the biggest hurdles for efficiently using MISP's alert system was that it could become quite verbose - if you are only interested in certain topics then receiving an alert about anything that gets published can easily cause alert-fatigue. Using the new system you can accurately configure MISP's behaviour when it comes to alerting you based on your own preferences. The system allows to restrict alert messages by tags and publishing organisation using a nested boolean tree of settings, allowing for complex rule systems.

## New feature user settings

One of the hurdles that has stopped us from implementing the above feature was the lack of a per user setting system. All configuration options in MISP have been based on system-wide, organisation-wide or role-based configurations. With the new user setting system, we have a simple but flexible tool to start adding more and more user level configurations.

## IPSum feeds

Another outcome of the cyber-exchange programme, thanks @stamparm we now have the different level IPsum feeds pre-configured in the default feed list.

## Performance improvements

We have identified and resolved several massive performance blockers in MISP. The issue reared its ugly head once larger, more object-heavy events started being shared, with some bringing even well provisioned servers to their knees. We have seen a rather drastic drop in CPU usage after applying the patch, resulting in our main sharing community's server dropping to about 20% of its previous CPU usage. We highly advise everyone to upgrade their MISP instances ASAP.

## PyMISP performance improvements

Similarly to the above fix, PyMISP was also suffering from performance issues in regards to massive events which have been addressed in the latest release, which includes a performance-oriented rework of the internals. Not only are we seeing a 50% cut in execution times when interacting with large events, but more importantly, the memory usage has been slashed to as little as ~5% of the usual numbers we've seen before the patch. It is therefore highly advised for anyone using PyMISP to upgrade to this release ASAP.

## Throttling restSearch

If you are running a larger community MISP instance, one of the biggest hurdles for coping with your community's resource requirements is organisations using your heavily used MISP instance as the backend for their internal querying. Not only does this put a potentially unmaintainable level of stress on your instance when it comes to large and active communities, it also encourages bad practices in regards to information disclosures via the executed queries themselves (more information regarding this can be found in our previous blog entry regarding the [benefits of running your own MISP instance](https://misp-project.org/2019/09/25/hostev-vs-own-misp.html)).

We have added a set of new options for administrators configuring user roles - it is now possible to enforce rate limits on API users. The setting controls how many heavy search-related queries users can execute within a 15 minute time-frame. The setting is completely optional per role and users are notified about their current quotas, reset times and remaining queries via headers in each request. The only endpoints affected currently are /events/restSearch and /attributes/restSearch, but we may extend this over time with other endpoints.

## Using custom CA bundles

MISP comes with CakePHP's default included CA bundle, which is based on the mozilla CA bundle. This can get rather stale, with the currently included bundle being several years old. Thanks to the contriution of @JakubOnderka, it is now possible to override the default bundle with a custom one.

## Redis diagnostics

The diagnostics page of MISP offers a wide range of tools to diagnose misconfigurations and issues that might arise with the instance, however, one aspect that was missing an easy way to diagnose was the redis configuration. Thanks to @JakubOnderka's new tool this can now be diagnosed directly from the UI.

## Various other improvements

Other improvements include a large list of general bug fixes, affecting UI and API users alike, an internal rework of the authentication workflow thanks to all the work of Andreas Rammhold in preparation for the merge of the LinOTP authentication module, various improvements to the STIX export, a new Netfilter export system and a host of other improvements.

# Acknowledgement

We would like to thank all the [contributors](/contributors), reporters and users who have helped us in the past months to improve MISP and information sharing at large. Special thanks to Jakub Onderka for the continuous stream of excellent improvements, Andreas Rammhold for making the AppController much more sane, the participants of the cyber-exchange programme for helping us improve MISP in all sorts of different ways.

As always, a detailed and [complete changelog is available](/Changelog.txt) with all the fixes, changes and improvements.

