# Java - Agent Installation and Setup

{% hint style="info" %}
The current installation guide assumes you completed the [steps](https://sealightstest.gitbook.io/sealights/\~/changes/eb0XHXKCcNH2eaJkNCBh/deployment/simple-deployment#setup) mentioned on the Simple Deployment page.&#x20;
{% endhint %}

## Prerequisites

### Download the Sealights Agent&#x20;

Download the Sealights agent to the machine with the application under test. If there are multiple machines, make the agent available on every machine (or container) in the environment.

The agent is downloadable from the following URL: [https://agents.sealights.co/sl-cd-agent/sl-cd-agent-latest.zip](https://agents.sealights.co/sl-cd-agent/sl-cd-agent-latest.zip)

You can use the following commands to automate the process in the environment setup script

{% tabs %}
{% tab title="Linux" %}
```bash
wget -nv https://agents.sealights.co/sl-cd-agent/sl-cd-agent-latest.zip 
unzip -oq sl-cd-agent-latest.zip 
echo "Sealights CD Agent version used is: $(cat version.txt)"
```
{% endtab %}

{% tab title="Powershell" %}
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
iwr https://agents.sealights.co/sl-cd-agent/sl-cd-agent-latest.zip -OutFile sl-cd-agent-latest.zip -ErrorAction Continue
if (Test-Path -Path sl-cd-agent-latest.zip -PathType Leaf) {
  Expand-Archive .\sl-cd-agent-latest.zip 
}
```
{% endtab %}
{% endtabs %}

### Download the Agent Token

[Download the Agent Token](../../../../administration/account-management/token-management.md#download-a-token) you have generated in the settings page, as a file (called by default sltokent.txt), and place it in the folder where you placed the agent.&#x20;

## Setup

In order to configure the agent, please add the Sealights agent to your Java virtual machine (JVM) as a `-javaagent`.&#x20;

The Sealights Agent relies on specific parameters that can be specified by setting Java system variables, which are simple key-value pairs, using the `-D` argument on the startup command.  Our agent will programmatically retrieve relevant parameters to it when they are specified with the specific `-Dsl.` prefix.

This is done by updating the JVM parameters of the application component with the following:

<pre class="language-bash"><code class="lang-bash"><strong>-javaagent:sl-cd-agent.jar -Dsl.tokenFile=sltoken.txt \
</strong>    -Dsl.appName=&#x3C;your-service-name> -Dsl.buildName=&#x3C;your-service-version> \
    -Dsl.includes=&#x3C;your-service-package> -Dsl.workspace=&#x3C;path-to-service-artifact> \
    -Dsl.labId=&#x3C;labid-defined-previously-in-settings> 
</code></pre>

For example, your configuration may look like this:&#x20;

<pre><code><strong>-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt \
</strong>    -Dsl.appName=backend-service -Dsl.buildName=1.0.26 \
    -Dsl.includes="*com.mycompany.*" -Dsl.workspace=/app/ \
    -Dsl.labId=integ_qa1_retail
</code></pre>

The required parameters are detailed as follows:

<table data-full-width="true"><thead><tr><th width="205.33333333333337">Parameter Name</th><th width="374">Description</th><th>Remarks</th></tr></thead><tbody><tr><td><strong>sl.tokenFile</strong></td><td>The agent token in a file to use for the secure connection</td><td>See the <a href="../../../../administration/account-management/token-management.md">token management</a> section for more details.<br>If you're managing your credentials via some manager, you can pass the token as an environment variable (for example <code>$SL_TOKEN</code>) and therefore you'll need to update the parameter to be <strong>sl.token</strong> (without the term File) , e.g. <code>sl.token=$SL_TOKEN</code></td></tr><tr><td><strong>sl.appName</strong></td><td>Name of the application component.</td><td>We recommend limiting the application name to a maximum of 50 characters and utilizing alphanumeric characters (A-Z and numbers).</td></tr><tr><td><strong>sl.labId</strong></td><td><a href="../../../../administration/account-management/testing-environments-and-identifiers-management.md">The labId generated in the dashboard settings</a> </td><td>This labId must be the same used by all the agents deployed in the same environment.</td></tr><tr><td><strong>sl.buildName</strong></td><td>The component version. <br><br>If the application component is being installed on multiple machines in the same environment, the exact same value has to be used.</td><td><p><strong>When the artifact is updated/modified, this version number must change accordingly.</strong> </p><p></p><p>We recommend limiting the application name to a maximum of 30 characters and utilizing alphanumeric characters (A-Z and numbers).</p></td></tr><tr><td><strong>sl.includes</strong></td><td>Comma separated list of search pattern with wildcards for the packages to be included in the scan</td><td>For example:<br>- <code>com.mycompany.*</code><br>- <code>io.demo.*, com.foo.*</code></td></tr><tr><td><strong>sl.workspace</strong></td><td>Comma-separated list of folders to search in for files to be scanned. </td><td>Default is the folder the artifact is located in and the classpath</td></tr></tbody></table>



<details>

<summary>Optional Agent Parameters</summary>

Use the following additional parameters to fine-tune your setup:

* **sl.excludes** - Comma-separated list of search patterns with wildcards for the packages to be excluded in the scan
* **sl.branchName** - Name of the branch of the component. If not provided, the lab branch name will be used
* **sl.workspace** - Comma-separated list of folders to search in for files to be scanned. Default is the folder the artifact is located in and the classpath
* **sl.recursive** - Indication if to scan the workspace paths recursively. Default is true
* **sl.proxy** - Proxy for the agent to go through when communicating with SeaLights
* **sl.tags** - Free text comma-separated tags to help identify the agents later in the cockpit.

</details>

## Common Integrations

We have gathered a list of the most common configurations below:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td>                            <strong>Docker</strong></td><td></td><td><a href="common-configurations-examples.md#docker-container">#docker-container</a></td><td><a href="../../../../.gitbook/assets/logo-1.png">logo-1.png</a></td></tr><tr><td></td><td>                         <strong>JBoss/Wildfly</strong></td><td></td><td><a href="common-configurations-examples.md#jboss-wildfly">#jboss-wildfly</a></td><td><a href="../../../../.gitbook/assets/logo-6.png">logo-6.png</a></td></tr><tr><td></td><td>                          <strong>Kubernetes</strong></td><td></td><td><a href="common-configurations-examples.md#kubernetes">#kubernetes</a></td><td><a href="../../../../.gitbook/assets/logo-2.png">logo-2.png</a></td></tr><tr><td></td><td>                             <strong>Tomcat</strong></td><td></td><td><a href="common-configurations-examples.md#tomcat">#tomcat</a></td><td><a href="../../../../.gitbook/assets/logo-4.png">logo-4.png</a></td></tr><tr><td></td><td>                                <strong>CLI</strong></td><td></td><td><a href="common-configurations-examples.md#java-cli">#java-cli</a></td><td><a href="../../../../.gitbook/assets/logo-5.png">logo-5.png</a></td></tr></tbody></table>

## Validation

{% hint style="success" %}
When the **application is up** and running and the **Sealights Agent configured**, you can see it is properly running from the _**Cockpit -> Live Agents Monitor**_ screen.
{% endhint %}

See example for properly running agents. Verify that the app, branch, build. labID and machine name match the agent you ran:

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-06-13 at 15.19.28.png" alt=""><figcaption><p>Live Agents Monitor</p></figcaption></figure>

If no agents appears please follow the [troubleshooting](./#troubleshooting) instructions below.

## Troubleshooting

#### Service is running:

You have the ability to validate the JVM parameters in use with your application via your terminal&#x20;

{% tabs %}
{% tab title="Linux" %}
```bash
ps -ef | grep java
```
{% endtab %}

{% tab title="Powershell" %}
```powershell
gwmi -Class Win32_Process -Filter "name like '%java%'" | Format-Table -Wrap -Property ProcessId, CommandLine
```
{% endtab %}
{% endtabs %}

#### Enabling agent logs:

You can enable logging using additional parameters as environment variables or add them as `-Dsl.*` parameters. Both console output and file options are compatible and non-exclusive.

{% tabs %}
{% tab title="Console" %}
For logging into the console, add:

```
-Dsl.log.toConsole=true -Dsl.log.level=info
```
{% endtab %}

{% tab title="File" %}
For logging into a file, add:

```
-Dsl.log.toFile=true -Dsl.log.level=info -Dsl.log.folder=<path/with/permissions/> 
```

{% hint style="warning" %}
The user running the Java process must have writing permissions to the folder specified as the `log.folder` parameter. Lack of permission may lead to an empty folder.
{% endhint %}

{% hint style="info" %}
The default file name is _java-agent.log._
{% endhint %}
{% endtab %}

{% tab title="Logging Parameters" %}
<table data-header-hidden><thead><tr><th width="255">Parameter</th><th width="117.66666666666666">Required</th><th></th></tr></thead><tbody><tr><td><strong>Parameter</strong></td><td><strong>Required</strong></td><td><strong>Description</strong></td></tr><tr><td><code>sl.log.level</code></td><td>No</td><td>Sets the log level to one of the following: "off", "error", "warn", "info", "debug"</td></tr><tr><td><code>sl.log.toConsole</code></td><td>No</td><td>Set to true to enable log output to the console</td></tr><tr><td><code>sl.log.toFile</code></td><td>No</td><td>Set to true to enable log output to a file</td></tr><tr><td><code>sl.log.folder</code></td><td>No</td><td>Provide a folder to save the log files in</td></tr><tr><td><code>sl.log.filename</code></td><td>No</td><td>Provide the name of the log file</td></tr><tr><td><code>sl.log.count</code></td><td>No</td><td>Limit the number of log files to create. Default: 10</td></tr><tr><td><code>sl.log.limit</code></td><td>No</td><td>Limit the size of the log file in megabytes (MB). Default value is 10 (i.e. 10*1024 KB)</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

#### Java classes found by the agent

After enabling [logs](./#enabling-agent-logs), search in the logs for the pattern ["scan report"](#user-content-fn-1)[^1] &#x20;

Verity agent was able to find your Java classes by writing to the log line similar to the below:

```
// Some code2023-06-11 06:23:36,859 INFO  [|Thread-4    |] i.s.o.a.f.s.i.MetricsCollector : scan report - jars: 3, classes: 18, methods: 42, total time: 698
```

if number of jars is 0 or less from the amount of jars in your application check **sl.workspace** parameter and verify it's correct and the jars are in that folder

if number of classes is 0 or low check the **sl.includes** parameter and verify it's in your application packages structure.&#x20;



If further assistance is required, please [contact Sealights Support](../../../../contact-sealights-support/).

## Next Step

You're now ready to [perform a quick Manual](../../running-your-tests/manual-tests/manual-tests-reported-via-the-dashboard-widget.md) Test to ensure the Sealights agent can capture coverage properly.

After the coverage is captured from Manual Tests, you're set to [integrate with your Test Automation framework](../#step-2-integrate-into-the-test-runner).

[^1]: Use a text editor and search for "scan report"
