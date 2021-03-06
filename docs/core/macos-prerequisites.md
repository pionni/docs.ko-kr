---
title: "Mac에서 .NET Core의 필수 구성 요소"
description: "macOS 컴퓨터에서.NET Core 응용 프로그램을 개발, 배포 및 실행하기 위해 지원되는 macOS 버전 및 .NET Core 종속성입니다."
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 07/07/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8feaee2cbfa55e23bd49c0ab76d995f15be343b4
ms.contentlocale: ko-kr
ms.lasthandoff: 07/28/2017

---

# <a name="prerequisites-for-net-core-on-mac"></a>Mac에서 .NET Core의 필수 구성 요소

이 문서에서는 macOS 컴퓨터에서.NET Core 응용 프로그램을 개발, 배포 및 실행하기 위해 필요한 지원되는 macOS 버전 및 .NET Core 종속성을 보여 줍니다. 다음에 나오는 지원되는 OS 버전 및 종속성은 Mac에서 .NET Core 앱을 개발하기 위한 세 가지 방법, 즉 [즐겨 사용하는 편집기를 통한 명령줄](tutorials/using-with-xplat-cli.md), [Visual Studio Code](https://code.visualstudio.com/) 및 [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)에 적용됩니다.

## <a name="supported-macos-versions"></a>지원되는 macOS 버전

.NET Core는 다음 macOS 버전에서 지원됩니다.

* macOS 10.12 "Sierra"
* macOS 10.11 "El Capitan"(.NET Core 1.x만)

[지원되는 OS 버전](https://github.com/dotnet/core/blob/master/roadmap.md#supported-os-versions)에서 지원되는 운영 체제의 전체 목록을 볼 수 있습니다.

## <a name="net-core-dependencies"></a>.NET Core 종속성

**.NET Core 1.x**

.NET Core 1.x를 macOS에서 실행할 때는 OpenSSL이 필요합니다. OpenSSL을 획득하는 쉬운 방법은 macOS용 [Homebrew("brew")](https://brew.sh/) 패키지 관리자를 사용하는 것입니다. *brew*를 설치한 후 터미널(명령) 프롬프트에서 다음 명령을 실행하여 OpenSSL을 설치합니다.

```console
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

[.NET 다운로드](https://www.microsoft.com/net/download/core)에서 .NET Core SDK를 다운로드하여 설치합니다. macOS에 설치하는 데 문제가 있는 경우 [1.0.0 알려진 문제](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md) 및 [1.0.1 알려진 문제](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md) 항목을 참조하세요.

**.NET Core 2.x**

[.NET 다운로드](https://www.microsoft.com/net/download/core)에서 .NET Core SDK를 다운로드하여 설치합니다. macOS에 설치하는 데 문제가 있는 경우 설치된 버전에 해당하는 [알려진 문제](https://github.com/dotnet/core/tree/master/release-notes/2.0) 항목을 참조하세요.

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

.NET Core SDK를 사용하여 .NET Core 응용 프로그램을 개발하기 위해 원하는 편집기를 사용할 수 있습니다. 그러나 통합 개발 환경의 Mac에서 .NET Core 응용 프로그램을 개발하려는 경우 [Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/)를 사용할 수 있습니다. 

Visual Studio for Mac을 사용하여 macOS에서 .NET Core로 개발하려면 다음이 필요합니다.

* 지원되는 macOS 운영 체제 버전
* OpenSSL(.NET Core 1.x 전용, .NET Core 2.x는 macOS에서 기본적으로 제공되는 보안 서비스를 사용함)
* .NET Core SDK for Mac
* [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

