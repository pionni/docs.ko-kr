---
title: "|| (OR) (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 8e649648-eb9a-4380-9d74-36e62260628c
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# || (OR) (Entity SQL)
두 `Boolean` 식을 결합합니다.  
  
## 구문  
  
```  
  
          boolean_expression OR boolean_expression  
or   
boolean_expression || boolean_expression  
```  
  
## 인수  
 `boolean_expression`  
 `Boolean`을 반환하는 유효한 식입니다.  
  
## 반환 값  
 조건 중 하나가 `true`이면 `true`이고 그렇지 않으면 `false`입니다.  
  
## 설명  
 OR는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 논리 연산자로 두 조건을 결합할 때 사용됩니다. 한 문에 논리 연산자를 둘 이상 사용하는 경우 OR 연산자가 AND 연산자 다음에 계산됩니다. 그러나 괄호를 사용하면 계산 순서를 변경할 수 있습니다.  
  
 이중 세로 막대\(&#124;&#124;\)는 OR 연산자와 같은 기능을 합니다.  
  
 다음 표에서는 가능한 입력 값과 반환 형식을 보여 줍니다.  
  
||`TRUE`|`FALSE`|`NULL`|  
|-|------------|-------------|------------|  
|`TRUE`|TRUE|TRUE|TRUE|  
|`FALSE`|TRUE|FALSE|NULL|  
|`NULL`|TRUE|NULL|NULL|  
  
## 예제  
 다음 Entity SQL 쿼리에서는 OR 연산자를 사용하여 두 `Boolean` 식을 결합합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  [방법: StructuralType 결과를 반환하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#OR](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#or)]  
  
## 참고 항목  
 [Entity SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)