---
title: "사물 인터넷에 대한 Azure 솔루션 | Microsoft Docs"
description: "샘플 솔루션 아키텍처 및 이를 Azure IoT Suite 및 미리 구성된 솔루션과 연결하는 방법을 포함한 Azure IoT 개요"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2016
ms.author: dobett
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 87b9b0685ab3401a617e1089312a65d2b5a90099


---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a>Azure IoT Suite
Microsoft Azure IoT Suite는 [원격 모니터링][lnk 미리 구성된 솔루션] 및 [예측 유지 관리][lnk 예측 유지 관리]와 같이 일반적인 IoT 시나리오를 해결하는 일련의 미리 구성된 확장 가능 솔루션을 통해 빠르게 시작할 수 있는 엔터프라이즈급 솔루션입니다. 이러한 솔루션은 이 문서에서 설명한 IoT 솔루션 아키텍처의 구현입니다.

미리 구성된 솔루션은 [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], [Azure 저장소][Azure 저장소] 및 솔루션 특정 관리 콘솔과 같은 미리 구성된 Azure 서비스를 시작하는 시뮬레이션된 장치를 포함한 완전히 작동하는 종단 간 솔루션입니다. 미리 구성된 솔루션은 프로덕션에 사용할 준비가 된 입증된 코드를 포함하며 이 코드는 고유한 특정 IoT 시나리오를 구현하도록 사용자 지정하고 확장할 수 있습니다.

다수의 미리 구성된 솔루션이 사용하는 [Azure IoT Hub][Azure IoT Hub] 서비스에 관심이 있을 수 있습니다. [Azure IoT Hub][Azure IoT Hub]는 미리 구성된 솔루션 아키텍처에서 사용되는 장치 및 클라우드 간에 안전하고 신뢰할 수 있는 양방향 통신을 제공합니다.

## <a name="next-steps"></a>다음 단계
IoT Suite 및 미리 구성된 솔루션에 대해 계속 알아보려면 다음 리소스를 탐색합니다.

* [Azure IoT Suite란?][lnk-whatissuite]
* [미리 구성된 Azure IoT Suite 솔루션은 무엇입니까?][lnk-whatarepreconfigured]

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure 이벤트 허브]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure 스트림 분석]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure 기계 학습]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure 저장소]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md



<!--HONumber=Nov16_HO2-->


