
# 경고와 오류

Sass 개발자들에 의해 간과되는 기능이 하나 있다면, 그것은 동적으로 경고와 오류를 출력하는 기능입니다. 사실, Sass에는 표준 출력 시스템(CLI, compiling app...)에 내용을 표시하는 세 가지의 지시어가 있습니다:

* `@debug`;
* `@warn`;
* `@error`.

`@debug`는 분명히 SassScript 디버그를 위해 의도된 것이므로 제쳐두겠습니다. 그건 지금 우리에게 중요한 게 아니니까요. 그럼 이제 하나는 컴파일러를 멈춰세우는 반면 다른 하나는 그렇지 않다는 점만 빼고 똑 닮은 `@warn`과 `@error`가 남았습니다. 무엇이 무엇인지 한 번 맞춰보세요.

Sass 프로젝트에는 경고와 오류의 여지가 많이 있습니다. 기본적으로 특정 유형의 매개변수를 기대하는 믹스인이나 함수는 뭔가가 잘못되었을 때 오류를 던지거나, 혹은 추정 시에는 경고를 표시합니다.

###### 참고

* [An Introduction To Error Handling](http://webdesign.tutsplus.com/tutorials/an-introduction-to-error-handling-in-sass--cms-19996)
* [Building a Logger Mixin](http://webdesign.tutsplus.com/tutorials/building-a-logger-mixin-in-sass--cms-22070)
* [SassyLogger](https://github.com/HugoGiraudel/SassyLogger)

## 경고

[Sass-MQ](https://github.com/sass-mq/sass-mq)의 `px` 값을 `em`으로 변환하려 시도하는 이 함수를 예로 들겠습니다:

{% include snippets/errors/01/index.html %}

만약 값에 단위가 없으면 이 함수는 그 값이 픽셀로 표현되어야 하는 것으로 추정합니다. 이 시점에서, 추정은 위험할 수 있으며 따라서 사용자는 소프트웨어가 예기치 않은 것으로 간주될 수 있는 행동을 했다는 경고를 받아야 합니다.

## 오류

오류는 경고와 달리 컴파일러의 진행을 막습니다. 기본적으로 오류는 컴파일을 멈추고 스택 트레이스와 출력 스트림에 메시지를 표시하는데, 이는 디버깅에 유용합니다. 이 때문에, 오류는 프로그램이 계속 실행될 방법이 없을 때 던져져야 합니다. 가능하면 이 문제를 피해 가려 노력하고 대신 경고를 표시하세요.

가령 특정 맵의 값에 접근하는 getter 함수를 만든다고 합시다. 만약 요청된 키가 맵에 존재하지 않으면 오류를 던질 수 있습니다.

{% include snippets/errors/02/index.html %}
