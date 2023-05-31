# Deployment Type Comparison

## Overview

Sealights have two types of installations:

* Simple Deployment - Install Sealights on your UAT environment.
* Advanced Deployment - Install Sealights in the CI Pipeline, where the source code is being built and configured.

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
