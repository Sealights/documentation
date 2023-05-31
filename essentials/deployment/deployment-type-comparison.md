# Deployment Type Comparison

## Overview

Sealights have two types of installations:

* Simple Deployment - Install Sealights on your User Acceptance Tests environment[^1].
* Advanced Deployment - Install Sealights in the CI Pipeline, where the source code is built and configured. As part of this setup, you'll also have to install Sealights in one or more environments[^2] where you'd like to use Sealights for them.&#x20;

| Feature           | Simple Deployment | Advanced Deployment |
| ----------------- | ----------------- | ------------------- |
| Code Coverage     | Yes               | Yes                 |
| Test Optimization | Yes               | Yes                 |
| Quality Risks     | Yes               | Yes                 |
| Quality Trends    | Yes               | Yes                 |
| Contributors      | No                | Yes                 |
| Commit messages   | No                | Yes                 |

### Simple Deployment - Illustration

<figure><img src="../../.gitbook/assets/Nadav - SeaLights Code Coverage for One Environment Architecture (1).pptx (4).png" alt=""><figcaption></figcaption></figure>

### Advanced Deployment - Illustration

<figure><img src="../../.gitbook/assets/Nadav - SeaLights Code Coverage for One Environment Architecture (1).pptx (1).png" alt=""><figcaption></figcaption></figure>

### Advanced Deployment (Parallel Test Stage for the same product) - Illustration

<figure><img src="../../.gitbook/assets/Nadav - SeaLights Code Coverage for One Environment Architecture (1).pptx (2).png" alt=""><figcaption></figcaption></figure>

[^1]: A set of machines/containers that are hosting your System Under Test (SUT).&#x20;

[^2]: Environment: a set of machines/containers that are hosting your System Under Test (SUT).&#x20;
