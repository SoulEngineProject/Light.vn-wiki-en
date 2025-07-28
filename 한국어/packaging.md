---
title: 20. Packaging
description: 
published: true
date: 2025-07-18T22:36:52.668Z
tags: 
editor: markdown
dateCreated: 2025-07-18T22:36:52.668Z
---

## 공통

모든 패키징 작업은 `Project` → `Publish` 메뉴에서 원하는 패키지 유형을 실행하는 것부터 시작합니다.

## C++ (데스크톱)

배포 후 C++ 버전의 Light.vn에서 고려할 수 있는 커스터마이징 옵션은 다음과 같습니다.

- **쓰기 디렉터리 설정**
  - `Settings.xml` 파일의 `writeDirectoryType` 속성 값을 수정할 수 있습니다.
    - `0`: 게임이 설치된 폴더에 데이터를 기록합니다.
    - `1`: 예) `C:\Users\{user name}\AppData\Roaming\{sysProjectFolder}` 경로에 데이터를 기록합니다.
      - 게임 폴더에 쓰기 권한이 보장되지 않는 경우(예: CD로 배포) 유용합니다.
      - Light.vn이 쓰기 불가능한 폴더에 기록하려 할 때 다음과 같은 오류가 발생할 수 있습니다.
      - <img alt="image" src="https://github.com/user-attachments/assets/3d91a6d0-667c-4ef3-bdc8-9af11d52c633" />

**패치 배포**

사용자에게 전체 게임을 다시 다운로드하게 하는 대신, 최소한의 `Patch`만 배포할 수 있습니다.

- <img alt="image" src="https://github.com/user-attachments/assets/83581d27-41ac-49e9-a74c-1141400b3b05" />
- 실행하면 `Patch` 폴더가 생성되며, 이를 압축(zip)하여 사용자에게 전달한 뒤 게임 루트 폴더에 넣도록 안내하면 됩니다.

## Web

### 준비 사항

- [python3](https://www.python.org/downloads/)
  - 설치 시 다음 옵션을 반드시 선택하세요.
    - **Add Python 3.9 to PATH**
    - **Disable path length limit**
- [cmder](https://cmder.app/)

### 웹 빌드 최종 준비

1. `scripts/emsdk_directory.txt` 파일을 업데이트합니다.
2. `emsdk`를 설치할 폴더(게임 배포 폴더 외부)로 이동해 `{game folder}/scripts/setup_emscripten.sh`를 복사합니다.
3. `cmder`를 열어 다음 명령을 실행합니다.
   - `sh setup_emscripten.sh`
   - 완료 후 출력되는 경로를 게임 내보낸 폴더의 `scripts/emsdk_directory.txt`에 붙여넣습니다.
   - 편의를 위해 `_export/webgl/scripts/emsdk_directory.txt`(즉, `LightEditor.exe`가 있는 폴더)에도 같은 경로를 넣어둡니다.
     - <img alt="image" src="https://github.com/user-attachments/assets/3d4d0d65-6a07-41e7-a3e6-cebaf1bcf71e" />
     - 예시 경로: `/c/Users/daego/Desktop/Light.vn_Sample/emsdk`

### 테스트 플레이

- 시작: `sh ./scripts/run.sh`
  - 명령이 실행되면 게임 파일이 `loader.js`, `project.data`로 패키징되고 브라우저에서 게임이 실행됩니다.
  - 브라우저 콘솔을 열어 `project.data`가 최신인지(브라우저 캐시 충돌 여부) 확인하세요.
  - <img alt="image" src="https://github.com/user-attachments/assets/b7a8fffe-c4a1-4c31-b7ec-9f1b396ac87c" />
- 종료: `Ctrl + C`

### 게임 업로드

- `data/`, `scripts/` 폴더를 제외한 모든 파일을 업로드하면 됩니다.

### C++ 버전과의 차이점

- 구현되지 않았거나 유의할 점
  - 텍스트 입력
  - `open` 명령: URL로만 제한됨
  - `lua` 사용 시 Windows 전용 함수를 호출할 수 없음
  - 사용자가 페이지를 클릭하기 전까지 오디오가 재생되지 않음
- 기능 차이
  - 게임 시작 시 모든 리소스를 한 번에 로드
  - FPS가 `60`으로 고정됨

### 배포 커스터마이징

- `settings.xml`
  - `disallowOpen`: `open` 명령 허용 여부
    - 배포 플랫폼의 `Content-Security-Policy` 등에 따라 URL 열기가 차단될 수 있습니다.
  - `disallowPopups`: 오류 알림 팝업 표시 여부
    - 데스크톱 게임과 달리 웹에서는 사용자 관용도가 낮을 수 있습니다.

### 자체 서버에 배포할 때 필수 설정

- `Response Header`에 다음을 추가해야 합니다.
  - `"Cross-Origin-Opener-Policy", "same-origin"`
  - `"Cross-Origin-Embedder-Policy", "require-corp"`
  - 자세한 내용은 `server.py` 참고

### 최적화는 필수!

게임 전체를 한 번에 로드하므로, 디스크 용량을 줄이기 위한 파일 최적화가 매우 중요합니다.  
- 목표 용량은 **90 MB 이하**를 권장합니다.