---
layout: post
title:  "react-native 06"
date: 2019-07-19
categories: react-native
---
# [플랫폼API](https://github.com/yanghyeryung/book-study/tree/master/react-native/06/smartWeather)

## 지리적 위치 정보 이용
- 플랫폼에 상관없이 geolocation 기능을 기본적으로 제공

### 사용자 위치 얻어오기
{% highlight ruby %}
 {% raw %}
navigator.geolocation.getCurrentPosition(
    initialPosition => {
        this.props.onGetCoords(
            initialPosition.coords.latitude,
            initialPosition.coords.longitude
        );
    },
    error => {
        alert(error.message);
    },
    { enableHighAccuracy: true, timeout: 20000, maximumAge: 1000 }
);
 {% endraw %}
{% endhighlight %}

### 권한 다루기
- 모바일 플랫폼은 사용자가 위치 정보 접근시 허용되거나 거절당할 수 있기 때문에 모든 경우를 고려하여 코드 작성
- 앱 설정 파일에 위치 정보에 접근할 필요가 있다는 것을 명시해야 위치 정보 접근을 요청 할 수 있음.
    - iOS의 경우 Info.plist 파일에 NSLocationWhenInUsageDescription 항목을 추가 
    - 안드로이드의 경우 AndroidManifest.xml 파일에 다음 코드를 추가
        - `<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />"`
- 위와 같이 처리하면 위치 정보 요청 팝업이 뜨고, 허용여부 선택시 콜백 호출
    - 보통 허용하지 않으면 다시 위치 정보 요청 팝업이 뜨도록 처리 

### 위치 관련 테스트
- iOS : Debug -> Location -> Custom Location 메뉴를 선택하여 다른 좌표 입력 가능
- 안드로이드 : Extended controls 팝업 -> Location 에서 다른 좌표 입력 가능 

### 사용자 위치 지켜보기
- 사용자 위치가 변했을 때 변경된 정보를 받을 수 있음.
- 지속적으로 사용자 위치를 추적하거나 최신 위치 정보를 유지시 사용 
{% highlight ruby %}
 {% raw %}
 this.watchID = navigator.geolocation.watchPosition((position) => {
    this.setState({position: position});
 });
 
 navigator.geolocation.clearWatch(this.watchID);
 {% endraw %}
{% endhighlight %}

## 사진/카메라 접근하기 
- 네이티브 코드 작성이 필요 (react-native-init으로 생성)

### 카메라 모듈 다루기
- CameraRoll 인터페이스 제공
- getPhotos를 호출하여 사진에 대한 정보를 가져올 수 있음.
{% highlight ruby %}
 {% raw %}
import { CameraRoll } from 'react-native';
 {% endraw %}
{% endhighlight %}

{% highlight ruby %}
 {% raw %}
CameraRoll.getPhotos({ first: 1 }).then(data => {
    this.setState({
        photoSource: { uri: data.edges[0].node.image.uri }
    });
}, error => {
    console.warn(error);
});
 {% endraw %}
{% endhighlight %}

### getPhotoParams를 이용한 사진 요청
- first (Number)
가져오려는 사진 개수, 사진 앱의 역순으로 가져온다.
- after (String)
이전에 getPhotos호출시 콜백의 파라미터로 전달 받은 객체의 page_info.end_cursor를 넣으면 그 이후의 사진을 가져온다.
- groupTypes (String)
결과에 포함시킬 그룹의 종류에 해당하며 Album, All, Event 등을 지정할 수 있다.
- groupName (String)
결과에 포함시킬 특정 그룹의 이름에 해당하며 Recent Photos나 앨범 이름으로 지정할 수 있다.
- assetType (String)
에셋 종류에 해당하며 All, Photos, Video로 지정할 수 있다.
- mimeTypes (String[])
mimetype을 지정하여 해당하는 사진만 가져올 수 있다.

### 카메라롤 이미지 렌더링
{% highlight ruby %}
 {% raw %}
CameraRoll.getPhotos({ first: 1 }).then(data => {
    this.setState({
        photoSource: { uri: data.edges[0].node.image.uri }
    });
}, error => {
    console.warn(error);
});
 {% endraw %}
{% endhighlight %}

{% highlight ruby %}
 {% raw %}
<Image source={this.state.photoSource} />
 {% endraw %}
{% endhighlight %}

### 사진을 서버에 올리기
- 리액트 네이티브에서 XHR 모듈에 이미지 올리기 기능이 내장

{% highlight ruby %}
 {% raw %}
let xmr = new XMLHttpRequest();
xhr.open('POST', 'http://posttestsetver.com/post.php');
let formdata = new FormData();
formdata.append('image', {...this.state.photo, name: 'image.jpg'});
xhr.send(formdata);
 {% endraw %}
{% endhighlight %}

## AsyncStore를 이용한 영속적 데이터 저장
- AsyncStore 데이터를 저장, 접근 가능하다.
- 키는 @앱이름:키 형태로 하는 것이 일반적이다.

{% highlight ruby %}
 {% raw %}
const STORAGE_KEY = '@SmarterWeather:zip';

AsyncStore.setItem(STORAGE_KEY, zip)
          .then(() => {})
          .catch(() => {})
          .done();
          
AsyncStore.getItem(STORAGE_KEY);
          
 {% endraw %}
{% endhighlight %}