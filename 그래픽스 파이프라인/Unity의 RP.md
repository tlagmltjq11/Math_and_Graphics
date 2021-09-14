## 🔔 Rendering Pipeline
폴리곤(Obj)으로 구성된 3차원 장면을 2D 화면으로 그려내는 과정을 의미한다.<br> 
<br>
<br>

## 🔔 Unity RP
**Built-In Renderer**<br>
유니티에 **기본적으로(Default) 내장 된** 렌더링 파이프라인이다.<br>
-> **커스텀 확장에 관해서 스크립터블 렌더 파이프라인(SRP)에 비해 제한적이며,<br>
-> 쉐이더 그래프를 사용할 수 없다.**<br>
<br>
<br>

**SRP(Scriptable Render Pipeline)**<br>
스크립터블 렌더링 파이프라인(SRP)을 사용하면 **스크립트로 렌더링을 제어하고 커스터마이징 할 수 있다.**<br>
개발자는 유니티가 프레임을 렌더링하는 방법을 c# 스크립트로 작성하여 프로젝트의 요구사항을 충족하기위해<br>
기존의 파이프 라인을 수정하거나 재구성 할 수 있다.<br>
**유니티는 2개의 빌트인 SRP를 제공한다(URP, HDRP)** ⭐<br>
-> 직접 스크립트로 렌더링 파이프라인을 컨트롤 하기 위해선 워크플로우라던지<br>
그래픽스에 관한 **충분한 학습이 필요하다.**<br>
<br>

(1). **URP (Universal) or LWRP (Light Weight)**<br>
유니티에 내장된 SRP로 LWRP의 업그레이드 버전이다(Unity 2019.3 버전부터 LWRP가 URP로 변경)<br>
URP는 뛰어난 성능 및 향상된 그래픽 품질을 제공하는 SRP로 **기본 빌트인 렌더 파이프라인보다<br>
유연하고 확장성이 좋으며** 다양한 플래폼(모바일, 콘솔, PC, VR)에 최적화된 그래픽을 제공한다.<br>
URP는 모바일 등 **저사양 기기에서도 적합하도록 만들어진 SRP이고** ⭐<br>
싱글 패스 포워드 렌더링, 셰이더 그래프, VFX 그래프를 지원한다(디퍼드 렌더러 지원 예정)<br>
<br>

어떤 효과를 보기 위해 빌트인 대신 URP를 선택하는지에 대한 **근거가 명확해야** 하며,<br>
기능 구현에 대한 시간 투자와 인력 할당이 필수적이다.<br>
단순히 '새로 나온 기능이고 다른 프로젝트에서 종종 채택한다'거나 '싱글패스니까 항상 빠르겠지' 같은<br>
안일한 접근으로는 열심히 작업하다 말고 도로 Built-in으로 유턴하는 경우가 생길지도 모른다.<br>
유니버설 렌더 파이프라인은 Built-in 렌더러보다 빨라질 여지가 존재할 뿐<br>
모든 경우에 대해 유리하지 않음을 인지해야 한다.<br>
<br>
<br>

![URPvsBIRP](https://user-images.githubusercontent.com/43705434/133225193-08b7e6d3-6185-40e6-82be-833654453700.PNG)<br>
<br>

**스크립터블 렌더가 기존 레거시 렌더의 문제점들을 해결하고 점차 대체하기 위해 나온거라,<br>
18-19년도 출시 및 전환기를 지나며 새로 시작하는 프로젝트에선 URP 모드가 권장되는 추세라고 한다.<br>
쉐이더 그래프 활용, 여러가지 확장성, 무엇보다도 렌더 성능에서 차이가 있으니 프로젝트 타겟 디바이스가<br>
URP를 지원하지 않는다거나 어쩔수 없이 사용하는 에셋이 레거시 쉐이더밖에 지원하지 않는게 아니라면<br>
URP를 기본으로 사용하시는게 낫다고 한다.** ⭐⭐⭐<br>
<br>

**장점**<br>
▶ Multi-Light Single-Pass <br>
Unity의 Built-in forward Render는 빛을 계산할 때 Multi-Light Multi-Pass로<br>
빛 계산을 할때마다 하나의 패스가 사용되지만, **URP에서는 여러개의 빛 계산을 하나의<br>
패스에서 처리하여 퍼포먼스가 향상 된다.**<br>
<br>

▶ SRP Batcher<br>
Unity의 Built-in Render Pipeline은 머테리얼을 기준으로 배칭을 했지만,<br>
**URP에서는 쉐이더를 기준으로 배칭을 처리함으로써 다른 메터리얼을 사용하고 있는 경우에도 배칭 처리가 된다.**<br>
<br>
<br>

(2). **HDRP (High Definition)**<br>
고해상도 렌더 파이프라인은 유니티에 내장된 SRP로 물리 기반의 렌더링과 우수한 GPU 성능으로<br>
정확하고 매우 사실적인 그래픽을 제공한다. **고사양 그래픽이 요구되는 프로젝트를 위해 HDRP를 사용 할 수 있다.** ⭐<br>
컴퓨트쉐이더(compute shader) 기술과 GPU 하드웨어를 사용하며 포워드 렌더링, 디퍼드 렌더링을 모두 지원한다.<br>
HDRP는 PC, 콘솔 플랫폼 용도로 권장된다.<br>
-> 성능이 낮은 플랫폼에서는 적합하지 않다.<br>
<br>
<br>

## 🔔 렌더링 기법

* 포워드 렌더링<br>
:3D공간에 존재하는 폴리곤을 픽셀화->그픽실마다 쉐이딩&라이팅연산<br>

(1)장점<br>
1.저사양에서도 잘작동한다<br>
2.pc는 안티앨리어스 처리를 하드웨어에서 지원<br>
->거의완벽한처리&반투명처리 문제x<br>
<br>

(2)단점<br>
1.라이팅 연산이 느림<br>
2.복잡한 화면구성하거나 폴리곤이 많은 모델을 렌더링 걸기 불합리<br>
3.그림자처리가 어려움<br>
4.화면깊이값을 이용한 포스트 이펙트는 따로 처리해야함<br>
사용하여 제작된 게임 : 리니지2<br>
<br>

* 디퍼드 렌더링<br>
:한화면에 수많은 라이팅 효과를 넣기위한 렌더링 기법(실시간 반응 쉐이더)<br>

(1) 구현방식<br>
폴리곤픽셀화->정보를 나누에 비디오 메모리에 저장<br>
->각종 쉐이터와 라이팅 효과를 거쳐 화면에 보여줌<br>
<br>

(2)장점<br>
1.다양한 동적 라이팅을 실시간으로 보여줄수 있음<br>
2.그림자를 쉽게 그릴수 있다.<br>
3.쉐이더를 간단하게 지원<br>
4.픽셀정보를 메모리에 저장하면서 생기는 여러가지 이점을 사용가능<br>
->화면의 깊이값을 이용한 특수효과<br>
5.수많은 오브젝트와 복잡한 모델링을 표현할떄 유리<br>
<br>

(3)단점<br>
1.뒤에 그려지는 오브젝트 정보가 비디오 메모리에서 소실<br>
->알파가 빠지는 오브젝트 표현x<br>
2.요구하는 하드웨어 사양이 높다.<br>
3.해상도가 올라갈수록 비디오 메모리가 기하급수적으로 늘어남<br>
4.안티앨리어스를 구현하기 까다로움<br>
<br>

* 현실감 넘치거나 눈부신 화면을 연출할때 강력한 효과를 보여줌<br>
* 현재는 디퍼드 랜더링의 단점을 해결한 방식을 사용<br>
<br>
<br>

**Mobile Device 같은 경우 Forward Rendering을 더 많이 사용한다.** ⭐⭐<br>
Deferred Rendering의 경우 여러 개의 Render Target을 저장하기 위해 많은 Memory 공간이 필요하다.<br>
이와 더불어 Render Target 데이터를 Loading 하기 위해서 High Memory Bandwidth가 필요하다.<br>
모바일의 경우 보통 Graphic Memory를 따로 가지고 있지 않고 System Memory를 같이 사용하고 있다.<br>
Mobile Device의 System 메모리는 보통 아주 제한적이다. 추가로 Mobile Device는 아주 제한된 Bandwidth로 인해서<br>
Render Target의 데이터 값을 로딩하는 데 오랜 시간이 걸린다.<br>
Deferred Rendering은 Transparent (투명한) Objects의 색상 연산을 수행할 수 없다.<br>
이와 더불어 Edge Detection을 할 수 없기 때문에 Anti-Aliasing 연산을 수행할 수 없다.<br>
<br> 
<br>

## 🔔 Shader Graph
Unity는 2018.1 버전에서 셰이더를 시각적으로 빌드할 수 있는<br>
새로운 셰이더 그래프(Shader Graph) 툴을 도입<br>
https://blog.unity.com/kr/technology/shader-graph-updates-and-sample-project <br>
<br>
<br>

## 🔔 참조링크
https://mkblog.co.kr/2019/01/30/gpu-forward-rendering-vs-deferred-rendering/ <br>
https://learnandcreate.tistory.com/477 <br>
https://mingyu0403.tistory.com/162 <br>
https://dreamzelkova.tistory.com/entry/UnityURP%EB%9E%80 <br>
https://everyday-devup.tistory.com/56 <br>
https://mathmakeworld.tistory.com/55 **(SRP 사용법)** <br>
https://hayeo-83.tistory.com/32 <br>
