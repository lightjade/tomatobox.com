Roll-A-Ball Tutorial
배우게 되는 작업의 원칙
Game Objects, Components, Prefabs, Physics and Scripting.

## ENVIRONMENT AND PLAYER
####Setting up the Game
- New Project
    - 3D is default value.
    - 비어있는 Scene 하나가 생성되어 있다.
- Save a Scene
	- Assets 폴더에 _Scene 폴더를 만들어 사용한다.
	- '_'는 해당 폴더가 상단에 위치하도록 사용함.
- Create game board or play field.
	- GameObject > 3D Object > Plane
	- New Name : 'Ground'
	- Reset Transform
- GameObject 한 눈에 보기
	- GameObject 선택 후 F 누름.
- Grid 없애기
	- Gizmos 메뉴 > Show Grid 선택 해제
- Transform 컴포넌트의 scale 값을 사용하여 크기를 조절할 수 있다.
- Create player
- Create Materials folder and Material as Background
- Plane에 Background material을 적용
	- Background material을 선택한 후 Scene View 안의 Plane 객체에 드래그 앤 드롭하여 적용한다.
- 메인 Directional light를 회전시킨다.

#### Moving the Player
- 동작에 대한 서술
	- 공은 게임 영역을 돌아다닌다.
	- 벽에 부딪힌다.
	- 땅에 그대로 있는다.
	- 날아다니지 않는다.
	- 모을 수 있는 Game Object들과 충돌한다.
- Physics
	- Game Object에 physic를 적용하려면 rigidbody 컴포넌트를 추가해야한다.
- 컴포넌트 추가 방법
	- GameObject 선택
	- Component 메뉴에서 추가 또는 inspector 안의 컴포넌트 버튼을 사용하여 추가.
- 컴포넌트 순서 변경
	- 게임의 성능과는 연관이 없다.
	- 개발 속도를 증가시켜줄 수는 있다.
- 사용자 input 받기
	- Script를 사용한다.
	- 나중에 이름 변경하기 어렵다. 처음에 이름을 잘 정의하는것이 좋다.
- 화면 업데이트
	- Update
		- 매 프레임마다 호출된다. (프레임 기반 호출)
		- 가장 빈번히 호출된다.
		- 물리 효과가 적용되지 않은 오브젝트의 움직임이나 단순한 타이머, 키 입력을 받을 때 사용된다.
		- Update는 불규칙한 호출임으로 물리엔진 충돌검사 등이 제대로 안될 수 있음.
	- FixedUpdate
		- Fixed timestamp에 설정된 값에 따가 일정한 간격으로 호출한다.
		- 물리 효과가 적용된 (RigidBody 컴포넌트가 추가된) 객체를 조정할 때 사용한다.
	- LateUpdate
		- 모든 Update 함수가 호출된 후 마지막으로 호출한다.
		- 주로 오브젝트를 따라가게 설정한 카메라는 LateUpdate 를 사용합니다(카메라가 따라가는 오브젝트가 Update함수 안에서 움직일 경우가 있기 때문)
- CMD + '
	- API 도움말
- Vector3(x, y, z)

## CAMERA AND PLAY AREA
#### Moving the Camera
- Hierachy View에서 Player의 자식 객체로 Main Camera 객체를 이동한다.
	- Player가 회전함에 따라 카메라도 회전하여 이상한 화면이 재생된다.
- CameraController.cs 생성
	- Main Camera 선택
	- Add Component : 스크립트
- LateUpdate
	- 카메라의 경우 LateUpdate 사용.

#### Setting up the Play Area
- Wall 생성
	- Empty Object : Wall 그룹
	- Wall : 3D Object > Cube

## COLLECTING, SCORING AND BUILDING THE GAME
#### Creating Collectable Objects
- Pick up 객체 생성
	- 3D Object > Cube
	- Transform 설정
	- Roataor.cs 스크립트 생성
		- Transform.Rotate() 메소드 사용.
- Prefab 생성
	- Prefab은 템플릿 또는 GameObject의 blueprint 또는 GameObject family를 포함하는 asset이다.
	- 한번 생성한 뒤에는 어떤 Scene에도 다시 사용할 수 있다.
	- Prefabs 폴더 생성
	- Pick Up 객체를 Prefabs 폴더에 drag & drop한다.
	- Empty GameObject를 생성하여 Pick Ups라는 그룹을 생성한다.
	- Pick Up을 Pick Ups 그룹에 포함시킨다.
	- Pick Up을 CMD + D 키로 중복 생성한다. (12개)
- Prefab으로 만든 객체의 Material 컴포넌트 추가.
	- Prefab으로 추가한 모든 객체의 정보가 동시에 변경된다.
- Local/Global????
	- 설정은 무엇인지 좀 더 찾아보기.
- Prefab 이란????
	- Prefab에 대한 정보 좀더 찾아보기.
	- ....

#### Collecting the Pick Up Objects
- 충돌 탐지.
- Sphere Collider
	- Message
        | Message | 설명 |
        |--------|--------|
        |OnCollisionEnter | OnCollisionEnter is called when this collider/rigidbody has begun touching another rigidbody/collider.|
        |OnCollisionExit | OnCollisionExit is called when this collider/rigidbody has stopped touching another rigidbody/collider.|
        |OnCollisionStay | OnCollisionStay is called once per frame for every collider/rigidbody that is touching rigidbody/collider.|
        |OnTriggerEnter | OnTriggerEnter is called when the Collider other enters the trigger.|
        |OnTriggerExit | OnTriggerExit is called when the Collider other has stopped touching the trigger.|
        |OnTriggerStay | OnTriggerStay is called almost all the frames for every Collider other that is touching the trigger.|

- Script
	```
    void OnTriggerEnter(Collider other) 
    {
        if (other.gameObject.CompareTag ("Pick Up"))
        {
            other.gameObject.SetActive (false);
        }
    }
	```
- Collider 종류
	- Dynamic Collider
		- 움직이는 객체들.
	- Static Collider
		- Scene에서 움직이지 않는 부분들.
		- 충돌체(Collider)는 있으나 리지드바디(Rigidbody)가 없는 게임오브젝트(GameObject).
	- Box Collider 사용은 Static?
	- Rigidbody 사용하면 Dynamic?
	- Rigidbody 추가하면 Gravity에 주의
		- Use Gravity ?
		- Is Kinematic ?
- Rigidbody
	- 사용자의 GameObjects가 물리엔진의 제어 내에서 동작할 수 있게 함. 
	- 이것은 실감나는 충돌, 여러 종류의 조인트들, 그리고 여타의 아주 멋진 동작을 가능하게 함. 
	- 사용자의 GameObjects에 리지드바디에 힘을 가하여 조종하게 되면 단순한 Transform Component보다는 아주 다른 느낌과 시각의 효과를 줄 수 있다. 
	- 일반적으로 사용자는 같은 GameObject에서 리지드바디를 조종하는 것과 변형(Transform)을 동시에 같이 할 수는 없고 하나를 선택해야 함.
	- 변형(Transform)과 리지드바디를 조종하는 것 사이의 가장 큰 차이는 힘의 사용이다. 
	- 리지드바디는 힘과 회전력을 받을 수 있지만, 변형(Transform)은 없다.
	- 변형(Transform)도 해석하고 회전할 수 있지만 물리력을 사용하는 것과 같은 것은 아니다.
	- 리지드바디에 힘과 회전력을 가하면 실제로 오브젝트의 Transform 컴포넌트의 위치와 회전을 변경함. 
	- 이렇기 때문에 사용자는 둘 중 하나만을 사용해야 함. 
	- 물리력을 사용하면서도 Transform을 변경하는 것은 충돌과 여타 다른 계산에서 문제를 일으킬 수 있다.
	- 리지드바디가 물리엔진에 의해 영향을 받으려면 명시적으로 사용자의 GameObject에 추가하여야만 함. 
	- 사용자는 메뉴바에서 Components→Physics→Rigidbody에서 선택한 오브젝트에 리지드바디를 추가할 수 있다. 
	- 해당 오브젝트는 중력하에서 추락하고 스크립트를 통해 힘을 받을 수 있으나, 만일 사용자가 원하는 대로 정확하게 행동하게 하려면 Collider난 조인트(Joint)를 추가해야 할 수도 있다.
- Collider 성능
	- 참고) [Collider, Collider+Rigidbody 성능](http://blog.naver.com/PostView.nhn?blogId=sspsos74&logNo=220633287244&categoryNo=0&parentCategoryNo=34&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView&userTopListOpen=true&userTopListCount=5&userTopListManageOpen=false&userTopListCurrentPage=1)  
	- Unity5 이전
		- Collider + Rigibody가 있을때 10배 이상 빠르다.
    - Unity5 (PhyX3.3)
	    - Dynamic collider와 static collider의 이동을 처리하기 위해 같은 data structure를 사용함.
	    - 성능적으로 좋아졌지만 적은 메모리를 사용했던 Static collider의 이점이 사라짐.
	    
#### Displaying the Score and Text
#### Building the Game