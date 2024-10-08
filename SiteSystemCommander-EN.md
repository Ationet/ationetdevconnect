![ationetlogo](Content/Images/ATIOnetLogo_250x70.png)
# Ationet Fleet Mobile Payment Fully Integrated #

|Document Information||
|--- |--- |
|File:|ATIONet - Dynamic QR Code Payments|
|Doc Version:|1.0|
|Release Date:|26, August 2021|
|Author:|ATIONet LLC|

|Change Log|||
|--- |--- |--- |
|Ver.|Date|Change Summary|
|1.0|26/August/2021|Initial version.|


## Contents ##

- [Overview](#overview)
	- [Introduction](#introduction)
	- [Entities](#Entities)
	- [Sequence diagram Pay at Pump with Above Site Payment Authorization](#Sequence-diagram-Pay-at-Pump-with-Above-Site-Payment-Authorization)
- [Site System configuration](#Site-System-configuration)
	- [STEP 1 Site Mobile Configuration](#STEP-1-Site-Mobile-Configuration)
	- [STEP 2 Host Mobile Configuation](#STEP2-Host-Mobile-Configuation)
	- [Values descriptions](#Values-descriptions)
- [Status Codes and Messages](#Status-Codes-and-Messages)
</br>


><h3>IMPORTANT: The following document is only valid for the COMMANDER configuration.</h3>

</br>
<h3> For API documentation please visit <a href="ATIONet_Mobile_Payment_Fleet_Api_-EN.md">here.</a> </h3>
</br>

## Overview

![ationetTR](Content/Images/SiteSystemCommander/Complete_Diagram.png)

### Introduction

This Implementation Guide is intended to guide petroleum convenience retailers and their associated vendors when implementing mobile payment solutions consistent with
ISO 12812. 
</br>
>Note: ISO 12812 is document that will provide requirements, guidance and use cases for all stakeholders in the mobile payments arena.


### Entities

This section outlines the logical entities, including location options, for Mobile Payment and identifies possible physical architectures. The term “entity” is used in this
document to differentiate logical processing functionality without regard to its physical location in an implementation. 


```Mobile Payment Application (MPA):```  This entity is a software application embedded in a Mobile Device or downloaded by a consumer onto a Mobile Device, such as a smart
phone or tablet, which enables mobile payments for in-store and forecourt transactions.

```Mobile Payment Processing Application (MPPA):``` This entity is an application provided by the Mobile Payment Processor (MPP) not on the Mobile Device that is responsible for
interfacing between the Token Vault or Token/Trusted Service Provider, the MPA, the Site System, the Payment Front End Processor (PFEP), and the Loyalty Front End Processor (LFEP) in order to authorize transactions.

```Payment Front End Processor (PFEP):``` This entity is a host that facilitates the authorization of payment transactions between the MPPA or the Site System and the
Issuer networks. The standard does not dictate the processing that is performed by the PFEP for each payment method. This entity is sometimes referred to as the Front End
Processor (FEP).

```Site System:``` This entity encompasses the site equipment and components (hardware and software) and may perform the function of local card processing business rules,
such as consumer prompting, local velocity checking and receipt formatting and printing. Examples of site systems include Point of Sale (POS), Outside Sales Processor
(OSP), Electronic Payment Server (EPS) and Forecourt Device Controller (FDC).
</br>
>Note: MOBILE PAYMENT API is the common interface through which the MPA sends and receives requests from the MPPA. The description, the methods and how to consume this interface is not part of the scope of this document. You can read more about this <a href="ATIONet_Mobile_Payment_Fleet_Api_-EN.md">here.</a>


### Sequence diagram Pay at Pump with Above Site Payment Authorization 


![ationetTR](Content/Images/SiteSystemCommander/SiteSystem_secuencia3.svg)

<ol>
	<li>Mobile Payment Application (MPA) is activated by consumer.</li>
	<li>MPA determines location and fueling point.</li>
	<li>MPA sends information to MPPA as an Authorization Request.</li>
	<li>MPPA optionally sends a Mobile Pump Reserve Request to the Site System to reserve the fueling point.</li>
	<li>Site System responds to the Mobile Pump Reserve Request.</li>
	<li>The MPPA sends a Mobile Auth Request to the Site System. If generated, the validation code in the payload.</li>
	<li>The PFEP (through the site system) sends the Mobile Auth Response to the MPPA.</li>
	<li>The MPPA sends a Mobile Auth Request to Site Systen.</li>
	<li>The Site Systen response to MPPA with a Mobile Auth Response.</li>
	<li>MPPA sends an Authorizacion Response to MPA</li>
	<li>Mobile Begin Fueling Response is sent from MPPA to Site System.</li>
	<li>Site System sends a Mobile Loyalty Award Request message to give the MPPA the opportunity to adjust the rewards. This message is always sent after fueling as
the final amount is not determined until fueling is complete.</li>
	<li>The MPPA sends a response to the Site System with the additional rewards information.</li>
	<li>Site System sends Mobile Finalize Request to MPPA with completion information.</li>
	<li>MPPA sends Completion Request to PFEP.</li>
	<li>PFEP send Completion Response message to MPPA.</li>
	<li>MPPA sends Mobile Finalize Response to Site System. Note: If additional or
updated receipt information is included in this response, the Site System may
need to regenerate the receipt information.</li>
	<li>Site System sends receipt information to the MPPA.</li>
	<li> MPPA sends receipt information to MPA.</li>
	<li>Site System prints the receipt (if applicable).</li>
	<li>MPPA sends a receipt response back to the Site System.</li>
</ol>

## Site System configuration

```Commander``` will provide a ConfigClient screen for configuration of Mobile Payments. These details will be provided by MPPA to commander. The screen will provide for configuration options for Site Details, and host configurations and connectivity parameters. The image below is an example. Some Mobile Payments
Processing Applications might require more information than others.
</br>
>You have to request de configuration's values to ATIONet

### STEP 1 Site Mobile Configuration

</br>

```
Note: The values in the image are for example. You must request the corresponding values from ATIONet.
```
</br>

![ationetTR](Content/Images/SiteSystemCommander/configA.PNG)


### STEP 2 Host Mobile Configuation

</br>

```
Note: The values in the image are for example. You must request the corresponding values from ATIONet.
```
</br>


![ationetTR](Content/Images/SiteSystemCommander/configB.PNG)

### Values descriptions

</br>
<table>
	<thead>
		<tr valign="center">
			<th>
				Site configuration Information
			</th>
			<th>
				Description
			</th>
		</tr>
	</thead>
	<tbody>
		<tr valign="top">
			<td>
				<p align="left">Enable Host</p>
			</td>
			<td>
				<p align="left">Enable/Disable messaging to this particular host. If the box is not checked messages will not be sent to this particular host.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Adapter</p>
			</td>
			<td>
				<p align="left">Mobile payment APIs used by commander for communication with MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Program Name</p>
			</td>
			<td>
				<p align="left">Program name as defined by MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Authentication Type</p>
			</td>
			<td>
				<p align="left">Authentication mode supported by MPPA for that adapter.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Host IP address</p>
			</td>
			<td>
				<p align="left">IP address will be used by commander for communication with MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Port</p>
			</td>
			<td>
				<p align="left">Service Port will be used by commander for communication with MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">SSL Enabled</p>
			</td>
			<td>
				<p align="left">Commander uses this Boolean for SSL communication or no-SSL communication between commander and MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Site Terminal ID</p>
			</td>
			<td>
				<p align="left">This number is supplied by MPPA as terminal identification number.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Merchant ID</p>
			</td>
			<td>
				<p align="left">Merchant Id given to the store by the MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Location ID</p>
			</td>
			<td>
				<p align="left">Location ID is given by the MPPA which identifies a site of a merchant during on boarding process.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Settlement Employee Number</p>
			</td>
			<td>
				<p align="left">Number used by commander for settlement with MPPA.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Settlement Passcode</p>
			</td>
			<td>
				<p align="left">Password used during settlement assigned by MPPA.</p>
			</td>
		 </tr>
		</tbody>
</table>

</br>


<table>
	<thead>
		<tr valign="center">
			<th>
				Site Initiated Loyalty
			</th>
			<th>
				Description
			</th>
		</tr>
	</thead>
	<tbody>
		<tr valign="top">
			<td>
				<p align="left">Never Allow Site Entered Loyalty</p>
			</td>
			<td>
				<p align="left">If this option is selected, the site will be restricted to accepting loyalty only from the site or only from the MPPA. If a transaction already contains loyalty (i.e. the consumer has swiped a loyalty card prior to starting the mobile transaction) the MobileReserve / Auth will be rejected. This enforces that mobile loyalty and site entered loyalty cannot co-exist.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Allow Site Entry i.e., Swiped Loyalty Card</p>
			</td>
			<td>
				<p align="left">Both Mobile loyalty and site card swipe loyalty are allowed and Mobile payments can be tendered at DCR.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">Allow Site Entered Loyalty if no Mobile Loyalty</p>
			</td>
			<td>
				<p align="left">
					<ol>
						<li>If Mobile Loyalty is not present, loyalty card swipe at DCR will be accepted.</li>
						<li>If Mobile Loyalty is present and Loyalty Card is swiped at DCR, MobileReserve/Auth will be rejected.</li>
					</ol>
				</p>
			</td>
		 </tr>
		</tbody>
</table>


## Status Codes and Messages

The first two digits of the response code identify the message pair type. The last 3 digits is the error identifier for the status. A ‘good’ status is always represented as 00000 regardless of the message type.


<table>
	<thead>
		<tr valign="center">
			<th>
				Message Type
			</th>
			<th>
				Response Code
			</th>
			<th>
				Message Code
			</th>
			<th>
				Overall Result
			</th>
			<th>
				Description
			</th>
		</tr>
	</thead>
	<tbody>
		<tr valign="top">
			<td>
				<p align="left">All</p>
			</td>
			<td>
				<p align="left">00000</p>
			</td>
			<td>
				<p align="left">Success</p>
			</td>
			<td>
				<p align="left">Success</p>
			</td>
			<td>
				<p align="left">Message was successfully processed.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">All</p>
			</td>
			<td>
				<p align="left">00001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">An unexpected error has occurred while processing the request message.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">All</p>
			</td>
			<td>
				<p align="left">00001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">Mandatory data is missing from the request header.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">Unexpected error while processing the MobileAuthRequest data.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">Mandatory data is missing from the MobileAuthRequest</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02002</p>
			</td>
			<td>
				<p align="left">Invalid info in MobileTxnInfo element</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The header info matches an already processed transaction.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02002</p>
			</td>
			<td>
				<p align="left">Invalid info in MobileTxnInfo element</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">The header is missing mandatory data to complete Auth processing.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02003</p>
			</td>
			<td>
				<p align="left">POS or Fueling Position in use</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The targeted fueling position is already in use. (Unused) </p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02004</p>
			</td>
			<td>
				<p align="left">POS or Fueling Position in use</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The Commander was unable to process the authorization request. Communication with the POS or fueling position has been lost.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileAuth</p>
			</td>
			<td>
				<p align="left">02005</p>
			</td>
			<td>
				<p align="left">Unknown POS or Fueling Position</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The targeted fueling position is not configured.(Unused)</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">Unexpected error while trying to cancel the transaction. It is likely too late in the transaction to honor.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04003</p>
			</td>
			<td>
				<p align="left">04003</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The Commander is beyond the point to honor a cancel request.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04004</p>
			</td>
			<td>
				<p align="left">Invalid state - dispenser is fueling</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">Cancel occurred while dispensing fuel.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04005</p>
			</td>
			<td>
				<p align="left">Invalid Dispenser number</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The targeted fueling position does not match the original authorized fueling position.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04006</p>
			</td>
			<td>
				<p align="left">Invalid payment/auth information</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The payment info does not match the original payment info.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04007</p>
			</td>
			<td>
				<p align="left">Unknown transaction or authorization</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">There is no active transaction to cancel matching the provided header.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileCancel</p>
			</td>
			<td>
				<p align="left">04008</p>
			</td>
			<td>
				<p align="left">04008</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">Unexpectedly failed to cancel</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">Unexpected pump reserve failure</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">Data mandatory to handling the pump reserve request is not present.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06002</p>
			</td>
			<td>
				<p align="left">Invalid info in MobileTxnInfo element</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The header information(UMTI) was present in an already processed transaction.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06002</p>
			</td>
			<td>
				<p align="left">Invalid info in MobileTxnInfo element</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">Data required to reserve a fueling position is missing from the request message.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06003</p>
			</td>
			<td>
				<p align="left">Fueling Position in use</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The dispenser is not ready to reserve for a mobile transaction. It is in use or handling configuration updates.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06004</p>
			</td>
			<td>
				<p align="left">Fueling Position inaccessible/offline</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The targeted dispenser is configured, but offline.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobilePumpReserve</p>
			</td>
			<td>
				<p align="left">06005</p>
			</td>
			<td>
				<p align="left">Unknown POS or Fueling Position</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">The targeted dispenser is not configured.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileTransactionData</p>
			</td>
			<td>
				<p align="left">13001</p>
			</td>
			<td>
				<p align="left">Generic Error</p>
			</td>
			<td>
				<p align="left">MissingMandatoryData</p>
			</td>
			<td>
				<p align="left">The transaction data request is missing data required for processing.</p>
			</td>
		 </tr>
		<tr valign="top">
			<td>
				<p align="left">MobileTransactionData</p>
			</td>
			<td>
				<p align="left">13002</p>
			</td>
			<td>
				<p align="left">Invalid Transaction Data Header</p>
			</td>
			<td>
				<p align="left">Failure</p>
			</td>
			<td>
				<p align="left">This is a duplicate transaction for an already processed transaction, or the transaction does not exist on the system.</p>
			</td>
		 </tr>
		</tbody>
</table>
