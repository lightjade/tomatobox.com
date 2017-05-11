## Survival shooter
#### 1. Environment setup
- - Directional light의 경우 position 설정은 중요하지 않는다. rotation 값만 유의하면 된다.
	- 참고) https://unity3d.com/kr/learn/tutorials/modules/beginner/graphics/lighting-and-rendering
	- 빛이 있는 환한 실외에서의 태양빛 같은 효과를 만들때 사용된다.
	- 무한히 멀리 떨어져 있는 광원을 생각하면 된다.
	- Directional light로부터 방출되는 light ray들은 모두 평행을 유지한다.
	- 그래서 광원의 위치는 큰 의미가 없다.
	- 광원의 위치에 따라 빛이 약해지지 않는다.
	- Ratation 값은 큰 영향을 준다.
- Ray cast
	- Camera가 Scene을 내려보게 하고 player를 추적하기위해서 사용.
	- 카메라에서 바닥까지 보이지 않는 선을 생성한다.
	- 바닥에 다양한 객체가 있기때문에 평평한 floor를 하나 생성한다.
	- 3차원 공간에서 어느 한 점(시작점)에서 Ray를 정해진 방향(direction vector)으로 쏴 Ray와 충돌되는 객체를 구하는 방법.
	- Ray
		- Ray Cast를 위한 중요 정보를 가진다.
		- origin : Ray가 시작되는 지점.
		- direction : Ray가 origin에서 쏘여지는 방향.
    - Physics.Raycast()
    	- Ray Cast를 실행하여 Ray와 객체가 충돌하는지 체크하는 메소드.
    	- 충돌될 경우 true값을 반환
    	- physics.Raycast 메서드를 실행하면, Ray 객체의 origin 에서 direction 으로 ray를 쏴 준다.
    	- ray(광선)와 충돌 되는 객체가 있으면 true 반환한다.
    	- RaycastHit 객체를 out 키워드를 통해 파라미터로 주면 충돌된 객체의 정보를 담아서 반환해 준다.
    	- 메서드 실행 시 Ray 길이를 float 값으로 받는데, 이 값은 ray가 얼마만큼 쏴 지도록 설정하는 것이다.
    	- Mathf.Infinity를 할당 하면 무한대로 쏴서 체크함.
    - RaycastHit
    	- Physics.Raycast 메서드의 파라메터로 값을 할당하며 Ray에 충돌된 객체의 정보를 가진다.
    - 참고)
    	- http://mingu.kr/82
    	- http://am-kwon.blogspot.kr/2014/08/unity3d-raycast-2d-3d.html
    - 샘플 코드

```cs
void Update()
{
    //Raycasthit 2D
    if (Input.GetMouseButtonDown(0))
    {
        Vector2 wp = Camera.main.ScreenToWorldPoint(Input.mousePosition);
        Ray2D ray = new Ray2D (wp, Vector2.zero);
        RaycastHit2D hit = Physics2D.Raycast(ray.origin, ray.direction);

        if(hit.collider != null)
        {
            Debug.Log("Complete"+hit.collider.name);
            Destroy(hit.collider.gameObject);
        }
    }

    //RaycastHit 3D
    if (Input.GetMouseButtonDown(0))
    {
        RaycastHit hit = new RaycastHit();

        //Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition); If you use main Camera..
        Ray ray = this.camera.ScreenPointToRay(Input.mousePosition);

        if(Physics.Raycast (ray, out hit))
        {
            if(hit.collider.tag == "DropBlock")
            {
                Debug.Log ("Touch to DropBlock!!");
                Destroy(hit.collider.gameObject);
            }else{
                Debug.Log ("Touch to RunBlock!!");
            }

        }
    }
}
```

- Background Music 추가
	- Create empty game object
	- Add audio source component.
	- To do ?
		- Backgroud music on/off
		- volume 설정.

#### 2. Player Character
- Model > Character 에서 추가.
- Tagging to 'Player'
- Animation 추가.
	- FPX, Maya, 3DS Max 파일들을 Unity안으로 가져온다.
	- 현재 추가된 모델은 Rig의 Generic Type의 애니메이션을 가지고 있다.
- Animator Controller asset 추가
	- Animator controller는 mecan animation system
	- Animator Controller는 어떤 animation들이 보여져야 하는지를 결정하고 애니메이션들이 원활히 동작할 수 있도록 하는 state machine이다.
	- Animation, Animator Override Controller가 아닌 Animator Controller를 생성한다.
	- 'Player AC'라고 이름짓고 Player에게 드래그한 뒤 Player에서 Animator Controller를 적용한다.
- Animation 설정
	- 'Player AC', animator Controller를 더블클릭하면 Animator 윈도우가 보인다.
	- 각 character 들의 animation들을 추가한다.
		- Idle, Move, Death
	- Default animation을 설정한다.
	- 로직을 구성하기위해 Parameter를 추가한다.
		- IsWalking, Die(Trigger)
    - Make Transition
    	- Inspector에서 condition을 설정할 수 있다. 
    	- Condition은 만들어 놓은 parameter들을 사용한다. 
    	- ex) IsWalking is true....
- Player 설정
	- Physic 설정 : rigidBody
	- 충돌 설정 : Add Capsule collider
		- Freeze 값 설정.
	- Audio component 추가.
	- 스크립트 추가, PlayerMovement.cs

- PlayerMovement
	- member
        - public float speed = 6f
        - Vector3 movement
        - Animator anim
        - Rigidbody playerRigidbody
        - int floorMask
        - float camRayLength = 100f
    - Awake()
    	- Start()와 유사.
    	- 스크립트의 활성 여부와 상관없이 동작한다.
	- Awake()
		- Awake 함수는 스크립트 객체가 로딩될 때 호출됩니다.
		- Awake 함수는 게임이 시작하기 전에 변수나 게임 상태를 초기화하기 위해 사용합니다.
		- Awake 함수는 스크립트 객체의 라이프타임 동안 단 한번만 호출됩니다.
		- Awake 함수는 모든 오브젝트가 초기화된 후 호출되기 때문에, 다른 오브젝트에 메시지를 날리거나 GameObject.FindWithTag 같은 함수를 안전하게 사용할 수 있습니다.
		- 이런 이유로 Awake 함수에서 스크립트를 레퍼런싱한 후, Start 함수에서 필요한 정보를 넘겨받거나 넘겨줄 수 있습니다.
		- Awake 함수는 언제나 Start 함수 전에 호출됩니다. 이것은 스크립트의 초기화 순서를 정할 수 있게 합니다.
		- Awake 함수는 coroutine 으로 동작할 수 없습니다.
	- Start()
		- Start 함수는 Update 함수가 처음 호출될 때 Update 함수 직전에 호출됩니다.
		- Start 함수는 스크립트가 동작하는 라이프타임 동안 단 한번만 호출됩니다.
		- Awake 함수와의 차이는 Start 함수는 스크립트가 켜져있을 때만 호출된다는 것입니다.
		- 이것은 정말로 필요할 때까지 초기화 코드 실행을 연기시킬 수 있습니다.
		- Awake 함수는 언제나 Start 함수가 호출되기 전에 호출됩니다. 이것은 스크립트의 초기화 순서를 정할 수 있게 합니다.
		- Start 함수는 모든 스크립트 객체의 Awake 함수가 호출된 후에 호출됩니다.
    - FixedUpdate()
    	- normalized : 크기가 1인 벡터로 만들어준다.
    	- 'movement = movement.normalized * speed * Time.deltaTime;'
    - Ray cast
    	- 마우스 위치에 맞도록 player의 방향을 설정.
```cs
	void Turning ()
    {
        // Create a ray from the mouse cursor on screen in the direction of the camera.
        Ray camRay = Camera.main.ScreenPointToRay (Input.mousePosition);

        // Create a RaycastHit variable to store information about what was hit by the ray.
        RaycastHit floorHit;

        // Perform the raycast and if it hits something on the floor layer...
        if(Physics.Raycast (camRay, out floorHit, camRayLength, floorMask))
        {
            // Create a vector from the player to the point on the floor the raycast from the mouse hit.
            Vector3 playerToMouse = floorHit.point - transform.position;

            // Ensure the vector is entirely along the floor plane.
            playerToMouse.y = 0f;

            // Create a quaternion (rotation) based on looking down the vector from the player to the mouse.
            Quaternion newRotation = Quaternion.LookRotation (playerToMouse);

            // Set the player's rotation to this new rotation.
            playerRigidbody.MoveRotation (newRotation);
        }
    }
```
    - 참고)
    	- [이벤트 함수의 실행 순서](http://docs.unity3d.com/kr/current/Manual/ExecutionOrder.html)
    	- [MonoBehaviour 오버라이딩 가능 함수 정리](http://kimseunghyun76.tistory.com/194)

#### 3. Camera setup


#### 4. Creating Enemy #1
- Nav Mesh Agent?
	- 간단한 AI를 위해 사용하는 Nav Mesh 시스템
	- 베이킹이라는 프로세스를 실행하여 레벨의 어느 부분을 탐색할 수 있는지 지정하는 것이다.
	- Nav Mesh Agent가 자동으로 타겟을 골라 추적하면서 한편으로 장애물 등을 피해 돌아다닌다.
	- 



























