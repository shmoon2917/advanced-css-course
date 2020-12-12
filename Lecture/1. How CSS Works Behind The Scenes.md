# How CSS Works Behind The Scenes

## 🙋‍♂️ TDIL

다음과 같은 과정을 거친다.

`Load HTML` :point_right: `Parse HTML` :point_right: `Document Object Model(DOM)`

HTML을 파싱할 때 CSS 로딩 및 파싱도 함께 한다.

`Parse HTML` :point_right: `Load CSS` :point_right: `Parse CSS`

CSS를 파싱할 때의 과정은 크게 두가지로 이루어지는데,

- **CSS 선언 충돌 해결 (cascade)**
- **최종 CSS 값 처리**

이 두 가지 과정을 거쳐 `CSS Object Model(CSSOM)` 을 만들어낸다.

이후

`DOM + CSSOM` :point_right: `Render Tree` :point_right: `Website rendering: the visual formatting model` :point_right: Final rendered website

이렇게 최종적으로 웹사이트에 렌더링된다. 앞으로의 강의에서는

**CSS 파싱이 이뤄지는 방법 두 가지와, 렌더트리를 이용하여 `Visual Formatting Model` 하는 과정을 배울 것이다.**
