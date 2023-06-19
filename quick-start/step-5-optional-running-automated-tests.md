# Step 5 (optional): Running Automated Tests

## Overview

Automated tests are executed using software tools and scripts without manual intervention, providing efficient and repeatable verification of software functionality. By integrating Sealights into your automated tests framework, you will be able to see code coverage and test recommendations.

## Integration Types

There are three Integration Types in Sealights:

1. **Coverage Only Integration -** Allows seeing code coverage for a product[^1] composed of multiple application components (backend services and front end) for a single environment[^2] and [test stage](#user-content-fn-3)[^3]. This type of onboarding is agnostic to the test runner. However, it doesn't allow a user to get Test Recommendations. See the [collecting coverage](../essentials/deployment/running-your-tests/guides/collecting-coverage.md) guide for more information.
2. **Deep Agent Integration -** Allows you to onboard a product[^4] composed of multiple application components (backend services and front end) for a single environment[^5] and [test stage](#user-content-fn-6)[^6]. This type of integration provides code coverage and test recommendation; however, it requires that Sealights will support your test framework/runner.
3. **Custom Integration -** For scenarios where Sealights doesn't support your test framework but still wants to get code coverage _and_ test recommendations, you can use our [public APIs](../essentials/apis/test-optimization.md) and create a custom integration.

## Setup

### Overview

The following section describes how to use a Deep Agent Integration, which allows you to onboard a product[^7] composed of multiple application components (backend services and front end) for a single environment[^8] and [test stage](#user-content-fn-9)[^9]. This type of integration provides code coverage and test recommendation; however, it requires that Sealights will support your test framework/runner.

### Prerequisites&#x20;

1. Scan and configure your application for code coverage collection. For more information, please refer to the [Deployment](../essentials/deployment/) page.
2. Verify that the machine(s) that run the test have connectivity to Sealights Cloud. See the [**how to verify connectivity**](../check-the-connectivity-to-the-sealights-server-from-my-machine.md) guide for more information.
3. Know your automated tests setup. You need to know the following:
   1. Which test framework is being used?&#x20;
   2. What is the command to run the tests?&#x20;
   3. Is there any customization that is being done to the framework

### Installation

{% hint style="info" %}
Configuring Deep Agent Integration results in our agent running as part of the Test Framework/Runner process. This allows the agent to hook to the relevant events and send test data & metadata to Sealights.

In order to ease the onboarding, we have created several plugins/integrations that will help you to configure the agent. In cases where an integration/plugin doesn't exist but your <mark style="color:red;">**test framework is listed as supported**</mark>, you can always revert to <mark style="color:red;">**manually integrating an agent into a test process**</mark>.
{% endhint %}

The following list contains a list of out-of-the-box integrations to our agent. When considering how to integrate, you must first consider the technology in which your tests are written. Once you know that, please search the list below for the relevant integration for the technology.

#### Java

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">JUnit 4</td><td></td><td><a href="../essentials/deployment/running-your-tests/automated-tests/java/junit-4.md">junit-4.md</a></td><td><a href="../.gitbook/assets/Untitled design (6).png">Untitled design (6).png</a></td></tr><tr><td></td><td align="center">JUnit 5</td><td></td><td><a href="../essentials/deployment/running-your-tests/automated-tests/java/junit-5.md">junit-5.md</a></td><td><a href="../.gitbook/assets/Untitled design (5).png">Untitled design (5).png</a></td></tr><tr><td></td><td align="center">TestNG</td><td></td><td><a href="../essentials/deployment/running-your-tests/automated-tests/java/testng.md">testng.md</a></td><td><a href="../.gitbook/assets/Untitled design (7).png">Untitled design (7).png</a></td></tr><tr><td></td><td align="center">Maven</td><td></td><td><a href="../essentials/deployment/running-your-tests/automated-tests/java/maven.md">maven.md</a></td><td><a href="../.gitbook/assets/Untitled design (8).png">Untitled design (8).png</a></td></tr><tr><td></td><td align="center">Gradle</td><td></td><td><a href="../essentials/deployment/running-your-tests/automated-tests/java/gradle.md">gradle.md</a></td><td><a href="../.gitbook/assets/Untitled design (9).png">Untitled design (9).png</a></td></tr><tr><td></td><td align="center">Ant</td><td></td><td></td><td><a href="../.gitbook/assets/Untitled design (10).png">Untitled design (10).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td><td></td></tr></tbody></table>

#### .NET Core

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">MSTest</td><td></td><td><a href="../.gitbook/assets/Untitled design (11).png">Untitled design (11).png</a></td></tr><tr><td></td><td align="center">NUnit</td><td></td><td><a href="../.gitbook/assets/Untitled design (12).png">Untitled design (12).png</a></td></tr><tr><td></td><td align="center">xUnit</td><td></td><td><a href="../.gitbook/assets/Untitled design (13).png">Untitled design (13).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td></tr></tbody></table>

#### .NET Framework

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">MSTest</td><td></td><td><a href="../.gitbook/assets/Untitled design (11).png">Untitled design (11).png</a></td></tr><tr><td></td><td align="center">NUnit</td><td></td><td><a href="../.gitbook/assets/Untitled design (12).png">Untitled design (12).png</a></td></tr><tr><td></td><td align="center">xUnit</td><td></td><td><a href="../.gitbook/assets/Untitled design (13).png">Untitled design (13).png</a></td></tr><tr><td></td><td align="center">Other</td><td></td><td></td></tr></tbody></table>

#### Node JS

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">Mocha</td><td></td><td><a href="../.gitbook/assets/Untitled design (14).png">Untitled design (14).png</a></td></tr><tr><td></td><td align="center">Jest</td><td></td><td><a href="../.gitbook/assets/Untitled design (15).png">Untitled design (15).png</a></td></tr></tbody></table>

#### Go

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th></tr></thead><tbody><tr><td></td><td align="center">Other</td><td></td></tr><tr><td></td><td align="center"></td><td></td></tr><tr><td></td><td align="center"></td><td></td></tr></tbody></table>

#### &#x20;Python

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td align="center">Nose</td><td></td><td><a href="../.gitbook/assets/Untitled design (16).png">Untitled design (16).png</a></td></tr><tr><td></td><td align="center">Py Test</td><td></td><td><a href="../.gitbook/assets/Untitled design (17).png">Untitled design (17).png</a></td></tr><tr><td></td><td align="center">Unittests</td><td></td><td><a href="../.gitbook/assets/Untitled design (18).png">Untitled design (18).png</a></td></tr><tr><td></td><td align="center">Unittests2</td><td></td><td><a href="../.gitbook/assets/Untitled design (19).png">Untitled design (19).png</a></td></tr></tbody></table>

###

### Verifying the installation

If the integration went as expected, you could validate that it worked by looking at the Sealights Dashboard and see:

1. Test counts - These should match the numbers you see in your CI. The only exception is in the Cucumber Test Framework, in which you can have more skipped tests showing, due to the way the agent classifies them.
2. Test Stage Coverage - if your test stage has coverage, it means your agent in the application under tests managed to connect to the agent in the test runner.

## Further Reading

* Test Optimization - [Public API](../essentials/apis/test-optimization.md) documentation.
* [Integrating Sealights into Gauge](../essentials/deployment/running-your-tests/guides/integrating-sealights-to-gauge.md)  - a walkthrough describing how to write a custom integration to Gauge

[^1]: A collection of application components (microservices, web applications, monolith backend, etc.).

[^2]: A set of machines/containers that are hosting your System Under Test (SUT).

[^3]: A test stage or test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.

[^4]: A collection of application components (microservices, web applications, monolith backend, etc.).

[^5]: A set of machines/containers that are hosting your System Under Test (SUT).

[^6]: A test stage or test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.

[^7]: A collection of application components (microservices, web applications, monolith backend, etc.).

[^8]: A set of machines/containers that are hosting your System Under Test (SUT).

[^9]: A test stage or test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.
