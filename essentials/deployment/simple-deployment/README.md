# Simple Deployment

## About This Guide <a href="#pagetitle" id="pagetitle"></a>

## Overview

Sealights allows you to collect code coverage and apply test selection to a Product.

**Product -** A collection of application components (microservices, web applications, monolith backend, etc.).

A complete Sealights installation of a product involves three logical steps:

1. **Scan the build artifacts** of the application components that you would like to report to Sealights. Scanning the application components will help Sealights understand which code should be tracked for code coverage and changes.&#x20;
2. **Collect Code Coverage.** In order to capture code coverage data & metadata from your application under tests while your tests are running.&#x20;
3. **Integrate into the test runner (test automation framework or manual runner).** In order to indicate to Sealights when a [Test Cycle](#user-content-fn-1)[^1] starts and to get [Test Recommendations.](#user-content-fn-2)[^2]

{% hint style="info" %}
In Simple Deployment, steps 1 and 2 happen together on the application under test.
{% endhint %}

## Setup

### Prerequisites&#x20;

The following prerequisites have to be completed before starting the deployment:

1. Verify that you have an account in Sealights. For instructions on how to create an account, refer to the [account creation](../../../administration/account-management/#creating-a-new-sealights-account) page.
2. Onboarding requires DevOps or Admin permissions in the Sealights Platform. [Please verify that you have the right permission](../../../administration/account-management/role-based-access-control/onboarding-permissions.md).
3. Verify that the environment of the application under test and the machine(s) that run the test have connectivity to Sealights Cloud. See the [How to verify connectivity](../../../check-the-connectivity-to-the-sealights-server-from-my-machine.md) guide for more information.
4. Installing Sealights requires modifying your application components' deployment scripts and possibly the CI Job that runs your tests. Please verify you have the necessary permissions in your organization.

### Installation

#### Step 1: Agent Installation - Scan Artifact and **Collect Code Coverage**

The following steps are required in order to install the agent:

1. [Create](../../../administration/account-management/token-management.md#creating-an-agent-token) an [agent token](#user-content-fn-3)[^3] (you'll need this token for the Sealights Agent configuration in step #3)
2. [Create a ](../../../administration/account-management/testing-environments-and-identifiers-management.md#create-a-simple-deployment-integration-build-lab)[Lab ID](#user-content-fn-4)[^4] (you'll need this generated identifier for the Sealights Agent configuration in step #3)
3. Download the Sealights Agent and configure your application to start with it.

{% hint style="info" %}
Note that the agent configuration step (step #3) must be repeated for each application component you want to capture coverage for.
{% endhint %}

{% hint style="warning" %}
When deploying an application component for the environment, do so from the same branch. This will allow Sealights to track code changes correctly for a given branch. Mixing branches for a single application component will lead to incorrect information.&#x20;
{% endhint %}

Please select your backend technology to get detailed installation instructions:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>Java</td><td></td><td><a href="../../../.gitbook/assets/java.png">java.png</a></td><td><a href="java-agent-installation-and-setup/">java-agent-installation-and-setup</a></td></tr></tbody></table>

{% hint style="success" %}
Congratulations! At the end of this step, you can already capture coverage from your Manual Tests. Please follow [these instructions ](../running-your-tests/manual-tests/manual-tests-reported-via-the-dashboard-widget.md)to see how to do so.&#x20;
{% endhint %}

#### Step 2: Integrate into the test runner

For integrating Sealights into your Test Runner (automated or manual), please refer to the [Running Your Tests](../running-your-tests/) section in the documentation.

{% hint style="success" %}
At the end of this step, you are able to see in the Sealights Dashboard the coverage for your tests (Manual and/or Automated), test results (success/failure), and potential savings via Sealights Test Optimization.
{% endhint %}

### Validation

{% hint style="success" %}
At the completion of the steps above, your application is set to provide coverage and get recommendations for the optimization of your tests.
{% endhint %}

## Troubleshooting

In case one of the steps above did not succeed and you were not able to resolve the issue based on the logs, please [contact Sealights Support ](../../../contact-sealights-support/)for assistance.

## Further Reading

* Enable logs
* Opening a support ticket

[^1]: A test cycle is a collection of tests organized to accomplish specific testing objectives, encompassing a broader scope than individual tests. Common examples are Regression Tests, End-To-End Tests, Manual Tests, and more.

[^2]: As part of the Test Optimization offering, Sealights recommends which tests should be run. This is done by considering historical runs of your tests and correlating them with your current code changes. You can accelerate your CI without compromising your quality by running these recommendations.

[^3]: Agent token is needed in order to allow the agent to securely communicate with  Sealights Cloud.

[^4]: Lab IDs enable SeaLights to establish a connection between data collected from multiple agents across various application components and test runners, consolidating them into a single product.
