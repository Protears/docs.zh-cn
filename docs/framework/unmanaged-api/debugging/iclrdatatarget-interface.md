---
title: ICLRDataTarget 接口
ms.date: 03/30/2017
api_name:
- ICLRDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget
helpviewer_keywords:
- ICLRDataTarget interface [.NET Framework debugging]
ms.assetid: e2f05155-9bef-4e11-b703-7f05890665ca
topic_type:
- apiref
ms.openlocfilehash: 2b5c99e40aabdbc654bdc612729b2756e3ef5bb4
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793717"
---
# <a name="iclrdatatarget-interface"></a>ICLRDataTarget 接口
提供与公共语言运行时（CLR）的目标项交互的方法。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetCurrentThreadID 方法](iclrdatatarget-getcurrentthreadid-method.md)|获取当前线程的操作系统标识符。|  
|[GetImageBase 方法](iclrdatatarget-getimagebase-method.md)|获取指定的图像的基本内存地址。|  
|[GetMachineType 方法](iclrdatatarget-getmachinetype-method.md)|获取目标进程正在使用的指令集类型的标识符。|  
|[GetPointerSize 方法](iclrdatatarget-getpointersize-method.md)|获取指向当前目标的指针的大小（以字节为单位）。|  
|[GetThreadContext 方法](iclrdatatarget-getthreadcontext-method.md)|获取一个指针，该指针指向具有指定标识符的线程的上下文。|  
|[GetTLSValue 方法](iclrdatatarget-gettlsvalue-method.md)|在线程本地存储（TLS）中获取指定线程的指定索引处的值。|  
|[ReadVirtual 方法](iclrdatatarget-readvirtual-method.md)|将数据从指定的虚拟内存地址读入指定的缓冲区。|  
|[Request 方法](iclrdatatarget-request-method.md)|由公共语言运行时（CLR）数据访问服务调用，用来请求操作，如实现所定义。|  
|[SetThreadContext 方法](iclrdatatarget-setthreadcontext-method.md)|设置目标进程中指定线程的当前上下文。|  
|[SetTLSValue 方法](iclrdatatarget-settlsvalue-method.md)|在目标进程中指定线程的线程本地存储（TLS）中设置一个值。|  
|[WriteVirtual 方法](iclrdatatarget-writevirtual-method.md)|将数据从指定的缓冲区写入指定的虚拟内存地址。|  
  
## <a name="remarks"></a>备注  
 API 客户端（即调试器）必须根据特定目标项实现此接口。 例如，活动进程的实现将不同于内存转储的。  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** ClrData，ClrData  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [ICLRDataTarget2 接口](iclrdatatarget2-interface.md)
- [调试接口](debugging-interfaces.md)
