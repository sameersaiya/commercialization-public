---
title: CaptureStateOnStart
description: CaptureStateOnStart
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: c29100b6-2eba-4100-8d15-a80a6766beed
ms.mktglfcycl: operate
ms.sitesec: msdn
ms.author: sapaetsc
ms.date: 05/05/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-oem
---


# CaptureStateOnStart

Represents a collection of keywords that describe events to be captured at the start of a recording. The library requests the provider to log its state information when the provider is enabled. If the **Operation** attribute is specified, the **Keyword** elements can be set or added to the collection.


## Element Hierarchy

* \<[WindowsPerformanceRecorder](windowsperformancerecorder.md)\>
  * \<[Profiles](profiles.md)\>
    * \<[EventProvider](eventprovider.md)\>
      * \<**CaptureStateOnStart**\>
    * \<[Profile](profile-wpr.md)\>
      * \<[Collectors](collectors.md)\>
        * \<[EventCollectorId](eventcollectorid.md)\>
          * \<[EventProviderId](eventproviderid.md)\>
            * \<**CaptureStartOnStart**\>
          * \<[EventProvider](eventprovider.md)\>
            * \<**CaptureStateOnStart**\>


## Syntax

```
<CaptureStateOnStart Operation = "Set" | "Add"> | “Remove”

  <!-- Child elements -->
  Keyword

</CaptureStateOnStart>
```


## Attributes and Elements


### Attributes

<table>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Description</th>
<th>Data type</th>
<th>Required</th>
<th>Default</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>Indicates whether keywords should be set or added.</p></td>
<td><p>This attribute can have one of the following values:</p>
<ul>
<li><p>Set</p></li>
<li><p>Add</p></li>
<li><p>Remove</p></li>
</ul></td>
<td><p>No</p></td>
<td><p>Set</p></td>
</tr>
</tbody>
</table>


### Child Elements

| Element                                                     | Description                                                                     | Requirement            |
|:------------------------------------------------------------|:--------------------------------------------------------------------------------|:-----------------------|
| [Keyword (in EventProvider)](keyword--in-eventprovider-.md) | Describes the Event Tracing for Windows (ETW) keyword for a user-mode provider. | Required, one or more. |


### Parent Elements

| Element                               | Description                                   |
|:--------------------------------------|:----------------------------------------------|
| [EventProvider](eventprovider.md)     | Represents an event provider for the profile. |
| [EventProviderId](eventproviderid.md) | Represents an event provider identifier.      |


## Example

The following code example shows how this element is used.

```
<EventProvider Id="sample-provider" Name="SampleProvider" NonPagedMemory="true" Level="5">
  <Keywords>
    <Keyword Value="0x98"/> <!-- Provider is enabled with these keywords throughout tracing session -->
  </Keywords>
  <CaptureStateOnStart>
    <Keyword Value="0xff4"/> <!-- Provider is  enabled with these keywords when tracing is started. -->
  </CaptureStateOnStart>
  <CaptureStateOnSave>
    <Keyword Value="0x118"/> <!-- Provider is enabled with these keywords when tracing is saved. -->
  </CaptureStateOnSave>
</EventProvider>
```


## Related topics

[Elements](elements.md)

[CustomKeyword](customkeyword.md)

[CaptureStateOnSave](capturestateonsave.md)

