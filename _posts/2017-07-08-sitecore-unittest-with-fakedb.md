---
layout: post
title: Sitecore UnitTest with FakeDb
tags:
  - sitecore
  - unit test
comments: true
---

![_config.yml]({{ site.baseurl }}/images/sitecore.png)
When you are working on the CMS solution, the solution design and architecture can be very different, that caused writing and maintaining the uint tests be even more difficult than bespoke solution.

A typical example of this is at some point your code calls the Sitecore API, how do you ensure your code is working when the code has related to external dependencies that you can’t remove?

Thanks for Sitecore FakeDb, it makes that happen and a lot simpler to write the unit tests on this CMS plateform. In the following sections, I will assume you are a Sitecore developer with passion of writing the unit tests.


## Dependencies

In order to use FakeDb for the unit tests, you need the following dlls within your Tests project

1. Sitecore.FakeDb – You can install this via the nuget package
2. Lucene.Net
3. Sitecore.Analytics
4. Sitecore.Kernel
5. Sitecore.Logging
6. Sitecore.Nexus


> NOTES: All above Sitecore related packages can be either reference from dll or via Sitecore nuget server.


Lastly, you also need to copy your Sitecore license.xml file into the root of your Test project.

> NOTE: When you install the Sitecore.FakeDb package, it will automatically update the app.config file by including the license file location (see screenshot below

![_config.yml]({{ site.baseurl }}/images/sitecorefakedb/2017-06-07_23-40-43.png)

## Sample Test (MSTest) 

![_config.yml]({{ site.baseurl }}/images/sitecorefakedb/2017-06-08_00-58-22.png)

## NCrunch Configuration

In order to run unit tests with [NCrunch](https://www.ncrunch.net), in the NCrunch Configuration window, select the tests project and configure the following settings:


![_config.yml]({{ site.baseurl }}/images/sitecorefakedb/2017-06-06_23-11-40.png)

## References


NCrunch

https://github.com/sergeyshushlyapin/Sitecore.FakeDb/wiki/Configuration

AutoFixture with Sitecore.FakeDb

https://github.com/sergeyshushlyapin/Sitecore.FakeDb/wiki/AutoFixture-Samples



