# Manual Tests reported via the Dashboard Widget

While a manual tester is performing a test, the relevant information about the test should be passed to Sealights via the Dashboard Widget.

There are three ways to ‘let the Sealights know’ which test is being performed by the tester:

1. Enter a single test name to the extension each time
2. Upload a list of tests from a CSV file
3. Use the tests recommended by the TIA engine for the build that is being tested

In any of the options, once the test is performed, it is registered by the system in the same way and is used for the production of recommendations for the next build in the branch

## _**Entering a single test name to the extension each time**_

1. Click on the “Manual Test” button<img src="../../../../.gitbook/assets/image (2).png" alt="" data-size="line"> on the top right corner of your Dashboard page.&#x20;
2.  Choose the 'By Lab' option in the top radio button and make sure the selected identifier matches the one defined in the parameters to the Sealights agent attached to your application under test. This will ensure all your Sealights agents are synchronized.



    <figure><img src="../../../../.gitbook/assets/image (12).png" alt="" width="218"><figcaption></figcaption></figure>
3. In the Test Details section, enter the test stage and, optionally a test suite. Typically, the Test stage would be 'Manual Tests'.
4.  Choose the radio button “single test” and enter the test name you're about to execute. If the test was previously run and reported to SeaLights, an auto-complete will help you find it quickly.\


    <figure><img src="../../../../.gitbook/assets/image (17).png" alt="" width="207"><figcaption></figcaption></figure>
5. Click on 'Start'<img src="../../../../.gitbook/assets/image (1) (1).png" alt="" data-size="line"> and begin the execution of your test.

After the click on start, the interface will minimize and will only show the name of the test that is being performed.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt="" width="241"><figcaption></figcaption></figure>

When the manual test had been completed, it is necessary to notify Sealights about it:

1. Click on the stop button in order to finish the execution of the test, and enter the result.
2. Once the result is entered click on “Submit and done” to save the test, click on 'Done' if you have finished, or enter the next one if you wish to continue performing more tests one by one.
   * If you are performing a list of tests, click on “Submit and start the next test”

{% embed url="https://www.loom.com/share/48582c58ddd744e49f184d433569a337" %}

{% hint style="success" %}
At the completion of your Manual Test, after the necessary time for computation (up to 60 seconds), you should see a coverage percentage associated with your application entry in the Dashboard.
{% endhint %}
