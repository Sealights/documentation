# Automated Tests

## Overview

Automated tests are executed using software tools and scripts without manual intervention, providing efficient and repeatable verification of software functionality. By integrating Sealights into your automated tests framework, you will be able to see code coverage and test recommendations.

## Integration Types

There are three Integration Types in Sealights:

1. **Coverage Only Integration -** Allows seeing code coverage for a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for a single <mark style="color:orange;">**environment**</mark> and [<mark style="color:red;">**t**</mark><mark style="color:orange;">**est**</mark>](#user-content-fn-1)[^1] <mark style="color:orange;">**stage**</mark>. This type of onboarding is agnostic to the test runner. However, it doesn't allow a user to get Test Recommendations. See the [collecting coverage](../guides/collecting-coverage.md) guide for more information.
2. **Deep Agent Integration -** Allows you to onboard a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for a single <mark style="color:orange;">**environment**</mark> and [<mark style="color:red;">**t**</mark><mark style="color:orange;">**est**</mark>](#user-content-fn-2)[^2] <mark style="color:orange;">**stage**</mark>. This type of integration provides code coverage and test recommendation; however, it requires that Sealights will support your test framework/runner.
3. **Custom Integration -** For scenarios where Sealights doesn't support your test framework but still wants to get code coverage _and_ test recommendations, you can use our [public APIs](../../../apis/test-optimization.md) and create a custom integration.

## Setup

### Overview

The following section describes how to use a Deep Agent Integration, which allows you to onboard a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for a single <mark style="color:orange;">**environment**</mark> and [<mark style="color:red;">**t**</mark><mark style="color:orange;">**est**</mark>](#user-content-fn-3)[^3] <mark style="color:orange;">**stage**</mark>. This type of integration provides code coverage and test recommendation; however, it requires that Sealights will support your test framework/runner.

### Prerequisites&#x20;

1. Scan and configure your application for code coverage collection. For more information, please refer to the [Deployment](../../) page.
2. Verify that the machine(s) that run the test have connectivity to Sealights Cloud. See the <mark style="color:red;">**how to verify connectivity**</mark> guide for more information.
3. Know your automated tests setup. You need to know the following:
   1. Which test framework is being used?&#x20;
   2. What is the command to run the tests?&#x20;
   3. Is there any customization that is being done to the framework

### Installation

{% hint style="info" %}
The result of configuring Deep Agent Integration is that our agent is running as part of the Test Framework/Runner process. This allows the agent to hook to the relevant events and send test data & metadata to Sealights.

In order to ease the onboarding, we have created several plugins/integrations that will help you to configure the agent. Suppose by any means you don't see an integration that is relevant to you, but your <mark style="color:red;">**test framework is supported**</mark>. In that case, you can always revert to <mark style="color:red;">**manually integrating an agent into a test process**</mark>.
{% endhint %}

The following list contains a list of out of the box integrations to our agent. When considering how to integrate, the first thing you must consider is the technology in which your tests are written. Once you know that, please search the list below for the relevant integration.

#### Java

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">JUnit 4</td><td></td><td><a href="java/junit-4.md">junit-4.md</a></td><td><a href="../../../../.gitbook/assets/Untitled design (6).png">Untitled design (6).png</a></td></tr><tr><td></td><td align="center">JUnit 5</td><td></td><td><a href="java/junit-5.md">junit-5.md</a></td><td><a href="../../../../.gitbook/assets/Untitled design (5).png">Untitled design (5).png</a></td></tr><tr><td></td><td align="center">TestNG</td><td></td><td><a href="java/testng.md">testng.md</a></td><td><a href="../../../../.gitbook/assets/Untitled design (7).png">Untitled design (7).png</a></td></tr><tr><td></td><td align="center">Maven</td><td></td><td><a href="java/maven.md">maven.md</a></td><td><a href="../../../../.gitbook/assets/Untitled design (8).png">Untitled design (8).png</a></td></tr><tr><td></td><td align="center">Gradle</td><td></td><td><a href="java/gradle.md">gradle.md</a></td><td><a href="../../../../.gitbook/assets/Untitled design (9).png">Untitled design (9).png</a></td></tr><tr><td></td><td align="center">Ant</td><td></td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (10).png">Untitled design (10).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td><td></td></tr></tbody></table>

#### .NET Core

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">MSTest</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (11).png">Untitled design (11).png</a></td></tr><tr><td></td><td align="center">NUnit</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (12).png">Untitled design (12).png</a></td></tr><tr><td></td><td align="center">xUnit</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (13).png">Untitled design (13).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td></tr></tbody></table>

#### .NET Framework

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">MSTest</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (11).png">Untitled design (11).png</a></td></tr><tr><td></td><td align="center">NUnit</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (12).png">Untitled design (12).png</a></td></tr><tr><td></td><td align="center">xUnit</td><td></td><td><a href="../../../../.gitbook/assets/Untitled design (13).png">Untitled design (13).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td></tr></tbody></table>

#### Node JS

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th></tr></thead><tbody><tr><td></td><td align="center">Mocha</td><td></td></tr><tr><td></td><td align="center">Jest</td><td></td></tr></tbody></table>

#### Go

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th></tr></thead><tbody><tr><td></td><td align="center">Other</td><td></td></tr><tr><td></td><td align="center"></td><td></td></tr><tr><td></td><td align="center"></td><td></td></tr></tbody></table>

#### &#x20;Python

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th></tr></thead><tbody><tr><td></td><td align="center">Nose</td><td></td></tr><tr><td></td><td align="center">Py Test</td><td></td></tr><tr><td></td><td align="center">Unittests</td><td></td></tr><tr><td></td><td align="center">Unittests2</td><td></td></tr></tbody></table>

###

### Verifying the installation

If the integration went as expected, you could validate that it worked by looking at the Sealights Dashboard and see:

1. Test counts - These should match the numbers you see in your CI. The only exception is in the Cucumber Test Framework, in which you can have more skipped tests showing, due to the way the agent classifies them.
2. Test Stage Coverage - if your test stage has coverage, it means your agent in the application under tests managed to connect to the agent in the test runner.

## Further Reading

* Test Optimization - [Public API](../../../apis/test-optimization.md) documentation.
* [Integrating Sealights into Gauge](../guides/integrating-sealights-to-gauge.md)  - a walkthrough describing how to write a custom integration to Gauge

[^1]: Bla bla bla

[^2]: Bla bla bla

[^3]: Bla bla bla
