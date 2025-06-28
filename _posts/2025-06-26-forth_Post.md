---
title: "[대모산개발단 인턴쉽]DAY-2 실 서비스 리팩토링 (랜더링 지연 부분 개선)"
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

## API 레벨에서의 데이터 준비

지금 수정하고 있는 페이지의 Logic 을 원론적으로 생각해볼 필요가 있었다.
강의는 하루에 하나 그리고 관리자가 설정한 날의 범위 ( 예를 들어 3일 )에 맞춰 
날마다 하나씩 들어있는 페이지였다. 

사용자가 보여지는 화면에선 이미 강의가 다 올라와있지만 Lock 이 걸려있고 그 강의에 맞는 날이 되면 Lock 이 풀려
사용자가 볼 수 있는 상태인 것이다. 

이걸 프론트단에서 lectures 라는 api 를 들고와서 lock 인지 체크를 한다음 서버시간 api 들고와서 시간을 또 체크한다면 
당연히 오래걸릴 수 밖에 없는 노릇이었다.

이걸 api 단에서 처리하면 어떨까 라는 생각으로 isLocked 를 서버시간으로 계산을 미리 한다음 
페이지 하위단에선 함수 하나로 처리를 하였다. 

``` 
useEffect(() => {
  const updateMainLecture = async () => {
    if (lectures[selectedVideoIdx]) {
      const isLocked = !(await isLectureOpen(lectures[selectedVideoIdx].open_at));
      setMainLecture({
        // ... 복잡한 로직
      });
    }
  };
});

const thumbnailUrl = useMemo(() => 
  getVideoThumbnailUrl(dailyLecture.upload_type, dailyLecture.url),
  [dailyLecture.upload_type, dailyLecture.url]
);

{new Date(dailyLecture.open_at).toLocaleDateString("ko-KR", {
  month: "long",
  day: "numeric",
})}
```
이런 중복된 로직의 코드가 페이지별로 작성되어 있어서 

```
const lectures = data?.map((item) => ({
  // ... 기본 데이터
  isLocked: serverDate < new Date(item.open_at),
  openDateFormatted: formatDate(item.open_at),
  thumbnailUrl: getThumbnail(item),
}));

// 컴포넌트는 그냥 사용만
<span>{lecture.openDateFormatted}</span>
<Image src={lecture.thumbnailUrl} />
{lecture.isLocked && <Lock />}
```
api 레벨에서 한번만 계산 하도록 하였다. 


## YouTube 썸네일의 화질개선

 < 기존 화면 >
 ![썸네일](/assets/images/lawthumb.png) 
 
 유툽 썸네일 화질 개선을 진행했다.

 아주 간단한 방법과 아주 까다로운 방법이 존재했다.

 < 개선 화면 >
 ![썸네일2](/assets/images/highthumb.png)

 
 
## 또 다른 배운 지식
 

api 레벨에서 한번에 계산하기 위해서 코드를 짜다보니 
정말로 api 정보만 넘겨주는 ts 파일에서 함수를 넣어버렸고

같이 일하는 팀원분이 api 정보를 넘겨주는 ts 파일은 api 정보에만 집중하고 
기능을 하는 부분은 기능을 하는 파일에 집중을 하고싶다고 하셔서 

생각해보니 애초에 설계한 아키텍쳐가 완전히 잘못되어져 짜잘짜잘한 수정은 
길게보면 의미가없다는것을 깨달았다. 

그래서 일단 아키텍쳐에 대해 생각을 하며 폴더 구조를 좀 더 개선해봐야겠다고 생각했다.
