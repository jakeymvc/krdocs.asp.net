ASP.NET 5 소개
==============

By Daniel Roth

.. toctree::
   :maxdepth: 0
   
   

ASP.NET 5를 설계 관점에서 한 마디로 설명하자면 ASP.NET의 심각한 재설계(significant redesign)라고 할 수 있다. 이번 주제는 ASP.NET 5 내의 새로운 개념을 소개하고 그 것들이 어떻게 현대적인 웹 앱을 개발하는데 도움이 되는지 설명하고자 한다.

ASP.NET 5는 무엇인가?
-------------------

ASP.NET 5는 닷넷을 사용하여 현대적인 클라우드 기반의 웹 애플리케이션을 만들기 위한 새로운 오픈소스이자 크로스-플랫폼 프레임워크다. 우리는 클라우드에 배포되거나 자체 호스팅 서버(on-premise)에서 동작하는 앱을 위한 최적의 개발 프레임워크를 제공하기 위해 프레임워크를 바닥부터 다시 만들었다. ASP.NET 5는 최소한의 오버헤드만으로 모듈화된 컴포넌트들로 구성되어 있기 때문에 솔루션을 구성하면서 유연성을 유지할 수 있다. 뿐만아니라, 여러분은 ASP.NET 5 애플리이션을 윈도우, 맥, 리눅스에서 개발하고 실행할 수 있다. ASP.NET 5는 `GitHub`_ 의 오픈 소스이다.


왜 ASP.NET 5를 만들었을까?
------------------------

ASP.NET 1.O의 최초 프리뷰가 나온 것이 어느 덧 15년 전의 일이다. 그 이래로 정말 많은 개발자들이 ASP.NET을 사용하여 훌륭한 웹 애플리케이션을 만들어 왔고 우리는 그 동안 수 많은 기능들을 추가하고 발전시켜왔다.

ASP.NET 5에서 우리는 꽤 많은 아키텍쳐 변경을 통해 군더더기 없이 모듈화된 코어(core) 웹 프레임워크를 만들고 있다. ASP.NET 5는 System.Web.dll 을 과감히 버리고 대신, 잘게 요소화된 NuGet 패키지들에 기반해서 여러분의 요구에 최적화된 앱을 만들 수 있게 해준다. 이렇게 사용한 만큼 지불하는(pay-for-what-you-use) 모델을 채택함으로써 애플리케이션에서 외부로 노출되는 것들이 줄어들어 보안 측면에서 개선을 기할 수 있고, 서비스 하는 부담 또한 줄어들어 성능면에서 개선효과를 볼 수 있다.

ASP.NET 5는 현대적인 웹 애플리케이션에 대한 필요를 염두에 두고 만들어졌다. 웹 사용자 인터페이스를 만드는 것, 클라이언트 측 프레임워크와 통합되는 Web API들을 만드는 것, 이런 개발 작업의 흐름이 하나의 통일된 스토리가 된다. ASP.NET 5는 또한 클라우드 준비된(cloud-ready) 프레임워크라고 할 수 있다. 환경 기반의 구성(environment-based configuration)을 도입하고, 빌트-인 종속성 주입(dependency injection)을 제공하기 때문이다.

보다 광범위한 개발자들의 관심을 끌기 위해, ASP.NET 5는 윈도우, 맥, 리눅스에서 크로스-플랫폼 개발을 지원한다. 전체 ASP.NET 5 스택은 오픈 소스이고 커뮤니티의 기여와 참여를 장려하고 있다. 비주얼 스튜디오는 완벽한 커맨드-라인 인터페이스도 지원하면서도 새로운 애자일 프로젝트 시스템을 도입했다. 그 덕에 여러분이 선택한 툴을 사용해서 개발할 수 있게 되었다.

정리하자면, 여러분은 ASP.NET 5에서 아래의 기초적인 개선사항들을 얻게 되었다.

* 새롭게 경량화되고 모듈화된 HTTP 요청 파이프라인
* IIS 또는 여러분 자신의 프로세스에서 셀프 호스트할 수 있는 능력
* 닷넷 코어에 기반한 진정한 sidy-by-side 앱 버전 관리(versioning)
* 모든 기능이 NuGet 패키지 형태로 추가
* NuGet 패키지들을 생성하고 사용하는 것에 대한 통합된 지원
* 웹 사용자 인터페이스와 웹 API를 위한 단일 웹 스택
* 클라우드 준비된 환경 기반의 구성
* 빌트-인 종속성 주입 기능
* 현대적인 웹 개발을 단순화 시킨 새로운 툴링(tooling)
* 윈도우, 맥, 리눅스에서 개발하고 실행할 수 있는 크로스-플랫폼
* 오픈 소스와 커뮤니티 중심


애플리케이션 해부하기
------------------

ASP.NET 5 애플리케이션은 `.NET Execution Environment (DNX)`_ 를 사용하여 작성되고 실행된다. 모든 ASP.NET 5 프로젝트는 곧 *DNX* 프로젝트이며 `ASP.NET Application Hosting`_ 패키지를 사용하여 통합된다.

ASP.NET 5 애플리케이션은 ``Startup`` 클래스를 사용하여 정의된다.

.. code-block:: c#

    public class Startup
    {
        public void ConfigureServices(IServiceCollection services)
        {
        }
        public void Configure(IApplicationBuilder app)
        {
        }
    }

``ConfigureServices`` 메서드는 애플리케이션에 사용될 서비스들을 정의하고 ``Configure`` 메서드는 요청 파이프라인을 구성할 미들웨어를 정의하는데 사용된다. 보다 자세한 사항은 `Understanding ASP.NET 5 Web Apps`_ 아티클을 참조하자.

서비스
-----

서비스는 애플리케이션에서 공통적으로 사용하고자 하는 목적의 컴포넌트다. 서비스들은 종속성 주입을 통해 사용이 가능하다. ASP.NET 5 는 간단한 빌트-인 제어 역전 (IoC) 컨테이너를 포함하고 있는데 생성자를 이용한 주입 방식을 기본으로 지원하고 있다. 그러나, 여러분이 사용하는 IoC 컨테이너로 쉽게 대체할 수도 있다. 자세한 내용은 `🔧 Dependency Injection`_ 아티클을 참조하자.

ASP.NET 5 에서 서비스는 세 가지 종류(singleton, scoped, transient)로 구분된다. Transient 서비스는 컨테이너로부터 요청될 때마다 생성되고 Scoped 서비스는 현재 scope에 서비스가 존재하지 않을 때만 서비스를 생성한다. 웹 애플리케이션에서 컨테이너의 범주는 매 요청에 해당하므로 scoped 서비스는 요청 당 서비스로 생각할 수 있다. 반면, Singleton 서비스는 오직 한번만 생성된다.

미들웨어
-------

ASP.NET 5 에서는 `🔧 Middleware`_ 를 사용하여 요청 파이프라인을 구성한다. ASP.NET 5 미들웨어는 ``HttpContext`` 에 대해 비동기 로직을 수행하고 선택적으로 다음 미들웨어를 호출하거나 요청 처리 작업을 중단한다. 일반적으로 미들웨어에 대응하는 ``IApplicationBuilder`` 의 확장 메서드를 ``Configure`` 메서드에서 호출하는 것으로 요청 파이프라인을 작성한다.

ASP.NET 5 는 미리 작성된 풍부한 미들웨어를 제공한다. 아래는 그 중 일부이다.

* `🔧 Working with Static Files`_
* `🔧 Routing`_
* `Diagnostics`_
* `Authentication`_

여러분은 여러분만의 custom middleware 를 작성할 수도 있고 OWIN 기반의 미들웨어를 작성할 수도 있는데 OWIN과 관련하여 자세한 내용은 `OWIN`_ 아티클을 참조하자.

서버
---

ASP.NET 애플리케이션 호스팅 모델은 요청을 직접 리스닝하지 않는다. 그 대신, HTTP 서버 구현에 의지하여 애플리케이션에 대한 요청을 (HttpContext 와 작용하는 기능적인 인터페이스들의 모음으로서) 표면화한다.

ASP.NET 5 는 IIS에서 운영하거나 자신의 프로세스에서 셀프 호스팅하는 서버를 지원한다. 윈도우에서는 HTTP.sys 에 기반한 `WebListener`_ 를 통해 IIS 밖에서 애플리케이션을 호스팅할 수 있다. 또한, 비 윈도우 환경에서도 크로스-플랫폼 `Kestrel`_ 웹 서버를 사용하여 여러분의 애플리케이션을 호스팅할 수 있다.

웹 루트 (Web root)
------------------

애플리케이션의 웹 루트는 프로젝트의 루트라고 할 수 있다. 이 곳으로부터 예를 들면, 정적 파일에 대한 접근 시도 같은 HTTP 요청이 처리된다. ASP.NET 5 애플리케이션의 웹 루트는 project.json 파일의 “webroot” 속성을 사용하여 설정된다.

구성 (Configuration)
--------------------

ASP.NET 5는 간단한 이름-값 쌍을 다루는 새로운 구성모델을 사용하며 이 새 모델은 System.Configuration 또는 web.config 에 기반하지 않는다. 새 구성 모델은 구성 제공자(configuration provider)의 순차적인 집합에서 정보를 얻는다. 빌트-인 구성 제공자는 XML, JSON, INI 파일등 다양한 파일 형식을 지원하며 또한, 환경 기반의 구성을 가능케 하는 환경 변수도 지원한다. 여러분은 이와 더불어 사용자 정의 구성 제공자를 작성할 수도 있다. 개발환경, 운영환경 처럼 환경이 ASP.NET 5에서는 최고의 개념이고 환경 변수를 통해 설정될 수도 있다.

.. code-block:: c#

    // Setup configuration sources.
    var configuration = new Configuration()
        .AddJsonFile("config.json")
        .AddJsonFile($"config.{env.EnvironmentName}.json", optional: true);
    if (env.IsEnvironment("Development"))
    {
        // This reads the configuration keys from the secret store.
        // For more details on using the user secret store see http://go.microsoft.com/fwlink/?LinkID=532709
        configuration.AddUserSecrets();
    }
    configuration.AddEnvironmentVariables();
    Configuration = configuration; 

새로운 구성모델에 대한 자세한 내용은 `Configuration`_ 아티클을 참조하고 ASP.NET 5에서 환경과 관련된 작업에 대한 자세한 내용은 `Working with Multiple Environments`_ 아티클을 참조하자.

클라이언트 측 개발
---------------

ASP.NET 5는 클라이언트 측 프레임워크와 매끄럽게 통합되도록 설계되었고 `AngularJS`_ , `KnockoutJS`_ and `Bootstrap`_ 와 같은 프레임워크를 포함한다. 이와 관련하여 자세한 내용은 `Client-Side Development`_ 아티클을 참조하자.

.. _`GitHub`: https://github.com/aspnet/home
.. _`.NET Execution Environment (DNX)`: http://docs.asp.net/en/latest/dnx/overview.html
.. _`ASP.NET Application Hosting`: https://www.nuget.org/packages/Microsoft.AspNet.Hosting
.. _`Understanding ASP.NET 5 Web Apps`: http://docs.asp.net/en/latest/conceptual-overview/understanding-aspnet5-apps.html
.. _`🔧 Dependency Injection`: http://docs.asp.net/en/latest/fundamentals/dependency-injection.html
.. _`🔧 Middleware`: http://docs.asp.net/en/latest/fundamentals/middleware.html
.. _`🔧 Working with Static Files`: http://docs.asp.net/en/latest/fundamentals/static-files.html
.. _`🔧 Routing`: http://docs.asp.net/en/latest/fundamentals/routing.html
.. _`Diagnostics`: http://docs.asp.net/en/latest/fundamentals/diagnostics.html
.. _`Authentication`: http://docs.asp.net/en/latest/security/index.html
.. _`OWIN`: http://docs.asp.net/en/latest/fundamentals/owin.html
.. _`WebListener`: https://www.nuget.org/packages/Microsoft.AspNet.Server.WebListener
.. _`AngularJS`: https://angularjs.org/
.. _`Kestrel`: https://www.nuget.org/packages/Kestrel
.. _`Configuration`: http://docs.asp.net/en/latest/fundamentals/configuration.html
.. _`Working with Multiple Environments`: http://docs.asp.net/en/latest/fundamentals/environments.html
.. _`KnockoutJS`: http://knockoutjs.com/
.. _`Bootstrap`: http://getbootstrap.com/
.. _`Client-Side Development`: http://docs.asp.net/en/latest/client-side/index.html



