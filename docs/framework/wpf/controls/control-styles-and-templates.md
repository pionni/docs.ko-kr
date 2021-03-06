---
title: "Control 스타일 및 템플릿 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "AutoGeneratedOrientationPage"
helpviewer_keywords: 
  - "ControlTemplate[WPF]"
  - "요소[WPF]"
  - "상태[WPF]"
  - "스타일[WPF]"
  - "템플릿[WPF]"
ms.assetid: c19049bb-5ceb-492d-afd2-751dca0ed8e3
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 35
---
# Control 스타일 및 템플릿
WPF\(Windows Presentation Foundation\)의 컨트롤에는 해당 컨트롤의 [시각적 트리](GTMT)가 있는 <xref:System.Windows.Controls.ControlTemplate>이 있습니다.  컨트롤의 <xref:System.Windows.Controls.ControlTemplate>을 수정하면 해당 컨트롤의 구조와 모양을 변경할 수 있습니다.  컨트롤의 시각적 트리 부분만 바꿀 수 있는 방법은 없습니다. 즉, 컨트롤의 시각적 트리를 변경하려면 컨트롤의 <xref:System.Windows.Controls.Control.Template%2A> 속성을 새로운 전체 <xref:System.Windows.Controls.ControlTemplate>으로 설정해야 합니다.  
  
 바탕 화면 테마는 사용할 리소스 사전을 결정합니다.  바탕 화면 테마는 사용할 리소스 사전을 결정합니다.  바탕 화면 테마의 리소스 사전을 구하려면 [Default WPF Themes](http://go.microsoft.com/fwlink/?LinkID=158252)를 참조하십시오.  
  
 다음 표에서는 리소스 사전 파일 이름과 해당하는 바탕 화면 테마를 설명합니다.  
  
|테마 파일|바탕 화면 테마|  
|-----------|--------------|  
|Classic.xaml|Windows XP 운영 체제의 기본 Windows 테마\(Windows 95, Windows 98 및 Windows 2000 기반\)|  
|Luna.NormalColor.xaml|Windows XP의 기본 파랑 테마|  
|Luna.Homestead.xaml|Windows XP의 올리브 테마|  
|Luna.Metallic.xaml|Windows XP의 은색 테마|  
|Royale.NormalColor.xaml|Windows XP Media Center Edition 운영 체제의 기본 테마|  
|Aero.NormalColor.xaml|Windows Vista 운영 체제의 기본 테마|  
  
## 단원 내용  
 [Button 스타일 및 템플릿](../../../../docs/framework/wpf/controls/button-styles-and-templates.md)  
 [Calendar 스타일 및 템플릿](../../../../docs/framework/wpf/controls/calendar-styles-and-templates.md)  
 [CheckBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/checkbox-styles-and-templates.md)  
 [ComboBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/combobox-styles-and-templates.md)  
 [ContextMenu 스타일 및 템플릿](../../../../docs/framework/wpf/controls/contextmenu-styles-and-templates.md)  
 [DataGrid 스타일 및 템플릿](../../../../docs/framework/wpf/controls/datagrid-styles-and-templates.md)  
 [DatePicker 스타일 및 템플릿](../../../../docs/framework/wpf/controls/datepicker-syles-and-templates.md)  
 [DocumentViewer 스타일 및 템플릿](../../../../docs/framework/wpf/controls/documentviewer-styles-and-templates.md)  
 [Expander 스타일 및 템플릿](../../../../docs/framework/wpf/controls/expander-styles-and-templates.md)  
 [Frame 스타일 및 템플릿](../../../../docs/framework/wpf/controls/frame-styles-and-templates.md)  
 [GroupBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/groupbox-styles-and-templates.md)  
 [Label 스타일 및 템플릿](../../../../docs/framework/wpf/controls/label-styles-and-templates.md)  
 [ListBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/listbox-styles-and-templates.md)  
 [ListView 스타일 및 템플릿](../../../../docs/framework/wpf/controls/listview-styles-and-templates.md)  
 [Menu 스타일 및 템플릿](../../../../docs/framework/wpf/controls/menu-styles-and-templates.md)  
 [NavigationWindow 스타일 및 템플릿](../../../../docs/framework/wpf/controls/navigationwindow-styles-and-templates.md)  
 [PasswordBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/passwordbox-syles-and-templates.md)  
 [ProgressBar 스타일 및 템플릿](../../../../docs/framework/wpf/controls/progressbar-styles-and-templates.md)  
 [RadioButton 스타일 및 템플릿](../../../../docs/framework/wpf/controls/radiobutton-styles-and-templates.md)  
 [RepeatButton 스타일 및 템플릿](../../../../docs/framework/wpf/controls/repeatbutton-syles-and-templates.md)  
 [ScrollBar 스타일 및 템플릿](../../../../docs/framework/wpf/controls/scrollbar-styles-and-templates.md)  
 [ScrollViewer 스타일 및 템플릿](../../../../docs/framework/wpf/controls/scrollviewer-styles-and-templates.md)  
 [Slider 스타일 및 템플릿](../../../../docs/framework/wpf/controls/slider-styles-and-templates.md)  
 [StatusBar 스타일 및 템플릿](../../../../docs/framework/wpf/controls/statusbar-styles-and-templates.md)  
 [TabControl 스타일 및 템플릿](../../../../docs/framework/wpf/controls/tabcontrol-styles-and-templates.md)  
 [TextBox 스타일 및 템플릿](../../../../docs/framework/wpf/controls/textbox-styles-and-templates.md)  
 [Thumb 스타일 및 템플릿](../../../../docs/framework/wpf/controls/thumb-syles-and-templates.md)  
 [ToggleButton 스타일 및 템플릿](../../../../docs/framework/wpf/controls/togglebutton-syles-and-templates.md)  
 [ToolBar 스타일 및 템플릿](../../../../docs/framework/wpf/controls/toolbar-styles-and-templates.md)  
 [ToolTip 스타일 및 템플릿](../../../../docs/framework/wpf/controls/tooltip-styles-and-templates.md)  
 [TreeView 스타일 및 템플릿](../../../../docs/framework/wpf/controls/treeview-styles-and-templates.md)  
 [Window 스타일 및 템플릿](../../../../docs/framework/wpf/controls/window-styles-and-templates.md)  
  
## 참조  
 <xref:System.Windows.Controls>  
  
 <xref:System.Windows.Controls.ControlTemplate>  
  
## 관련 단원  
 [컨트롤 제작 개요](../../../../docs/framework/wpf/controls/control-authoring-overview.md)  
  
 [스타일 지정 및 템플릿](../../../../docs/framework/wpf/controls/styling-and-templating.md)