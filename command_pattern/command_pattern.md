
## 커맨드 패턴 
# 개념 정의 
  - 호출의 캡슐화 ( behavioural pattern 이라고 하기도 함 )
  - 메소드(행위) 호출을 캡슐화 
  - 작업을 요청 하는 쪽과 행동하는 쪽을 분리
  - client / command / invoker / receiver의 개념으로 구성되어 있음 
  - 바뀌거나 추가 되는 부분에 대한 관리가 편하다. 
  - 다만 추가가 되는 부분이 있다면 작업이 명확하게 존재한다. 
  - client와 reciver의 관계를 command와 invoker를 통해서 분리 한다.

# 구조 정의 
 - client  : command를 생성하고 invoker를 통해서 command를 실행한다.
 - command : 해당 행위의 주체가 receiver를 가지고 있고 receiver를 실행하는 인터페이스를 가지고 있다.
 - invoker : 어떤 command가 와도 실행할수 있고 command를 실행하는 역활만 가지고 있다.
 - reciver : 해당 행위자의 고유한 행동을 가지고 있다.

# 개인적인 생각 
 - 다른 언어(java/c++가 아닌)를 쓸 경우 좀 더 불필요한 부분이 개선될수 있다. 자바의 장점이자 단점인 명확함을 통해 overSpec의 코드가 좀 산출 되긴 하지만 그만큼 명확하다고 개인적으로 느낀다.

# 클래스 다이어그램 
![screenshot_class_diagram](https://github.com/fbwotjq/DESIGN_PATTERN_STUDY/blob/master/command_pattern/class_diagram.png)

# 시퀀스 다이어그램 
![screenshot_sequence_diagram](https://github.com/fbwotjq/DESIGN_PATTERN_STUDY/blob/master/command_pattern/sequence_diagram.png)

# 관련 코드 
```
//커맨드 클래스들 
//행위를 추상화 한 인터페이스 
public interface Command{
  public void execute();
}

// invoker에서 실행할수 있도록 동일한 인터페이스를 가짐으로써 각자 행위 자체가 추상화 된다.
public class LightOnCommand implements Command{
  //reference to the light
  Light light;
  public LightOnCommand(Light light){
    this.light = light;
  }
  public void execute(){
    light.switchOn();
  }
}
// 해당 행동에 Light라는 Receiver를 가지고 있다. Receiver도 결국 추상화 될수 있다. 
public class LightOffCommand implements Command {
  //reference to the light
  Light light;
  public LightOffCommand(Light light){
    this.light = light;
  }
  public void execute(){
    light.switchOff();
  }
}
```

```
// Receiver, 즉 실제 행위자에 대한 구현이다. 
public class Light{
  private boolean on;
  public void switchOn(){
    on = true;
  }
  public void switchOff(){
    on = false;
  }
}
```

```
//Invoker, 즉 커맨드/행위를 실행시킨다. 클라이언트 개념에서의 추상화된 인터페이스이다. 
public class RemoteControl{
  private Command command;
  public void setCommand(Command command){
    this.command = command;
  }
  public void pressButton(){
    command.execute();
  }
}
```

```
//Client 모든 행위를 커맨드 객체를 통해 실행 자체를 invoker에게 위임한다.
public class Client{
  public static void main(String[] args)    {
    RemoteControl control = new RemoteControl();
    Light light = new Light();
    Command lightsOn = new LightsOnCommand(light);
    Command lightsOff = new LightsOffCommand(light);
    //switch on
    control.setCommand(lightsOn);
    control.pressButton();
    //switch off
    control.setCommand(lightsOff);
    control.pressButton();
  }
}
```
