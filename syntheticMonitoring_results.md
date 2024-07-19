# Synthetic monitoring

Last Updated: 2024-07-09

Synthetic monitoring, also known as active monitoring or proactive monitoring, can simulate actions that a user takes on an application from different locations and continuously monitor at a specific interval for performance characteristics such as availability and response time.

Instana Synthetic monitoring, which is built on the product Instana, provides a fully integrated solution with other Instana capabilities. By using Instana Synthetic monitoring, you can create Synthetic tests to monitor an application.

*   Do you want to monitor the availability of your websites? Write an API Simple test.
    
*   Do you want to monitor the APIs of your application? Write an API Script test.
    
*   Do you want to check your webpage for HTTP errors? Write a Browser Simple test.
    
*   Do you want to imitate user interactions with your web pages? Write a Browser Script test.
    
*   Do you want to check when the certificate for your webserver expires? Write an SSL Certificate Check test.

These Synthetic tests can be configured to run at specific continuous intervals. You can also create a Smart Alert to inform you if the Synthetic tests fail.

The tests can be configured to run on a Point of Presence (PoP) that you deploy or a PoP provided by Instana.

To get started, determine the type of PoP you will use, create a Synthetic test through the Instana UI or Open APIs, and assign the test to the location that represents the Synthetic PoP. For more information, see [Getting started](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#getting-started).

*   [General information](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#general-information)
*   [Terminology](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#terminology)
*   [Getting started](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#getting-started)
*   [Deciding where to run Synthetic tests](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#deciding-where-to-run-synthetic-tests)
*   [The Synthetic monitoring user interface](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#the-synthetic-monitoring-user-interface)
*   [Setting permissions for Synthetic monitoring](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#setting-permissions-for-synthetic-monitoring)
*   [Security for Synthetic test scripts](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#security-for-synthetic-test-scripts)
*   [Monitoring endpoints with Synthetic tests](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#monitoring-endpoints-with-synthetic-tests)
*   [Using API scripts](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#using-api-scripts)
*   [Using browser scripts](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#using-browser-scripts)
*   [Instana integration](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#instana-integration)
*   [Synthetic CLI command](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#synthetic-cli-command)

## General information

Synthetic monitoring is supported on Instana SaaS. For self-hosted (on-premises) Instana, Synthetic monitoring is supported on Standard Edition and Custom Edition.

  

**Notes:**

*   You need to choose the type of PoP you will use to run the tests. You can deploy a self-hosted PoP or update your license to gain access to an Instana-hosted PoP. Additional charges apply for using an Instana-hosted PoP. No additional charges apply for using a PoP that you deploy.
*   Synthetic test result data will be retained in the Instana backend for 60 days.

## Terminology

Point of Presence (PoP): A PoP is an agent where Synthetic tests are run. When the PoP is deployed, it registers itself with the Instana backend as a 'location'. Deployment implies the PoP and the Synthetic test configuration implies the 'location' configuration.

Instana 269 and later support two types of PoPs and corresponding locations.

*   You can deploy a PoP in your establishment; it is known as the self-hosted PoP (or private PoP). After the PoP is deployed, it registers with the server as a **Private** location.
*   You can use a PoP provided by Instana; it is known as the Instana-hosted PoP. Instana-hosted PoP registers with the server as a **Managed** location.

Datacenter: The representation of geographic regions where Instana-hosted PoPs are supported.

Activation: The activation represents deploying and managing a Synthetic PoP in a selected datacenter for a tenant unit. You must initiate the activation on the Synthetic Monitoring page on the Instana UI.

Synthetic tests: A Synthetic test is code that you write that simulates the way your end-users use your applications. Multiple types of Synthetic tests are supported:

*   API Simple test: The test to check a single REST API. An HTTP GET request is sent to a URL to confirm that it is responsive. The test fails if the return code is not in the range of successful HTTP return codes.
*   API Script test: The test to check the sequence of multiple REST APIs. Multiple API requests are sent to an application to confirm that the responses are expected. The return codes and the content of the response are evaluated.
*   Browser Simple test: a test to check a single web page for HTTP errors.
*   Browser Script test: a test to check web applications. The actions that users take on your web pages are simulated. Browser Script tests include Node.js based [browser scripts](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/browser_script/browser_script.html) or [Selenium IDE scripts](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/browser_script/selenium_ide_script.html).
*   SSL Certificate test: a test to check whether the certificate for a web server is approaching expiration. Set the number of days before certification expiration when you want to be notified by a test failure.

After the Synthetic test is created, and assigned to one or more 'locations' with a specified frequency, the PoP will begin to run the test on the requested schedule. For each run, the PoP will send the results of the test to the Instana backend as a Synthetic test result. Each test result might have some additional details, such as logs or subtransactions. Additional details are not available for every test type. If details are available, the information is sent to the Instana backend separately as Synthetic test result details. In summary, each Synthetic test has a result for each run, and each test result might contain additional details.

  

**Note**

By using the Open API, you can create API Simple tests that use additional HTTP methods including `GET`, `HEAD`, `OPTIONS`, `PATCH`, `POST`, `PUT`, and `DELETE`. Test creation in the Instana UI supports only the `GET` method.

## Getting started

When you click the Synthetic monitoring icon in the main navigation menu, you will see a page that lists the Synthetic tests that you created. You can also see a **Locations** tab, an entry is added in the tab if you deploy your self-hosted PoP. If you cannot see the Synthetic monitoring icon, refer to [Setting permissions for Synthetic monitoring](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#setting-permissions-for-synthetic-monitoring).

To get started with Synthetic monitoring, first you need to work with the Synthetic PoP. Refer to [Deciding where to run Synthetic tests](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#deciding-where-to-run-synthetic-tests)

To use a self-hosted PoP, complete the following steps:

1.  Prepare the environment to run the PoP.
2.  Download the helm charts.
3.  Deploy the PoP. Install an Instana agent on the same Kubernetes cluster where you deploy the PoP. For more information, see [Deploying a self-hosted PoP](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/pop_deployment.html).

To use an Instana-hosted PoP, complete the following steps:

1.  Update your license. Contact IBM Sales to update the license.
2.  After the license is updated, go to **Synthetic Monitoring** and initiate a request to deploy an Instana-hosted PoP for using with your tenant unit.
3.  Complete the steps that are covered in [Using an Instana-hosted PoP](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/synmon_managed_location.html).

After a PoP is deployed either by you or by Instana, you can check the **Locations** tab in the Instana UI to confirm that the PoP location is successfully registered. You can also use the Open APIs to confirm whether the PoP location is registered.

*   For a self-hosted PoP, if the **Private** location does not appear or you get an empty response in the Open API, you can check the logs of the PoP controller. For more information, see [PoP Deployment Troubleshooting](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/pop_deployment.html#troubleshooting).
*   For an Instana-hosted PoP, it might take up to 10 minutes for each queued activation request to process before the managed location appears. If the location does not appear after 20 to 30 minutes, open a support case for IBM Support to investigate the status of the deployment.

After the location is registered, you are ready to create Synthetic tests. You can either use the **Add** > **Add Synthetic Test** buttons in the Instana UI or use the Open APIs to create your Synthetic tests. Creation of the Synthetic test includes specifying how frequently the test will run and the location where it will run.

To ensure security for your Synthetic tests, see the instructions in [Setting permissions for Synthetic monitoring](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#setting-permissions-for-synthetic-monitoring) and [Securely using Synthetic test scripts](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-synthetic-monitoring#security-for-synthetic-test-scripts).

For more information about how to write scripted API (HTTPScript) tests, see the [API Script documentation](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/api_script.html).

For more information about how to write scripted browser test, see the [Browser Script document](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/browser_script/overview.html).

For more information about the Open APIs for Synthetic monitoring, see the **Synthetic Monitoring** section of the [Open API documentation](https://www.ibm.com/links?url=https%3A%2F%2Finstana.github.io%2Fopenapi%2F%23tag%2FSynthetic-Settings). All the views that you can see in the Instana UI can also be retrieved by using the Open APIs.

When you see that your Synthetic test is running as expected, and Synthetic test results are being sent to the Instana backend, you might wish to create an alert that indicates whether the test has failed. For information and instructions about creating alerts for Synthetic tests, see [Smart Alerts for Synthetic monitoring](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/smart_alerts.html).

## Deciding where to run Synthetic tests

With Instana 269 and later, you can run your tests by using a self-hosted PoP or an Instana-hosted PoP.

A self-hosted PoP is deployed in your private network. You can deploy, maintain, and manage the PoP to run tests. It is included as part of your Instana license. You can use a self-hosted PoP for the following purposes:

*   Monitor applications that are not publicly available
*   Run the tests from your own specific locations or offices

An Instana-hosted PoP is a managed PoP. Instana deploys, maintains, and manages the PoP to run tests. It is an add-on to your Instana license with additional fees. You can use an Instana-hosted PoP to monitor applications that are publicly available.

Determine the type of PoP that you want to use.

*   To deploy a self-hosted PoP, see [Deploying a Self-hosted PoP](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/pop_deployment.html).
*   To use Instana-hosted PoP, see [Using an Instana-hosted PoP](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/synmon_managed_location.html)

## The Synthetic monitoring user interface

For a detailed explanation of the pages for Synthetic monitoring in the Instana UI, see [Using the user interface](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/synmon_ui.html).

## Setting permissions for Synthetic monitoring

Before you set the permissions for Synthetic monitoring, you need to log in Instana UI with a user ID that has the **Owner** level permissions so that you can set the permissions for yourself or others. Alternately, you can ask another user with **Owner** permissions to give you the permissions for Synthetic monitoring. For more information about setting permissions to use Synthetic monitoring, see [Permissions for Synthetic monitoring](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/synmon_permissions.html).

## Security for Synthetic test scripts

Before you set the permissions for Synthetic monitoring, familiarize yourself with the requirements for securing Synthetic tests; see [Securely using Synthetic test scripts](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/synmon_security.html).

## Monitoring endpoints with Synthetic tests

You can monitor endpoints by creating and managing Synthetic tests and Smart Alerts for such tests.

For more information about monitoring endpoints, see the [Monitoring endpoints with Synthetic tests](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/mon_endpoints.html) section.

## Using API scripts

For guidance about writing an API Script Synthetic test, see the [API Script Guide](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/api_script.html).

## Using browser scripts

Instana browser testing is supported for Synthetic PoP Helm chart 1.0.15 or later.

A new playback engine is used to run these tests. You must upgrade your Synthetic PoP version to 1.0.15 or later to enable the browser playback engine.

Instana browser testing supports Browser Simple test and Browser Script test. For more information, see [Browser Script document](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/browser_script/overview.html).

## Instana integration

Synthetic monitoring is integrated with some other capabilities of the Instana product including Applications, Events and Kubernetes monitoring. For more information, see the **Instana integration** section of [Monitoring endpoints with Synthetic tests](https://www.ibm.com/docs/en/SSE1JP5_current/src/pages/synthetic_monitoring/mon_endpoints.html#instana-integration).

## Synthetic CLI command

You can use the `synctl` CLI commands to manage Synthetic tests, locations, and credentials. For example, you can create a Synthetic test by using a CLI command. For more information, see the [Readme file](https://www.ibm.com/links?url=https%3A%2F%2Fgithub.com%2Finstana%2Fsynthetic-synctl).
