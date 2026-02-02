# Build a Wingmate on AI Database 26ai 

## Introduction

This lab walks the user on how to provision an Autonomous AI Database, generate API keys, and use these keys to connect Oracle GenAI services to the APEX application. Using synthetic data, the Security and Multicloud data will be modeled in the database as a reference for the GenAI services. Additionally, RESTful data collection from the tenancy can collected to generate live reporting of the Tenancy. This provides the Wingmate Application a streamlined observability into the tenancy operations using natural language.

> **Note:** For reference, the list of available APIs that can be utilized for the optional Lab #7: [OCI API Reference and Endpoints](https://docs.oracle.com/en-us/iaas/api/)

Estimated time - 20 minutes

### Objectives

* Provision a Oracle AI Database 26ai ADB and APEX App
* Generate API Keys
* Update the Credentials to Connect to OCI Resources
* Create GenAI Service
* Create the Application
* Load Synthetic Data
* (Optional) Connect RESTful data from Tenancy

### Prerequisites

* An OCI cloud account
* Subscription to US-Central Chicago, US-Ashburn-1, or US-Phoenix-1 Region

## Task 1: Provision a Oracle AI Database 26ai ADB  and APEX App

1. Navitage to the OCI home console and expand the side-menu bar.

	![home menu bar](./images/home-menu.png "")

2. Select the **Oracle Database** and click the **Autonomous Database** Option.

	![Navigate to Autonmous Database](./images/nav-adb.png "")

3. Ensure you are in the correct compartment and select **Create Autonmous AI Database**. The region in which you provision the ADB doesn't matter as much as the previous GenAI services Lab as the ADB will use the service route to access the model. 

	![Console create ADB button](./images/create-adb-button.png "")

4. Give the ADB a unique name, such as **WINGMATE**, select database version **26ai**, and provide a password. Leave everything else as default and click **Create**.

	![Name the ADB](./images/name-adb.png "")

	![Choose database version dropdown](./images/choose-26ai.png "")

5. Navigate to the newly created ADB by selecting the name that you provided, then click the **Tool Configuration** tab and select the Public Access URL **Copy** button for Oracle APEX. Paste that in a new tab.

	![Copy URL for APEX app](./images/open-apex.png "")

6. Enter your password used during the creation of the ADB and click **Sign in to Administration**.

	![Signin to Admin Portal](./images/access-admin.png "")

7. Create a new workspace by clicking **Create Workspace**.

	![Create workspace button](./images/create-workspace.png "")

8. Create a new schema by clicking the **New Schema** button.

	![New Schema button](./images/new-schema.png "")

9. Enter the following credentials and click **Create Workspace**.
	* **Workspace Name:** *WINGMATE*
	* **Workspace Username:** *WINGMATE*
	* **Workspace Password:** *Welcome2Oracle* (or choose a secure password that you will remember)

	![Create Credentials for Workspace](./images/workspace-creds.png "")

10. Sign out of the admin management by selecting the profile button on the top right and click **Sign out**

	![Sign out of admin console](./images/sign-out-admin.png "")

11. Click **Return to Sign in Page** 

	![Return to sign in page button](./images/return-sign-in.png "")

12. Sign in using the new credentials:
	* **Workspace Name:** *WINGMATE*
	* **Workspace Username:** *WINGMATE*
	* **Workspace Password:** *Welcome2Oracle* (or whichever password you chose to remember)

	![Sign in workspace credentials](./images/sign-in-workspace.png "")

## Task 2: Generate API Keys

1. Navigate back to the OCI console and click your profile icon on the upper-right-hand side of the screen. Select **User Settings**. 

	![Profile menu button](./images/profile.png "")

2. On the menu in the center, select **tokens and keys**.

	![Menu button on profile](./images/tokens-and-keys.png "")

3. Make sure **Generate API Key Pair** is selected. Download your private & public key because you will need these for later. After downloading, select **Add**. You will see a configuration file preview, you can save this on a notepad as it will helpful in the next lab. You may proceed to the next lab. 

	  ![Create Bucket button](./images/save-key.png "")

## Task 3: Update the Credentials to Connect to OCI Resources

1. Click **App Builder** to access the Web Credentials.

	![App Builder Button](./images/app-builder.png "")

2. Click the **Workspace Utilities** button.

	![Workspace Utilities button](./images/workspace-utilities.png "")

3. Click the **Web Credentials** button.

	![Web Credentials Button](./images/web-credentials.png)

4. Click **Create** to update your web credentials.

	![Web Credentials Create button](./images/create-web-credentials.png "")

5. Change the Authentication Type to **OCI Native Authentication**. Paste the information collected on the notepad in the previous lab into the cooresponding fields (be sure to name the credentials and static ID: **api_key**). 
Additionally under **Valid for URLs** include the following endpoint for the GenAI Service and select **Create**: 
	```
	<copy>https://inference.generativeai.us-chicago-1.oci.oraclecloud.com</copy>
	```
* **Note:** Be sure this matches the subscribed region which hosts GenAI Services. 

	![api_key credentials for oci access](./images/save-api-key-creds.png "")

## Task 4: Create GenAI Service

1. Navigate back to the **Workspace Utilities** by selecting the first menu option on the breadcrub bar.
	
	![breadcrub bar for workspace utilities](./images/nav-utilities.png "")

2. Select **Generative AI button** to navigate to configure the services.
	
	![genai services button on workspace utilities](./images/genai-services-button.png "")

3. Create a GenAI service by selecting the **create** button.

	![create button on genai service console](./images/create-genai-service.png "")

4. Name the service **OCI_GENAI** and 

## Task 5: Create the Application

1. Navigate back to the App Builder by selecting the menu button **App Builder**.

	![App Builder Button](./images/nav-app-builder.png "")

2. Create an application by selecting the **create** button.

	![create button on console](./images/create-app.png "")

3. Name the App **WINGMATE** and click **Create Application**.

	![Naming of the App](./images/name-app.png "") 

## Task 6: Load Synthetic Data 

1. Navigate to the SQL Workshop by pressing the **SQL Worshop button** at the top, and then **SQL Scripts**.

	![SQL Workshop button](./images/sql-workshop.png "")


2. Select **Upload** and upload **wingmate-ddl.sql** in the popup.

	![Upload DDL script and run button](./images/execute-ddl-script.png "")

	![load DDL script and upload button](./images/upload-script.png "")


2. Click the **Run button** to execute the script.

	![Run button](./images/run-sql.png "")

3. Confirm the run script by clicking **Run Now** on the popup at the bottom. 

	![Confirm button](./images/confirm-run.png "")

4. Verify the script ran to completion.

	![Sucessful DDL](./images/ddl-complete.png "")

	>**Note:** If you see any errors, validate the error and identify if any conflicts exists with any tables/views.

5. Navigate to Object Browser by clicking **SQL Workshop** and select **Object Browser**. 

	![load csv navigation](./images/data-workshop.png "")

6. Observe the new tables created and select the first one **CIS_IAM_POLICIES**, and select **Data** and **Load Data** in the center module.

	![load data in tables](./images/data-loading.png "")

7. Verify that the columns are automatically mapped and hit the green **Load Data** button at the bottom. 

	![confirm data load](./images/load-data.png "")

5. Repeat for each table with each dataset located in the unzipped directory.

## Task 7: (Optional) Connect RESTful data from Tenancy

1. Navigate back to the application by selecting **App Builder** and then the **OCI Wingmate** app name.

	![Navigate to the Application](./images/nav-back-app.png "")

2. Select **Shared components** to navigate to the RESTful operations.

	![Navigate to the shared components](./images/shared-components.png "")

3. Select **REST Data Sources** under Data Sources.

	![Navigate to the REST Data Sources](./images/rest-data-services.png "")

4. Select **Create** to create your first RESTful data source.

	![Create RESTfull Data source Button](./images/create-rest-button.png "")
	
5. Select **Next** to create RESTful Data source from scratch.

	![Create RESTfull Data source from scratch button](./images/create-from-scratch.png "")

6. Name the service, such as the following **HostInsightsSummary** and paste an endpoint URL for example: 
* **https://operationsinsights.us-ashburn-1.oci.oraclecloud.com/20200630/hostInsights/resourceStatistics**

	> **Note:** For full list of endpoints, please check [Oracle Docs](https://docs.oracle.com/en-us/iaas/api/).
	
	Select **Next**.

	![Create RESTfull Data source from scratch button](./images/endpoint-name.png "")


7. Validate the endpoint and select **Next**.

	![Next button for remote server](./images/remote-server.png "")

8. Select **Next** if no pagination is likely true.

	![Next button with no pagination](./images/no-pagination.png "")

9. Select the qualified credentails that allow for API queries of the tenancy. Select **Next**.

	![Set credentials for Rest](./images/credentials-rest.png "")

10. Navigate back if the endpoint requires parameters by selecting **back arrow**.

	![Discovery Error](./images/discovery-error.png "")

11. Select **Advanced** to define the parameters.

	![Advanced Data Discovery](./images/advanced-data-source.png "")

12. Insert the required parameters and select **Discover**.

	![Header Compartment Example](./images/header-compartment.png "")

	>**Note:** If the response says not authorized, navigate back to the credentials and select the correct credentials. This might require going back to Task 3 and creating a separate Web Credential for API, distinct from the GenAI service. Additionally, manage resource permissions are necessary for utilizing the API.

	![Example Not Authorized Error](./images/not-authorized.png "")

13. Validate a successfull data source discovery matches the expected profile. Select **Create REST Data Source** to finish the creation process for the REST endpoint. 

	![Host details of successful discovery](./images/host-details.png "")

	>**Note:** If not all columns are mapped, select **Configure button** to make sure it maps correctly.

	![Configure map button](./images/configure-columns.png "")

	![unmapped column](./images/unmapped-column.png "")

You may now **proceed to the next lab**.

## Acknowledgements

* **Authors:**
	* Royce Fu - Master Principle Cloud Architect
	* Nicholas Cusato - Cloud Architect
* **Last Updated by/Date** - Nicholas Cusato, Febuary 2026