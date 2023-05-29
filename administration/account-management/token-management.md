# Token Management

## Overview

As part of the installation process of Sealights, users are required to use token. To date, there are three types of tokens:

* **Agent Token** - Used to configure agents reporting data to Sealights or in public APIs related to agents, such as downloading an agent or reporting test results.
* **Browser Extention Token -** Being used with the Sealights Chrome extension.
* **API Token -** Being used with our public APIs, apart from the APIs related to data from the agents.

### Creating An Agent Token

{% hint style="info" %}
Creating an Agent Token requires a DevOps user role. Please refer to the [Onboarding Permissions](role-based-access-control/onboarding-permissions.md#how-to-verify-my-role) page to verify that you have the right permissions.
{% endhint %}

1. Go to the _**settings**_ page. This can be done by clicking on the _**cog**_ icon in the top right corner of the screen (next to your user's avatar).
2. Go to the _**Cockpit & Onboarding**_ section in the menu and click _**Agent Tokens**._
3. In the _**Agent Tokens**_ screen, click on the _**Create New Token**_ button. Make sure to click on the button and not on the text. This will allow you to input a new name for the token.
4. Name the token. As tokens are shared across the organization, name them in a descriptive name and click on _**Save**._&#x20;
5. If successful, the token will be added to the list of tokens. In addition, an _"Agent token created and copied to the clipboard successfully"_ message will appear at the bottom of the screen.&#x20;

{% hint style="info" %}
An Agent Token can be passed as a parameter to Sealights agent in three ways: as a file, as a hard-coded value, or via an environment variable (usually via a Credential Manager).

You're free to select the convenient option for your configuration, but, in this documentation, we'll most of the time refer to the file option for simplicity and readability.
{% endhint %}

### Creating A Browser Extention Token

{% hint style="info" %}
Creating a Browser Extention Token doesn't require special permissions. All user types can create them.
{% endhint %}

In order to create a Browser Extention Token, follow the following steps:

1. Go to the _**settings**_ page. This can be done by clicking on the _**cog**_ icon in the top right corner of the screen (next to your user's avatar).
2. Go to the _**Integration**_ section in the menu and click _**Browser Extension Tokens**._
3. In the _**Browser Extension Tokens**_ screen, click on the _**Create New Token**_ button. Make sure to click on the button and not on the text. This will allow you to input a new name fo the token.
4. Name the token. As tokens are shared across the organization, name them in a descriptive name and click on _**Save**._&#x20;
5. If successful, the token will be added to the list of tokens. In addition, an _"Agent token created and copied to the clipboard successfully"_ message will appear in the bottom of the screen.&#x20;

### Creating An API Token&#x20;

{% hint style="info" %}
Creating an API Token requires DevOps or Admin user role. Please refer to the [Onboarding Permissions](role-based-access-control/onboarding-permissions.md#how-to-verify-my-role) page to verify that you have the right permissions.
{% endhint %}

In order to create an API Token, follow the following steps:

1. Go to the _**settings**_ page. This can be done by clicking on the _**cog**_ icon in the top right corner of the screen (next to your user's avatar).
2. Go to the _**Integration**_ section in the menu and click _**API Tokens**._
3. In the _**API Tokens**_ screen, click on the _**Create New Token**_ button. Make sure to click on the button and not on the text. This will allow you to input a new name fo the token.
4. Name the token. As tokens are shared across the organization, name them in a descriptive name and click on _**Save**._&#x20;
5. If successful, the token will be added to the list of tokens. In addition, an _"Agent token created and copied to the clipboard successfully"_ message will appear at the bottom of the screen.&#x20;

### Download a Token

Press the '**Download**' button<img src="../../.gitbook/assets/image (23).png" alt="" data-size="line"> for the token you have selected (or just created), and a file called _sltoken.txt_ will be downloaded to your computer. Copy it to the location you want to use it.

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="info" %}
Alternatively, you could press the '**Copy**' button<img src="../../.gitbook/assets/image (24).png" alt="" data-size="line"> and paste the token through the clipboard into the file and location you want or to any variable or credential manager tool.
{% endhint %}
