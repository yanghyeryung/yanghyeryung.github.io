---
layout: post
title:  "react-native 03"
date: 2019-06-28
categories: react-native
---
# [나의 첫 어플리케이션 만들기](https://github.com/yanghyeryung/book-study/tree/master/react-native/03)

## 개발 환경설정
#### Create React Native App
- 자바스크립트만 사용하는 앱을 지원
- npm install -g create-react-native-app
- npm install -g expo-cli [리액트 네이티브 문서](https://facebook.github.io/react-native/docs/getting-started.html)
- create-react-native-app first-project 
- npm start
- Expo 앱을 사용하여 스마트폰에서 실행 가능 (컴퓨터와 스마트폰이 같은 네트워크 접속시)

#### React Native
- 네이티브 코드를 함께 사용하는 앱을 지원 
- npm install -g react-native-cli
- 플랫폼별 설치 항목 [리액트 네이티브 문서](https://facebook.github.io/react-native/docs/getting-started.html)
    - ios 개발환경 (Xcode)
    - 안드로이드 개발환경 (JDK, 안드로이드 SDK, 안드로이드 스튜디오)
- react-native init FirstProject
- react-native run-ios
- react-native run-android

## 샘플코드 
- 사용하려는 네이티브로 제공되는 모듈을 모두 명시적으로 import
{% highlight ruby %}
import {StyleSheet, Text, View, TextInput, ImageBackground} from 'react-native';
{% endhighlight %}

- 스타일은 스타일 객체를 통해 작성
    - flexbox를 이용하여 비율에 따른 레이아웃 지정 가능
    - flexDirection으로 배치를 지정 가능 (column: ↓ , row: →)
    - alignItems로 정렬 지정 가능

{% highlight ruby %}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        paddingTop: 30
    },
    backdrop: {
        flex: 1,
        flexDirection: 'column'
    },
    overlay: {
        paddingTop: 5,
        backgroundColor: '#000',
        opacity: 0.5,
        flexDirection: 'column',
        alignItems: 'center'
    },
    row: {
        flexDirection: 'row',
        flexWrap: 'nowrap',
        alignItems: 'flex-start',
        padding: 30
    },
});
{% endhighlight %}

- TextInput 컴포넌트로 사용자 입력 처리
{% highlight ruby %}
<TextInput
    style={[styles.zipCode, styles.mainText]}
    onSubmitEditing={e => this._handleTextChange(e)}>
</TextInput>
{% endhighlight %}

- Fetch API를 이용한 Ajax 요청 처리
{% highlight ruby %}
function fetchForecast(zip) {
    return fetch(zipUrl(zip))
        .then(response => response.json())
        .then(responseJSON => {
            return {
                main: responseJSON.weather[0].main,
                description: responseJSON.weather[0].description,
                temp: responseJSON.main.temp,
            };
        })
        .catch(error => {
            console.log(error);
        })
}
{% endhighlight %}

- ImageBackground 컴포넌트로 배경 이미지 처리 
{% highlight ruby %}
<ImageBackground
    source={require('./assets/flowers.png')}
    style={styles.backdrop}
>
...
</ImageBackground>
{% endhighlight %}