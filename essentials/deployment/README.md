# Deployment

## Overview

Sealights allows you to collect code coverage and [apply test selection](#user-content-fn-1)[^1] to a Product.

**Product -** A collection of application components (microservices, web applications, monolith backend, etc.).

A complete Sealights installation of a product involves three logical steps:

1. **Scan the build artifacts** of the application components that you would like to report to Sealights. Scanning the application components will help Sealights understand which code should be tracked for code coverage and changes.&#x20;
2. **Collect Code Coverage.** In order to capture code coverage data & metadata from your application under tests while your tests are running.&#x20;
3. **Integrate into the test runner (test automation framework or manual runner).** In order to indicate to Sealights when a [Test Cycle](#user-content-fn-2)[^2] starts and to get [Test Recommendations.](#user-content-fn-3)[^3]

{% hint style="info" %}
All of the aforementioned steps are mandatory, regardless of the Sealights offering you are using.
{% endhint %}

## <mark style="color:red;">Diagram Placeholder</mark>

<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

## Deployment Types

There are two Deployment Types in Sealights:

1. **Simple Deployment -** Allows for quick onboarding of a <mark style="color:orange;">**product**</mark> composed of backend services for a single environment[^4] and [test stage](#user-content-fn-5)[^5]. It allows you to use most of Sealights offering in a quick and easy setup. This is the recommended deployment for getting started with a new team.
2. **Advanced Deployment. -** Allows you to onboard a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for multiple environments[^6], [test stages](#user-content-fn-7)[^7], and technologies.

{% hint style="info" %}
For a complete comparison between Simple Deployment and Advanced Deployment, [click here](deployment-type-comparison.md).
{% endhint %}

Choose a deployment type:

<table data-view="cards"><thead><tr><th></th><th align="center"></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td align="center">Simple Deployment</td><td></td><td><a href="simple-deployment/">simple-deployment</a></td></tr><tr><td></td><td align="center">Advance Deployment</td><td></td><td><a href="advanced-deployment.md">advanced-deployment.md</a></td></tr></tbody></table>

[^1]: As part of the Test Optimization offering, Sealights recommends which tests should be run. This is done by considering historical runs of your tests and correlating them with your current code changes. You can accelerate your CI without compromising your quality by running these recommendations. Applying test selection means adhering to these recommendations and running only the recommended tests.

[^2]: A test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.

[^3]: As part of the Test Optimization offering, Sealights recommends which tests should be run. This is done by considering historical runs of your tests and correlating them with your current code changes. You can accelerate your CI without compromising your quality by running these recommendations.

[^4]: A set of machines/containers that are hosting your System Under Test (SUT).&#x20;

[^5]: A test stage or test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.

[^6]: Environment: a set of machines/containers that are hosting your System Under Test (SUT).&#x20;

[^7]: A test stage or test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.
