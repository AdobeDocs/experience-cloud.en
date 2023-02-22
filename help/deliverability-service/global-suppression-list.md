---
title: Global suppression list
description: Discover the global suppression list
hide: yes

---
# Global suppression list {#global-suppression-list}

A suppression list consists of email addresses that customers want to exclude from their deliveries, because sending to these contacts could hurt their sending reputation and delivery rates. Presently, Adobe keeps an updated list of known bad email addresses which have been proven to be detrimental to engagement and mailing reputation, and ensures emails are not delivered to them. This list is managed in a global suppression list which is common across all Adobe customers. The addresses and domain names contained in the global suppression list are hidden. Only the number of excluded recipients is indicated in the delivery reports.

It is now possible to manage the global suppression list from an interface that is available internally. This list will be maintained by Deliverability consultants only. The global suppression list can include email or domain addresses.

## Access the global suppression list

To access the detailed list of excluded email addresses and domains, go to **[!UICONTROL Gloabl suppression list]**.

>[!CAUTION]
>
>Permissions to view, export and manage the global suppression list depend on the distribution list your are assigned to. Learn more

Two tabs are displayed: **[!UICONTROL Email]** and **[!UICONTROL Domain]**.

Filters are available to help you browse through the list.

## Add addresses and domains

Currently there are two ways addresses are added to the global suppression list:

* List curated by the deliverability team.
* List provided by the third-party service provider Blackbox.

You may add email addresses or domains [one at a time](#add-one-address-or-domain), or [in bulk mode](#upload-csv-file) through a CSV file upload.

To do this, select the **[!UICONTROL Add email or domain]** button, then follow one of the methods below.

### Add one address or domain {#add-one-address-or-domain}

1. Select the **[!UICONTROL One by one]** option.

1. Choose the address type: **[!UICONTROL Email address]** or **[!UICONTROL Domain address]**.

1. Enter the email address or domain you want to exclude from your sending.

    >[!NOTE]
    >
    >Make sure you enter a valid email address (such as abc@company.com) or domain (such as abc.company.com).

1. Specify a reason if needed.

    >[!NOTE]
    >
    >All ASCII printable characters comprised between 32 and 126 are allowed in this field. The full list can be found on [this page](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} for example.

1. Click **[!UICONTROL Submit]** to confirm.

### Upload a CSV file {#upload-csv-file}

1. Select the **[!UICONTROL Upload CSV]** option.

1. Download the CSV template to use, which includes the columns and format below:

    ```
    TYPE,VALUE,COMMENT
    EMAIL,abc@somedomain.com,Comment
    DOMAIN,somedomain.com,Comment
    ```

    >[!CAUTION]
    >
    >Do not change the names of the columns in the CSV template.
    >
    >The file size should not exceed 1 MB.

1. Fill in the CSV template with the email addresses and/or domains you want to add to the suppression list.

    >[!NOTE]
    >
    >All ASCII characters comprised between 32 and 126 are allowed in the **Comment** column. The full list can be found on [this page](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} for example. 

1. Once completed, drag and drop your CSV file, then click **[!UICONTROL Submit]** to confirm.

>[!NOTE]
>
>Once the upload is done, make sure it was successful by checking its status from the interface. [Learn how](#recent-uploads)

### Check recent uploads status {#recent-uploads}

Click the **[!UICONTROL Recent uploads]** button to check the status of the latest CSV files you uploaded..

Possible statuses are:

* **[!UICONTROL Pending]**: The file upload is processing.
* **[!UICONTROL Error]**: The file upload process failed due to a technical issue or to a file format error.
* **[!UICONTROL Complete]**: The file upload process was successfully completed.

During the upload, if some addresses are not in the correct format, they are not added to the global suppression list.

In that case, when the upload is complete, it is associated with a report. You can download it to check the errors encountered.

## Remove addresses

To remove an address from the gloabl suppression list, use the **[!UICONTROL Delete]** button.

>[!CAUTION]
>
>Addresses or domains automatically added by the third-party service provider Blackbox cannot be removed by consultants through the interface. This can be done via a backend ticket only.

