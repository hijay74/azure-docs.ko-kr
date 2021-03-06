---
title: Azure DevTest Labs에서 Azure 마켓플레이스 이미지 설정 구성 | Microsoft Docs
description: Azure DevTest Labs에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지 구성
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''

ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: tarcher

---
# Azure DevTest Labs에서 Azure 마켓플레이스 이미지 설정 구성
DevTest Lab에서는 Azure 마켓플레이스 이미지를 랩에서 사용하도록 구성한 방법에 따라 Azure 마켓플레이스 이미지를 기준으로 VM을 만들 수 있습니다. 이 문서에서는 랩에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지(있는 경우)를 지정하는 방법을 보여 줍니다.

## VM을 만들 때 허용되는 Azure 마켓플레이스 이미지를 선택합니다.
1. [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.
2. **서비스 더 보기**를 선택한 후 목록에서 **DevTest Lab**을 선택합니다.
3. 랩 목록에서 원하는 랩을 탭합니다.
4. 랩의 블레이드에서 **구성**을 선택합니다.
5. 랩의 **구성** 블레이드에서 **마켓플레이스 이미지**를 선택합니다.
6. 모든 정규화된 Azure 마켓플레이스 이미지를 새 VM의 기반으로 사용할 수 있게 할지 여부를 지정합니다. **예**를 선택하는 경우 다음 조건을 모두 충족하는 모든 Azure 마켓플레이스 이미지가 랩에서 허용됩니다.
   
   * 이 이미지는 단일 VM을 만듭니다. **그리고**
   * 이 이미지는 Azure Resource Manager를 사용하여 VM을 프로비전합니다. **그리고**
   * 이 이미지는 추가 라이선스 계획을 구입하지 않아도 사용할 수 있습니다.
     
     이미지를 허용하지 않거나 사용할 수 있는 이미지를 지정하려면 **아니요**를 선택합니다.
     
     ![모든 마켓플레이스 이미지를 VM에 대한 기본 이미지로 사용할 수 있도록 허용하는 옵션](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. 이전 단계에 대해 **아니요**를 선택하는 경우 **허용 이미지/모두 선택** 확인란을 사용할 수 있게 됩니다. 검색 상자와 함께 이 옵션을 사용하면 목록에 표시된 모든 항목을 빠르게 선택하거나 선택 취소할 수 있습니다. 각 이미지의 해당 확인란을 선택하여 VM 만들기를 개별적으로 허용하려는 Azure 마켓플레이스 이미지를 선택할 수도 있습니다. 랩에서 Azure 마켓플레이스 이미지를 사용하도록 허용하지 않으려면 목록에서 아무 것도 선택하지 않습니다.
   
    ![VM에 대한 기본 이미지로 사용할 수 있는 Azure 마켓플레이스 이미지를 지정할 수 있습니다.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## 다음 단계
VM을 만들 때 Azure Marketplace 이미지를 허용하는 방법을 구성한 후에는 [랩에 VM을 추가](devtest-lab-add-vm-with-artifacts.md)해야 합니다.

<!---HONumber=AcomDC_0907_2016-->