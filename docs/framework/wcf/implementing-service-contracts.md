---
title: "Реализация контрактов служб"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: implementing service contracts [WCF]
ms.assetid: aefb6f56-47e3-4f24-ab0a-9bc07bf9885f
caps.latest.revision: "17"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1b4085e23120ad654121f33111eda68276259096
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-service-contracts"></a>Реализация контрактов служб
Служба - это класс, который предоставляет клиентам имеющиеся функциональные возможности в одной или нескольких конечных точках. Для создания службы необходимо создать класс, реализующий контракт [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]. Это можно сделать одним из двух способов. Во-первых, можно определить контракт отдельно в качестве интерфейса, а затем создать класс, реализующий этот интерфейс. Во-вторых, можно непосредственно создать класс и контракт, разместив атрибут <xref:System.ServiceModel.ServiceContractAttribute> в самом классе, а атрибут <xref:System.ServiceModel.OperationContractAttribute> - в методах, доступных клиентам службы.  
  
## <a name="creating-a-service-class"></a>Создание класса службы  
 Ниже приведен пример службы, реализующей отдельно определенный контракт `IMath`.  
  
```csharp  
// Define the IMath contract.  
[ServiceContract]  
public interface IMath  
{  
    [OperationContract]   
    double Add(double A, double B);  
  
    [OperationContract]  
    double Multiply (double A, double B);  
}  
  
// Implement the IMath contract in the MathService class.  
public class MathService : IMath  
{  
    public double Add (double A, double B) { return A + B; }  
    public double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 Кроме того, контракт может непосредственно предоставляться службой. Ниже приведен пример класса службы, который определяет и реализует контракт `MathService`.  
  
```csharp  
// Define the MathService contract directly on the service class.  
[ServiceContract]  
class MathService  
{  
    [OperationContract]  
    public double Add(double A, double B) { return A + B; }  
    [OperationContract]  
    private double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 Обратите внимание, что описанные службы предоставляют разные контракты, так как имена контрактов различаются. В первом случае предоставленный контракт называется "`IMath`", а во втором - "`MathService`".  
  
 Некоторые свойства (такие как параллелизм и создание экземпляров) можно задать на уровне реализации службы и операции. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Проектирование и реализация служб](../../../docs/framework/wcf/designing-and-implementing-services.md).  
  
 После реализации контракта службы необходимо создать для службы одну или более конечных точек. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Общие сведения о создании конечной точки](../../../docs/framework/wcf/endpoint-creation-overview.md). [!INCLUDE[crabout](../../../includes/crabout-md.md)]Запуск службы см. в разделе [размещение служб](../../../docs/framework/wcf/hosting-services.md).  
  
## <a name="see-also"></a>См. также  
 [Проектирование и реализация служб](../../../docs/framework/wcf/designing-and-implementing-services.md)  
 [Практическое руководство. Создание службы с помощью класса контракта](../../../docs/framework/wcf/feature-details/how-to-create-a-wcf-contract-with-a-class.md)  
 [Практическое руководство. Создание службы с помощью интерфейса контракта](../../../docs/framework/wcf/feature-details/how-to-create-a-service-with-a-contract-interface.md)  
 [Указание поведения службы во время выполнения](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)
