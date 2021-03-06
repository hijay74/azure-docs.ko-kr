### <a name="server-auth"></a>방법: 공급자를 사용하여 인증(서버 흐름)
모바일 서비스가 앱에서 인증 프로세스를 관리하게 하려면 앱을 ID 공급자에 등록해야 합니다. 그런 다음, Azure 앱 서비스에서 공급자로부터 제공된 응용 프로그램 ID 및 암호를 구성해야 합니다. 자세한 내용은 [앱에 인증 추가] 자습서를 참조하세요.

ID 공급자를 등록하고 나면 공급자의 이름을 사용하여 .login() 메서드를 호출합니다. 예를 들어 Facebook으로 로그인하려면 다음 코드를 사용합니다.

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

Facebook 이외의 ID 공급자를 사용하는 경우 위의 login 메서드에 전달된 값을 `microsoftaccount`, `facebook`, `twitter`, `google`, `aad` 중 하나로 변경합니다.

이 경우 Azure 앱 서비스는 선택한 공급자의 로그인 페이지를 표시하고 ID 공급자 로그인 후 앱 서비스 인증 토큰을 생성하여 OAuth 2.0 인증 흐름을 관리합니다. login 함수를 완료하면 사용자 ID와 앱 서비스 인증 토큰을 각각 userId 및 authenticationToken 필드에 표시하는 JSON 개체(user)가 반환됩니다. 이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.

### <a name="client-auth"></a>방법: 공급자를 사용하여 인증(클라이언트 흐름)
앱이 독립적으로 ID 공급자에 연결한 후 반환된 토큰을 인증을 위해 앱 서비스에 제공할 수도 있습니다. 이 클라이언트 흐름을 사용하면 단일 로그인 환경을 사용자에게 제공하거나 ID 공급자로부터 더 많은 사용자 데이터를 검색할 수 있습니다.

#### 소셜 인증 기본 예제
이 예제에서는 인증을 위해 Facebook 클라이언트 SDK를 사용합니다.

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```
이 예제에서는 각 공급자 SDK에서 제공된 토큰이 token 변수에 저장되어 있다고 가정합니다.

#### Microsoft 계정 예제
다음 예제는 Microsoft 계정을 사용하여 Windows 스토어 앱용 Single Sign-On을 지원하는 Live SDK를 사용합니다.

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});
```

이 예제는 login 함수를 호출하여 앱 서비스에 제공된 토큰을 Live Connect에서 가져옵니다.

### <a name="auth-getinfo"></a>방법: 인증된 사용자에 대한 정보 얻기
모든 AJAX 메서드를 사용하여 현재 사용자에 대한 인증 정보를 `/.auth/me` 끝점에서 검색할 수 있습니다. `X-ZUMO-AUTH` 헤더를 인증 토큰으로 설정했는지 확인합니다. 인증 토큰은 `client.currentUser.mobileServiceAuthenticationToken`에 저장되어 있습니다. 예를 들어, fetch API를 사용하려면 다음과 같이 합니다.

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

fetch는 npm 패키지로 제공되거나 CDNJS에서 브라우저 다운로드할 수 있습니다. 또한 jQuery 또는 AJAX API를 사용하여 정보를 가져올 수도 있습니다. 데이터는 JSON 개체로 수신됩니다.

<!---HONumber=AcomDC_0615_2016-->