---
layout: post
title:  "react-native 08"
date: 2019-07-24
categories: react-native
---
# [플랫폼 특정 컴포넌트](https://github.com/yanghyeryung/book-study/tree/master/react-native/08/first-project)

## iOS 혹은 안드로이드만을 위한 컴포넌트
- 특정 플랫폼에서만 동작하는 컴포넌트
    - 특정 플랫폼에 맞는 접미사를 붙임.
    - IOS : '<TabBarIOS>'
    - Android : '<SwitchAndroid>'
- 특정 플랫폼에서만 사용가능한 컴포넌트 props
    - IOS : 'https://facebook.github.io/react-native/docs/view#accessibilityviewismodal
    - Android : 'https://facebook.github.io/react-native/docs/view#accessibilityliveregion

## 플랫폼별로 구현되어 있는 컴포넌트
### 파일 확장자로 플랫폼 선택하기
- 'Newsflash.android.js' / 'Newsflash.ios.js'와 같이 중간 확장자로 파일 구분
- import 시 리액트 네이티브가 각 플랫폼에 맞는 확장자를 선택하여 불러온다.

{% highlight ruby %}
 {% raw %}
import Newsflash from './Newsflash';
 {% endraw %}
{% endhighlight %}

### Platform 모듈 사용하기
- Platform 모듈을 사용하여 운영체제, 운영체제 버전을 확인 가능
- Platform API는 플랫폼에 따라 컴포넌트 코드는 완전히 분리하지 않고 작성시 유용하게 사용됨.

{% highlight ruby %}
 {% raw %}
import { Platform } from 'react-native';

console.log(Platform.OS + ':' + Platform.Version);
 {% endraw %}
{% endhighlight %}

{% highlight ruby %}
 {% raw %}
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
    color: (Platform.OS === 'ios') ? '#FF6666' : '#DD4444'
});
 {% endraw %}
{% endhighlight %}

## 언제 플랫폼 특정 컴포넌트를 사용?
- 해당 플랫폼의 인터렉션 패턴을 따르고 싶은 경우 사용 
    - https://developer.apple.com/design/human-interface-guidelines/ios/overview/themes
    - https://developer.android.com/design/index.html