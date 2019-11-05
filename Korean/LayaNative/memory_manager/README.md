#현존지 관리

현존이 너무 커서 혹은 개발자가 명존하는 것을 잊어버리기 위해 응용 프로그램이 시스템 직접 kill 위험에 의해 LayaPlayer 에서 현존 관리 메커니즘이 있습니다. 원리도 1개 그대로 보여 줍니다.


![图1](img/1.jpg)  




**왜 자동적으로 보관 관리가 필요합니까? 초기 iphone4S, ipad2) 또는 초기 android 설비, 메모리는 512MB, 응용 프로그램 메모리가 270MB 정도면 응용 프로그램이 직접 kill, 사용자 체험이 매우 좋지 않습니다. 게임에서 자원을 가장 많이 사용하는 것은 그림자원입니다.**

###1. 어떻게 설정



####1.1. 기본 설정

저장소 size, 개발자는 프로그램을 시작하기 전에 설정해야 합니다. 개발자가 설정하지 않으면 LayaPlayer 내부에 장치의 메모리 상황에 따라 기본값 설정을 설정합니다.

```javascript

var nMem = conchConfig.getTotalMem();
if (nMem <= 524288) {
    conchConfig.maxTextureMemSize = 64 * 1024 * 1024;
}
else if (nMem > 524288 && nMem <= 1048576) {
    conchConfig.maxTextureMemSize = 84 * 1024 * 1024;
}
else if (nMem > 1048576) {
    conchConfig.maxTextureMemSize = 128 * 1024 * 1024;
}
```




####1.2. 개발자 설정
개발자도 자신의 수요에 따라 설정을 할 수 있으며, config.js 설정에 따라 코드:


```javascript

var loadingView= window.loadingView;
if(loadingView)
{
    loadingView.loadingAutoClose=true;
    loadingView.bgColor("#ffffff");
    loadingView.setFontColor("#000000");
    loadingView.setTips(["新世界的大门即将打开", "敌军还有30秒抵达战场", "妈妈说，心急吃不了热豆腐"]);
}
//在这进行设定
var nMem = conchConfig.getTotalMem();
if (nMem <= 524288) {
    conchConfig.maxTextureMemSize = 80 * 1024 * 1024;
}
else if (nMem > 524288 && nMem <= 1048576) {
    conchConfig.maxTextureMemSize = 128 * 1024 * 1024;
}
else if (nMem > 1048576) {
    conchConfig.maxTextureMemSize = 200 * 1024 * 1024;
}
```


**Tips: 이 현존지 size 의 설정은 응용 프로그램이 시작하는 곳에 놓아야 합니다. 프로그램에서 움직일 수 없습니다. config.js 는 Layaplayer가 시작하면 바로 실행될 js입니다. 그래서 여기에 두는 것이 가장 안전합니다.**



####1.3. config.js 어디 있어요?

ios 버전: 프로젝트의 resourcescriptsconfig.js
android 버전: 프로젝트의 asetsscriptsconfig.js



###2. 심각한 카튼, 화면 반짝이는 현상

레이플레이어에서 프로젝트를 실행하는데, 심각한 카튼이나 스크린이 반짝이는 현상이 나타난다면.이 때 장치를 컴퓨터에 연결해서 log 을 볼 수 있습니다. 만약 log에서 계속 다음 내용으로 인쇄할 수 있습니다.


```verilog

freeRes(0):Total:8,left:5,clearedMem:115620
```


다음 그림 2개 시:
![图1](img/2.jpg)  


이 상황에 나타난 원인: 현재 화면 아래에서 그리는 그림은 현존지의 최대 size 를 넘어, 현존지는 계속 수리함수를 촉발하며 반짝이는 현상이 나타날 수 있다.


###3. 어떻게 해결

####3.1. 현저지의 크기를 확대

먼저 1.2의 방법에 따라 현존지 size 를 크게 설치하고 재테스트 항목을 재검할 경우 freeRes 의 log, 그리고 카튼, 스크린이 반짝이는 현상도 존재하지 않고, 현존문제로 인한 문제로 인한 문제를 입증할 수 있다는 것을 증명할 수 있다. 이때 기분이 좋아질 수 있다.

####3, 2. 근본적으로 문제를 해결하다

근본적으로 문제를 해결하려면, 개발자는 사진의 생명주기, 현존 크기, 잔류 화면을 엄격히 통제해야 한다.
#####3.2.1. 사진의 현존을 어떻게 계산할 것인가
(1)、한 장`1024*1024`그림 사용 현존 크기는:`1024 * 1024 * 4 = 4MB`.
(2)、한 장`768*890`그림 사용 현존 크기는:`1024 * 1024 * 4 = 4MB`일부 디스플레이 하드웨어 제한 으로 창설 의 사이즈 는 반드시 2 의 n 차멱, 모든 것 이다`768*890`현카드`1024*1024`창건하다.
(3)、강력 건의 미술은 그림을 제작할 때, 그림 너비 또는 512픽셀이 넘는 경우에는 사진 사이즈가 2의 n 차로 513, 1025 같은 사이즈를 피하고 512에 낮춘 사진 레이플레이어 엔진이 자동으로 통합 그래프를 처리할 수 있다.
#####3.2.3. 사진 메모리, 현카드 관계
![图3](img/3.jpg)  


**그림:**
(1)、png 사진 한 장,사이즈`768*890`파일 크기는 420KB입니다.
(2)、로더 함수를 통해 네트워크 가재, 소모 유량은 420KB다.
(3)、png 디코딩을 통해 ImagebitmapData로, 메모리를 점용합니다.`768*890*4=2.73MB`.
(4), 이 그림을 화면에 그릴 때, 우선 디카에 텍스처를 만들어야 하는데, 이 무늬의 크기는 2n 2의 n 의 크기로 만들어서 한 장을 만들었습니다`1024*1024`텍스처에 ImagebitmapData 데이터를 현카에 올리고 메모리 메모리 복사.
(5)、이때 점용`1024*1024*4=4MB`메모리 복사 메모리 복사 및 현카드 이후 메모리 메모리 비트mapData, 엔진에서 자동으로 방출됩니다.
(6)、사진 한 장을 싣는다면, 이 그림은 오랫동안 그릴 수 없이 메모리를 점용하고, LayaPlayer 엔진은 기본적으로 그림에 20초 가재 후 이 그림의 메모리를 석방할 때 하드디스크에서 다시 재재재합니다.

#####3, 2, 3. 사진 추가
많은 응용은 다운로드 기능에 사용되며 미리 메모리에 싣고 있는 것으로 알려져 있지만 이 그림은 그리지 못했습니다. 이 때 메모리가 긴장됩니다. LayaPlayer 엔진은 기본적으로 그림에 20초 가재 후 이 자원을 삭제합니다.그래서 사진의 수를 미리 다운로드하는 것을 조절해야 한다.
프로젝트의 수요는 단지 그림을 로고로 다운로드하고 싶을 뿐 사용하지 않으려면 자원 포장 방식이나 레이디CC의 방식을 사용할 수 있다.
하여튼 사진에 미리 다운로드하는 수량은 신중해야 한다.
다음 코드를 통해 메모리 그림을 삭제하는 시간을 설정할 수 있습니다:


```javascript

conch.config.setImageReleaseSpaceTime(15000);//单位为毫秒，默认是20000
```

log 출력`JCImageManager::setReleaseSpaceTime=15000`대표 설정 성공

**Tips:setImageRelease SpaceTime 함수 또한 config.js 호출**

#####3.2.4. 일부 노드 삭제 되지 않은 현존 문제

여러 항목에서 게임에 들어가는 첫 번째 스크린 인터페이스를 자주 만듭니다. 하지만 몇 번의 인터페이스를 교체하거나 몇 번의 장면으로 다시 돌아오는 것을 발견하고, 첫 스크린을 반짝이며 log 은 freeRes 를 인쇄하고 있습니다.
이런 경우는 대부분 노드가 삭제되지 않았기 때문이다. 화면은 아직 계속 과장되고 있지만, 다만 홈 인터페이스에 가려져 이때 응용 프로그램이 노드를 조절하고 노드 삭제, 숨은 메커니즘을 확보하기 때문이다.


###4. 디버그 수단

프로젝트에서 3.2.4의 현상이 나타났다면, LayaPlayer 엔진이 작은 방법을 제공한다면 이 함수를 통해 모든 화면을 투명하게 설정할 수 있다. 이러한 노드 화면을 숨기지 않고 삭제하거나 삭제하지 않은 현존 문제를 찾을 수 있다.


```javascript

if( window.conch )
{
    window.conch.config.setTransparentMode();
}
```

**Tips**  
*1, conch, LayaPlayer 환경에서만 호출됩니다. 웹 버전에서는 conch 가 정의되지 않습니다. 존재 여부를 판단해야 합니다.*
*2. as 언어를 사용하면 통과할 수 있다`Browser.window['conch'] `이런 방식은 conch 대상을 받는다.*

그림 4개처럼:

![图3](img/4.jpg)  
