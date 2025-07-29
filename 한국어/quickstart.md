---
title: 00. Quickstart
description: 
published: true
date: 2025-07-17T02:37:35.767Z
tags: 
editor: markdown
dateCreated: 2025-07-17T02:35:45.497Z
---

## 첫 번째 [Light.vn](https://soulengineproject.itch.io/lightvn) 프로젝트를 위한 스타터 팁

- 샘플 게임을 처음부터 끝까지 플레이해 보세요  
  - 어떤 부분을 복사·붙여넣기하거나 커스터마이즈할 수 있을지 감을 잡을 수 있습니다.
- `LightEditor.exe` 실행  
  - 오른쪽 상단의 `New Script` 버튼을 눌러 새 스크립트를 만듭니다.
  - `Project` → `Settings`를 열고, `Start Script`에 방금 만든 스크립트의 경로를 지정합니다.
  - 아래 코드를 붙여넣습니다.
    ```
    ~bg0 id0 bg/street_bg_noon.png | .fadein id0 300

    script /Plugins/lvui/_system/macros.txt // macros

    ~textbox_bottom

    "This is my project!

    ~cg0 id1 scg2.png 310 125 80 | zoom id1 100% | .fadein id1 300
    ```
- **PRO 팁**: Discord 서버에 꼭 참여하세요  
  - 질문 및 정보 교환의 허브 역할을 합니다.

## 폴더 구조

개발자로서 알아두어야 할 최소한의 구조입니다.

**폴더**
- `Data` : 프로젝트 데이터
- `SaveData` : 세이브 데이터
- `Screenshots` : 스크린샷

**파일**
- `LightApp.exe` : 게임 실행 파일
- `LightEditor.exe` : 에디터
- `LightTests.exe` : 실행 환경 테스트용 프로그램
- `settings.xml` : 게임 설정

그 외 폴더·파일은 신경 쓰지 않아도 됩니다.

## 에디터 단축키 익히기

- `ctrl + f` : 찾기 및 바꾸기
- `ctrl + c` `ctrl + v` : 복사·붙여넣기
- `ctrl + z` : 실행 취소
- `tab` `shift + tab` : 들여쓰기 / 내어쓰기

## 에디터 탐색 (1: 현재 스크립트 이동)

[Light.vn](https://soulengineproject.itch.io/lightvn)을 처음 사용할 때는 `LightEditor.exe`에서 탐색법을 먼저 익히는 것이 좋습니다.

1. 파일 선택 (예: `start0.txt`)
2. `Scripts` 탭 열기
3. 스크립트의 여러 줄을 클릭해 보면서  
   - 미리보기 화면이 업데이트되는지  
   - 탭 정보의 줄 번호가 커서 위치에 맞춰 변하는지 확인합니다.

![image](https://github.com/user-attachments/assets/0e7a0742-eda9-4eed-b711-c557b5061858)

## 에디터 탐색 (2: 테스트 플레이 ↔ 편집 모드)

- 특정 줄을 클릭한 뒤 `F5`를 눌러 테스트 플레이 시작
- 다시 확인해 보세요  
  - 미리보기 화면이 업데이트  
  - `Scripts` 탭의 줄 번호가 현재 재생되는 줄로 변경
- `F5`를 다시 눌러 편집 모드로 복귀  
  - 미리보기가 커서가 있는 줄로 돌아갑니다  
  - `Scripts` 탭에서 다시 확인 가능합니다.

`F5`를 반복해서 눌러 전환 감각을 익혀 보세요.

![image](https://github.com/user-attachments/assets/dc47dd62-8cd5-4f9f-9683-9cb15c28df0b)

## 명령어 문법 읽는 방법

![image](https://github.com/user-attachments/assets/19fdb11b-4ca5-4ef1-875d-e76f3552137b)

스크립트에서 아무 명령어나 더블 클릭하면 `Commands` 탭이 열립니다.  
각 명령어의 문법은 다음과 같이 표시됩니다.
```
cg [name] [filename / animation name] [x] [y] [layer] (camera_option)
```
- `[]` 안의 항목은 필수 입력
- `()` 안의 항목은 선택 입력

따라서 다음 두 가지 형태 모두 유효합니다.
- `cg alice2 alice.png 150 30 50`
- `cg alice2 alice.png 150 30 50 on_camera`

## 왼쪽의 명령어 삽입 버튼

공통으로 자주 쓰는 명령어를 빠르게 삽입할 수 있도록 왼쪽(파란색)에 명령어 버튼이 있습니다.  
해당 명령어는 **현재 스크립트 커서 위치**에 삽입됩니다.  

현재 커서 위치는 에디터의 `Scripts` 탭(분홍색)에서 확인할 수 있습니다.

테스트 플레이 중에는 실행된 줄에 맞춰 자동으로 갱신되므로, 어떤 줄이 실행 중인지 바로 알 수 있습니다.

![image](https://github.com/user-attachments/assets/4f2062cb-2739-4bd4-9113-b7d3eb09c221)

## '스크립트'를 구성하는 요소

- [Light.vn](https://soulengineproject.itch.io/lightvn) 스크립트는 `.txt` 파일이며, LightEditor.exe 또는 선호하는 텍스트 편집기로 열 수 있습니다.
- 스크립트는 크게 3가지 구성 요소로 나뉩니다.
  1. [Light.vn](https://soulengineproject.itch.io/lightvn) 명령어
  2. 대사(Dialogue)
  3. 매크로(Macros)

**[Light.vn](https://soulengineproject.itch.io/lightvn) 명령어** 예시:

```fadein title_bg0 1500 markdown```

- 명령어인지 구분하는 방법:  
  - 더블 클릭 시 에디터가 `Commands` 탭으로 이동하여 문법·사용법을 보여줍니다.

![image](https://github.com/user-attachments/assets/dcf5fee4-4cc1-4ece-859f-4fd1143b7247)

**대사(Dialogue)**  
스크립트에서 `파란색`으로 전부 하이라이트되는 부분입니다.  
다음 명령어로 시작합니다.
- `"`
- `-"`

이후 줄들은 모두 대사 구간으로 처리됩니다.  
다시 [Light.vn](https://soulengineproject.itch.io/lightvn) 명령어 구간으로 돌아가려면 새 줄을 `~` 기호로 시작하세요.

![image](https://github.com/user-attachments/assets/056caff1-6acc-4fa6-8a8b-96160a7524c0)

**매크로(Macros)**  
예: `commandMacro` 또는 `macro` 명령으로 생성됩니다.  
매크로 여부를 확인하는 방법:
- 파란색이 아님
- 더블 클릭해도 `Commands` 탭으로 이동하지 않음

`commandMacro`로 등록된 경우 더블 클릭 시 `Macros` 탭으로 이동하므로 매크로임을 쉽게 알 수 있습니다.

![image](https://github.com/user-attachments/assets/35a108f1-1660-41a4-8b62-4eeb3db7d088)

매크로는 기본적으로 **찾아바꾸기** 기능입니다.  
반복해서 길게 입력해야 하는 [Light.vn](https://soulengineproject.itch.io/lightvn) 명령어를 캡슐화하여 편의를 제공하는 것이 목적입니다.

예시는 `/Plugins/lvui/_system/macros.txt`에서 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/c0611c86-a103-40b4-b3e2-3a6b408a21e3)

## 스크립트 처리 방식

기억해야 할 핵심 두 가지:

- 기본적으로 스크립트는 `wait` 명령을 만날 때까지 계속 실행됩니다  
  - (또는 wait 상태를 유발하는 다른 명령어를 만날 때까지).
- `continueRead` 명령이 호출되면 wait 상태를 벗어나 다시 실행이 이어집니다.

따라서 예) `/Plugins/lvui/_system/keys.txt` 안에서 여러 `keyDown` 명령에 `continueRead`가 바인딩되어 있는 것을 볼 수 있습니다.  
특정 키를 누르면 스크립트가 계속 진행되도록 하는 구조입니다.

> 참고: `/Plugins/lvui/_system/keys.txt`는 `/Plugins/lvui/_system/textbox.txt` 내부에서 호출됩니다.  
> 기본 텍스트박스를 사용할 때 키 바인딩이 자동으로 적용되는 이유입니다.

**PRO 팁**: 스크립트가 진행되지 않는다면, `continueRead`를 `keyDown` 명령에 바인딩하지 않았을 가능성이 큽니다.  
(또는 문제 위치에 `script /Plugins/lvui/_system/keys.txt keybind_continueRead`를 추가하세요)

에디터의 `Key Triggers` 탭에서 키 바인딩을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/13979a26-5d85-412f-9d1d-e91503bf3215)

## 스크립트 처리 방식 2

스크립트는 위에서 아래로 순차적으로 읽습니다.  
흐름을 바꿀 수 있는 주요 명령은 두 가지입니다:

- `jump`
- `script`

`jump`  
- 현재 스크립트 파서를 다른 스크립트 혹은 동일 스크립트의 북마크 위치로 점프시킵니다.  
- 점프 후에는 해당 위치부터 계속 실행되며, 이전 wait 상태도 해제됩니다.  
- 예: 사용자 선택지 구현에 활용.

![image](https://github.com/user-attachments/assets/ccdecd67-1a25-49ff-be61-35534db82cb1)

`script`  
- 대상 파일로 새 스크립트 파서를 생성해 스택 최상단에 push합니다.  
- 스크립트 스택은 `Scripts` 탭에서 확인할 수 있습니다.  
- 스크립트가 `script_fin` 명령으로 종료되면 파서가 pop되고, 호출한 스크립트가 이어서 실행됩니다.

예시로 스크립트 스택이 증가하는 과정:

- 게임 시작(`start0.txt`)
- 우클릭으로 메뉴 호출(`/Plugins/lvui/_system/menu.txt`) → 스택 1 → 2
- 설정 클릭(`/Plugins/lvui/_system/config-system.txt`) → 스택 2 → 3

ID 탭에서 각 스크립트의 호출 관계를 확인할 수 있습니다.  
- `0 (from: n/a)` : 최초 스크립트  
- `1 (from: 0)` : ID 0번 스크립트가 호출  
- `7 (from: 1)` : ID 1번 스크립트가 호출

호출 순서와 일치함을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/a2068ed8-5f06-4441-9533-888563f45647)  
![image](https://github.com/user-attachments/assets/d8541cb1-8d07-4e25-8258-e287d868d75e)

그리고 역순으로,

- 우클릭으로 설정 페이지 종료 → 스택 3 → 2
- 우클릭으로 메뉴 종료 → 스택 2 → 1

결국 `start0.txt` 211번째 줄로 돌아가며(시작 위치), 다시 이어서 실행됩니다.

![image](https://github.com/user-attachments/assets/43203e71-f765-49e6-a541-59278b050b16)

## 스크립트 처리 예시: 사용자 선택지

앞서 설명한 내용을 바탕으로 [Light.vn](https://soulengineproject.itch.io/lightvn)에서 사용자 선택지가 생성되는 구조를 이해할 수 있습니다.

- `wait preventContinueRead`
  - 파서를 wait 상태로 만들고  
  - `continueRead`(예: `keyDown`에 바인딩)를 통한 진행 해제를 차단
- `jump`는 선택지 버튼에 연결
  - 사용자가 버튼을 클릭하면 `jump` 명령 실행
  - wait 상태가 해제되고 파서가 지정된 위치로 이동해 계속 파싱

결과: 사용자가 버튼을 클릭해야만 진행됩니다.

![image](https://github.com/user-attachments/assets/1ab82570-1708-42c1-964f-b850e6453dd7)

## 오브젝트 레이어와 표시 우선순위

기본적으로 레이어 값(`r`)이 높은 오브젝트가 낮은 오브젝트보다 위에 표시됩니다.

같은 레이어 값을 가진 오브젝트 간에는 **순서가 보장되지 않으며**  
(**실행 중에도 변동 가능!**)

`Objects` 탭에서 레이어 값을 확인할 수 있습니다:
- 파란색 하이라이트는 다른 오브젝트와 레이어 값이 겹친다는 의미
- 값이 겹치면 이미지가 직접 겹치지 않도록 주의하세요  
  - 예: 텍스트박스 하단의 skip·auto 버튼 등은 이미지가 겹치지 않으므로 같은 레이어 값 사용 가능

![image](https://github.com/user-attachments/assets/e56e9742-9c69-4769-b6ac-607375ae418c)

## 게임 내보내기

`Project` → `Publish` 메뉴로 진행합니다.

![image](https://github.com/user-attachments/assets/9a5b9732-9d5b-4cfc-90f9-1fad118625e1)

**주의 사항**

- 배포 전 테스트 플레이를 했다면 `SaveData`와 `Screenshots` 폴더를 비워 두세요.

**Q. 배포용 게임에서 LightTests.exe를 삭제해도 되나요?**

- 삭제하지 않는 것을 권장합니다.  
- `LightTests.exe`는 사용자의 환경이 게임 실행에 적합한지 확인하는 도구입니다.  
  - (배포 전에는 개발 PC 환경도 점검합니다)
- 테스트를 통과하면 게임이 정상 실행될 가능성이 높습니다.  
  - 실패 시 문제 발생 가능성이 매우 높습니다.
- 웹 페이지의 체크리스트보다 사용자에게 직관적입니다.  
  - 게임 실행 문제가 보고되면 먼저 `"LightTests.exe는 정상 실행되었나요?"`라고 확인할 수 있습니다.

## 앱 아이콘 변경

- [Smileflower 작성 튜토리얼](https://en.yorubox.eu/light-vn-tutorial-ep-09-export-game-change-app-icon/#change-application-icon-in-lightvn)

## 리소스 다시 불러오기

[Light.vn](https://soulengineproject.itch.io/lightvn) 16.7부터는 텍스트·이미지 등 리소스를 새 버전으로 교체해야 할 때

`Project` → `Reload Resources`

를 클릭하면 최신 리소스를 즉시 로드합니다.

![image](https://github.com/user-attachments/assets/4fc29fe0-7f17-4ab5-a305-6c40b58c1fde)
