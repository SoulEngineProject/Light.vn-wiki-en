---
title: 21. Packaging Optimisations
description: Optimisations when packaging your game
published: true
date: 2025-07-18T22:37:32.456Z
tags: 
editor: markdown
dateCreated: 2025-07-18T22:37:32.456Z
---

## 파일 최적화

**권장 파일 형식**

디스크 용량을 최소화하려면 다음 형식으로 파일을 최적화하는 것을 권장합니다.

- 이미지: webp  
  - 변환에는 예를 들어 [tinypng](https://tinypng.com/)을 사용할 수 있습니다.
- 오디오: ogg  
  - 오디오 파일에 **비디오 스트림이 포함되어 있지 않은지** 반드시 확인하세요. 예시:  
  - <img alt="image" src="https://github.com/user-attachments/assets/74b9909a-15d7-4561-a729-5acf28a3e9ed" />

**권장 파일 이름 규칙**

가능한 많은 운영체제에서 호환성을 확보하려면 파일 이름에 영문자, 숫자, 그리고 `_`만 사용하는 것을 권장합니다.  
예시: `momo_costume_1.webp`

## 하드웨어 최적화

- 사용자 평균 사양을 파악하려면 [Steam Hardware & Software Survey](https://store.steampowered.com/hwsurvey/Steam-Hardware-Software-Survey-Welcome-to-Steam)를 참고하세요.  
  - 목표로 하는 GPU에 따라 `maximum texture size`가 달라진다는 점을 유의하세요!
- 일반적으로 Windows 환경에서는 사용자의 RAM 및 VRAM의 **최대 50%**만 사용할 수 있다고 가정해야 합니다.  
  그 이상을 사용하려 하면 게임이 **크래시**될 수 있습니다.  
  - 예) `1920 x 1080` 이미지를 GPU VRAM에 비압축 상태로 올리면  
    - 1920 × 1080 × 4(RGBA) 바이트 = 8,294,400 바이트 ≈ 8 MB  
    - 사용자의 VRAM이 8 GB라면, 8 GB / 2 = 4 GB  
      - 4 GB / 8 MB ≈ 500장  
        - 특히 애니메이션을 사용한다면 생각보다 많지 않습니다!  
        - 컴퓨터 공학에서 `시간`(예: 리소스 로딩 시간)과 `공간`(예: RAM·디스크 용량)은 언제나 상충 관계라는 점을 명심하세요.
