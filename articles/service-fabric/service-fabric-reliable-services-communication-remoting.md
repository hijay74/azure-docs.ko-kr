---
title: 서비스 패브릭의 서비스 원격 호출 | Microsoft Docs
description: 서비스 패브릭 원격 호출을 사용하면 클라이언트와 서비스가 원격 프로시저 호출을 사용하여 서비스와 통신할 수 있도록 합니다.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman

ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 07/06/2016
ms.author: vturecek

---
# Reliable Services로 서비스 원격 호출
특정한 통신 프로토콜 또는 스택에 얽매여 있지 않는 서비스(예: WebAPI, WCF(Windows Communication Foundation) 등)의 경우, Reliable Services 프레임워크가 원격 메커니즘을 제공하여 서비스에 대한 원격 프로시저 호출을 신속하고 간편하게 설정합니다.

## 서비스에 원격 호출 설정
서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.

1. 서비스로 구현할 인터페이스를 만듭니다. 이 인터페이스는 서비스의 원격 프로시저 호출에 사용할 수 있는 메서드를 정의합니다. 메서드는 작업을 반환하는 비동기 메서드여야 합니다. 인터페이스는 서비스에 원격 호출 인터페이스가 있다는 것을 신호하기 위해 `Microsoft.ServiceFabric.Services.Remoting.IService`를 구현해야 합니다.
2. 서비스에서 원격 수신기를 사용합니다. 이것은 원격 호출 기능을 제공하는 `ICommunicationListener` 구현입니다. `Microsoft.ServiceFabric.Services.Remoting.Runtime` 네임스페이스는 기본 원격 전송 프로토콜을 사용하여 원격 수신기를 만드는 데 사용할 수 있는 상태 비저장 및 상태 저장 서비스에 대해 확장 메서드인 `CreateServiceRemotingListener`을 포함합니다.

예를 들어 다음의 상태 비저장 서비스는 단일 메서드를 노출하여 원격 프로시저 호출에 "Hello World"를 가져옵니다.

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> GetHelloWorld();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorld()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context => 
            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> 서비스 인터페이스의 인수 및 반환 형식은 간단한 형식, 복합 형식 또는 사용자 지정 형식이 가능하지만 .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)에 의한 직렬화가 가능해야 합니다.
> 
> 

## 원격 서비스 메서드 호출
원격 스택을 사용하여 서비스에서 메서드를 호출하는 작업은 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 클래스를 통해 서비스에 대한 로컬 프록시를 사용하여 수행됩니다. `ServiceProxy` 메서드는 서비스가 구현하는 것과 동일한 인터페이스를 사용하여 로컬 프록시를 만듭니다. 이 프록시를 통해 원격으로 인터페이스의 메서드를 간단하게 호출할 수 있습니다.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.GetHelloWorld();

```

원격 호출 프레임워크는 서비스에 throw된 예외를 클라이언트에 전파합니다. 따라서 `ServiceProxy`을 사용하여 클라이언트에서 논리를 예외 처리하는 작업은 서비스가 throw하는 예외를 직접 처리할 수 있습니다.

## 다음 단계
* [Reliable Services에서 OWIN을 사용하는 Web API](service-fabric-reliable-services-communication-webapi.md)
* [Reliable Services와 WCF 통신](service-fabric-reliable-services-communication-wcf.md)
* [Reliable Services에 대한 통신 보안 유지](service-fabric-reliable-services-secure-communication.md)

<!---HONumber=AcomDC_0713_2016-->