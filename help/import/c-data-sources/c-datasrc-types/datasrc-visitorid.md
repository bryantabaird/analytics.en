---
description: Visitor IDs can be integrated by selecting the Generic (Transaction ID) category.
seo-description: Visitor IDs can be integrated by selecting the Generic (Transaction ID) category.
seo-title: Visitor ID
solution: Analytics
subtopic: Data sources
title: Visitor ID
topic: Developer and implementation
uuid: c91b7ddc-b812-455e-9e37-ea1c51226a17
index: y
internal: n
snippet: y
---

# Visitor ID

Visitor IDs can be integrated by selecting the Generic (Transaction ID) category.

See [Integrating Offline Data](../../../import/c-data-sources/datasrc-integrating-offline-data.md#concept_B5C576220F1548B5A3A57112AA3960C6). 

<p class="head"> <b>Visitor ID Dimensions</b> </p>

<table id="table_8F90F820E7D2465582DA00F2DFC5B21C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <p>Column Name </p> </th> 
   <th colname="col2" class="entry"> <p>Description </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Visitor ID </p> </td> 
   <td colname="col2"> <p>(<b>Required</b>) Unique value that represents a customer in both the online and offline systems. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Date </p> </td> 
   <td colname="col2"> <p>Use the following date format: <span class="codeph"> MM/DD/YYYY/hh/mm/ss</span> (for example, <span class="codeph"> 07/14/2017/06/00/00</span>) </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Tracking Code </p> </td> 
   <td colname="col2"> <p>Tracking code name. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Category </p> </td> 
   <td colname="col2"> <p>Category name. </p> <p>If you specify a category, then you must also select a product. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Channel </p> </td> 
   <td colname="col2"> <p>Channel name. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>eVar<i>n</i> </p> </td> 
   <td colname="col2"> <p>eVar<i>n</i> name. Valid values for <i>n</i> are whole number 1 - 75. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Product </p> </td> 
   <td colname="col2"> <p>Product name. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>State </p> </td> 
   <td colname="col2"> <p>State name. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Zip </p> </td> 
   <td colname="col2"> <p>Zip name. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Visitor ID Metrics** 

<table id="table_D4EA0F08447148B0A1750981A2AAA604"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <p>Column Name </p> </th> 
   <th colname="col2" class="entry"> <p>Description </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Clickthroughs </p> </td> 
   <td colname="col2"> <p>Number of tracking code views. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Cart Adds </p> </td> 
   <td colname="col2"> <p>Number of cart additions. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Cart Opens </p> </td> 
   <td colname="col2"> <p>Number of cart opens. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Cart Removes </p> </td> 
   <td colname="col2"> <p>Number of cart removals. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Cart Views </p> </td> 
   <td colname="col2"> <p>Number of cart views. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Checkouts </p> </td> 
   <td colname="col2"> <p>Number of checkouts. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Event <i>n</i> </p> </td> 
   <td colname="col2"> <p>Number of times event <i>n</i> occurred. Valid values for <i>n</i> are whole number 1 - 100. </p> <p>If you specify a View event, you must also specify the corresponding data dimension (eVar). For example, if you include eVar2 views, then you must list eVar2 with a value. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>eVar<i>n</i> Views </p> </td> 
   <td colname="col2"> <p>Number of times eVar <i>n</i> was viewed. Valid values for <i>n</i> are whole number 1 - 75. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Price </p> </td> 
   <td colname="col2"> <p>Product price. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Orders </p> </td> 
   <td colname="col2"> <p>Number of orders placed. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Product Views </p> </td> 
   <td colname="col2"> <p>Number of product views. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Quantity </p> </td> 
   <td colname="col2"> <p>Number of units sold. </p> </td> 
  </tr> 
 </tbody> 
</table>
