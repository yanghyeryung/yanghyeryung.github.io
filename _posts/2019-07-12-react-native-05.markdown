---
layout: post
title:  "react-native 05"
date: 2019-07-12
categories: react-native
---
# [스타일](https://github.com/yanghyeryung/book-study/tree/master/react-native/05/style)

## 스타일
- 리액트 네이티브는 자바스크립트 기반 스타일 객체를 사용

### 인라인 스타일
 - render 함수 호출시마다 스타일 객체가 생성되어 비효율적 
{% highlight ruby %}
 {% raw %}
<Text style={{fontStyle: 'italic'}}>italic</Text>
<Text style={{fontStyle: 'bold'}}>bold</Text>
 {% endraw %}
{% endhighlight %}
 
### 오브젝트 스타일
- 스타일 객체를 따로 분리

{% highlight ruby %}
const italic = {
    fontStyle: 'italic'
};
const bold = {
    fontStyle: 'bold'
 };
{% endhighlight %}
 
{% highlight ruby %}
 {% raw %}
<Text style={italic}>italic</Text>
<Text style={bold}>bold</Text>
 {% endraw %}
{% endhighlight %}
 
### StyleSheet.create
- 반복적인 객체 할당을 줄여주는 이점이 있음
- 한번 생성된 스타일은 변경 불가
{% highlight ruby %}
const styles = StyleSheet.create({
    italic: {
        fontStyle: 'italic'
    },
    bold: {
        fontStyle: 'bold'
    }
});
{% endhighlight %}

{% highlight ruby %}
 {% raw %}
<Text style={styles.italic}>italic</Text>
<Text style={styles.bold}>bold</Text>
 {% endraw %}
{% endhighlight %}
 
### 스타일 병합
- 스타일 객체로 구성된 배열로 지정 
    - 배열에서 오른쪽에 있는 객체의 속성이 우선순위가 더 높음
    - 부정값(false, null, undefined)이 있을 시 해당 속성은 무시
    
{% highlight ruby %}
 {% raw %}
<Text style={[styles.italic, styles.bold]}>italic, bold</Text>
<Text style={[styles.italic, this.state.white && {color: '#FFF'}]}>italic</Text>
 {% endraw %}
{% endhighlight %}


## 레이아웃
- 리액트 네이티브의 위치 지정 방법은 flexbox, 절대 위치 지정 방식이 있음.
    
### [Flexbox](https://facebook.github.io/react-native/docs/flexbox)
### 절대적 위치 지정
- position: absolute 로 지정
- 스마트폰의 상태바 바로 아래에 위치할 컨테이너 뷰를 만들고 싶을때 사용