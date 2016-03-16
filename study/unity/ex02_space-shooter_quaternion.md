## Quaternion Slerp
##### from Biny님 정리.

```
Quaternion Slerp(Quaternion a, Quaternion b, float t);
Quaternion.Slerp(from.rotation, to.rotation, Time.timeQuaternion.Slerp * speed)`
```
인자값을 정리하자면
1. from.rotation - 시작 각도
2. to.rotaion - 목표 각도
3. 세번째 값은 진행도. 0~1 사이의 값을 넣으면 된다.
  - 0을 넣으면 시작 각도.
  - 1일 때는 목표각도를 반환. 0~1은 %값이라고 보시면 이해가 되실려나요..

세번째 인자의 값이 중요함.
"30도 회전"을 위해 OnUpdate()에 위에 함수를 반복해서 호출한다고 치면

```
Quaternion.Slerp(0,30, 0) => 0
Quaternion.Slerp(0,30, 0.1f) => 1(예시값이에요..)
Quaternion.Slerp(0,30, 0.2f) => 2
.....
Quaternion.Slerp(0,30, 0.9f) => 29
Quaternion.Slerp(0,30, 1) => 30

```

이런식으로 3번째 값이 0~1까지 자연스럽게 들어가주면 0~30까지의 값을 구할수 있게 되서 자연스럽게 회전할수 있음.
유니티 회전 함수 및 다른 수학 함수들 중에 이런 개념으로 쓰는게 제법 많은 듯 하오니 참고해주시기 바랍니다.