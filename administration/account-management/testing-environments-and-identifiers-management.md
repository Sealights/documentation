# Testing Environments and Identifiers Management

Sealights maps your testing environments based on dedicated identifiers predefined in the Settings.&#x20;

These identifiers are called LabID and have a few variants depending on your topology:

* Simple Deployment Lab (a.k.a CD Only) when Sealights is configured on a testing environment and not in the CI
* Multiple Environment Lab, for configurations where the same application version is tested and promoted on several (dedicated) environments and you're willing to aggregate all the coverage analytics into a single entry of your Sealights dashboard and reports&#x20;

## Create a Simple Deployment Integration Build Lab ID

To create a Lab ID for the Simple Deployment, go to the settings page of your SeaLights dashboard:

1. Under 'Cockpit & Onboarding → Integration Build Labs', click on the button "Create new Integration Build Lab” ![](<../../.gitbook/assets/image (6).png>)
2.  In the form that opens, define an App Name that reflects your Product Name.&#x20;

    * A Product reflects a collection of application components (microservices, web applications, monolith backend, etc.). For example, your "Online Store" project.

    <figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
3.  Define the Branch Name: the name of the environment where you deploy the Sealights Agent. For example: 'QA1' \


    <figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
4. Select the “CD only” option![](<../../.gitbook/assets/image (26).png>) and click on Create.

A new LabID was created and appears in the list, with the type 'CDOnly' highlighted.&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Copy its generated identifier using the copy button<img src="../../.gitbook/assets/image (15).png" alt="" data-size="line"> and save it for later usage in the following configuration steps.
