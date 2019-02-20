---
description: Before deploying the Experience Cloud ID service, you should understand how this service affects visitor tracking on multiple domains and potential issues if you are collecting data with different methods or through JavaScript files.
keywords: ID Service
seo-description: Before deploying the Experience Cloud ID service, you should understand how this service affects visitor tracking on multiple domains and potential issues if you are collecting data with different methods or through JavaScript files.
seo-title: Experience Cloud ID Service Migration Decision Points
solution: Marketing Cloud
title: Experience Cloud ID Service Migration Decision Points
uuid: ee56b5de-fcf3-4cfb-9e53-762af7c4d2ff
index: y
internal: n
snippet: y
---

# Experience Cloud ID Service Migration Decision Points{#experience-cloud-id-service-migration-decision-points}

Before deploying the Experience Cloud ID service, you should understand how this service affects visitor tracking on multiple domains and potential issues if you are collecting data with different methods or through JavaScript files.

Answers to the questions in this section help determine any additional migration steps you should take.

* [Do you have a data collection CNAME?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-e23785daa3a14abdbf007bd35e093f88) 
* [If you have a data collection CNAME, do you have multiple domains?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-69eb55192f8b40a5833da41aaff5bfc0) 
* [If you are keeping your data collection CNAME, is it mapped to omtrdc.net?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-c9009cbf58594746a5b78bbf44acafbd) 
* [If you do not have a data collection CNAME, is your data collection server *.2o7.net or *.sc.omtrdc.net?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-34dabde7780e4a339f134c0ca7768961) 
* [Do you have multiple Analytics JavaScript files, or are you tracking Flash applications or videos?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-943a04529f3d456ab608252d146658b3) 
* [Are you using unsupported data collection methods?](../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-6af5ff728c054a3f8d27ba073e5b268b)

## Do you have a data collection CNAME? {#section-e23785daa3a14abdbf007bd35e093f88}

Many customers can migrate away from a data collection CNAME as part of the ID service migration.

<table id="table_13F7C1E3D64D4F86B0149C9D3B54AADD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Data Collection Method </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>With a CNAME </p> </td> 
   <td colname="col2"> <p>See the next question to decide if you should migrate away from a data collection CNAME. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Without a CNAME </p> </td> 
   <td colname="col2"> <p>Skip to <a href="../../mcvid-reference/mcvid-analytics-reference/mcvid-migration-decisions.md#section-34dabde7780e4a339f134c0ca7768961" format="dita" scope="local"> If you do not have a data collection CNAME, is your data collection server *.2o7.net or *.sc.omtrdc.net?</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## If you have a data collection CNAME, do you have multiple domains? {#section-69eb55192f8b40a5833da41aaff5bfc0}

If you have multiple domains that send data to the *same report suite*, then we recommend data collection with a CNAME. This helps you track visitors across domains. If you are collecting data on a single domain, there is no advantage to maintaining a data collection CNAME.

<table id="table_D132BCA243E54657AEC930559343FDD3"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Collecting Data From </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Multiple domains </p> </td> 
   <td colname="col2"> <p>If you are tracking visitors across multiple domains, and you also have a main entry site where customers can be identified before they visit other domains, then you should continue to use your data collection CNAME. See <a href="../../mcvid-reference/mcvid-analytics-reference/mcvid-cname.md#concept-4df91f8a30ad4ec7a01eb943d579cc9d" format="dita" scope="local"> Data Collection CNAMES and Cross Domain Tracking</a> for a detailed explanation. </p> <p>Note that you need to specify two additional tracking-server parameters, <span class="codeph"> visitor.marketingCloudServer</span> and <span class="codeph"> visitor.marketingCloudServerSecure</span>, to configure a CNAME with the ID service. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>A single domain </p> </td> 
   <td colname="col2"> <p>Working with a single domain means you can migrate away from a data collection CNAME if you no longer wish to manage it. However, there's no requirement to change if your CNAME is working. </p> <p>If you do remove the CNAME: </p> 
    <ul id="ul_12CDECEFC7BB41A18895B507CAA42315"> 
     <li id="li_32E2CD3E58454E20A642BADE507AE86E">Make sure your new tracking server is <a href="https://marketing.adobe.com/resources/help/en_US/whitepapers/rdc/" format="https" scope="external"> RDC compliant</a>. </li> 
     <li id="li_865BB6DAA3594EBBAB688E73C8343762">Move from the CNAME to an RDC tracking server a few months in advance of your migration to the <span class="keyword"> Experience Cloud</span> ID service. </li> 
     <li id="li_284A015177554C848C8648DC5BBAA365"> <i>Do not</i> use a <span class="codeph"> *.2o7.net</span> tracking server. </li> 
     <li id="li_B1ABF03DC46C42059F61542CDE0FE5A1">Contact <a href="https://helpx.adobe.com/marketing-cloud/contact-support.html" format="https" scope="external"> Customer Care</a> to set up a visitor migration. This helps ensure consistent visitor counts. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## If you are keeping your data collection CNAME, is it mapped to omtrdc.net? {#section-c9009cbf58594746a5b78bbf44acafbd}

If you decided to keep your CNAME, open a command prompt and ping your CNAME:

```
$: ping metrics.example.com
PING example.com.d1.sc.omtrdc.net (66.235.139.256)
```

<table id="table_8023DDC56EE44F9286ED844DEBD965D0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> CNAME Resolves To </th> 
   <th colname="col2" class="entry"> Required Actions </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> *.omtrdc.net</span> </p> </td> 
   <td colname="col2"> <p>Your CNAME is configured correctly. No additional action is necessary. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Someplace other than <span class="codeph"> *.omtrdc.net</span></p> </td> 
   <td colname="col2"> <p>Update the CNAME record to point to your <a href="https://marketing.adobe.com/resources/help/en_US/whitepapers/rdc/" format="http" scope="external"> RDC</a> hostname. </p> </td> 
  </tr> 
 </tbody> 
</table>

## If you do not have a data collection CNAME, is your data collection server *.2o7.net or *.sc.omtrdc.net? {#section-34dabde7780e4a339f134c0ca7768961}

<table id="table_0C0F018F309B473784C875341C379EFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Server Address </th> 
   <th colname="col2" class="entry"> Required Actions </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> *.2o7.net</span> </p> </td> 
   <td colname="col2"> <p>If you are using <span class="codeph"> *.2o7.net</span>, migrate to the <a href="https://marketing.adobe.com/resources/help/en_US/whitepapers/rdc/" format="http" scope="external"> RDC</a> data collection domain, <span class="codeph"> *.sc.omtrdc.net</span>. </p> <p>To make this migration, configure visitor migration from <span class="codeph"> *.2o7.net</span> to <span class="codeph"> *.sc.omtrdc.net</span>, and then update <span class="codeph"> s.trackingServer</span> to <span class="codeph"> [namespace].sc.omtrdc.net</span> when you update your Analytics JavaScript code later as part of the <a href="../../mcvid-implementation-guides/mcvid-setup-analytics.md#section-70ec9ebff47940d8ab520be5ec4728c5" format="dita" scope="local"> implementation process</a>. If you have any questions at all about the hostname of your tracking server, contact <a href="https://helpx.adobe.com/marketing-cloud/contact-support.html" format="https" scope="external"> Customer Care</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> *.sc.omtrdc</span> </p> </td> 
   <td colname="col2"> <p>Continue to use your current data collection server. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Do you have multiple Analytics JavaScript files, or are you tracking Flash applications or videos? {#section-943a04529f3d456ab608252d146658b3}

If you have multiple Analytics JavaScript files or Flash applications or videos across your site that send data to the *same report suite*, You should configure a grace period so that visitors continue to be identified by an Analytics ID while you roll out the [!DNL Experience Cloud] ID service.

<table id="table_8A4EA063AF4345B69BC98537E2E702BA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Data Collection With </th> 
   <th colname="col2" class="entry"> Required Actions </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 
    <ul id="ul_910DD99E074E49C6907F86426EFA5BF2"> 
     <li id="li_4366CC8EB7A54A959568E3761ABBBF23">Multiple Analytics Javascript files </li> 
     <li id="li_B8A8132019EA48088E4F37E36F153D76">Other Data collection methods </li> 
    </ul> </td> 
   <td colname="col2"> <p>You should configure a visitor ID service grace period so that you can roll out the visitor ID service to each JavaScript file and other data collection libraries. See <a href="../../mcvid-reference/mcvid-analytics-reference/mcvid-grace-period.md#concept-e4c0d796412b4985badae11e5aecb2fd" format="dita" scope="local"> ID Service Grace Period</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>A single Analytics JavaScript file </p> </td> 
   <td colname="col2"> <p>You can update your single JavaScript file to use the visitor ID service without a grace period. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Are you using unsupported data collection methods? {#section-6af5ff728c054a3f8d27ba073e5b268b}

You might need to update the way you track links or migrate away from Sliverlight.

<table id="table_A72AEB92F48345DD83F136B9989F4EF9"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Data Collection Method </th> 
   <th colname="col2" class="entry"> Required Actions </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>JavaScript and/or Flash </p> </td> 
   <td colname="col2"> <p>None. The <span class="keyword"> Experience Cloud</span> ID service supports these data collection methods. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Silverlight </p> </td> 
   <td colname="col2"> <p>You need to migrate away from Silverlight if visitors can access Silverlight content and other sections of your site that use the <span class="keyword"> Experience Cloud</span> ID service. Silverlight is not supported by the ID service. </p> <p> If you are tracking a Silverlight-based video player, the vendor likely provides JavaScript APIs that you can use instead. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Hard-coded image tags </p> </td> 
   <td colname="col2"> <p>Update hard-coded links to use JavaScript. </p> </td> 
  </tr> 
 </tbody> 
</table>
