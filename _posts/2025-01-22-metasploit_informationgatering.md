---
layout: posts
title: "[metasploit 2] Information gathering "
categories:
  - 칼리리눅스
  - metasploit
tags:
  - 개념 
---

# **다양한 프로토콜**에서 정보 수집 및 열거

## TCP (Transmission Control Protocol)
 : reliable 한 packet transmission을 보장하는 connection-oriented 프로토콜.     
 Telnet, SSH, FTP, SMTP와 같은 많은 서비스들이 TCP 프로토콜을 사용한다.      
**이 모듈**은 대상 시스템에 대해 간단한 포트 스캔을 수행하여 열려 있는 TCP 포트를 알려준다.  

auxiliary module name : **auxiliary/scanner/portscan/tcp**      
    - RHOSTS (공격할 대상의 주소)      
    - PORTS 

<img src="https://github.com/user-attachments/assets/b35d2f2a-c320-496a-af74-18f18b743451"> |<img src="https://github.com/user-attachments/assets/8a22b28c-f005-4069-b019-45bd9f6c73af">

## UDP (User Datagram Protocol)  
TCP 보다 lightweight 하지만 TCP 만큼 reliable 하지 않다. 주로 SNMP / DNS 에서 사용.     
이 모듈은 대상 시스템에 대해 간단한 포트 스캔을 수행하여 열려 있는 UDP 포트를 알려준다.        

auxiliary module name : **auxiliary/scanner/discovery/udp_sweep**     
    - RHOSTS (공격할 대상의 주소)

![Image](https://github.com/user-attachments/assets/d2e84a8b-b3a7-4384-8f4d-0008765748e3) | ![Image](https://github.com/user-attachments/assets/1fbf1806-8f00-4956-87f6-48d51b03f4e6)

## FTP (File Transfer Protocol)
클라이언트와 서버 간의 파일 공유를 위해 가장 일반적으로 사용되는 프로토콜. 통신을 위해 **TCP 포트 21**을 사용한다. 
- 그 중 **fpt_login 모듈** : 대상 FTP 서버에 대해 브루트 포스(무차별 대입 공격)을 수행하는 데 사용된다. 즉, 여러 개의 사용자 이름과 비밀번호를 시도하여 인증을 우회할 수 있는지 테스트한다.         
auxiliary module 경로 : **auxiliary/scanner/ftp/ftp_login**     
    - RHOSTS (스캔할 대상의 IP 주소 또는 IP 범위 설정)  
    - USERPASS_FILE (사용자 이름 및 비밀번호 목록이 포함된 파일의 경로. 예: /root/userpass.txt)

## SMB(Server Message Block) 
애플리케이션 계층 프로토콜로, 파일 및 프린터 공유 등의 목적으로 주로 사용된다. SMB는 통신을 위해 **TCP 포트 445**를 사용한다.  

1. **auxiliary/scanner/smb/smb_version**
   - RHOSTS
    : 대상 시스템에서 실행 중인 SMB 프로토콜의 버전(SMB1, SMB2, SMB3 등)이 표시된다.   
2. **auxiliary/scanner/smb/smb_enumusers**
   - RHOSTS
    :  대상 시스템의 SMB RPC 서비스를 통해 사용자 계정을 열거(나열)하는 기능을 수행. 타겟 시스템의 사용자 계정 목록이 출력된다.         

## HTTP (Hypertext Transfer Protocol)
HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜. stateless 애플리케이션 계층 프로토콜로, 월드 와이드 웹(World Wide Web)에서 정보를 교환하는 데 사용된다.  HTTP는 **TCP 포트 80**을 통해 통신한다.   

<details><summary>window 에서 http 실행</summary>

<p><img src="https://github.com/user-attachments/assets/0fc4f01c-dd65-4670-bcce-28fb1a86b269" alt="Image"></p>

</details>

1. **auxiliary/scanner/http/http_version** : 대상 시스템에서 실행 중인 웹 서버의 버전을 탐색하고 검색한다. 

    ![Image](https://github.com/user-attachments/assets/5928ed64-7fd9-4962-83d3-c5552ac48435) 
  * window cmd에서 8080 html킴.   
  * 이를 확인하기 위해 set RHOSTS, RPORTS 한 후 run.  

2. **auxiliary/scanner/http/backup_file** 
3. **auxiliary/scanner/http/dir_listing** : 웹 서버가 루트 디렉토리에 포함된 파일 목록을 표시하도록 잘못 구성된 경우가 많다. 디렉토리에는 웹사이트의 링크를 통해 일반적으로 노출되지 않는 파일이 포함되어 있어 민감한 정보가 유출될 수 있다.
이 보조 모듈은 대상 웹 서버가 디렉토리 목록에 취약한지 여부를 확인한다.
   - RHOSTS
   - PATH 
4. **auxiliary/scanner/http/ssl** :SSL 인증서는 전송 중인 데이터를 암호화하는 데 매우 일반적으로 사용되지만, 종종 잘못 설정되었거나 약한 암호화 알고리즘을 사용한다. 이 보조 모듈은 대상 시스템에 설치된 SSL 인증서의 잠재적인 취약점을 확인한다. 

## SMTP(Simple Mail Transfer Protocol) 
: 이메일 전송을 위한 프로토콜. 이메일을 발송하는데 사용된다. 주로 TCP port 25번 사용.  

## SSH(Secure Shell) 
: SSH 원격지의 셸에 접속하기 위해 사용되는 네트워크 프로토콜. 주로 TCP port 22번 사용. 
1. **auxiliary/scanner/ssh/ssh_enumusers** : SSH 서버에 대한 사용자 이름 열거(Enumeration).






---

※ **포트(port)**? "논리적인 접속장소" 이며 특히 인터넷 프로토콜인 TCP/IP 를 사용할 때에는 클라이언트 프로그램이 네트워크 상의 특정 서버 프로그램을 지정하는 방법으로 사용된다. 네트워크 상에서는 통신 시 IP를 토대로 해당 서버가 있는 컴퓨터에 접근하게 되는데, 대표적으로 인터넷 웹서비스, 메일 서비스, DNS 서비스, FTP 서비스 등이 있다.

이때, 대부분의 컴퓨터에는 하나의 컴퓨터에서 여러개의 서버가 실행된다.이때, 어느 서버에 접속해야 하는지 컴퓨터에게 알려주어야 하는데. 이를 위해 사용되는 것이 **포트 번호**이다.   

※ **포트 번호**? 해당 컴퓨터에서 실행되고 있는 서버를 구분 짓기 위한 16비트의 논리적 할당으로 0 ~ 65536번이 존재한다. 이 중 0~ 1023 번 까지(=well-known port)는 어떤 통신이 어떤 포트를 사용할 것인지 정해져 있는데 예를들면 http 통신은 80번 포트, ssh통신은 22번 포트 를 사용한다.   
👉🏻[더 많은 포트 번호](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.txt)    

만약 웹서버를 하나 더 사용하고 싶은 경우 80번 포트는 이미 기존 웹서버에서 사용중이기 때문에 사용할 수 없다. 이럴때 well-known-port가 아닌 다른 포트들과 연결해서 사용하여야 하는데, 이때 관습적으로 사용하는 것이 **8080**이다.