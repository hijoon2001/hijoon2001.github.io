---
layout: posts
title: "[칼리리눅스 0.5] 칼리리눅스 setting"
categories:
  - 칼리리눅스
tags:
  - 개념 
---

👉🏻[참고유튜브](https://www.youtube.com/watch?v=g4dElX7yYUc)


<details><summary><strong>oh my zsh</strong> 란? </summary>
 <strong>zsh 설정 관리를 위한 프레임워크로, zsh를 더 쉽고 편리하게 사용할 수 있도록 도와주는 플러그인</strong> <br>
 Zsh (Z shell, zsh) 은 상호 작용 로그인 셸이자, 셸 스크립트를 위한 강력한 명령줄 인터프리터로 사용할 수 있는 유니스 셸.<br>
 shell 셸 은 application 을 실행시키는 도구로 OS 의 커널에 직접 접근 할 수 없기 때문에 사용하는 명령어 해석기..... 현재 가장 보편적으로 쓰이는 shell 은 bash (본쉘)..            
</details>

1. oh my zsh 검색후 

``` bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

커널에 설치!     
![Image](https://github.com/user-attachments/assets/f979d3b1-5364-4eaa-a202-7bbc88455731){: width="50%" height="50%"}

Oh My Zsh 라는 프레임 워크를 제대로 활용하기 위해 설정파일인 **.zshrc** 를 먼저 검토! 

```zsh
vi .zshrc
```

![Image](https://github.com/user-attachments/assets/aa5eb9b0-43d2-47e0-9a8a-e76fd445bca2){: width="50%" height="50%"}

```shell
plugins=(git eza zsh-autosuggestions grc sudo colorize zsh-syntax-highlighting tmux)

ZSH_COLORIZE_STYLE="colorful"
ZSH_TMUX_AUTOSTART=true
```
* 플로그인 목록에 다양한 기능 추가
  * eza: 개선된 ls 명령 제공 
  * zsh-autosuggestions: 명령어 자동 제안 기능 추가 
  * grc: 명령어 결과 색상 적용 
  * colorize: 파일 내용을 색상으로 표시 
  * zsh-syntax-highlighting: 명령어 구문 강조 기능 설정 
* .tmux.conf 설정 -> 창 및 패널 최적화 
* batcat설치 -> 코드 및 파일 미리보기를 위한 도구.
* Nerd Fonts 설치 - 개발자 친화적인 아이콘 폰트 적용. 

### 결과 
![Image](https://github.com/user-attachments/assets/ac7a101a-1625-4c9c-a2da-9400efd38bb7){: width="50%" height="50%"}



## 쉘 에러 

![Image](https://github.com/user-attachments/assets/5ba59cd6-f652-4837-a5f6-6ca876e1190c){: width="50%" height="50%"}

다음처럼 **quote>** 프롬프트가 반복적으로 나타남.   
    -> 특정 쉘 환경에 진입했거나 명령어 입력중 따음표를 닫지 않았기 때문!   
        -> Ctrl + C 키