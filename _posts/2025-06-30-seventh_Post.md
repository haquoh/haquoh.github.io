---
title: "[대모산개발단 인턴쉽]DAY-4 AI Cli 다뤄보기"
excerpt: 
categories: 
  - 업무일지
tags:
  - 대모산개발단
  - AI Cli 
toc: true  # 목차 표시 여부
toc_sticky: true  # 목차를 스크롤에 따라 고정
last_modified_at: 2025-06-30T17:43:00+09:00  # 마지막 수정 시간
---

## Claude-Code 사용기 

  나는 윈도우를 쓰다보니 리눅스 가상 환경이 필요했다.
  
  관리 권한으로 터미널에서 wsl --install -d Ubuntu 로 wsl 을 깔아주었고 

  wsl 기본작업 디렉토리 설정을 해주면된다. 

  이제 나의 계정과 비밀번호 설정을 하게 되면서 

  wsl 실행 위치가 기본적으로 default 값이 설정되는데 

  실제 내 노트북에 있는 파일을 수정하고 claude code 를 실행하려면 

  wsl 실행 위치를 cd c:\Users\[사용자명] 이런식으로 변경해서 사용하여야 한다. 

  npm 으로 실행하고 싶다면 sudo apt-get install -y nodejs  이렇게 nodejs 깔려있는지 확인하고 

  npm install -g @anthropic-ai/claude-code 로 설치를 완료해주면 

  ![클로드](/assets/images/claudecode.png)

  이렇게 쌈뽕하고 귀여운 CLAUDE CODE 문구가 뜬다. 

  이걸 이제 vscode 에서 왼쪽 하단 원격 창을 열어서 wsl 연결해서 사용하면 된다. 
  
