# Step 2: Preparing for Integration

The following prerequisites have to be completed before starting the deployment:

1. Verify that you have an account in Sealights. For instructions on how to create an account, refer to the [account creation](../administration/account-management/#creating-a-new-sealights-account) page.
2. Onboarding requires DevOps or Admin permissions in the Sealights Platform. [Please verify that you have the right permission](../administration/account-management/role-based-access-control/onboarding-permissions.md).
3. Verify that the environment[^1] of the system under test and the machine(s) that run the test have connectivity to Sealights Cloud. See the [How to verify connectivity](../check-the-connectivity-to-the-sealights-server-from-my-machine.md) guide for more information.
4. Installing Sealights requires modifying your application components' deployment scripts and possibly the CI Job that runs your tests. Please verify you have the necessary permissions in your organization.

Once these items are ready, [installing an agent](step-3-collecting-code-coverage.md) on your application under test is the next step.

[^1]: A set of machines/containers that are hosting your System Under Test (SUT).&#x20;
