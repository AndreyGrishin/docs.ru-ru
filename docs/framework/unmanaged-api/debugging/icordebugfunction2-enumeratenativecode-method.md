---
title: "Метод ICorDebugFunction2::EnumerateNativeCode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugFunction2.EnumerateNativeCode
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugFunction2::EnumerateNativeCode
helpviewer_keywords:
- ICorDebugFunction2::EnumerateNativeCode method [.NET Framework debugging]
- EnumerateNativeCode method [.NET Framework debugging]
ms.assetid: d383f5cc-1144-4b6d-b57a-db34d9134ab2
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 264eac8be96fad0ed72177c2b497f438f08b9f2a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugfunction2enumeratenativecode-method"></a>Метод ICorDebugFunction2::EnumerateNativeCode
Получает указатель интерфейса на объект ICorDebugCodeEnum, содержащий инструкции машинного кода в функцию, который ссылается данный объект ICorDebugFunction2.  
  
> [!NOTE]
>  `EnumerateNativeCode`не реализован в текущей версии платформы .NET Framework.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT EnumerateNativeCode (  
    [out] ICorDebugCodeEnum   **ppCodeEnum  
);  
```  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** CorDebug.idl, CorDebug.h
