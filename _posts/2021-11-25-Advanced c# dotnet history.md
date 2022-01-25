---
layout:     post
title:      2021-11-25-c# dotnet history
subtitle:   Advanced topics on c#
date:       2021-11-25
author:     BY HY
header-img: img/post-bg-csharp-dotnet.png
catalog: true
tags:
    - c#
    - Advanced Topics
---
# .Net Framework, Mono and .Net Core

## .Net Schedule

| -         | -             | -                         |
| --------- | ------------- | ------------------------- |
| July 2019 | .Net Core 3.0 | RC- release candidate     |
| Sept 2019 | .Net Core 3.0 | GA - general availability |
| Nov 2019  | .Net Core 3.1 | LTS(long Term support)    |
| Nov 2020  | .Net Core 5.0 | GA                        |
| Nov 2021  | .Net Core 6.0 | LTS                       |
| Nov 2022  | .Net Core 7.0 | GA                        |
| Nov 2023  | .Net Core 8.0 | LTS                       |

* .Net Core 3.0 release in September
* .Net Core 3.1 = Long Term Support (LTS)
* .Net 5.0 release in November 2020
* Major releases every year, LTS for even numbered releases
* Predictable schedule, minor releases if needed

### [Software Release Life Cycle](https://en.wikipedia.org/wiki/Software_release_life_cycle)

* pre-alpha, aka, development releases/nightly builds

  Pre-alpha refers to all activities performed during the software project before formal testing. These activities can include [requirements analysis](https://en.wikipedia.org/wiki/Requirements_analysis), [software design](https://en.wikipedia.org/wiki/Software_design), [software development](https://en.wikipedia.org/wiki/Software_development), and [unit testing](https://en.wikipedia.org/wiki/Unit_testing).

* Alpha

  The alpha phase of the release life cycle is the first phase of [software testing](https://en.wikipedia.org/wiki/Software_testing). In this phase, developers generally test the software using [white-box techniques](https://en.wikipedia.org/wiki/White-box_testing). Additional validation is then performed using [black-box](https://en.wikipedia.org/wiki/Black-box_testing) or [gray-box](https://en.wikipedia.org/wiki/Grey_box_testing#Grey_box_testing) techniques, by another testing team. Moving to black-box testing inside the organization is known as *alpha release*.

* **Beta**

  It is the software development phase following alpha. Software in the beta stage is also known as *betaware*. A beta phase generally begins when the software is feature complete but likely to contain a number of known or unknown bugs. Software in the beta phase will generally have many more bugs in it than completed software and speed or performance issues, and may still cause crashes or data loss. The focus of beta testing is reducing impacts to users, often incorporating [usability testing](https://en.wikipedia.org/wiki/Usability_testing). 

  The process of delivering a beta version to the users is called *beta release* and is typically the first time that the software is available outside of the organization that developed it. Beta version software is often useful for demonstrations and previews within an organization and to prospective customers. 

* **Release Candidate (RC)**, aka, gamma/delta (going silver)

  It is a beta version with potential to be a stable product, which is ready to release unless significant bugs emerge. A release is called *code complete* when the development team agrees that no entirely new source code will be added to this release. There could still be source code changes to fix defects, changes to documentation and data files, and peripheral code for test cases or utilities.

  * Stable Release, aka, production release

    It is the last *release candidate* (*RC*) which has passed all verifications / tests. The remaining bugs are considered as acceptable. Some domains (for example, [Linux distributions](https://en.wikipedia.org/wiki/Linux_distribution)), have two types of stable releases: normal, or stable releases and **long-term support (LTS)** releases which are maintained for a longer period of time.

* RTM(Release to Manufacturing), aka, release to Marketing

  It is a term used when a software product is ready to be delivered. This build may be [digitally signed](https://en.wikipedia.org/wiki/Code_signing), allowing the end user to verify the integrity and authenticity of the software purchase. RTM precedes general availability (GA) when the product is released to the public. A golden master build (GM) is typically the final build of a piece of software in the beta stages for developers. 

* **General Availability (GA)**

  It is the marketing stage at which all necessary [commercialization](https://en.wikipedia.org/wiki/Commercialization) activities have been completed and a software product is available for purchase, depending, however, on language, region, electronic vs. media availability.

* Production/Live release, aka, gold



![image-20211126151309681](C:\Users\103232\AppData\Roaming\Typora\typora-user-images\image-20211126151309681.png)

CLR - Common Language Runtime

![image-20211126151338684](C:\Users\103232\AppData\Roaming\Typora\typora-user-images\image-20211126151338684.png)

