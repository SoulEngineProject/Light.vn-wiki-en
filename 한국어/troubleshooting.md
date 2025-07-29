---
title: 80. Troubleshooting
description: 
published: true
date: 2025-07-17T02:39:25.746Z
tags: 
editor: markdown
dateCreated: 2025-07-17T02:39:25.746Z
---

## 버그 공유(Sharing Bugs)

**엔진 버그로 보이는 현상을 발견했다면**

- [플러그인](./extensions.md#developer-extensions-plugins) 형태로 *최소 재현 예제*를 만들어 보세요.
- 해당 플러그인을 Discord에 올리고 증상을 설명합니다.

**도저히 이해되지 않는 오류나 드물게 발생하는 오류라면**

옵션 1:  
- `Pause` 버튼을 눌러 게임을 멈추고 더 이상 상태가 바뀌지 않도록 합니다.  
  - 에디터의 다양한 기능을 이용해 진단하세요.

옵션 2:  
- 테스트 플레이 중 에디터의 `Interop` 탭에서 `Debug Save` 클릭  
  - `SaveData/saveslot_debug.xml` 파일이 생성됩니다.  
- 프로젝트 전체와 `SaveData/` 폴더를 그대로 공유하고,  
  - Discord에 증상을 설명하며 도움을 요청합니다.  
    - 상대방은 테스트 플레이 중 `Debug Load`를 눌러 동일 지점으로 바로 복귀할 수 있습니다.

![image](https://github.com/user-attachments/assets/6a4be95e-055b-45b0-a930-866b6188a546)

## 논리 오류(Logical Errors)

스크립트에서 이상 현상 또는 논리적 오류가 의심된다면 다음을 시도하세요.

- 오류 가능 위치에 `breakpoint` 또는 `SystemError`를 삽입  
  - 해당 줄에 도달하면 에디터가 일시 정지되고, 정보를 통해 원인을 파악할 수 있습니다.
- 변수 관련 오류가 의심된다면, `if` 명령과 결합해 가정을 검증하세요.  
  - 예: `if (my_variable != 0) SystemError "my_variable is {{my_variable}}!"`

## 기본 텍스트박스 이름 매크로 변경

기본적으로 캐릭터 이름 표시에 `【】` 매크로를 사용합니다.

![image](https://github.com/user-attachments/assets/33a48aad-7f54-4dc2-832e-8f5a1429eb8f)

변경하려면 `Macros` 탭에서 해당 매크로가 포함된 스크립트를 열어 다음과 같은 줄을 찾습니다.
```
~macro "~【(.*)】" "~script /Plugins/lvui/_system/textbox.txt name \"$1\""
```
예를 들어 이름 구분 기호를 `<>`로 바꾸고 싶다면 다음과 같이 수정합니다.

```
~macro "~<(.*)>" "~script /Plugins/lvui/_system/textbox.txt name \"$1\""
```

## 오브젝트가 표시되지 않아요!

아래 절차를 차례로 점검하세요.

### 1) 명령어 자체가 정상인지 확인
- 오브젝트를 생성·표시하는 명령 바로 앞에서 테스트 플레이를 시작합니다.  
  - 오류 메시지가 없다면 다음 단계로 이동.

### 2) 오브젝트 존재 여부 확인
- 오브젝트가 표시되어야 하는 위치로 스크립트를 설정합니다.
- 에디터의 `Objects` 탭에서 오브젝트 이름을 입력해 목록에 표시되는지 확인합니다.

![image](https://github.com/user-attachments/assets/776ffc0d-d704-413a-8ad5-2839d4d1c61b)

### 3) 다른 오브젝트 아래에 가려졌는지 확인
- `Objects` 탭에서 `Center R` 열을 확인합니다.
- 더 높은 `r` 값을 가진 오브젝트가 의심된다면 스크립트에서 해당 오브젝트를 제거(예: `fadeout`)합니다.

![image](https://github.com/user-attachments/assets/0adcd4f9-f0ed-479b-8689-e599ea4a1c46)

### 4) 화면 밖에 위치했는지 확인
- 카메라 모드를 `Free Camera`로 전환합니다.
- 마우스 휠로 줌 아웃하는 등 카메라를 이동해 오브젝트가 화면 밖에 표시되는지 확인합니다.  
  - (아래 예시에서는 검은 텍스처가 카메라 프레임 밖에 위치)  
  - 그렇다면 오브젝트의 좌표를 수정하면 됩니다.

![image](https://github.com/user-attachments/assets/dcb477f3-5e63-4b2a-b536-58bf3c2559d2)

## 오브젝트가 갑자기 변했어요!

오브젝트·변수 등이 예상치 못하게 변했다면,  
에디터 각 탭의 `Created at` 열을 활용해 변경 위치를 추적하세요.

![image](https://github.com/user-attachments/assets/447b1811-21bc-43bf-98c8-d2000cc08760)

`Variables`, `Key Triggers` 등 일부 탭에서는 `Created at`이  
**마지막으로 업데이트된 줄**을 의미하기도 합니다.

![image](https://github.com/user-attachments/assets/7e13210d-7832-430d-9884-5523584cc3b5)

## 오브젝트가 갑자기 사라졌어요!

1. 오브젝트 `name`을 파악합니다.  
2. 생성 이후 줄에 다음을 추가합니다.  `onDestroy [name] SystemError "my object disappeared!"`
3. 오브젝트가 파괴되면 에디터가 일시 정지하며 오류를 표시합니다.  
- `Scripts` 탭을 확인해 파괴가 발생한 위치를 파악하세요.

## 게임이 느려졌어요!

대부분 **화면에 남아 있는 불필요한 오브젝트**가 원인입니다.

![image](https://github.com/user-attachments/assets/33f099ff-c48c-4bcc-9719-d5b1a4dbccf9)

- 에디터 좌하단 `Render Count`를 확인합니다.
- `Objects` 탭에서 이전 씬에서 남아 더 이상 필요 없는 오브젝트가 있는지 확인합니다.  
- `Created at` 열을 통해 오브젝트 발생 위치를 빠르게 찾을 수 있습니다.

**PRO 팁**: 씬 시작·종료 시 `clear` 명령을 추가하면 대부분의 느려짐을 예방할 수 있습니다.