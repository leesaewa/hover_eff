# Pure CSS Hover Effects
## [데모 페이지 확인하기](https://leesaewa.github.io/hover_eff/)

## 목표
+ 이미지 안과 밖의 글자 색상을 다르게 함.
+ 이미지를 hover했을 때, 글자도 같이 확대, 축소되어, 이미지만 움직이는 것 같은 착시를 줌.
+ 이미지를 hover했을 때, 이미지가 확대됨.
+ 이미지를 hover했을 때, img를 감싸고 있는 div를 축소함.


# 기술
### HTML
``` html
<div class="container">
  <a href="#0">
    <div class="inner-text">
      <span>save the polar bear.</span>
    </div>
        
    <div class="img-wrap">
      <img src="https://images.unsplash.com/photo-1589656966895-2f33e7653819?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80" alt="" srcset="">
    </div>
  </a>

  <div class="outer-text">
    <span>save the polar bear.</span>
  </div>
</div>
```
+ 이미지를 감싼 div(.img-wrap), 안쪽에 흰색으로 넣을 텍스트 div(.inner-text), 바깥에 검은색으로 넣을 텍스트 div(.outer-text)를 div(.container)로 감쌈.
+ (.img-wrap)과 (.inner-text)를 a태그로 감쌈.

### CSS
#### .img-wrap, .inner-text, .outer-text를 감싼 요소 꾸미기
```css
.container {position: absolute; top:15vh; left: 50%; transform: translateX(-50%); width: 80vw; text-align: center;}
.container a {display: block; position: relative; overflow: hidden; z-index: 1; margin:0 25vw; height:100%;}
```
+ .container를 센터 정렬 시킴. 굳이 'position: absolute'를 주지 않고 'position: relative'만 줘도 됨. (position~이후 전부 삭제해도 무방.)
+ 바깥 텍스트를 보여줘야 하기 때문에 'a'태그에 margin-left, margin-right값을 입력해줌. (width값을 줘도 무방.)

#### .img-wrap
``` css
.img-wrap {transition:transform 0.65s cubic-bezier(0.22, 0.9, 0.5, 1), opacity 0.65s cubic-bezier(0.5, 0, 0, 1); overflow: hidden; z-index: 1;}
.img-wrap img {width:100%; transition:transform 0.65s cubic-bezier(0.22, 0.9, 0.5, 1);}
```

+ hover했을 때, 부드러운 움직임 효과를 위해 (.img-wrap)과 (.img-wrap img)에 'transition cubic-bezier' 줌.
+ (.inner-text)를 hover했을 때, 함께 축소되는 효과를 나타내기 위하여 'overflow: hidden'을 입력하여 숨겨줌.
+ 'z-index:1'로 검은색 텍스트 위에 올라갈 수 있도록 순서를 정한다.

#### .outer-text, .inner-text 공통
```css
.inner-text, .outer-text {position: absolute; font-size:80px; text-transform: uppercase; transition:transform 0.65s cubic-bezier(0.22, 0.9, 0.5, 1), opacity 0.65s cubic-bezier(0.5, 0, 0, 1);}
```
+ 텍스트를 전체 대문자로 바꾸기 위해 'text-transform: uppercase' 입력
+ 텍스트를 (.img-wrap)위에 겹치게 하기 위해 'position:absolute' 입력
+ 


#### .inner-text
``` css
.inner-text {display: flex; align-items: center; justify-content: center; width:100%; height:100%; overflow: hidden; z-index: 1; color:#fff; white-space:nowrap;}
.inner-text span {transition:transform 0.65s cubic-bezier(0.22, 0.9, 0.5, 1)}
```

+ 텍스트를 중앙으로 정렬시키기 위해 'display: flex;'를 입력해 가로, 세로를 중앙 정렬 시킴. (align-items: center; justify-content: center;)
+ hover할 때, (.img-wrap)과 함께 축소되는 효과를 나타내기 위하여 'overflow: hidden'을 입력하여 숨겨줌.
+ 마찬가지로 텍스트를 hover(span)할 때, 함께 확대, 축소되는 착시를 보여주고 싶으므로, 부드러운 움직임 효과를 위해 'transition cubic-bezier' 줌.
+ 'z-index:1'로 검은색 텍스트 위에 올라갈 수 있도록 순서를 정한다.
+ 'white-space:nowrap'로 텍스트가 줄바꿈 되지 않도록 한다.
+ 'width: 100%', 'height:100%'를 입력해 영역을 정해준다.


#### .outer-text
```css
.outer-text {display: flex; align-items: center; justify-content: center; height: 100%; left:0; top:0; width:100%; transition: opacity 0.65s cubic-bezier(0.5, 0, 0, 1);}
```

+ (.inner-text)와 마찬가지로 텍스트를 중앙으로 정렬시키기 위해 'display: flex;'를 입력해 가로, 세로를 중앙 정렬 시킴. (align-items: center; justify-content: center;)
+ 'width: 100%', 'height:100%'를 입력해 영역을 정해준다.


#### hover effects
```css
/* hover */
.container a:hover .img-wrap, .container a:hover .inner-text {transform: scale(0.9075);}
.container a:hover .img-wrap > img {transform: scale(1.2);}
.container a:hover .inner-text > span {transform: scale(1.1);}
```

+ (.container a)를 hover할 때, (.inner-text)와 (.img-wrap)의 scale(크기)를 0.9075로 축소한다. (scale => 1보다 큰 수는 확대, 1보다 작은 수는 축소한다.)
+ (.container a)를 hover할 때, (.inner-text img)의 scale(크기)를 1.2 확대한다.
+ (.container a)를 hover할 때, (.inner-text span)의 scale(크기)를 1.1 확대한다.
  - (.inner-text img)와 같이 확대되어야 텍스트가 축소되지 않고, 본래 크기를 유지하기 때문.


# 전하고 싶은 말
해외 사이트를 보다가 꼭 만들어보고 싶은 효과였기에 분석해보고 직접 만들어보고 싶었다.

내가 원하는 효과를 나타내려면 아직도 부족하다.

또한, 이 방법말고도 수많은 방법이 있을 것이고, 내 코드가 최선이 아니다.

적어도 나처럼 도움이 필요했던 누군가에게 도움이 되었으면 좋겠다.
