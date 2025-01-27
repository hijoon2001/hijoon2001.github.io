---
layout: posts
title: "[metasploit]1 기초 "
categories:
  - 칼리리눅스
  - metasploit
tags:
  - 개념 
---

# Metasploit Framework (메타스플로잇 프레임워크)
버퍼 오버플로우, 패스워드 취약점, 웹 응용 취약점, 데이터베이스, 와이파이 취약점 등에 대한 약 300개 이상의 공격 모듈을 가지고 있는 오픈 소스 도구.    

![Image](https://github.com/user-attachments/assets/e6a347fa-0796-4e71-a66e-8a12d8fafb16)|![Image](https://github.com/user-attachments/assets/80d43f63-245a-4dd6-9e60-3a7b824269b4)

## In modules: 
- **auxiliary**(어그질러리. 보조의..): 다양한 보조 모듈(스캐닝, 정보 수집 등).    
- **encoders**: 페이로드 인코딩을 위한 모듈.     
- **evasion**: 탐지를 피하기 위한 모듈.     
- **exploits**: 공격을 수행하는 익스플로잇 모듈.    
- **nops**: NOP 슬라이드 관련 모듈.    
- **payloads**: 공격 대상에서 실행될 페이로드.    
- **post**: 공격 후 단계에서 사용할 모듈.    
- **README.md**: 모듈에 대한 설명이 포함된 문서.     

### Auxiliary 
특정 시스템을 공격하지 않고도 다양한 보안 관련 작업을 수행할 수 있도록 설계된 모듈. 많지만 압도될 필요 없어용. 개별적으로 어떻게 사용하는지만 알면 되니까는 ㅎㅎ  

<details><summary><strong>msf? CVE?</strong></summary>
Metasploit(메타스플로잇): CVE 넘버링이 붙은 알려진 취약점 공격을 사용할 수 있도록 제공되는 도구. 해킹을 간단하게 하도록 도와주는 모의 해킹 테스트 도구.<br>  
CVE란? Common Vulnerabilities and Exposure 약자로 공개적으로 알려진 소프트웨어 보안 취약점을 가리키는 고유 표기이다.
</details>

예시.      
1. 터미널 열기 및 metasploit 실행 
   ```bash
   msfconsole
   ```
   - 프롬프트가 msf>로 변경된다. 
2. 포트 스캔 모듈 선택
    ```bash 
    use auxiliary/scanner/portscan/tcp
    ```
3. 모듈이 요구하는 설정을 확인
   ```bash
   show options
   ```
   ![Image](https://github.com/user-attachments/assets/87929fba-2e60-46df-a91e-df0319db4cc9)

   ![Image](https://github.com/user-attachments/assets/db8df7b7-f751-4060-8761-faf768839cc6)
   - metasploitable2-의 ip 주소 : 192.168.111.130 

4. 스캔 대상 ip 주소, 포트 범위 설정 
    ```bash
    set RHOSTS 192.168.111.130 / 대상 IP 주소 설정 
    set PORTS 1-1000 / 포트 범위 설정
    run  / 스캔 실행
    ```
   
   ![Image](https://github.com/user-attachments/assets/575afbf9-fa3c-45f4-808c-d8dff779b673)
   

### Payloads 
익스플로잇이 성공한 이후 목표 시스템에서 수행할 작업을 결정하는 요소. 즉 최종 목적 코드.   
예를들어 설명하면... 미사일에 장착하는 **폭약**같은느낌s. 미사일이 동일하더라도, 목표에 따라 다른 종류의 페이로드(폭약)를 장착할 수 있는 것이라고 생각해봥.          

예시. ****reverse_tcp** 페이로드 설정. (타겟 시스템이 공격자 시스템으로 연결을 시도하도록 하여 공격자가 대상 시스템을 원격 제어할 수 있도록 해준다.)
1. 터미널 열기 및 metasploit 실행 
   ```bash
   msfconsole
   ```
   - 프롬프트가 msf>로 변경된다. 
2. Metasploit에서 reverse_tcp 페이로드를 선택하여 타겟 시스템이 Kali Linux로 연결을 시도하도록 설정한다. 
    ```bash
   use payload/windows/shell/reverse_tcp
   ```
   ![Image](https://github.com/user-attachments/assets/db03a1dd-5ba9-41d3-abba-8d02f6aabc40)
   - LHOST: 공격자가 대기할 IP 주소 (공격자의 IP)
   - LPORT: 공격자가 대기할 포트 (기본값 4444)

### Encoders
침투시 보안 소프트웨어에 의해 탐지될 가능성이 있다. 이를 방지해주는 역할... 즉! **exploit(익스플로잇), payload(페이로드)를 jeopardize(난독화)하여 탐지를 피하게** 한다. 종류가 다양함..!  

### NOPs 
어셈블리 언어에서 No Operation instruction. 즉, 아무 작업도 수행하지 않는 명령어를 뜻한다.  
NOP는 익스플로잇이나 셸코드를 작성할 때 유용하게 사용될 수 있다. NOP를 추가하면 페이로드의 시그니처를 변경하여 보안 소프트웨어의 탐지를 피할 수 있다.  

### Post
contain various scripts and utilities -> **공격에 성공한 후 타겟 시스템에 추가로 침투할 수 있도록 도와준다.**  
<details><summary>영어</summary>
vulnerability: 취약점  <br>
exploit: 공격/ 악용      
</details>

### Evasion
탐지를 피하기 위해 페이로드를 수정해야 한다. 최신 버전의 메타스플롯 프레임워크는 탐지를 피하기 위해 페이로드를 수정하는 데 도움이 되는 특수 회피 모듈을 제공한다. 그게 바로 Evasion?!

---

# msfconsole 
: A simple command-line interface of the Metasploit Framework.      

## commands 살펴보기 
1. banner
2. version 
![Image](https://github.com/user-attachments/assets/a64497cf-e502-4460-bbc0-e8a12c39e467)
3. connect <ip:port>
4. help 
5. route : 
6. save : 저장
7. sessions
8. spool :
    콘솔과 함께 모든 출력을 사용자 정의 파일로 출력한다. 출력 파일은 나중에 필요한 경우 분석할 수 있다.
9. show :
10. info : 
11. irb : Ruby platform 호출. 일반적으로 익스플로잇 후 단계에서 사용자 지정 스크립트를 생성하고 호출하는 데 사용.  
12. makerc <output rc file> : 특정 세션의 전체 명령 기록을 사용자 정의 출력 파일에 간단히 기록한다. 

----

# Variables 변수

we need to set values to some of the **variables**

| 변수 이름          | 변수 설명 |
|-------------------|----------|
| **LHOST**  | 로컬 호스트: 공격자의 시스템 IP 주소를 의미. 익스플로잇을 시작하는 시스템의 IP를 설정한다. |
| **LPORT**  | 로컬 포트: 공격자의 시스템에서 사용하는 (로컬) 포트 번호. 보통 리버스 셸을 받을 때 필요. |
| **RHOST**  | 원격 호스트: 공격할 대상 시스템의 IP 주소. |
| **RHOSTS** | 여러 개의 타겟에 대해 익스플로잇을 수행하려면 이 변수를 사용. 예를 들어 `RHOSTS 192.168.0.1/24`로 설정하면 전체 서브넷을 대상으로 설정할 수 있다. 또는 `RHOSTS file:/opt/targets.txt`를 사용해 IP 주소 목록이 포함된 파일을 설정할 수도 있다. |
| **RPORT**  | 원격 포트: 공격할 대상 시스템의 포트 번호. 예를 들어, 원격 시스템의 FTP 취약점을 공격하려면 RPORT를 21로 설정한다. |

## 변수 확인을 위한 명령어 
1. get [변수명] : 현재 로드된 모듈에서 설정된 변수 확인
2. getg [변수명] : 전체 세션(전역)에서 설정된 변수 확

## 변수 설정/해제를를 위한 명령어 

set <변수> <변수 값> 
unset <변수명> : 초기화 

---

# Update 
```bash
msfupdate
``` 

