---
title: "방법: FTP로 디렉터리 내용 나열"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 130c64c9-7b7f-4672-9b3b-d946bd2616c5
caps.latest.revision: 5
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 08edb5be23d55a9a825ca80a8e575cb02b5f07a8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-list-directory-contents-with-ftp"></a>방법: FTP로 디렉터리 내용 나열
이 샘플은 FTP 서버의 디렉터리 콘텐츠를 나열하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
  
```csharp  
using System;  
using System.IO;  
using System.Net;  
using System.Text;  
  
namespace Examples.System.Net  
{  
    public class WebRequestGetExample  
    {  
        public static void Main ()  
        {  
            // Get the object used to communicate with the server.  
            FtpWebRequest request = (FtpWebRequest)WebRequest.Create("ftp://www.contoso.com/");  
            request.Method = WebRequestMethods.Ftp.ListDirectoryDetails;  
  
            // This example assumes the FTP site uses anonymous logon.  
            request.Credentials = new NetworkCredential ("anonymous","janeDoe@contoso.com");  
  
            FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
  
            Stream responseStream = response.GetResponseStream();  
            StreamReader reader = new StreamReader(responseStream);  
            Console.WriteLine(reader.ReadToEnd());  
  
            Console.WriteLine("Directory List Complete, status {0}", response.StatusDescription);  
  
            reader.Close();  
            response.Close();  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   **System.Net** 네임스페이스에 대한 참조.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
  
## <a name="net-framework-security"></a>.NET Framework 보안

