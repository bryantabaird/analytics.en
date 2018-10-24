---
description: Redirects point the browser to a new location without user interaction. They are executed at either the web browser (client-side redirect) or at the web server (server-side redirect).
keywords: Analytics Implementation
seo-description: Redirects point the browser to a new location without user interaction. They are executed at either the web browser (client-side redirect) or at the web server (server-side redirect).
seo-title: Redirects and aliases
solution: Analytics
subtopic: Redirects
title: Redirects and aliases
topic: Developer and implementation
uuid: 9f632721-2912-48e7-ab43-dbc425c5ca3f
index: y
internal: n
snippet: y
---

# Redirects and aliases

Redirects point the browser to a new location without user interaction. They are executed at either the web browser (client-side redirect) or at the web server (server-side redirect).

## Redirects and aliases {#concept_F4F1D53D473947FE8554897332545763}

Redirects point the browser to a new location without user interaction. They are executed at either the web browser (client-side redirect) or at the web server (server-side redirect). 

Because redirects do not require any user interaction, redirects are often executed without the user ever noticing. The only thing that indicates a redirect has occurred is the browser's address bar. The address bar displays a URL that is different from the link the browser initially requested.

Although there are only two types of redirects, they can be implemented in numerous ways. For example, client-side redirects can occur because the web page to which a user has pointed his or her browser contains scripting or special HTML code that redirects the browser to another URL. Server-side redirects can occur because the page contains server-side scripting or because the web server has been configured to point the user to another URL. 

## Analytics and redirects {#concept_F9132879D0CB4AC1BE7AF45E388A47F7}

[!DNL Analytics] gathers some of its data from the browser, and relies upon certain browser properties. Two of those properties, the "Referring URL" (or "referrer") and the "Current URL" can be changed by a server-side redirect. Because the browser is aware that one URL has been requested, but a different URL has been returned, it clears the Referring URL. The result is the referring URL is blank, and [!DNL Analytics] might report that no referrer existed for the page.

<!-- 

redirects_sc.xml

 -->

The following examples illustrate how browsing is affected without and with redirects:

* [Example: Browsing Without Redirects](../../implement/js-implementation/redirects-overview.md#section_5C835A4D665A4625A23333C2C21F152D) 
* [Example: Browsing With Redirects](../../implement/js-implementation/redirects-overview.md#section_921DDD32932847848C4A901ACEF06248)

## Example: Browsing Without Redirects {#section_5C835A4D665A4625A23333C2C21F152D}

Consider the following hypothetical scenario in which the user does not encounter a redirect:

1. User points his or her browser to [!DNL www.google.com], and types, "discount airline tickets" into the search field, and then clicks the **[!UICONTROL Search]** button. 
1. The browser displays the search results including a link to your site, [!DNL http://www.flywithus.com/]. After displaying the search results, the browser's address bar displays the search terms that the user entered in the search field ( `http://www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets`). Notice that the search terms are included in the URL query string parameters that follow `http://www.google.com/search?`. 
1. The user clicks the link to your hypothetical site [!DNL http://www.flywithus.com/]. When the user clicks this link and lands on the [!DNL flywithus.com] website, [!DNL Analytics] uses JavaScript to collect the referring URL ( [!DNL http://www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets]) as well as the current URL ( [!DNL http://www.flywithus.com/]). 
1. [!DNL Analytics] reports the information collected during this interaction in various reports, such as [!UICONTROL Referring Domains], [!UICONTROL Search Engines], and [!DNL Search Keywords].

## Example: Browsing With Redirects {#section_921DDD32932847848C4A901ACEF06248}

Redirects can cause the browser to blank out the true referring URL. Consider the following scenario:

1. User points his or her browser to [!DNL www.google.com], and types, "discount airline tickets" into the search field, and then clicks the **[!UICONTROL Search]** button. 
1. The browser window's address bar displays the search terms that the user typed into the search field ( [!DNL http://www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets]). Notice that the search terms are included in the URL query string parameters that follow " [!DNL http://www.google.com/search?]". The browser also displays a page that contains the search results including a link to one of your domain names: [!DNL http://www.flytohawaiiforfree.com/]. This *vanity* domain is configured to redirect the user to [!DNL http://www.flywithus.com/]. 
1. The user clicks on the link [!DNL http://www.flytohawaiiforfree.com/] and is redirected by the server to your main site, [!DNL http://www.flywithus.com]. When the redirection occurs, the data that is important to [!DNL Analytics] data collection is lost because the browser clears the referring URL. Thus, the original search information used in the [!DNL Analytics] reports (for example, [!UICONTROL Referring Domains], [!UICONTROL Search Engines], [!UICONTROL Search Keywords]) is lost.

<a id="section_C46D60203C2247CBBDA210440033781B"></a>

[Implementing Redirects](../../implement/js-implementation/redirects-overview.md#concept_5EC2EE9677A44CC5B90A38ECF28152E7) discusses how to leverage [!DNL Analytics] variables to capture the data lost in the redirect. Specifically, the section discusses how to fix the "discount airline tickets" situation described above. 

## Implement redirects {#concept_5EC2EE9677A44CC5B90A38ECF28152E7}

In order to capture [!DNL Analytics] data from redirects, four minor alterations need to be made to the code that creates the redirect and the AppMeasurement for JavaScript file.

<!-- 

redirects_implement.xml

 -->

Completing the following steps will retain the information that the original referrer (for example, [!DNL http://www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets] in the scenario above) passes to your site:

## Configure referrer override JavaScript code {#section_87BB1D47D9C345C18339078824645CC4}

<!-- 

redirects_js_override.xml

 -->

The code snippet below shows two JavaScript variables, *`s_referrer`* and *`s_pageURL`*. This code is placed on the ultimate landing page of the redirect.

```js
<script language="JavaScript" src="//INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/AppMeasurement.js"></script> 
<script language="JavaScript"><!-- 
/* You may give each page an identifying name, server, and channel on 
the next lines. */ 
s.pageName="" 
s.server="" 
s.campaign="" 
s.referrer="" 
s.pageURL=""
```

>[!IMPORTANT]
>
>Set *`s.referrer`* only once on the page. Setting it more than once with every tracking call or with every link click that is tracked causes double counting of the referrer and related dimensions, such as search engines and keywords.

## Redirects using getQueryParam {#section_EE924E399F7A431C8FC8E8A2BEF84DEC}

While the [!UICONTROL getQueryParam] is an easy way to populate [!DNL Analytics] variables with query string values, it must be implemented in connection with a temporary variable so that legitimate referrers are not overwritten when the query string is empty. The best way to use [!UICONTROL getQueryParam] is in connection with the [!UICONTROL getValue] plug in as outlined with the following pseudo-code.

```js
// AppMeasurement 1.x 
var tempVar=s.Util.getQueryParam('origref') 
if(tempVar) 
  s.referrer=tempVar;

```

```js
// H Code 
var tempVar=s.getQueryParam('origref') 
if(tempVar) 
  s.referrer=tempVar;

```

## Modify the redirect mechanism {#section_2FF9921E8FCA4440B6FF90F15386E548}

<!-- 

redirects_modify_mechanism.xml

 -->

Because the browser strips referring URL, you must configure the mechanism that handles the redirect (for example, the web server, server-side code, client-side code) to pass along the original referrer information. If you would also like to record the alias link URL, this must also be passed along to the ultimate landing page. Use the *`s_pageURL`* variable to override the current URL.

Because there are many ways to implement a redirect, you should check with your web operations group or your online advertising partner to identify the specific mechanisms that execute redirects on your website.

## Capture the original referrer {#section_7F1A77F447CF485385B456A64B174050}

<!-- 

redirects_referrer.xml

 -->

Normally, [!DNL Analytics] will obtain the referring URL from the browser's [!UICONTROL document.referrer] property, and the current URL from the [!UICONTROL document.location] property. By passing values to the *`referrer`* and *`pageURL`* variables, you can override the default processing. By passing a value to the referrer variable, you are telling [!DNL Analytics] to ignore the referrer information in the [!UICONTROL document.referrer] property and to use an alternative value that you define.

Therefore, the final version of the landing page would need to contain the following code to correct the issues introduced in the "discount airline tickets" scenario.

```js
<script language="JavaScript" src="http://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/AppMeasurement.js"></script> 
<script language="JavaScript"><!-- 
/* You may give each page an identifying name, server, and channel on 
the next lines. */ 
s.pageName="" 
s.server="" 
s.campaign="" 
s.referrer="http://www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets" 
// Setting the s.pageURL variable is optional. 
s.pageURL="http://www.flytohawaiiforfree.com"
```

## Verify the referrer with the Adobe Debugger {#section_B3E85941982E4E1698B271375AD669B9}

<!-- 

redirects_verify_referrer.xml

 -->

Run a test to verify that the referrer, originating URL ( *`s_server`*) and campaign variables are being captured.

These variables will be represented as the following parameters in the [Experience Cloud Debugger](https://marketing.adobe.com/resources/help/en_US/experience-cloud-debugger/).

<table id="table_5F3B987D4D514CA283F7B9F52EBC2301"> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> <b>URL or Query String Value</b> </th> 
   <th class="entry"> <b>Value as Shown in the DigitalPulse Debugger</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <p>Original Referrer </p> </td> 
   <td> <p> <span class="filepath"> http://www.google.com/search%3F hl%3Den %26ie%3DUTF826q%3 Ddiscount%2Bairline%2Btickets </span> </p> </td> 
   <td> <p> <span class="filepath"> r=http:/ref=www.google.com/search?hl=en&amp;ie=UTF -8&amp;q=discount+airline+tickets </span> </p> </td> 
  </tr> 
  <tr> 
   <td> <p>Page URL </p> </td> 
   <td> <p> <span class="filepath"> http://www.flytohawaiiforfree.com </span> </p> </td> 
   <td> <p> <span class="filepath"> g=http://www.flytohawaiiforfree.com </span> </p> <p>This value will appear in the DigitalPulse Debugger if the <span class="varname"> pageURL </span> variable is used. </p> </td> 
  </tr> 
  <tr> 
   <td> <p>Ultimate Landing Page URL </p> </td> 
   <td> <p> <span class="filepath"> http://www.flywithus.com </span> </p> </td> 
   <td> <p>This value will NOT appear in the DigitalPulse Debugger if the <span class="varname"> pageURL </span> variable is used. </p> </td> 
  </tr> 
 </tbody> 
</table>

The text that the debugger displays should correspond to the following example:

```
Image 
 
http://flywithuscom.112.2o7.net/b/ss/flywithuscom/1/JS-1.4/s61944015791667?[AQB] 
ndh=1 
t=4/8/2014 13:34:28 4 360 
pageName=Welcome to FlyWithUs.com 
r=http://ref=www.google.com/search?hl=en&ie=UTF-8&q=discount+airline+tickets 
cc=USD 
g=http://www.flytohawaiiforfree.com 
s=1280x1024 
c=32 
j=1.3 
v=Y 
k=Y 
bw=1029 
bh=716 
ct=lan 
hp=N 
[AQE]
```

After verifying that the Adobe Debugger displays these variables, it is always helpful to confirm that the search terms and the original referring domain (prior to the redirect) are registering traffic in reports. 