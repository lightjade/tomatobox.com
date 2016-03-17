## Space Shooter Tutorial
- simple top down arcade style shooter.
- imported Mesh Models, Audio, Textures and Materials

## INTRODUCTION
#### 1. Introduction to Space Shooter

## GAME SETUP, PLAYER AND CAMERA
#### 1. Setting up the project
- Project 생성
- Import assets from asset store
	- https://www.assetstore.unity3d.com/en/#!/content/13866
- Save Scene
	- Scene은 asset 디렉토리에 저장되어야 한다.
	- Scene 이름 : Main
- Build Settings
	- Shift + CMD + B
	- Player Settings에서 설정한다.
	- 해상도를 제외하고 기본값으로 설정한다.
- 개발 화면 구성
	- Game View를 Web(600x900)으로 설정하면 작게 보인다.
	- 개발 화면 layout을 변경한다.

#### 2. The player gameobject
- Add Player ship model
	- Assets > Models 디렉토리 안의 model을 추가한다.
	- Transform 값을 reset한다.
	- Mesh filter와 Mesh Render가 정의되어 있음.
- 물리 동작 추가
	- RigidBody 컴포넌트 추가
	- 우주에서 게임을 진행한다. Use Gravity를 끈다.
- 충돌 처리
	- 충돌 처리를 위해 오브젝트의 볼륨을 정의해야한다.
	- 충돌을 감지하려면 오브젝트가 어느정도의 공간을 차지하는지 알아야하기 때문이다.
	- Capsule Collider 컴포넌트를 추가.
	- Capsule Collider 크기 변경
		- Direction
			- Y-Aixs는 사람 객체에 사용된다.
			- 우주선은 z축을 따라 긴 형태이다.
        - Radius
        - Height
    - Box, Sphere, Capsule Collider가 Mesh Collider보다 성능이 좋다. 
	    - 참고 : RigidBody의 복합 충돌체 섹션 참고 
    - Mesh Collider 추가
	    - 기존의 Capsule Collider를 지워야 한다. 
	    - 기본값은 Mesh Filter의 mesh가 추가됨. 
	    - 복잡하기 때문에 느려진다. 
	    - 간단한 mesh를 만들어 추가한다.
	    - 지정한 Mesh 를 보기 위해서는 Convex항목을 켜 놓아야 한다. 
	    - 전체 물리 충돌을 감지할 필요가 없다. 행동을 트리거하는 충돌정도면 충분한다. 
		    - Trigger collider로 만든다. 
		    - is Trigger : on

#### 3. Camera and lighting
- Transfrom 변경
- Projection
	- Perspective : Field of View 값으로 영역 설정
	- Orthographic : size로 영역 설정.
- 우주선의 위치를 아래로 내리려면?
	- 씬뷰에서 우주선의 위치를 이동하는 방법
	- inspector 에서 직접 우주선의 transform값을 변경.
	- inspector 에서 직접 카메라의 transform값을 변경.
- 카메라 배경 변경
	- 디폴트값은 skybox
	- 배경색으로 변경 가능하다.
- Ambient light
	- Windows > light : Scene Tab
	- 고정점 없이 씬의 모든 표면을 비추는 조명. 방향성이 없다. 
- 조명
	- Directional light 추가
		- 방향성이 있는 조명
		- 가장 밝은 메인 라이트
    - Main light
    - Fill light
    - Rim light

#### 4. Adding a background
- Game Object > 3D Object > Quad
- Transform을 변경해야 게임 뷰에서 보이게 된다. (카메라 안으로 들어온다.)
- Background에 Texture를 추가
	- Texture의 preview 화면에서 이미지의 크기를 알 수 있다. 
- Quad 크기 조정
	- z값은 변하지 않는다. 


#### 5. Moving the player
#### 6. Creating shots
#### 7. Shooting Shots

## BOUNDARIES, HAZARDS AND ENEMIES
#### 1. Boundary
#### 2. Creating hazards
#### 3. Explosions
#### 4. Game Controller
#### 5. Spawning Waves

## SCORING, FINISHING AND BUILDING THE GAME
#### 1. Audio
#### 2. Counting points and displaying the score
#### 3. Ending the game
#### 4. Building the game

## EXTENDING SPACE SHOOTER
#### 1. Extending Space Shooter: Enemies, More Hazards, Scrolling BG...

#### 2. Mobile Development: Converting Space Shooter to Mobile