---
layout: post
title:  "react-native 04"
date: 2019-07-09
categories: react-native
---
# [모바일 컴포넌트](https://github.com/yanghyeryung/book-study/tree/master/react-native/04) 

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

- 웹에 있는 이미지 소스를 사용해야 할 경우 이미지 사이즈를 따로 지정

{% highlight ruby %}
 {% raw %}
<Image source={{uri: 'https://facebook.github.io/react/img/logo_og.png'}}
       style={{width: 400, height: 400}}/>
 {% endraw %}
{% endhighlight %}

## 터치와 제스쳐 컴포넌트

### `<TouchableHighlight>`

- 뷰가 터치될때 오버레이를 추가하여 사용자에게 시각적 피드백 제공 
- onPressIn, onPressOut, onLongPress 콜백 제공 

{% highlight ruby %}
render() {
    return (
        <View style={styles.container}>
            <TouchableHighlight
                onPressIn={this._onPressIn}
                onPressOut={this._onPressOut}
                style={styles.touchable}>
                <View style={styles.button}>
                    <Text style={styles.welcome}>
                        {this.state.pressing ? 'EEK!' : 'PUSH ME'}
                    </Text>
                </View>
            </TouchableHighlight>
        </View>
    );
}
{% endhighlight %}

### `PanResponder`

- 컴포넌트가 아닌 클래스
- 현재 제스처의 속도, 누적 이동거리 등의 원시 위치 데이터에 접근 가능
- PanResponder 객체 생성시 콜백함수를 지정
    - onStartShouldSetPanResponder: 터치 이벤트에 반응할지 결정
    - onMoveShouldSetPanResponder: 터치 이벤트에 반응할지 결정
    - onPanResponderGrant: 터치 이벤트 발생시 실행
    - onPanResponderMove: 터치 이벤트 진행중 실행
    - onPanResponderRelease: 터치 이벤트 끝날때 실행 
    - onPanResponderTerminate: 터치 이벤트 끝날때 실행 

{% highlight ruby %}
this._panResponder = PanResponder.create({
    onStartShouldSetPanResponder: this._handleStartShouldSetPanResponder,
    onMoveShouldSetPanResponder: this._handleMoveShouldSetPanResponder,
    onPanResponderGrant: this._handlePanResponderGrant,
    onPanResponderMove: this._handlePanResponderMove,
    onPanResponderRelease: this._handlePanResponderEnd,
    onPanResponderTerminate: this._handlePanResponderEnd
});
{% endhighlight %}

- PanResponder 객체를 컴포넌트 전개 연산자(...)로 결합하여 렌더

{% highlight ruby %}
render() {
    return (
        <View style={styles.container}>
            <View
                ref={circle => {
                    this.circle = circle;
                }}
                style={styles.circle}
                {...this._panResponder.panHandlers}>
            </View>
        </View>
    );
}
{% endhighlight %}

- 애니메이션을 다룰때는 컴포넌트의 setNativeProps를 직접 호출하여 변화를 줄 수 있음

{% highlight ruby %}
_handlePanResponderMove = (event, gestureState) => {
    this._circleStyles.style.left = this._previousLeft + gestureState.dx;
    this._circleStyles.style.top = this._previousTop + gestureState.dy;
    this._updatePosition();
};
    
_updatePosition = () => {
    this.circle && this.circle.setNativeProps(this._circleStyles);
};
{% endhighlight %}

## 리스트 컴포넌트

### `<FlatList>`

- props로 data와 renderItem을 반드시 지정
    - data: 렌더링할 데이터 []
    - renderItem: 데이터를 바탕으로 렌더링할 컴포넌트를 리턴하는 함수

{% highlight ruby %}
render() {
    return <FlatList data={this.state.data} 
                     renderItem={this._renderItem} />
}
{% endhighlight %}

- data 배열의 각 항목에는 반드시 key 속성 지정

{% highlight ruby %}
this.state = {
    data: [
        {
            key: 'GATHERING PREY',
            rank: 1,
            title: 'GATHERING PREY',
            author: 'John Sandford',
            book_image: 'http://du.ec2.nytimes.com.s3.amazonaws.com/prd/books/9780399168796.jpg'
        },
        {
            key: 'MEMORY MAN',
            rank: 2,
            title: 'MEMORY MAN',
            author: 'David Baldacci',
            book_image: 'http://du.ec2.nytimes.com.s3.amazonaws.com/prd/books/9781455586387.jpg'
        },
    ]
};
{% endhighlight %}

- renderItem의 인자로 넘어오는 객체의 item 속성으로 데이터에 접근 가능

{% highlight ruby %}
_renderItem = ({ item }) => {
    return (
        <BookItem
            coverURL={item.book_image}
            title={item.key}
            author={item.author} />
    );
};
{% endhighlight %}

### `<SectionList>`

- 데이터를 섹션으로 구분해서 보여줘야 하는 경우 사용
- props로 sections와 renderItem, renderSectionHeader를 반드시 지정
    - sections: 섹션을 구분하여 렌더링할 데이터 []
    - renderItem: 데이터를 바탕으로 렌더링할 컴포넌트를 리턴하는 함수
    - renderSectionHeader: 섹션 헤더를 렌더링할 컴포넌트를 리턴하는 함수
    
{% highlight ruby %}
render() {
    return <SectionList sections={this.state.section} 
                        renderItem={this._renderItem} 
                        renderSectionHeader={this._renderHeader} />
}
{% endhighlight %}

- section 배열의 각 항목에는 반드시 title, data 속성 지정 
    - data 배열의 각 항목에는 반드시 key 속성 지정

{% highlight ruby %}
this.state = {
    section: [
        {
            title: 'GATHERING PREY5',
            data: this._addKeysToBooks(mockBooks)
        },
        {
            title: 'MEMORY MAN6',
            data: this._addKeysToBooks(mockBooks2)
        }
    ]
};
{% endhighlight %}

- renderSectionHeader의 인자로 넘어오는 객체의 section 속성으로 title에 접근 가능
{% highlight ruby %}
 _renderHeader = ({ section }) => {
    return (
        <Text style={styles.headingText}>
            {section.title}
        </Text>
    );
};
{% endhighlight %}