---
title: "기본 쿼리(LINQ to XML)(C#) | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: d333bb7d-20c1-448a-95b7-e5ba07915744
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e3879dfe92f158c545a1f4a42c6bfc35aae06f3c
ms.lasthandoff: 03/13/2017


---
# <a name="basic-queries-linq-to-xml-c"></a>기본 쿼리(LINQ to XML)(C#)
이 단원에서는 기본 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 쿼리의 예제를 제공합니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[방법: 특정 특성으로 요소 찾기(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-an-element-with-a-specific-attribute.md)|특정 값을 가진 특성이 포함된 특정 요소를 찾는 방법을 보여 줍니다.|  
|[방법: 특정 자식 요소로 요소 찾기(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-an-element-with-a-specific-child-element.md)|특정 값을 가진 자식 요소가 포함된 특정 요소를 찾는 방법을 보여 줍니다.|  
|[XDocument 쿼리와 XElement 쿼리 비교(C#)](../../../../csharp/programming-guide/concepts/linq/querying-an-xdocument-vs-querying-an-xelement.md)|<xref:System.Xml.Linq.XElement>에서 시작하는 XML 트리에 대한 쿼리 작성과 <xref:System.Xml.Linq.XDocument>에서 시작하는 XML 트리에 대한 쿼리 작성의 차이점에 대해 설명합니다.|  
|[방법: 특정 요소 이름으로 하위 항목 찾기(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-descendants-with-a-specific-element-name.md)|특정 이름을 가진 요소의 하위 요소를 모두 찾는 방법을 보여 줍니다. 이 예제에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축을 사용합니다.|  
|[방법: Descendants 메서드를 사용하여 단일 하위 항목 찾기(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-a-single-descendant-using-the-descendants-method.md)|<xref:System.Xml.Linq.XContainer.Descendants%2A> 축 메서드를 사용하여 고유하게 명명된 단일 요소를 찾는 방법을 보여 줍니다.|  
|[방법: 복합 필터링으로 쿼리 작성(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-write-queries-with-complex-filtering.md)|더욱 복잡한 필터를 사용하여 쿼리를 작성하는 방법을 보여 줍니다.|  
|[방법: 선택적 요소로 필터링(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-filter-on-an-optional-element.md)|불규칙적인 모양의 트리에서 노드를 찾는 방법을 보여 줍니다.|  
|[방법: 네임스페이스에서 모든 노드 찾기(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-all-nodes-in-a-namespace.md)|특정 네임스페이스에 있는 노드를 모두 찾는 방법을 보여 줍니다.|  
|[방법: 요소 정렬(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-sort-elements.md)|결과를 정렬하는 쿼리를 작성하는 방법을 보여 줍니다.|  
|[방법: 여러 키로 요소 정렬(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-sort-elements-on-multiple-keys.md)|여러 키에 대해 정렬하는 방법을 보여 줍니다.|  
|[방법: 중간 값 계산(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-calculate-intermediate-values.md)|
          `Let` 절을 사용하여 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 쿼리에서 중간 값을 계산하는 방법을 보여 줍니다.|  
|[방법: 컨텍스트에 따라 요소를 찾는 쿼리 작성(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-write-a-query-that-finds-elements-based-on-context.md)|트리의 다른 요소를 기반으로 요소를 선택하는 방법을 보여 줍니다.|  
|[방법: 빈 쿼리 결과 집합 디버그(C#)](../../../../csharp/programming-guide/concepts/linq/how-to-debug-empty-query-results-sets.md)|기본 네임스페이스에 있는 XML에 대한 쿼리를 디버깅할 때 적절한 해결 방법을 보여 줍니다.|  
  
## <a name="see-also"></a>참고 항목  
 [XML 트리 쿼리(C#)](../../../../csharp/programming-guide/concepts/linq/querying-xml-trees.md)