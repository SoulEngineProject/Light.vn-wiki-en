---
title: 10. Productivity Tips
description: 
published: true
date: 2025-07-17T02:37:21.392Z
tags: 
editor: markdown
dateCreated: 2025-07-17T02:37:21.392Z
---

## 새 줄을 만드는 `.` 사용법

시나리오 줄의 시작에 `.`을 붙이면 새 줄이 생성됩니다.  
하나 이상 연속으로 사용할 수도 있습니다!
```...hello```
위 예시는 새 줄을 **3줄** 생성합니다.

## 씬 정리

각 씬의 시작 또는 끝에  
- `clear`  
명령을 추가하세요.

이렇게 하면 이전 씬의 잔여 오브젝트가 모두 제거되어

- 매 실행마다 현재 씬이 **결정적**(반복 실행해도 동일)으로 유지되고
- 게임의 리소스 사용량을 **최소화**할 수 있습니다.

## 시나리오 자동화: `textAutoWait` 활용

`textAutoWait` 명령을 사용하면 다음과 같은 시나리오를
```
"This is great\w
.This is even great\w
.This is triple great\w
```
다음과 같이 단순화할 수 있습니다.
```
textAutoWait 1
"This is great
.This is even great
.This is triple great
```
(각 줄 끝에서 자동으로 대기)

`textAutoWait`에는 다양한 옵션이 있어  
시나리오를 Light.vn으로 가져오는 시간을 크게 단축할 수 있습니다.  
여러 옵션을 시험해 보며 최적의 설정을 찾아보세요!

## 적절할 때 `|` 사용하기

`|` 기호를 사용하면 한 줄에 여러 명령어를 작성할 수 있습니다.  
예를 들어 아래와 같은 스크립트가 있을 때:

**예시 A)**
```
~cg0 logo light_splash_1280.png 0 0 90
.fadein logo 800
```

다음과 같이 바꾸는 것을 고려해 보세요.

**예시 B)**
```
~cg0 logo light_splash_1280.png 0 0 90 | .fadein logo 800
```

- **예시 A**에서는 오브젝트 위치를 수정하려면
  1. `cg0` 줄을 수정
  2. `.fadein` 줄로 커서를 옮겨 미리보기를 확인
  3. 올바른 위치가 될 때까지 반복해야 합니다.
- **예시 B**에서는 `cg0` 줄에서 위치만 수정하면 `.fadein`이 같은 줄에 있으므로 **즉시** 미리보기에 반영됩니다.

Light.vn 샘플에는 입문자 친화성을 위해 **예시 A**가 많이 쓰이지만,  
실무에서는 가능하면 **예시 B**를 추천합니다!

![image](https://github.com/user-attachments/assets/bceeb69f-046b-4d0d-96e9-d68acdc3bf48)

## 적절할 때 `|` 사용하기 (2)

아래와 같은 버튼 명령어는
```
~button0 choice_02 30 50 80 jump my_file.txt choice
zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```
다음과 같이 개선할 수 있습니다.
```
~button0 choice_02 30 50 80 "jump my_file.txt choice" | zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```

위에서 설명한 실시간 미리보기의 이점을 그대로 누릴 수 있습니다.  

또한 명령어를 `""`로 감싸면 실제 명령인지 명확해져  
엔진이 `|`를 해석하기도 쉬워집니다.

## 여러 오브젝트를 한 번에 타깃팅하기

여러 오브젝트에 동일한 명령을 적용하기 위해 다음과 같이 작성하는 경우가 많습니다.

```
fadeout alice1 800
fadeout alice2 800
fadeout alice3 800
fadeout alice4 800
``` 
이를 한 줄로 단순화할 수 있습니다.

```
fadeout alice1, alice2, alice3, alice4 800
```
정규식을 사용하면 더 간결해집니다.
```
fadeout alice.* 800
```

이 예시는 **좋은 네이밍 규칙**의 중요성을 다시 한 번 보여 줍니다. ([참고](https://github.com/SoulEngineProject/Light.vn/issues/12))

## 스크립트 자동화: 안전한 매크로 작성

매크로는 텍스트 A를 B로 치환하는 기능입니다.  
보통 `커스텀 명령어`를 만들 때 사용하지만,  
원치 않는 A까지 치환될 위험이 있으므로 다음을 권장합니다.

**A. `commandMacro` 사용**
- 예시  
  - `~macro my_textbox "script system\textbox.txt default"`  
  - → `~commandMacro my_textbox "script system\textbox.txt default"`
- 이유  
  - `commandMacro`는 **명령어 형태**를 만족하는 텍스트만 치환하므로 안전합니다.  
  - 단, 정규식을 사용할 수 없는 제약이 있습니다.

**B. 매크로 앞에 `~` 추가**
- 예시  
  - `~macro my_textbox "script system\textbox.txt default"`  
  - → `~macro ~my_textbox "~script system\textbox.txt default"`
- 이유  
  - Light.vn에서 `~`는 해당 줄을 **명령어 줄**로 간주합니다.

**C. 매크로 앞에 `^` 추가**
- 예시  
  - `~macro my_textbox "script system\textbox.txt default"`  
  - → `~macro ^~my_textbox "^~script system\textbox.txt default"`
- 이유  
  - `^`는 **줄의 시작**을 의미하므로 치환 범위를 더 제한해 안전성을 높입니다.

## 프로토타입 버튼을 빠르게 만드는 방법

```
textureCreateRect btn_prototype.png 300 50 255 0 0
textureCreateRect btn_prototype_touch.png 300 50 0 255 0
textureCreateRect btn_prototype_click.png 300 50 0 0 255

~touchableRes btn_prototype.png btn_prototype_touch.png btn_prototype_click.png
~button test1 100 300 80
~btnText test1 NotoSansCJKjp-Regular.otf 24 "click me"

~button test2 100 400 80
~btnText test2 NotoSansCJKjp-Regular.otf 24 "click me too"
```

`textureCreateRect`는 animation, textureCreate 등과 마찬가지로  
이름이 게임에 캐시되어 반복 사용 가능합니다.  
- (Images/btn_prototype.png, … 등으로 캐시)  
- 초기 버튼 프로토타입을 위한 스크립트에 저장해 두고 재사용할 수 있습니다.  
- 실제 이미지가 준비되면 같은 이름으로 교체하면 스크립트 수정이 필요 없습니다.

![image](https://github.com/user-attachments/assets/63863795-cdc2-4777-8c0e-921762f9a5de)
