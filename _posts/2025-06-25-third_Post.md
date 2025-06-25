---
title: "[대모산개발단 인턴쉽]DAY-1 실서비스 리팩토링 (랜더링 지연 부분 개선)"
excerpt: 
categories: 
  - 업무일지
tags:
  - 대모산개발단
  - 프론트성능개선
toc: true  # 목차 표시 여부
toc_sticky: true  # 목차를 스크롤에 따라 고정
last_modified_at: 2025-06-25T17:43:00+09:00  # 마지막 수정 시간
---

## YouTube 썸네일의 랜더링 문제

 < 기존 화면 >
 ![썸네일](/assets/images/lecture1.gif) 
 
 기존엔 4개의 강의 내역에서 강의가 오픈되는지 안되는지 체크하는 함수의 logic 이 너무 길고 오래 걸린다는 문제가 있었다.

 각 강의 컴포넌트가 useEffect 로 개별적으로 API 를 호출해 lock 상태를 확인하고 있었고 
 이 컴포넌트들을 API 레벨에서 한번에 처리하는 logic 으로 해결하였다.

 하위 컴포넌트에서의 빈도성 강한 API 호출의 문제와 useEffect 남발에 대해 다시 한번 생각을 해보아야 하는 문제점이라고 생각한다. 

 < 개선 화면 >
 ![썸네일2](/assets/images/lecture.gif)

 랜더링 시간이 8000ms 에서 2000mc 로 약 80% 성능 개선을 보였다. 
 
## 또 다른 배운 지식
 
 강의를 IsLocked 하는 과정에서 시간을 기준으로 설정하는데 
 프론트 단에서 new Date() 의 비교값으로 처리하면 보안상의 문제가 있다는걸 알았다.

 이럴땐 서버단의 const serverTime = await getServerTime(); 으로 서버단의 시간을 가져와 설정해야한다.

