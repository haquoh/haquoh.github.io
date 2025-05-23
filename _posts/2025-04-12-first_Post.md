---
title: "MCP 란 무엇인가?"
excerpt: "MCP 에 대해 알아보겠습니다다."
categories:
  - AI
tags:
  - MCP
  - claude
toc: true  # 목차 표시 여부
toc_sticky: true  # 목차를 스크롤에 따라 고정
last_modified_at: 2025-04-13T18:43:00+09:00  # 마지막 수정 시간
---

MCP (Model Context Protocol) : LLM (Large Language Model) 모델이 외부 어플리케이션과 연동할 수 있도록 해주는 스펙을 가진 protocol 입니다.
우리가 흔히 생각하는 AI 는 LLM 기반으로 LLM 은 학습을 통한 지식들에 대해 질문을 답변합니다. 
하지만 LLM 은 학습은 통한것에 국한되고 더 이상 넓은 범위를 가질 수 없어 Agent Framework들이 각각 방대한 정보를 가진 Tool 을 통해 다른 방대한 정보와 결합할 수 있게 됩니다.
이러한 Agent Framework 와 Tool 의 협업 방식에는 커뮤니케이션에 대한 부하가 심해 등장한 것이 MCP 라고 할 수 있습니다.

## Why MCP ?
 ![whatisMCP](/assets/images/what-is-mcp.png)
 왜 MCP 를 써야하냐? 라고 물어본다면 매우 간단하게 이 사진을 들고 설명할 수 있을것입니다.
 MCP 를 쓰기전엔 여러가지 타입의 충전기를 가지고 다니며 대비를 했다라면 요즘 대세인 C 타입의 충전기로 통합해서 하나의 타입의 충전기만 준비가 되어 있다면 모든것을 가져와 쓸 수 있는것이 바로 MCP 가 추구하는 방향이기 때문입니다.

  1. 회사 내 지원 서비스를 만들때에도 <u>사전 구축된 데이터베이스 기능 사용</u>이 가능
  2. 통합된 타입의 충전기를 사용하는것 처럼 <u>LLM 의 변경에도 유연스러운 변경</u>이 가능
 

## 그래서 개발자 입장에선?

 본인도 프론트엔드 개발자로서 개발자들이 API를 활용해서 코딩을 한다면 다양한 서비스가 가능한 것처럼 
 이 MCP 는 AI가 개발자 포지션이 되어 AI 들이 잘 개발할 수 있도록 즉, 서비스를 잘 이해하고 만들수 있도록 도와주는
 소통 방식인것입니다.
  
  ![ListTool](/assets/images/다운로드.png)
  MCP는 프로토콜이다. JSON-RPC/HTTP 를 이용하는 LLM 어플리케이션과 Tool 서버가 어떻게 통신하는지 이해를 하면된다.
  이 걸 잘하기 위해 만든 규약이 곧 MCP 이기 때문입니다.

## 주의점?

 MCP는 REST 처럼 JSON/HTTP 기반의 프로토콜을 정의한 스펙입니다다. 즉 통신 규약만 정의하고 실제 어플리케이션 구현에선는
 많은 부분이 생략되어 있습니다. 그래서 보안 인증, 에러 처리 같은 다양한 부분에서 내용이 생략되어 있는 경우가 있다보니 
 보안을 위한 추가 스펙 개발이 따라와야 한다는점도 꼭 알아야 하겠습니다.