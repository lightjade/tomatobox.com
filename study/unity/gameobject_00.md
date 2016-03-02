아래 내용은 Unity 사이트의 내용을 번역한 글입니다.
* * *
[원문 보기](http://docs.unity3d.com/Manual/GameObjects.html)
###### GameObjects
GameObject는 Unity에서 가장 중요한 객체 타입(object type)이다.
GameObject가 무엇이고 어떻게 사용할 수 있는지 이해하는것은 매우 중요하다.

##### What are GameObjects?
게임 안의 모든 객체는 GameObject이다. 그러나 GameObject들은 스스로 아무런 동작을 하지 않는다.
GameObject들이 캐릭터나 환경 또는 특수한 효과가 되기 전에 특별한 속성들이 필요하다. 그러나 각 객체들은 매우 다른 일들을 한다.
만약 모든 객체가 GameObject 라면 어떻게 static room에서 상호작용하는 power-up 객체를 구별할 수 있을까?
어떻게 서로 다른 GameObject들을 만들 수 있을까?

Sample) Four different Game Objects, an animated character, a light, a tree and an audio source
![Four different Game Objects, an animated character, a light, a tree and an audio source](http://docs.unity3d.com/uploads/Main/GameObjectsExamples.png_######)

이러한 질문의 답은 GameObject들은 컨테이너들(Container)이라는 것이다.
GameObject(컴포넌트)들은 캐릭터나 빛, 나무, 사운드 또는 당신이 만들고 싶은 무엇을 만들기 위해 필요한 다른 부분들을 포함할 수 있다.
/....

그래서 GameObject를 정확히 이해하기 위해서는 컴포넌트(Component)라 불리우는 것들을 이해해야 한다.
The answer to this question is that GameObjects are containers. 
They can hold the different pieces that are required to make up a character, a light, a tree, a sound, or whatever else you would like to build. 
So to really understand GameObjects, you have to understand these pieces which are called Components.


Depending on what kind of object you want to create, you will add different combinations of Components to the GameObject. Think of a GameObject as an empty cooking pot, and Components as different ingredients that make up your recipe of gameplay. Unity has lots of different built-in component types, and you can also make your own Components using Scripts.

This section explains how Game Objects, Components and Scripts fit together, and how to create and use them.