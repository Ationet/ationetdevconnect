# Commander configuration for Loyalty (External Host)


## Important Prerequisites

In this section you’ll find our recommended steps to be taken into consideration before
starting the Loyalty configuration itself.

### Firewall
Take into consideration that some networks may have been deployed under a firewall
system (e.g.: Cybera), so ensure that all **IPs** provided in this document and their
associated **Ports,** are correctly configured in your firewall’s whitelist. Please contact your
network administrator to get this done.


### Fuel codes
Please make sure to have at hand the list of all fuel products and their corresponding
codes configured in Commander. 

To obtain this information inside the Commander, go to: **Store Operation ->
Merchandise -> Product Codes**. <br>

<img width="849" height="489" alt="image" src="https://github.com/user-attachments/assets/a81a5662-94bf-4f7a-9a15-58f9c7e6bd55" />



## Step 1

Within this section you will be able to configure the IP address and port of ATIONET loyalty
Gateway. You will also need to configure the Dealer ID, which is used to identify the terminal. This code must be provided by ATIONET in advance.

Inside the commander configuration, go to: **Payment Controller** -> **EPS Configuration**
-> **PCATS** ****0**** **x** **Loyalty configuration**
You can choose any PCATS (from 1 to 4) to configure this information.

<img width="556" height="686" alt="commander eps 1" src="https://github.com/user-attachments/assets/41dd92f8-b739-4409-a01f-0c255aa25607" />

> **Note:** _Dealer ID and Program name provided in this image is for guidance purposes only._

- **Dealer ID:** Input the **Terminal/Controller Code** provided by the ATIONET team
- **IP/Domain Name:** 4.227.34.236
- **Ports:** 35176 (BETA environment) / 35166 (PROD environment)



## Step 2

Now the Loyalty section needs to be enable in the Commander. For that, go to:
**Payment Controller** -> **POS Configuration** -> **POS**

Make sure all the parameters match the same values as shown in the following image:

<img width="746" height="803" alt="image" src="https://github.com/user-attachments/assets/f39dc565-3b6b-404c-8f5b-5a738bcebf10" />

> **Note:** _Batch Close Period shown on the image is for guidance purposes only. The default config in Commander should be “Daily”._




## Step 3

Go to: **Payment Controller -> EPS Configuration -> EPS Global Configuration** ->
**Loyalty**

Make sure all the parameters match the same values as shown in the following image:
<img width="865" height="672" alt="image" src="https://github.com/user-attachments/assets/9cdfaa2f-0467-4dc9-89af-bba7fbabbb14" />



## Step 4

Finally, the Loyalty cards need to be configure inside the Commander. To do so, go to:
**Payment Controller -> EPS Configuration -> Loyalty Card Configuration**

In this tab we need to configure the BIN range used for the **Loyalty Cards Identifications**, so that the Commander recognized them as Loyalty, during a
transaction.

<img width="717" height="544" alt="image" src="https://github.com/user-attachments/assets/d7e33d9a-4dcf-4c9f-9eb0-3dfec56934c6" />



Complete the **Lower ISO** and **Upper ISO** fields with the proper BIN range of the cards (they can be left empty).
Also select the proper **Supported FEPs** option with the same value as chosen in **Step 1** .



## Step 5

Now that everything is correctly configured, we recommend confirming that the Loyalty
module is ONLINE. For that, inside the Commander go to: **Tools -> Helpdesk
Diagnostics -> General**.

<img width="668" height="328" alt="image" src="https://github.com/user-attachments/assets/776a2cc1-2abb-474a-b926-218a2ff3d660" />


> **Note:** _You may need to reboot Commander (consider that this procedure could take a couple of minutes)._





## Congratulations!

After configuring and saving all the aforementioned parameters, the connection
between the Commander controller and ATIONET’s Loyalty gateway is now enabled.

To see the operation flow go [here](Commander_Config_ATIONET_Host.md).

In case of any questions or concerns regarding these procedures, please contact
[support@ationet.com](mailto:support@ationet.com) for assistance.




