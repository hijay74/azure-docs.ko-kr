---
title: Media Services PlayReady 라이선스 템플릿 개요
description: 이 토픽에서는 PlayReady 라이선스를 구성하는 데 사용되는 PlayReady 라이선스 템플릿에 대해 간략히 설명합니다.
author: juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''

ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako

---
# <a name="media-services-playready-license-template-overview"></a>Media Services PlayReady 라이선스 템플릿 개요
Azure 미디어 서비스는 현재 Microsoft PlayReady 라이선스를 배달하는 서비스를 제공합니다. 최종 사용자 플레이어(예: Silverlight)가 PlayReady로 보호된 콘텐츠를 재생하려고 하면 라이선스 배달 서비스로 요청을 보내 라이선스를 얻습니다. 라이선스 서비스에서 요청을 승인하면 클라이언트로 전송하여 지정된 콘텐츠의 암호를 해독하고 재생하는 데 사용할 수 있는 라이선스가 발급됩니다.

또한 미디어 서비스는 PlayReady 라이선스를 구성할 수 있는 API를 제공합니다. 라이선스에는 사용자가 보호된 콘텐츠를 재생하려고 할 때 PlayReady DRM 런타임에서 적용하도록 하려는 권한 및 제한이 포함됩니다.
지정할 수 있는 PlayReady 라이선스 제한 사항의 몇 가지 예는 다음과 같습니다.

* 라이선스가 유효한 날짜/시간.
* 라이선스가 만료될 대 날짜/시간 값. 
* 클라이언트의 영구 저장소에 라이선스를 저장할지 여부. 일반적으로 영구 라이선스는 콘텐츠의 오프라인 재생을 허용하는 데 사용됩니다.
* 플레이어에서 콘텐츠를 재생해야 하는 최소 보안 수준. 
* 오디오/비디오 콘텐츠에 대한 출력 컨트롤의 출력 보호 수준. 
* 자세한 내용은 [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) (영문) 문서에서 출력 컨트롤 섹션(3.5)을 참조하세요.

> [!NOTE]
> 현재 PlayReady 라이선스의 PlayRight만 구성할 수 있습니다(이 권한은 필수임). PlayRight는 콘텐츠를 재생할 능력을 클라이언트에 제공합니다. PlayRight를 사용하여 재생과 관련된 제한 사항을 구성할 수 있습니다. 자세한 내용은 [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight)를 참조하세요.
> 
> 

미디어 서비스를 사용하여 PlayReady 라이선스를 구성하려면 미디어 서비스 PlayReady 라이선스 템플릿을 구성해야 합니다. 템플릿은 XML로 정의됩니다.

다음 예제에서는 기본 스트리밍 라이선스를 구성하는 가장 간단하고 가장 일반적인 템플릿을 보여 줍니다. 이 라이선스를 보유한 클라이언트는 PlayReady 보호 콘텐츠를 재생할 수 있습니다.

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

XML은 PlayReady 라이선스 템플릿 XML 스키마 섹션에 정의된 PlayReady 라이선스 템플릿 XML 스키마를 따릅니다.

미디어 서비스는 XML에 대해 serialize 및 deserialize하는 데 사용할 수 있는 일련의 .NET 클래스를 정의합니다. 기본 클래스에 대한 설명은 [Media Services .NET 클래스](media-services-playready-license-template-overview.md#classes)를 참조하세요. 이 클래스는 라이선스 템플릿을 구성하는 데 사용됩니다.

.NET 클래스를 사용하여 PlayReady 라이선스 템플릿을 구성하는 종단 간 예제는 [PlayReady 동적 암호화 및 라이선스 배달 서비스 사용](https://msdn.microsoft.com/library/azure/dn783467.aspx)을 참조하세요.

## <a name="<a-id="classes"></a>media-services-.net-classes-that-are-used-to-configure-license-templates"></a><a id="classes"></a>라이선스 템플릿을 구성하는 데 사용되는 미디어 서비스 .NET 클래스
미디어 서비스 PlayReady 라이선스 템플릿을 구성하는 데 사용되는 기본 .NET 클래스는 다음과 같습니다. 이들 클래스는 [PlayReady 라이선스 템플릿 XML 스키마](media-services-playready-license-template-overview.md#schema)에 정의된 유형에 매핑됩니다.

[MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) 클래스는 미디어 서비스 라이선스 템플릿 XML에 대해 serialize 및 deserialize하는 데 사용됩니다.

### <a name="playreadylicenseresponsetemplate"></a>PlayReadyLicenseResponseTemplate
[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - 이 클래스는 다시 최종 사용자에게 보내는 응답에 대한 템플릿을 나타냅니다. 이 클래스는 라이선스 서버와 응용 프로그램 간의 사용자 지정 데이터 문자열에 대한 필드와 하나 이상의 라이선스 템플릿 목록을 포함합니다.

템플릿 계층 구조에서 “최상위” 클래스입니다. 응답 템플릿에 라이선스 템플릿 목록이 포함되고 라이선스 템플릿에 serialize될 템플릿 데이터를 구성하는 모든 기타 클래스가 직접 또는 간접적으로 포함됨을 의미합니다.

### <a name="playreadylicensetemplate"></a>PlayReadyLicenseTemplate
[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - 이 클래스는 최종 사용자에게 반환될 PlayReady 라이선스를 만들기 위한 라이선스 템플릿을 나타냅니다. 이 클래스는 라이선스의 콘텐츠 키 데이터 및 콘텐츠 키를 사용할 때 PlayReady DRM 런타임에서 적용될 모든 권한이나 제한 사항을 포함합니다.

### <a name="<a-id="playreadyplayright"></a>playreadyplayright"></a><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight
[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - 이 클래스는 PlayReady 라이선스의 PlayRight를 나타냅니다. 라이선스 및 재생 관련 정책의 PlayRight 자체에 구성된 0개 이상의 제한 사항이 적용되는 콘텐츠를 재생할 권한을 사용자에게 부여합니다. PlayRight에 대한 대부분 정책은 특정 출력을 사용할 때 적용되어야 하는 제한 사항과 콘텐츠가 재생될 수 있는 출력 유형을 제어하는 출력 제한 사항과 관련이 있습니다. 예를 들어 DigitalVideoOnlyContentRestriction이 사용되면 DRM 런타임에서는 디지털 출력을 통해 비디오가 재생되도록 허용합니다(아날로그 비디오 출력은 콘텐츠를 전달하도록 허용되지 않음).

> [!IMPORTANT]
> 이들 제한 사항 유형은 매우 강력할 수 있지만 소비자 환경에도 영향을 줄 수 있습니다. 출력 보호가 너무 제한적으로 구성되면 몇몇 클라이언트에서는 콘텐츠를 재생하지 못할 수 있습니다. 자세한 내용은 [PlayReady 준수 규칙](https://www.microsoft.com/playready/licensing/compliance/) 문서를 참조하세요.
> 
> 

Silverlight에서 지원하는 보호 수준의 예는 [출력 보호를 위한 Silverlight 지원](http://go.microsoft.com/fwlink/?LinkId=617318)을 참조하세요.

## <a name="<a-id="schema"></a>playready-license-template-xml-schema"></a><a id="schema"></a>PlayReady 라이선스 템플릿 XML 스키마
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!--HONumber=Oct16_HO2-->


