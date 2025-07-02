---
title: "[대모산개발단 인턴쉽]DAY-3 실서비스 리팩토링 (랜더링 지연 부분 개선)"
excerpt: 
categories: 
  - 업무일지
tags:
  - 대모산개발단
  - 프론트성능개선
toc: true  # 목차 표시 여부
toc_sticky: true  # 목차를 스크롤에 따라 고정
last_modified_at: 2025-06-27T17:43:00+09:00  # 마지막 수정 시간
---

## 단일 책임 원칙 

 기존 코드들을 살펴 보았을 때 
 가장 눈에 띈 큰 문제점은 하나의 컴포넌트안에 서로 다른 기능을 하는 로직들이 많다는 거 였다.

 ```
  //  UI 로직  
 function DailyPlay() {
  const [isPlaying, setIsPlaying] = useState(false);
 }
 
 // 비즈니스 로직
 const findLecture = () => {
  const openLectures = lectures.filter(); 
 }

 이렇게 둘 다의 로직을 한 컴포넌트가 담당하고있던것 
 이걸 utils와 기존 컴포넌트로 분리 
 ```

 이렇게 API 레벨에서 한번에 로직을 들고 와서 쓸 수 있도록 다 바꿔야 할 것 같다.
 
## 또 다른 배운 지식
 


