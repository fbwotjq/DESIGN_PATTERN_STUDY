
** 커맨드 패턴 
 * 개념 정의 
  - 호출의 캡슐화 ( behavioural pattern 이라고 하기도 함 )
  - 메소드(행위) 호출을 캡슐화 
  - 작업을 요청 하는 쪽과 행동하는 쪽을 분리
  - client / command / invoker / reciver의 개념으로 구성되어 있음 
  - 바뀌거나 추가 되는 부분에 대한 관리가 편하다. 
  - 다만 추가가 되는 부분이 있다면 작업이 명확하게 존재한다. 
  - client와 reciver의 관계를 command와 invoker를 통해서 분리 한다.

 * 구조 정의 
 client  : command를 생성하고 invoker를 통해서 command를 실행한다.
 command : 해당 행위의 주체가 reciver를 가지고 있고 reciver를 실행하는 인터페이스를 가지고 있다.
 invoker : 어떤 command가 와도 실행할수 있고 command를 실행하는 역활만 가지고 있다.
 reciver : 해당 행위자의 고유한 행동을 가지고 있다.
