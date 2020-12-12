# Lecture

## 🙋‍♂️ TDIL

### How CSS Works Behind the Scenes: An Overview

Load HTML -> Parse HTML -> Document Object Model(DOM)

Parse HTML -> Load CSS -> Parse CSS

Parse CSS

- **Resolve conflicting CSS declarations(cascade)**
- **Process final CSS values**
  -> CSS Object Model(CSSOM)

DOM + CSSOM -> Render Tree -> Website rendering: the visual formatting model

-> Final rendered website

### How CSS is parsed, Part 1: The Cascade and Specificity

#### 용어 정리

```css
.my-class {
  color: blue;
  text-align: center;
  font-size: 20px;
}
```

- .my-class: `Selector`
- { }: `Declaration block`
- font-size: 20px;: `Declaration`
  - font-size: `Property`
  - 20px: `Declared value`

#### THE CASCADE (THE "C" IN CSS)

> 서로 다른 스타일시트들을 결합하고, 특정한 엘리먼트에 적용되는 규칙이 하나 이상일 때 서로 다른 규칙과 선언 간에 충돌을 해결하는 과정

CSS can come from different sources.

1. Author (developers write)
2. User
3. Browser (user agent)

Cascade는 이러한 다른 소스로부터 오는 CSS declaration 들을 결합한다. 그렇다면 어떻게 하나 이상의 규칙이 적용된 것들의 충돌을 해결할까? 바로 다음과 같은 과정을 거쳐 어떤 것이 우선적으로 오는지 결정한다.

`IMPORTANCE (WEIGHT)` -> `SPECIFICITY` -> `SOURCE ORDER`

자세히 살펴보자

##### IMPORTANCE (WEIGHT)

중요도를 매기는 과정이다.

1. User `!important` declarations
2. Author `!important` declarations
3. Author declarations
4. User declarations
5. Default browser declarations

그렇다면 선언들의 중요도가 모두 같은 경우에는?

##### SPECIFICITY

바로 특성을 이용한다.

1. Inline styles
2. IDs
3. Classes, pseudo-classes, attribute
4. Elements, pseudo-elements

예시를 들어보자.

```css
.button {
  font-size: 20px;
  color: white;
  background-color: blue;
}

nav#nav div.pull-right .button {
  background-color: green;
}

a {
  background-color: purple;
}

#nav a.button:hover {
  background-color: yellow;
}
```

특성은 네 가지 카테고리의 숫자들의 카운팅으로 계산할 수 있다.

첫 셀렉터를 통해 클래스를 가지므로 `(0, 0, 1, 0)` 카운팅을 할 수 있다. 이후 두 번째 셀렉터를 보면 IDs, Classes, Elements 를 가지므로 `(0, 1, 2, 2)` 가 된다. 세 번째 셀렉터를 통해 `(0, 0, 0, 1)` 카운팅, 이후 마지막 셀렉터를 통해 `(0, 1, 2, 1)`이 된다.

다음 각 카테고리 별로 숫자를 비교하는데, `Inline`의 경우는 차이가 없으니 패스, IDs의 경우 첫 번째와 세 번째 카운팅은 0이니 우선순위에서 제거, Classes(with pseudo-classes, attribute) 의 경우 같으니 패스, 마지막으로 Elements는 2번째 카운팅의 숫자가 크므로 결국 **두 번째 셀렉터가 우선순위를 차지한다**

이렇게 우선순위를 가져가는 declarations 을 바로 `cascaded value`라고 부른다.

그런데 이렇게 specificity 비교 과정을 거친 이후에도 같다면? 바로 다음 과정을 거친다.

##### SOURCE ORDER

코드의 마지막으로 적힌 선언이 모든 선언들을 오버라이딩하고 적용된다.
