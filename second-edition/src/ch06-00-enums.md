> **이 문서는 2판 번역본입니다.**
>
> 최신 2021 에디션 문서는 **[https://doc.rust-kr.org](https://doc.rust-kr.org)** 에서 확인하실 수 있습니다.

# 열거형과 패턴 매칭

이번 장에서는 *열거(enumerations)* 에 대해 살펴볼 것입니다. *열거형(enums)* 이라고도 합니다.
열거형은 하나의 타입이 가질 수 있는 값들을 열거 함으로써 타입을 정의할 수 있도록 합니다.
우선, 하나의 열거형을 정의하고 사용해 봄으로써, 어떻게 열거형에 의미와 함께 데이터를 담을 수 있는지 보여줄 것입니다.
다음으로, `Option` 이라고 하는 특히 유용한 열거형을 자세히 볼 텐데, 이것은 어떤 값을 가질 수 도 있고, 갖지 않을 수 도 있습니다.
그다음으로, 열거형의 값에 따라 쉽게 다른 코드를 실행하기 위해 `match` 표현식에서 패턴 매칭을 사용하는 방법을 볼 것입니다.
마지막으로, 코드에서 열거형을 편하고 간결하게 다루기 위한 관용 표현인 `if let` 구문을 다룰 것입니다.

열거형은 다른 언어들에서도 볼 수 있는 특징이지만, 각 언어마다 열거형으로 할 수 있는 것들이 다릅니다.
러스트의 열거형은 F#, OCaml, Haskell 과 같은 함수형 언어의 *대수 데이터 타입*과 가장 비슷합니다.
