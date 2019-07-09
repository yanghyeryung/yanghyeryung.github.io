---
layout: post
title:  "react-native 04"
date: 2019-06-28
categories: react-native
---
# 모바일 컴포넌트 

## 기본 컴포넌트

### `<Text>`

- 리액트 네이티브는 같은 스타일을 반복적으로 적용해야 할 경우 컴포넌트의 재사용을 권장

{% highlight ruby %}
class Em extends Component {
    render() {
        return(
            <Text style={styles.italic}>{this.props.children}</Text>
        );
    }
}
{% endhighlight %}

{% highlight ruby %}
<Text>
    The quick <Em>brown</Em>
</Text>
{% endhighlight %}

### `<Image>`

- 웹에 있는 이미지 소스를 사용해야 할 경우 이미지 사이즈를 따로 지정해야함.

{% highlight ruby %}
<Image source={{uri: 'https://facebook.github.io/react/img/logo_og.png'}} 
    style={{width: 400, height: 400}}/>
{% endhighlight %}

## 터치와 제스쳐 컴포넌트
## 리스트 컴포넌트
