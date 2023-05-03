# 버섯동산 
## 버섯동산 팀의 henac 저장소 <br>
-------------------------------------
- 대화창
    1. QuestPanelLogic(Logic)
        - 퀘스트 페널을 출력해주는 Logic.(메인, 서브, 빅뱅)
        - 서브 대화창과 빅뱅 전 대화창은 동일한 퀘스트(서브 퀘)를 출력하며 하나를 선택하여 출력할 수 있다.
        - 출력 후 유저의 퀘스트 데이터를 업데이트 함.(분리 예정)
    
    2. QuestComponent(Component)
        - NPC에 붙어 있는 Component로 유저의 퀘스트데이터를 받아와 현재 퀘스트 정보를 QuestPanelLogic에 보낸다.

    3. QuestButton(Component)
        - 비슷한 QuestPanelUI(Entity)가 많아 각각의 버튼들이 동일한 기능을 수행할 수 있도록 하는 Component.
    
    4. PanelTable(Script)
        - 퀘스트 페널 Entity의 id를 담고있는 Table
    
    5. 퀘스트 테이블(Data set)
        - 하나의 퀘스트의 정보를 담고 있는 Data set
    
    6. etc
        - 전체적인 퀘스트 정보는 GlobalDataStorage에 저장하고 각각의 퀘스트는 Data set에 저장
        - QuestComponent에서 UserDataStorage에 있는 유저가 진행중인 퀘스트의 정보를 불러옴 -> 퀘스트 정보에 맞는 QuestPanelLogic을 불러옴 -> 대화 출력 -> 대화 종료 후 UserDataStorage 업데이트
    
    7. Issue
        - 페널 엔티티가 너무 많음 -> _EntityService:GetEntity()가 아닌 _SpawnService:SpawnByModelId()사용 고려했으나 _SpawnService:SpawnByModelId()는 ui가 아닌 map에 소환됨 --> ui에 소환되도록 변경
        - 출력 후 유저의 퀘스트 데이터를 업데이트 함.(로직을 분리해야 할 듯)
        - 퀘스트 관련 DataStorage미구현 -> 기획 완성 후 구현
        - esc키 관련 Issue(하나의 키를 누르면 관련된 모든 함수가 한꺼번에 실행)

- 마우스 커서
    1. Mouse.MODPACKAGE 사용
    2. 기존 마우스를 안 보이게 하고 마우스 엔티티를 덮어씌어 구현
    3. ui엔티티에 ButtonComponent와 자체 제작한 Component를 추가하여 버튼 Hold 시 마우스 엔티티의 상태를 변경

- 도도
    1. 플레이어블 캐릭터에서 자식으로 생성
    2. 기존 캐릭터는 안 보이게 하고 도도 스프라이트(엔티티)를 덮어 씌움
    3. 기존 캐릭터의 state를 공유
    4. 이미 만들어진 전투 로직과 인벤토리가 기존 캐릭터에 묶여있어 위 방식을 사용

- KeyConfigLogic
    1. KeyConfigLogic
        - 유저 입장 시 해당 유저의 커스텀 키 세팅이 있는지 확인
        - 없으면 디폴트 키 세팅을, 있으면 커스텀 한 키세팅을 불러와 KeyConfig테이블 구성
        - SaveUserKeySetting() = 커스텀 한 키세팅을 저장하기 위한 함수
        - SendServer() = 키 세팅을 데이터 스토리지로 보내기 위한 함수(SERVER)
    2. KeyConfigScript
        - 디폴트 키 세팅과 아이콘들의 실행 함수(event)를 담은 Script
    3. IconCmponent
        - UiMovingComponent를 확장한 Component
        - 스킬 아이콘으로서 작동하기 위한 Component
    4. SlotComponent
        - 슬롯으로서 작동하기 위한 Component
    5. KeyConfigComponent
        - 아이콘과 슬롯이 원활하게 작동하기 위해 필요한 Component
        - KeyConfigUI에 있음


- etc.MODPACKAGE(기타 파일이 있음)
    - 플레이어 움직임을 통제하는 Logic --> 대화Logic 실행 시 사용
    - 스킬, 아이템 등의 정보를 보여주는 Component
    - 스킬, 아이템 등의 정보를 보여주는 ui Model
    - escKey 관련 Logic
        - 하나의 키를 누르면 관련된 모든 함수가 한꺼번에 실행하는 Issue
        - ESCkey를 사용하는 ui들을 UIGroup에 따로 넣어 순서대로 창이 닫히게 구현(+ 혹시나 추가하신 거 있으시면 추가해 주세요)
    - 마우스 클릭을 이용한 ui 이동 Component
    - 마우스 커서와 서브 대화창 이미지를 선택 할 수 있는 ui Model
    - 핀님이 주신 Component
다시 연결 했습니다.
test
1. ui base
2. 인터페이스
    1. stat창
    2. 인벤토리
    3. 장비창
    4. 키세팅
    5.
3. 전투 시스템
    1. 몬스터
    2. DB