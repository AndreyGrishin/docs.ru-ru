---
title: "Практическое руководство. Изменение цвета элемента с помощью событий фокуса"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- focus events [WPF], changing element color for
- colors of elements [WPF], changing
- elements [WPF], changing color of
ms.assetid: 7e246802-3625-47a7-ae9d-c8a2a40fd040
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a8b0e3f1b0a3287be89aba6e26f0621525c458a8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-change-the-color-of-an-element-using-focus-events"></a>Практическое руководство. Изменение цвета элемента с помощью событий фокуса
В этом примере показано, как изменить цвет элемента при получении и потере фокуса с помощью <xref:System.Windows.UIElement.GotFocus> и <xref:System.Windows.UIElement.LostFocus> события.  
  
 В этом примере состоит из [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] файл и файл кода.  
  
## <a name="example"></a>Пример  
 Следующие [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] создает пользовательский интерфейс, состоящий из двух <xref:System.Windows.Controls.Button> объектов, а также присоединяет обработчики событий для <xref:System.Windows.UIElement.GotFocus> и <xref:System.Windows.UIElement.LostFocus> событий для <xref:System.Windows.Controls.Button> объектов.  
  
 [!code-xaml[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml#gotlostfocussamplexaml)]  
  
 Следующий код создает <xref:System.Windows.UIElement.GotFocus> и <xref:System.Windows.UIElement.LostFocus> обработчики событий.  Когда <xref:System.Windows.Controls.Button> прибыли фокус <xref:System.Windows.Controls.Control.Background%2A> из <xref:System.Windows.Controls.Button> изменяется на красный.  Когда <xref:System.Windows.Controls.Button> теряет фокус ввода, <xref:System.Windows.Controls.Control.Background%2A> из <xref:System.Windows.Controls.Button> изменяется обратно на белый.  
  
 [!code-csharp[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml.cs#gotlostfocussampleeventhandlers)]
 [!code-vb[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/VisualBasic/Window1.xaml.vb#gotlostfocussampleeventhandlers)]  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о входных данных](../../../../docs/framework/wpf/advanced/input-overview.md)
