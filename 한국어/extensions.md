---
title: 70. Extensions
description: 
published: true
date: 2025-07-17T02:38:52.695Z
tags: 
editor: markdown
dateCreated: 2025-07-17T02:38:52.695Z
---

## 개발자 확장: 플러그인

플러그인은 `Data/Plugins/` 아래에 배치할 수 있는 **독립형 폴더(모듈)** 입니다.  
해당 폴더를 다른 프로젝트로 복사·붙여넣기만 해도 **그대로** 작동해야 합니다.

이를 통해 다음과 같은 작업이 가능합니다.
- 커스텀 플러그인을 배포하여 다른 사용자가 활용하도록 지원 (예: 판매용 UI 플러그인)
- 문제가 발생한 부분을 최소 재현 프로젝트 형태로 공유하여 디버깅 지원 요청

**나만의 플러그인 만드는 방법**

1. `Data/Plugins` 폴더 아래에 새 폴더 생성 (예: `my_plugin`)
2. 플러그인에서 사용할 모든 리소스를 해당 폴더 안에 저장
3. 에디터에서 플러그인 폴더 안에 새 스크립트 작성 (예: `plugin.txt`)
   - 스크립트에서 사용하는 모든 리소스는 절대 경로로 참조해야 합니다.  
     - 예: `/Plugins/my_plugin/Common_PopupBg.png`

이제 플러그인 폴더를 압축(zip)하여 공유하면 됩니다.  
사용자는 다음과 같이 스크립트를 호출할 수 있습니다.  
- `script /Plugins/my_plugin/plugin.txt`

![image](https://github.com/user-attachments/assets/83ef0abe-69f3-4349-a212-1c5c46b7cd9e)

![image](https://github.com/user-attachments/assets/b72a7434-33dd-494c-83a0-ddc1d2b5b30a)

![image](https://github.com/user-attachments/assets/08d42040-fd91-47f9-9628-99d43903bc93)

## 플레이어 확장: 리소스 커스터마이즈

개발자는 특정 리소스를 교체 가능하도록 공개하여 플레이어가 게임을 커스터마이즈할 수 있게 할 수 있습니다.

이를 위해 `Data/encrypt_exclusions.txt` 파일을 사용하며, 다음과 같이 설정할 수 있습니다.

```
// --------------------------------------------------------
//
// 배포 시 암호화하지 않을
// 에셋 파일 또는 폴더 경로를 추가합니다.
// (경로마다 새 줄에 작성)
//
// ex：Scripts/scenario/ <- 폴더 전체 제외
// ex：Images/extra/extra0.png
//
// --------------------------------------------------------

// 예) 플레이어가 csv 시나리오 파일을
// 자유롭게 번역할 수 있도록 허용
Scripts/scenario_tables/
```