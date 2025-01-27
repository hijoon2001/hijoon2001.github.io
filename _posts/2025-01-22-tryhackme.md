---
layout: posts
title: "[tryhackme] Agent Sudo"
categories:
  - 칼리리눅스
tags:
  - 개념 
---

# CTF란?

CTF(Capture The Flag, 깃발뺏기)는 사이버세계에서 공격방어대회를 뜻한다. 즉 **Flag** 는 정답을 뜻한다! 

![Image](https://github.com/user-attachments/assets/d7e815f5-ede5-4bf5-b5cc-bbac8cd6e413)

1. "enumerate" 단계
   : 머신을 조사하여 필요한 정보 찾기 

   1. How many open ports? (몇 개의 열린 포트가 있나요?)

   2. How you redirect yourself to a secret page? (어떻게 숨겨진 페이지로 리다이렉션되나요?) 
   3. What is the agent name? (에이전트 이름은 무엇인가요?)

---
포트(Port)란? 네트워크 서비스나 특정 프로세스를 식별하는 논리적 단위.    
          
## nmap
network mapper. 네트워크 스캐닝 툴. 대상(target)의 포트 및 서비스를 스캔하는데 사용되는 툴.          
