# Maven

## Overview

This guide covers how to integrate Sealights into your tests running in [Maven](https://maven.org). You can use the SeaLights agent to update your Maven's pom.xml with the needed changes to run your Maven tests using the Sealights Maven Plugin

## Prerequisites

1. Verify that the environment of the application under test and the machine(s) that run the test have connectivity to Sealights Cloud. See the [how to verify connectivity](../../../../../check-the-connectivity-to-the-sealights-server-from-my-machine.md) guide for more information.
2. Installing Sealights requires modifying your application components' deployment scripts and possibly the CI Job that runs your tests. Please verify you have the necessary permissions in your organization.

## Setup

{% hint style="info" %}
**TL;DR:** You can jump directly to the [Sample script section](maven.md#sample-script) below.
{% endhint %}

### Download the Sealights Agent

Download the Sealights Agent form: [https://agents.sealights.co/sealights-java/sealights-java-latest.zip](https://agents.sealights.co/sealights-java/sealights-java-latest.zip) and place it in your workspace where your Maven project is located.

You can use the following commands to automate the process in the environment setup script

{% tabs %}
{% tab title="Linux" %}
```bash
wget -nv https://agents.sealights.co/sealights-java/sealights-java-latest.zip
unzip -oq sealights-java-latest.zip
echo "Sealights CI Agent version used is: $(cat version.txt)"

#cURL tool can also be used
#curl -L "https://agents.sealights.co/sealights-java/sealights-java-latest.zip" --output sealights-java-latest.zip
```
{% endtab %}

{% tab title="Powershell" %}
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
iwr https://agents.sealights.co/sealights-java/sealights-java-latest.zip  -OutFile sealights-java-latest.zip -ErrorAction Continue
if (Test-Path -Path sealights-java-latest.zip -PathType Leaf) {
  Expand-Archive .\sealights-java-latest.zip
}
```
{% endtab %}
{% endtabs %}

### Create a JSON configuration file

Create a JSON configuration file with the following parameters in order to provide the necessary configuration fields to the SeaLights Maven plugin:&#x20;

| Parameter                               | Value                                                                                                                                                                                                       | Remarks                                                                                                                                                                                                                        |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **tokenFile**                           | set with the relative or absolute path to a file containing the agent token [obtained from the SeaLights dashboard](../../../../../administration/account-management/token-management.md#download-a-token). |  This can be either the same or a different valid token than the one used with the agent attached to your application under test.                                                                                              |
| **createBuildSessionId**                | False                                                                                                                                                                                                       |                                                                                                                                                                                                                                |
| **executionType**                       | testsonly                                                                                                                                                                                                   | Provide which executions need to be handled by the Maven plugin. In our case, **testsonly** to capture only the tests execution and not the project compilation.                                                               |
| [**testStage**](#user-content-fn-1)[^1] | \<Test Stage Name>                                                                                                                                                                                          | Set the name of the test stage as will be displayed on the SeaLights dashboard. For example, "Regression Tests", "Selenium Tests" or "Functional Tests".                                                                       |
| **labId**                               | \<Lab ID>                                                                                                                                                                                                   | Unique Identifier of the testing environment where the Sealights agent is attached and [that was defined in the Settings](../../../../../administration/account-management/testing-environments-and-identifiers-management.md) |
| **runFunctionalTests**                  | true                                                                                                                                                                                                        | for Testing projects using Sealights Maven plugin                                                                                                                                                                              |

As a result, your JSON configuration file should look like this:

{% code lineNumbers="true" %}
```json
{
  "tokenFile": "./sltoken.txt",
  "createBuildSessionId": false,
  "executionType": "testsonly",
  "testStage": "<My_Test_Stage>",
  "labId": "<my_lab_id>",
  "runFunctionalTests": true,
  
  "proxy": null,
  "logEnabled": false,
  "logDestination": "console",
  "logLevel": "warn"
}
```
{% endcode %}

{% hint style="info" %}
In the file above, you need to make sure the following lines are specific to your environment and configuration:

* line 2: path to the token file,
* line 5: Name the stage as you want to see it in your Sealights Dashboard,
* line 6: Lab ID you have defined in your settings and provided to your Coverage agent
* line 9: If required, proxy details. &#x20;
{% endhint %}



<details>

<summary>Optional Agent Parameters</summary>

There are additional parameters you can provide

1. **proxy** - (Optional) Address of proxy to run connection through
2. **filesStorage** - Set to the temp folder for the agent to create temporary files in. For example **/tmp**
3. **logEnabled** - Set to **true** if you want a log to be created
4. **logLevel** - Set the log level to create. For example, **WARN** or **INFO**

</details>



Name this file with a convenient name (`slmaventest.json` for example) and place it in your Project workspace for the next steps below.

### Integrate Sealights dynamically into the Maven project

Before running your Maven command, you'll run Sealights Advanced agent with the `-pom` flag to add the SeaLights Maven Plugin into your project configuration. This command will use the JSON configuration file defined above to inject Sealights plugin integration into the pom.xml settings.

The parameters it receives are:

* **configfile** - The path to the JSON configuration you created with the parameters to be provided to the SeaLights Maven Plugin
* **workspacepath** - The base path to the location of the pom.xml files to update

```bash
java -jar sl-build-scanner.jar -pom -configfile slmaventesth.json -workspacepath .
```

{% hint style="success" %}
At the successful completion of the command, you’ll see the following last line in the console:

`[Sealights Build Scanner] - Pom integration was completed.`

This step will update all the _pom.xml_ files and back them up to _pom.xml.slback_ copies in the same directory
{% endhint %}

If your workspace is not reset for each build, you will need to restore them at the end of the run (see command [below](maven.md#restore-your-maven-configuration-to-its-previous-state)).

### Execute your tests

You can use your regular maven command to execute your tests. Typically, the command is '**mvn clean install**' or '**maven clean verify**' for example.

## Sample script

{% hint style="info" %}
Make sure to update the token value on line 7 and labId on line 16 before running this sample. These values need to be aligned with your specific configuration and account settings.
{% endhint %}

{% code lineNumbers="true" %}
```sh
echo "Downloading Sealights Agents..."
wget -nv https://agents.sealights.co/sealights-java/sealights-java-latest.zip
unzip -o sealights-java-latest.zip
echo "Sealights agent version used is:" `cat sealights-java-version.txt`

#Replace the Token value below with the proper value from your Accounts settings
export SL_TOKEN="123"
echo $SL_TOKEN>sltoken.txt 

echo  '{ 
  "executionType": "testsonly",
  "tokenFile": "./sltoken.txt",
  "createBuildSessionId": false,
  "testStage": "Functional Tests",
  "runFunctionalTests": true,
  "labId": "my_lab_id",
  "proxy": null,
  "logEnabled": false,
  "logDestination": "console",
  "logLevel": "warn",
  "sealightsJvmParams": {}
  }' > slmaventests.json
 
echo "Adding Sealights to Tests Project POM file..."
java -jar sl-build-scanner.jar -pom -configfile slmaventests.json -workspacepath .

#your tests execution command: mvn test
```
{% endcode %}

{% embed url="https://www.loom.com/share/8ed55a986ff54d6082edd5326b3f2779" %}

## Optional&#x20;

### Restore your Maven configuration to its previous state

In case the pom file is to be restored to its previous state before the Sealights plugin was applied, use the build scanner with the `-restorePom` flag on the workspace where the _pom.xml_ file is located:

```
java -jar sl-build-scanner.jar -restorePom -workspacepath .
```



[^1]: glossary
