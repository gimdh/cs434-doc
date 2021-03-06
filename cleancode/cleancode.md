# Clean Code Summary

**참고**

아래와 같은 Blockquote는 개인적인 생각입니다.
> 유익한 책입니다.


## Chapter 2 - 의미 있는 이름

반복문에 쓰이는 `i, j, k` 정도를 제외하면 반드시 길이가 길어지더라도 약어 없이 스스로를 표현하는 이름을 사용해야 한다. 또, 함수 이름은 동사, 클래스와 변수 이름은 명사로 짓고, 자연스럽게 발음 할 수 있는 이름을 선택해 자연어로 쉽게 코드를 풀 수 있도록 해야 생각하기도 쉽고, 의사 소통도 원활하다.

> 이러한 작명법이 코드를 이해하는데 큰 도움이 되지만, 한 줄이 너무 길어져서 불편하기도 하다. 80자 규칙은 100, 120자로 점점 늘어가지만 이것으로도 감당하기 힘든 경우도 꽤 있는것 같다. 어디까지 허용해야 할까?

단어를 선택할 때는 일정한 규칙을 두고, 가능하면 관련된 영역에서 사용하는 용어를 씀으로써 일관성을 유지하고 검색을 용이하게 한다. 만약 모호함이 발생할 경우, 문맥을 단어에 추가해 유일성을 보장해야 한다. 이때, 불필요하게 범위를 한정짓지 않아야 한다.


## Chapter 3 - 함수

함수는 단 하나의 기능에 집중해서 최대한 작게 만들어야 한다. 이때, 하나의 기능이란 함수 안에서 실행하는 코드가 모두 같은 추상화 수준을 가진다는 것으로, 작은 일과 큰 일을 섞지 않는 것으로 볼 수 있다. 또, 함수의 이름에 명시된 행위 외에 다른 부수적인 효과를 일으키지 않는 것도 포함된다.

또, 함수 안에서 코드는 분기 없이 하나의 일관된 흐름을 가질 수록 좋다. `switch case` 문 같은 경우 클래스 다형성 등으로 대체 하고, 조건문이나 반복문이 지나치게 중첩되면 내부를 다른 메소드로 추출하는 것을 고려해야 한다.

인수가 여러개일 경우 자연적인 순서가 있지 않은 이상 프로그래머가 임의로 인수의 순서를 결정하게 되므로 실수를 범할 가능성이 크다. 따라서 가능하면 인수를 줄일 수 있도록 하고, 지나치게 많아질 경우 다른 클래스에 필드로 이를 넣고 클래스 하나를 전달하는 것을 고려해야 한다.

끝으로 예외를 처리할 때 오류 코드를 사용하지 않음으로써 의존성을 없애고, `try/catch`문 역시 각각의 작업이므로 다른 메소드로 분리하는 것이 좋다.

> 함수 이름이 곧 동사이므로 이름에서 표현한 만큼만 동작이 일어나야 한다는 부분은 동의한다. 그러나 자연어는 순서대로 일어나는 일이 공간적으로 가깝기에 쉽게 이어서 읽을 수 있는 반면, 코드는 함수가 여러 곳에 산재되어 있으므로 이를 연결하는 과정이 수고스럽다.

> 극단적으로 단계를 나눠 작은 함수를 달성한 경우를 보면, 숲을 파악하기는 편하지만 오류가 발생했을 때 중요한 나무를 보는 것은 상당히 어려웠다. 본문에서 주장하는대로 최대한 작은 함수가 항상 옳은지 적어도 지금은 받아들이기 어렵다.


## Chapter 4 - 주석

주석은 웬만해선 아예 없는 것이 좋다. 코드가 간결하게 잘 작성되어있으면 굳이 코드와 분리되어있는 줄글로 다시 설명할 필요가 없기 때문이다.

이는, 앞선 장에서 작은 메소드 크기, 그리고 좋은 필드와 메소드 이름을 강조한 것과 일맥상통한다. 코드를 줄글에 비유하면 변수 이름은 명사, 메소드 이름은 동사에 대응한다. 따라서 나쁜 이름을 지으면 정보를 전달하기 힘들고, 메소드의 크기가 너무 커질 경우 동사 하나로 많은 일을 표현할 수 없게 된다.

쓸모없는 주석은 그 자체로 잘못되었으며, 필요한 주석은 곧 코드에 문제가 있어 표현력이 떨어진 것을 보완하기 위함이므로 나쁘다고 할 수 있다.

다만, 프로그래밍 언어의 구조가 한정되어 있는 만큼 코드만으로 표현하기 까다로운 정보도 있고, 이러한 경우에만 제한적으로 조심스럽게 주석을 사용해야한다.



## Chapter 7 - 오류 처리

좋은 코드를 작성하기 위해서는 프로그램의 논리 전개를 방해하지 않고 오류를 처리해야 한다. C 스타일의 오류 코드는 호출 코드와 오류 처리 코드가 붙어 있어 코드가 복잡해지므로 예외 처리를 사용하는 것이 좋다.

> 이는 반대로 예외 처리를 사용하면 필연적으로 예외 처리 코드와 오류를 발생시킨 코드가 분리된다는 뜻 아닌가?
> 정상 동작 흐름의 코드와 오류 처리 코드 둘 중 무엇이 떨어지는게 옳은가?
> 또, '작은 메소드'를 잘 지켰다면 무엇이든 상관없지 않은가?

> 예외 처리가 오류 코드 보다 나은 것은 당연히 동의하지만, 오류 처리 코드가 붙어 있을 수 밖에 없기 때문에 나쁘다는 주장은 생각이 더 필요할 것 같다.

확인된 예외(Checked Exception)은 중요한 경우에는 예외 처리를 강제한다는 장점이 있지만, `catch/throw` 의존성으로 인해 OCP를 위반하므로 대부분의 경우 지양하는 것이 좋다.

전반적으로 예외에도 앞선 장과 비슷한 원칙을 적용한다. 우선 예외 메시지는 설명이 충분해 필요한 정보를 모두 제공해야 한다. 또, 여러 예외는 필요하다면 API를 래퍼로 감싸는 조치를 취해서라도 일정한 수준을 아우르는 단계로 엮는 것이 좋다.

한편, 주석과 마찬가지로 꼭 필요한 곳에만 예외 처리를 사용해야 한다. 논리 전개와 같은 부분은 코드를 수정하여 해결하고, `null`의 사용을 지양하여 무의미한 예외가 많이 발생하지 않도록 해야 한다.



## Chapter 8 - 경계

프로젝트에서 아직 개발되지 않은 부분이 있거나, 외부 라이브러리를 사용할 경우 직접 작성하여 잘 알고 있는 코드와 그렇지 않은 코드 사이에 경계가 생기게 된다. 이 경계를 어댑터 패턴이나 래퍼를 사용해 사용자가 바라는 바를 명확히 하는 것이 코드 이해와 유지보수에 좋다.

> 인턴을 하며 기존에 사용하던 프로그램을 리팩토링 한 경험이 있는데, 외주를 맡겼다는 라이브러리가 구조도 엉망일 뿐더러 어떤 문서나 주석도 없이 프론트엔드와 엉켜 있어서 고생을 꽤나 했다. 특히, 이 경우는 프론트엔드도 같은 곳에서 외주를 진행해서 양쪽을 조금씩 맞춰가며 수정해서 구현을 쉽게 하려는 유혹에 쉽게 넘어간 것 같았다.

한편, 인터페이스를 설계할 때도 꼭 필요한 기능만을 제공해 원치 않는 동작을 초래하지 않도록 하는 것이 바람직하다.

> 라이브러리를 사용하다 보면 내가 알아서 조심해서 쓸 테니 더 다양한 인터페이스를 제공했으면 싶은 경우가 있다. 작성자와 사용자는 대립할 수 밖에 없지 않을까.

외부 라이브러리를 처음 사용할 때는 외부 라이브러리의 기초적인 부분에서부터 이해를 바탕으로 테스트를 작성하고, 동작 결과를 확인하며 배워나가는 것이 좋다. 바로 적용하는 것보다 속도가 빠를 뿐더러, 기초적인 테스트를 동시에 작성하기 때문에 만약 사용자가 이해한 것과 라이브러리 작성자가 의도한 것이 달라 나중에 문제가 생겼을 때에도 빨리 이를 짚어낼 수 있다.



## Chapter 9 - 단위 테스트
TDD의 법칙 세 가지는 다음과 같다.
* 실패하는 단위 테스트를 작성할 때까지 실행 코드를 작성하지 않는다
* 컴파일은 가능하되 실행이 실패하는 수준의 단위 테스트만 작성한다
* 현재 실패하는 단위 테스트만 통과할 정도의 실행 코드를 작성한다

실행 코드와 마찬가지로 테스트 코드도 깨끗한 상태를 유지해야 테스트 코드 자체의 유지 보수가 쉬워진다. 이때 테스트 코드가 잘 관리 되어야 단위 테스트를 믿고 실행 코드를 과감히 수정할 수 있으므로 결과적으로 테스트 코드의 품질은 실행 코드의 품질에도 영향을 미친다.

테스트 코드는 실행 코드 이상으로 가독성이 중요하므로 앞서 말한 함수 작성 요령을 적용하고, 테스트에 쓰이는 API를 따로 마련해 DSL을 사용하는 등의 노력으로 가독성을 확보해야 한다.

또, 함수와 마찬가지로 한 번에 하나의 일만 해야 한다. 이와 함께 자료의 작성-조작-확인의 순서로 테스트를 세 부분으로 나누고, 이 코드 블록을 given*-when*-then* 이름을 갖는 세 함수로 추출하면 깔끔한 테스트를 만들 수 있다.

깨끗한 테스트의 다섯 가지 규칙 F.I.R.S.T.는 다음과 같다.
1. Fast: 빨라야 테스트를 자주 실행한다.
2. Independent: 독립적이어야 오류와 테스트가 직접 연결되어 문제점을 찾기 쉽다.
3. Repeatable: 반복 가능해야 다양한 환경에서 일관적인 결과를 낸다.
4. Self-Validating: 실패/성공으로 명료하게 결과가 나뉘어야 문제를 명확히 보여준다.
5. Timely: 테스트를 실행 코드 바로 전에 작성해야 테스트 가능한 실행 코드를 쓰게 된다.

> 패키지에서 사용하는 데이터 구조를 만드는 함수 등은 다른 기능을 테스트할 때 필수적이기에 의존성을 피하기 힘들다. 다른 좋은 방법이 있을까?



## Chapter 10 - 클래스

자바에서는 다음과 같은 순서로 클래스를 작성하도록 장려한다.
1. 정적 공개 상수
2. 정적 비공개 변수
3. 비공개 인스턴스 변수
4. 공개 함수
5. 비공개 함수(호출되는 공개 함수 직후에)

변수와 함수는 가능한 캡슐화를 하되, 테스트에 꼭 필요하다면 Protected나 Public을 고려할 수 있다.

다른 것들과 마찬가지로 클래스도 단일 책임 원칙(SRP) 아래 단 한 가지에 대해서만 책임을 가지도록 작게 설계되어야 한다. 이는 반대로 클래스를 수정할 이유가 하나라는 것으로 이해할 수도 있다. 여러 개의 단일 책임 클래스에 책임을 분산시키고, 또 관련있는 것들은 하나의 작은 클래스로 모음으로써 큰 규모의 프로젝트를 더 잘 관리할 수 있다.

클래스 이름 역시 클래스가 하는 일을 충실하게 표현해야 하며, 이를 위해서 자연스래 작은 크기의 클래스를 작성하게 된다.

> Manager, Processor와 같은 추상적인 이름의 클래스를 즐겨 사용했는데, 명시적으로 적신호라고 밝히고 있어 양심의 가책이 느껴졌다.

응집도는 인스턴스 변수가 얼마나 많은 메소드에서 사용되는지를 말한다. 일부 메소드에서만 사용되는 인스턴스 변수가 많다는 것은 이를 새로운 클래스로 빼내기 좋다는 것을 뜻한다. 따라서 적당히 낮은 수준의 응집도가 유지되도록 클래스를 관리해야 한다. 혹은, 위의 규칙을 지켜 클래스를 작게 유지하면 자연스래 응집도가 낮아질 것이라고 생각할 수도 있다. 

작고 의존적이지 않은 클래스는 다른 클래스에 손 대지 않고도 수정이 가능하기 때문에 오류의 위험이 적고 훌륭한 구조를 유지하기 쉽다는 선순환의 장점이 있다.

끝으로 클래스는 항상 더 추상적인 클래스에 의존적이어야 한다. 이 원칙을 염두에 둠으로써 구현이 아닌 개념에 초점을 맞추어 클래스를 설계하고 사용할 수 있다.





