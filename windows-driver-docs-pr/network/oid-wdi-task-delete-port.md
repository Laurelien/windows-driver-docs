---
title: OID\_WDI\_TASK\_DELETE\_PORT
description: OID\_WDI\_TASK\_DELETE\_PORT requests that the IHV component releases all resources (including MAC and PHY) allocated to the specified port.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: c84b6cd6-a8e7-4ba7-a9d9-04b2881904c8
keywords: ["OID_WDI_TASK_DELETE_PORT Network Drivers Starting with Windows Vista"]
topic_type:
- apiref
api_name:
- OID_WDI_TASK_DELETE_PORT
api_location:
- dot11wdi.h
api_type:
- HeaderDef
---

# OID\_WDI\_TASK\_DELETE\_PORT


OID\_WDI\_TASK\_DELETE\_PORT requests that the IHV component releases all resources (including MAC and PHY) allocated to the specified port.

| Object  | Abort capable | Default priority (host driver policy) | Normal execution time (seconds) |
|---------|---------------|---------------------------------------|---------------------------------|
| Adapter | No            | 6                                     | 1                               |

 

## Task parameters


| TLV                                                                               | Multiple TLV instances allowed | Optional | Description                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_DELETE\_PORT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926288) |                                |          | The delete port parameters. |

 

## Task completion indication


[NDIS\_STATUS\_WDI\_INDICATION\_DELETE\_PORT\_COMPLETE](ndis-status-wdi-indication-delete-port-complete.md)
Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Minimum supported client</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>Minimum supported server</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WDI_TASK_DELETE_PORT%20%20RELEASE:%20%286/30/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




