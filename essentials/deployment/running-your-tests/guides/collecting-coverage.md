# Collecting Coverage

## Overview

Sealights supports three types of integrations to your tests framework:

1. **Coverage Only Integration -** Allows seeing code coverage for a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for a single <mark style="color:orange;">**environment**</mark> and [<mark style="color:red;">**t**</mark><mark style="color:orange;">**est**</mark>](#user-content-fn-1)[^1] <mark style="color:orange;">**stage**</mark>. This type of onboarding is agnostic to the test runner. However, it doesn't allow a user to get Test Recommendations. See the [collecting coverage](collecting-coverage.md) guide for more information.
2. **Deep Agent Integration -** Allows you to onboard a <mark style="color:orange;">**product**</mark> composed of multiple application components (backend services and front end) for a single <mark style="color:orange;">**environment**</mark> and [<mark style="color:red;">**t**</mark><mark style="color:orange;">**est**</mark>](#user-content-fn-2)[^2] <mark style="color:orange;">**stage**</mark>. This type of integration provides code coverage and test recommendation; however, it requires that Sealights will support your test framework/runner.
3. **Custom Integration -** For scenarios where Sealights doesn't support your test framework but still wants to get code coverage _and_ test recommendations, you can use our [public APIs](../../../apis/test-optimization.md) and create a custom integration.

This guide covers how to collect coverage for a product, which requires notifying Sealights that a Test Cycle is starting in a certain environment.

{% hint style="info" %}
This guide assumes that you can run one of the CLIs of our agents. If that's not possible, you can accomplish the same by starting a Test Session using our [Test Optimization](../../../apis/test-optimization.md#starting-a-test-session) public APIs.
{% endhint %}

## Setup

### Prerequisites&#x20;

1. Please complete the prerequisites on the [Automated Tests](../automated-tests/#prerequisites) page.
2. <mark style="color:red;">**Download the Sealights agent**</mark> to the machine that starts the test cycle. In this guide, the agents will be used as CLIs, so you will not have to integrate them to your running processes.

{% hint style="warning" %}
You can run the following command more than once, assuming you keep the same Build Session Id, Lab Id, and Stage. However, if you attempt to run a different Build Session Id or Test Stage on the same lab concurrently, the previously opened Test Stage will be closed. This can lead to flaky or wrong data. <mark style="color:red;">**Please refer to...**</mark>
{% endhint %}

### Installation

Assuming you have completed the prerequisites, the configuration itself involves the following three steps:

1. Notify Sealights that your Test Cycle is starting
2. Run your tests as you do today.
3. Notify Sealights that your Test Cycle has ended.

With that in mind you can find below sample commands. Make sure to use select the tab of the technology for the agents you have downloaded as part of the prerequisites.

&#x20;

{% tabs %}
{% tab title="Java" %}
//TODO - start/end execution commands
{% endtab %}

{% tab title="Node JS" %}

{% endtab %}

{% tab title=".NET Framework" %}

{% endtab %}

{% tab title=".NET Core" %}

{% endtab %}

{% tab title="Python" %}

{% endtab %}

{% tab title="Go" %}

{% endtab %}
{% endtabs %}

## Further Reading

* For more information on running your tests, see the [Running Your Tests](../) page.

[^1]: Bla bla bla

[^2]: Bla bla bla
