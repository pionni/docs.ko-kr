---
title: "방법: 형식 라이브러리에서 Interop 어셈블리 생성"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- importing type library
- interop assemblies, generating
- Type Library Importer
- type libraries
- COM interop, importing type library
ms.assetid: 4afd40c3-68f2-41c5-8ec1-4951bc148b9c
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ff406fb14a21b0425444d04e98bbaca127d3687b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-generate-interop-assemblies-from-type-libraries"></a>방법: 형식 라이브러리에서 Interop 어셈블리 생성
[형식 라이브러리 가져오기(Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)는 COM 형식 라이브러리에 포함된 coclass 및 인터페이스를 메타데이터로 변환하는 명령줄 도구입니다. 이 도구는 형식 정보에 대한 interop 어셈블리 및 네임스페이스를 자동으로 만듭니다. 클래스 메타데이터가 제공된 후 관리되는 클라이언트는 COM 형식 인스턴스를 만들고 .NET 인스턴스인 것처럼 메서드를 호출할 수 있습니다. Tlbimp.exe는 전체 형식 라이브러리를 메타데이터로 즉시 변환하지만 형식 라이브러리에 정의된 형식 하위 집합에 대한 형식 정보를 생성할 수는 없습니다.  
  
### <a name="to-generate-an-interop-assembly-from-a-type-library"></a>형식 라이브러리에서 interop 어셈블리를 생성하려면  
  
1.  다음 명령을 사용합니다.  
  
     **tlbimp** \<*type-library-file*>  
  
     **/out:** 스위치를 추가하면 변경된 이름(예: LOANLib.dll)을 가진 interop 어셈블리가 생성됩니다. Interop 어셈블리 이름을 변경하면 원래 COM DLL과 구별하고 중복 이름으로 인해 발생할 수 있는 문제를 방지할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 명령은 `Loanlib` 네임스페이스에서 Loanlib.dll 어셈블리를 생성합니다.  
  
```  
tlbimp Loanlib.dll  
```  
  
 다음 명령은 변경된 이름(LOANLib.dll)을 가진 interop 어셈블리를 생성합니다.  
  
```  
tlbimp LoanLib.dll /out: LOANLib.dll  
```  
  
## <a name="see-also"></a>참고 항목  
 [형식 라이브러리를 어셈블리로 가져오기](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)   
 [.NET Framework에 COM 구성 요소 노출](../../../docs/framework/interop/exposing-com-components.md)

