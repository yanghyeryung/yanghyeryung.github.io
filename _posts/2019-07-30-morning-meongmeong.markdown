---
layout: post
title:  "모닝멍멍"
date: 2019-07-30
toyproject: true
---
## 깃 레파지토리
[https://github.com/yanghyeryung/morning-meongmeong](https://github.com/yanghyeryung/morning-meongmeong)

## 설명
- 멍멍이 소리가 나는 알람 앱
- 멍멍이 수와 속도를 설정 가능하고 설정한 멍멍이를 전부 터치했을때 알람 종료
- 알람을 끄는 속도가 늦어지면 화난 멍멍이의 소리가 나옴

## 프로토타이핑

### 목록 조회 화면
- 목록은 오전/오후, 시간, 일의 정보로 구성
- 토글 버튼으로 알람 온오프

![목록 조회 화면]({{site.url}}/assets/img/morningmeongmeong/list.png){:width="300px"}

### 생성 수정 화면
- 타임피커, 일, 멍멍이 수, 멍멍이 속도로 구성

![생성 수정 화면]({{site.url}}/assets/img/morningmeongmeong/addedit.png){:width="300px"}

### 삭제 화면
- 목록에서 LongPress를 통해 삭제 버튼이 보여짐.
- 삭제 버튼 클릭시 삭제

![삭제 화면]({{site.url}}/assets/img/morningmeongmeong/delete.png){:width="300px"}

### 알람 화면
- 설정한 멍멍이 수와 멍멍이 속도의 값으로 멍멍이 얼굴이 나와서 움직임.
- 멍멍이를 모두 터치해야 알람이 꺼짐
- 멍멍이 소리는 3단계로 구성됨. (15초가 지나면 다음 단계의 소리가 나옴)

![알람 화면]({{site.url}}/assets/img/morningmeongmeong/alarm.png){:width="300px"}

## 사용기술
- React Native 

## 데모

<video autoplay="autoplay" loop="loop" width="300">
  <source src="{{site.url}}/assets/img/morningmeongmeong/result.webm" type="video/webm">
</video>
