## 외부 라이브러리를 감싸는 클래스를 만들어 예외를 잡아내라
p.135

아래는 외부 라이브러리를 호출하는 try-catch-finally 문을 포함한 코드로, 외부 라이브러리가 던질 예외를 모두 잡아내고 있다.

```
    ACMEPort port = new ACMEPort(12);

    try {

    } catch (DeviceResponseException e) {
        logger.log(..., e);
    } catch (ATM1212UnlockedException e) {
        logger.log(..., e);
    } catch (GMXError e) {
        logger.log(..., e);
    } finnally {
        ...
    }
```
위 코드는 중복이 심하지만, 대다수 상황에서 우리가 오류를 처리하는 방식은 비교적 일정
1) 오류를 기록한다.
2) 프로그램을 계속 수행해도 좋은지 확인 

위 경우는 예외에 대응하는 방식이 예외 유형과 무관하게 동일하다. 그래서 코드를 간결하게 고치기가 아주 쉽다.
호출하는 라이브러리 API를 감싸면서 예외 유형 하나를 반환하면 된다.

```
    LocalPort port = new LocalPort(12);
    try {
        port.opne();
    } catch (PortDeviceFailure e) {
        reportError(e);
        logger.log(..., e);
    } finnally {
        ...
    }
```
여기서 LocalPort 클래스는 단순히 ACMEPort 클래스가 던지는 예외를 잡아 변환하는 Wrapper 클래스일 뿐이다.


```
    public class LocalPort {
        private ACMEPort innerPort;

        public LocalPort(int portNumber) {
            innerPort = new ACMEPort(portNumber);
        }

        public voic open() {
            try{
                innerPort.opne();
            } catch (DeviceResponseException e) {
                throw new PortDeviceFailure(e);
            } catch (ATM1212UnlockedException e) {
                throw new PortDeviceFailure(e);
            } catch (GMXError e) {
                new PortDeviceFailure(e);
            }
            ...
        }   
    }
```

LocalPort 클래스처럼 AMCEPort를 감싸는 클래스는 유용하다. 실제로 외부 API를 사용할 떄는 감싸기 기벙이 최선이다.
외부 API를 감싸면 외부 라이브러리와 프로그램 사이의 의존성이 크게 줄어든다. 나중에 다른 라이브러리로 갈아타도 비용이 적다.
또한 감싸기 클래스에서 외부 API를 호출하는 대신 테스트 코드를 넣어주는 방법으로 프로그램을 테스트하기도 쉬워진다.

마지막 장점으로 감싸기 기법을 사용하면 특정 업체가 API를 설계한 방식에 발목 잡히지 않는다. 프로그램이 사용하기 편리한 API를 정의하면 그만이다.
위 예제에서 우리는 port 디바이스 실패를 표현하는 예외 유형 하나를 정의했는데, 그랬더니 프로그램이 훨씬 깨끗해졌다.
