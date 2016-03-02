# GameObjects
아래 내용은 Unity 사이트의 내용을 번역해서 요약한 내용입니다.
[원문 보기](http://docs.unity3d.com/Manual/GameObjects.html)

* * *

## GameObjects
GameObject는 Unity에서 가장 중요한 객체 타입(object type)이다.
GameObject가 무엇이고 어떻게 사용할 수 있는지 이해하는것은 매우 중요하다.

* * *

## What are GameObjects?
- 게임 안의 모든 객체는 GameObject이다.
- GameObject들은 스스로 아무런 동작을 하지 않는다.
- GameObject들은 캐릭터나 환경 또는 특수한 효과가 되기 전에 특별한 속성들이 필요하다. 각 객체들은 다른 일들을 한다.
- 예) GameObject들 : animated character, light, tree, audio source
![Four different Game Objects](http://docs.unity3d.com/uploads/Main/GameObjectsExamples.png)

* * *
만약 모든 객체가 GameObject 라면

- 어떻게 static room에서 상호작용하는 power-up 객체를 구별할 수 있을까?
- 어떻게 서로 다른 GameObject들을 만들 수 있을까?

* * *

질문의 답

- GameObject들은 컨테이너들(Container)이다.
- GameObject(컴포넌트)들은 캐릭터나 빛, 나무, 사운드 또는 당신이 만들고 싶은 무엇을 만들기 위해 필요한 다른 부분들을 포함할 수 있다.
- GameObject를 정확히 이해하기 위해서는 컴포넌트(Component)라 불리우는 것들을 이해해야 한다.

* * *

- 생성하려는 객체의 종류에 따라 GameObject에 다른 컴포넌트의 조합을 추가한다.
- GameObject를 비어 있는 냄비라 생각한다면 Component는 gameplay의 조리법을 이루는 다른 재료들이다.
- Unity는 만들어져 있는 여러개의 컴포넌트 타입들이 많다.
- 사용자는 스크립트를 사용하여 자신의 컴포넌트를 만들수 있다.
