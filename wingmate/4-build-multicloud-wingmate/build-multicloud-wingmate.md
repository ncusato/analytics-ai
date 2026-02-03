# Lab 3: Build a RAG Chatbot using Low-Code APEX

## Introduction

This lab walks the user through the creation of a multicloud Wingmate dashboard. This is helpful for managing compute and resources across multiple cloud service providors. 

Estimated time - 20 minutes

### Objectives

* Build a Multicloud Page of Wingmate App
* Load Synthetic Data to populate the App
* Test the App's Chat Feature

### Prerequisites

* Completed the first lab
* Some SQL knowledge is perfered but not necessary

## Task 1: Build a Multicloud Page of Wingmate App 

1. Use the existing template from Compute Wingmate to make the MultiCloud Wingmate by selecting the plus sign in the top right of the page and select **Copy Page**.

	![navigate home buttons](./images/copy-page.png "")

2. Select **Next** to use the existing page.

	![create page button](./images/copy-page-next.png "")

3. Name the page **MultiCloud Wingmate** and select **Next**.

	![name the page](./images/copy-security.png "")

4. Select **Create a new navigation menu entry** and **Next**. Leave menu entry as _No parent selected_.

	![name page and next button](./images/nav-wingmate.png "")

5. Rename Security to MultiCloud in the highlighted sections for value and static-id and select **Copy**.

	![rename value and id and copy button](./images/rename-security.png "")

6. Update AI Assistant, by navigating to **Show AI Assistant** in the navigation tree under MultiCloud Wingmate Region -> StartWingmate -> Chat -> Show AI Assistant. Update System Prompt with following:

	```
	<copy/>
	I want you to be an OCI compute expert who is providing guidance to the customers about resource capacity planning best practices. 
	The following list is the oci compute host insights details we have captured, please use these compute metrics data for answering questions. 
	--------
	&P3_OCI_HOSTINSIGHTS_DETAILS.
	--------
	The following list is the OCI documentation references for compute, please use these documentation references for answering recommendation related questions.
	--------
	&P3_OCI_DOC_REF_COMPUTE.

	</copy>
	```

	>**Note:** Ensure you update the refence page number if its not matching. ie. &P3_OCI_DOC_REF_COMPUTE -> &P4_OCI_DOC_REF_COMPUTE

Update the **Welcome Message** from OCI Security Wingmate to OCI MultiCloud Wingmate as well.

7. Navigate to the bottom of the Navigation Tree to the hidden items. Select the OCI_CLOUDGUARD and rename it to **P4_OCI_HOSTINSIGHTS_DETAILS** on the right side Indentification. 

	![select hidden value](./images/select-hidden.png "")

	![rename hidden](./images/update-hidden.png "")

8. Update the computation as the following:

	```
	<copy/>
	Select CONTEXT_PROMPT FROM oci_doc_ref_compute_sv
	</copy>
	```

	![update computation](./images/update-computation.png "")

9. Create another **Hidden Item** by right clicking **P4_HOSTINSIGHTS_Listed**, selecting **Duplicate** and name it: **P4_OCI_HOSTINSIGHTS_DETAILS** 

	![create hidden item](./images/duplicate-hidden.png "")

	![host insights hidden value](./images/update-hostinsights-name.png "")

10. Right Click **P4_OCI_HOSTINSIGHTS_DETAILS** and select **Create Computation**. Paste this under **SQL Query** on the right side:

	```
	<copy/>
	Select CONTEXT_PROMPT FROM hostinsights_report_sv
	</copy>
	```

	![host insights hidden value](./images/update-hostinsights-computation.png "")

10. Repeat **Step 9** to create another hidden item named **P4_OCI_DATABASE_DETAILS**

	![create hidden item](./images/duplicate-hidden-details.png "")

	![host insights hidden value](./images/update-hostinsights-computation.png "")

11. Right Click **P4_OCI_DATABASE_DETAILS** and select **Computation**. Paste this under SQL Query:

	```
	<copy/>
	SELECT CONTEXT_PROMPT FROM CIS_MULTICLOUD_DETAILS_V
	</copy>
	```

12. 


Thank you for completing this lab.

## Acknowledgements

* **Authors:**
	* Royce Fu - Master Principle Cloud Architect
	* Nicholas Cusato - Cloud Architect
* **Last Updated by/Date** - Nicholas Cusato, Febuary 2026