---
title: "Метод ICorDebugStepper::StepRange"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugStepper.StepRange
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugStepper::StepRange
helpviewer_keywords:
- StepRange method [.NET Framework debugging]
- ICorDebugStepper::StepRange method [.NET Framework debugging]
ms.assetid: b9776112-6e6d-4708-892a-8873db02e16f
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a02efe1b701506cc3de695c5b79d5e9c84b25b8f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugsteppersteprange-method"></a>Метод ICorDebugStepper::StepRange
В результате ICorDebugStepper выполнить один шаг через содержащую и возвратить при достижении кода за последним из указанных диапазонов.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT StepRange (  
    [in] BOOL     bStepIn,  
    [in, size_is(cRangeCount)] COR_DEBUG_STEP_RANGE ranges[],  
    [in] ULONG32  cRangeCount  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `bStepIn`  
 [in] Значение `true` на шаг с заходом в функцию, которая вызывается в потоке. Значение `false` на шаг с обходом функции.  
  
 `ranges`  
 [in] Массив структур COR_DEBUG_STEP_RANGE, каждый из которых задает диапазон.  
  
 `cRangeCount`  
 [in] Размер массива `ranges`.  
  
## <a name="remarks"></a>Примечания  
 `StepRange` Действия метода [ICorDebugStepper::Step](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-step-method.md) метода, за исключением того, что она не завершается до кода за пределами данного диапазона достигается.  
  
 Это может быть более эффективным, чем пошаговое выполнение одной инструкции за раз. Диапазоны задаются в виде списка пар смещения от начала пошаговым кадра.  
  
 Диапазоны относятся к Microsoft кода промежуточного языка MSIL метода. Вызовите [ICorDebugStepper::SetRangeIL](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setrangeil-method.md) с `false` вносить диапазоны машинному коду метода.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
