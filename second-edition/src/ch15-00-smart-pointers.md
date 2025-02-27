> **이 문서는 2판 번역본입니다.**
>
> 최신 2021 에디션 문서는 **[https://doc.rust-kr.org](https://doc.rust-kr.org)** 에서 확인하실 수 있습니다.

# 스마트 포인터

*포인터 (pointer)* 는 메모리의 주소 값을 담고 있는 변수에 대한 일반적인 개념입니다.
이 주소 값은 어떤 다른 데이터를 참조합니다. 혹은 바꿔 말하면, “가리킵니다”. 러스트에서
가장 흔한 종류의 포인터는 참조자인데, 이는 여러분들이 3장에서 배웠던 것입니다. 참조자는
`&` 심볼에 의해 나타내지고 이들이 가리키고 있는 값을 빌립니다. 이들은 값을 참조하는 것
외에 다른 어떤 특별한 능력도 없습니다. 또한, 이들은 어떠한 오버헤드도 발생하지 않으며
우리가 가장 자주 사용하는 포인터의 한 종류입니다.

한편, *스마트 포인터 (smart pointer)* 는 포인터처럼 작동하지만 추가적인 메타데이터와
능력들도 가지고 있는 데이터 구조입니다. 스마트 포인터의 개념은 러스트에 고유한 것이
아닙니다: 스마트 포인터는 C++로부터 유래되었고 또한 다른 언어들에도 존재합니다.
러스트에서는, 표준 라이브러리에 정의된 다양한 종류의 스마트 포인터들이 참조자들에 의해
제공되는 것을 넘어서는 추가 기능을 제공합니다. 우리가 이번 장에서 탐구할 한 가지 예로는
*참조 카운팅 (reference counting)* 스마트 포인터 타입이 있습니다. 이 포인터는
소유자의 수를 계속 추적하고, 더 이상 소유자가 없으면 데이터를 정리하는 방식으로, 여러분들이
어떤 데이터에 대한 여러 소유자들을 만들 수 있게 해 줍니다.

소유권과 빌림의 개념을 가지고 있는 러스트에서, 참조자와 스마트 포인터 간의 추가적인
차이점은 참조자가 데이터를 오직 빌리기만 하는 포인터라는 점입니다; 반면, 많은 경우에서
스마트 포인터는 그들이 가리키고 있는 데이터를 *소유*합니다.

우리는 이미 이 책에서 8장의 `String`과 `Vec<T>`와 같은 몇 가지 스마트 포인터들을
마주쳤습니다. 비록 그때는 이것들을 스마트 포인터라고 부르지 않았지만요. 이 두 타입
모두 스마트 포인터로 치는데 그 이유는 이들이 얼마간의 메모리를 소유하고 여러분이 이를
다루도록 허용하기 때문입니다. 그들은 또한 (그들의 용량 등의) 메타데이터와 (`String`이
언제나 유효한 UTF-8일 것임을 보장하는 것 등의) 추가 능력 혹은 보장을 갖고 있습니다.

스마트 포인터는 보통 구조체를 이용하여 구현되어 있습니다. 스마트 포인터가 일반적인
구조체와 구분되는 특성은 바로 스마트 포인터가 `Deref`와 `Drop` 트레잇을 구현한다는
것입니다. `Deref` 트레잇은 스마트 포인터 구조체의 인스턴스가 참조자처럼 동작하도록
하여 참조자나 스마트 포인터 둘 중 하나와 함께 작동하는 코드를 작성하게 해 줍니다.
`Drop` 트레잇은 스마트 포인터의 인스턴스가 스코프 밖으로 벗어났을 때 실행되는 코드를
커스터마이징 가능하도록 해 줍니다. 이번 장에서는 이 두 개의 트레잇 모두를 다루고 이들이
어째서 스마트 포인터에게 중요한지를 보여줄 것입니다.

스마트 포인터 패턴이 러스트에서 자주 사용되는 일반적인 디자인 패턴으로 주어지므로,
이번 장에서는 존재하는 스마트 포인터를 모두 다루지는 않을 것입니다. 많은 라이브러리들이
그들 자신만의 스마트 포인터를 가지고 있고, 심지어 여러분도 여러분 자신만의 것을 작성할
수 있습니다. 우리는 표준 라이브러리 내의 가장 흔한 스마트 포인터들을 다룰 것입니다:

* 값을 힙에 할당하기 위한 `Box<T>`
* 복수개의 소유권을 가능하게 하는 참조 카운팅 타입인 `Rc<T>`
* 빌림 규칙을 컴파일 타임 대신 런타임에 강제하는 타입인, `RefCell<T>`를 통해
  접근 가능한 `Ref<T>`와 `RefMut<T>`

추가로, 우리는 불변 타입이 내부 값을 변경하기 위하여 API를 노출하는 *내부 가변성
(interior mutability)* 패턴에 대해 다룰 것입니다. 또한 *참조 순환
(reference cycles)*이 어떤 식으로 메모리가 세어나가게 할 수 있으며,
이를 어떻게 방지하는지에 대해서도 논의해 보겠습니다.

함께 뛰어들어 볼까요!
