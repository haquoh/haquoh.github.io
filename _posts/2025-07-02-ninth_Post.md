---
title: "[대모산개발단 인턴쉽]DAY-6 funnel 페이지 리팩토링"
excerpt: 
categories: 
  - 업무일지
tags:
  - 대모산개발단
  - 유지보수 
toc: true  # 목차 표시 여부
toc_sticky: true  # 목차를 스크롤에 따라 고정
last_modified_at: 2025-07-02T17:43:00+09:00  # 마지막 수정 시간
---

## Demo-funnel 

  로직을 분리 하는 과정을 공부해 보았다. 
  
  비즈니스 로직과 UI 로직을 분리하는거에 대해 프로젝트 설계 단계에서 생각한게 아닌 

  Refactoring 단계에서 생각을 하려니 머리가 너무 아프고 어떤 부분부터 손을 봐야할지 막막했다.

  일단 components 안에 파일들을 하나하나 살피고 

  useState, useEffect 가 남발된 부분을 중점적으로 고쳐보기로 했다.

  일정 메세지값을 반환하는 처리에 관해서는 constants 파일에 상수로 분리를 시켰다.

  그리고 useMutation 이 핵심 비즈니스 로직으로 들어가있어서 보고 있는데 

  ```
  const { mutate: handleSubmit } = useMutation({
  mutationFn: async (submissionId: number) => {
    const imageFile = editedImageUrl
      ? await fetch(editedImageUrl)
          .then((r) => r.blob())
          .then((blob) => new File([blob], "image.jpg", { type: "image/jpeg" }))
      : undefined;
    
    return updateSubmission({
      submissionId,
      link: editedUrl,
      text: editedComment,
      imageFile: imageFile || undefined,
    });
  },
```
  이런 이상한 로직의 코드가 들어가 있었다. 

  기존 이미지 URL 을 다시 fetch 해서 file 로 변환하는 비효율적인 방식으로 되어있길래

```
  const handleImageChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  const file = e.target.files?.[0];
  if (file) {
    // 파일 크기 검증
    if (!validateFileSize(file)) {
      toast.error("이미지 파일 크기는 3MB를 초과할 수 없습니다.");
      e.target.value = "";
      return;
    }
    
    setImageFile(file);
    // Object URL 생성 (메모리 효율적)
    const imageUrl = URL.createObjectURL(file);
    setImagePreview(imageUrl);
    setEditedImageUrl(imageUrl);
  }
};
  
```
  그냥 파일을 URL 형식으로 저장할 수 있게 만들어 주었다. 

  이 외에도 커스텀 훅을 다 분리해주는 등의 작업을 완료하였다.
