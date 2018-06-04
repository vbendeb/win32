---
Description: Contains a port number used for IP or IPX protocols.
ms.assetid: 730f6ee6-7b7d-4e10-91ee-a4ba87aae5aa
title: GENERIC\_PORT union
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: structure
ms.date: 05/31/2018
---

# GENERIC\_PORT union

The **GENERIC\_PORT** structure contains a port number used for IP or IPX protocols.

## Syntax


```C++
typedef union {
  BYTE IPPort;
  WORD ByteSwappedIPXPort;
} GENERIC_PORT;
```



## Members

<dl> <dt>

**IPPort**
</dt> <dd>

IP port number filled in.

</dd> <dt>

**ByteSwappedIPXPort**
</dt> <dd>

IPX port number filled in.

</dd> </dl>

## Requirements



|                                     |                                                                                     |
|-------------------------------------|-------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 2000 Professional \[desktop apps only\]<br/>                          |
| Minimum supported server<br/> | Windows 2000 Server \[desktop apps only\]<br/>                                |
| Header<br/>                   | <dl> <dt>Netmon.h</dt> </dl> |



 

 



