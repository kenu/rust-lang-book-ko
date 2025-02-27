> **이 문서는 2판 번역본입니다.**
>
> 최신 2021 에디션 문서는 **[https://doc.rust-kr.org](https://doc.rust-kr.org)** 에서 확인하실 수 있습니다.

# 들어가기에 앞서

항상 그렇게 명확지는 않았지만, 러스트 프로그래밍 언어는 근본적으로 *권한 분산*에
관한 것입니다: 여러분이 어떠한 종류의 코드를 작성하는 중이던 간에, 러스트는
여러분에게 더 멀리 뻗어갈 권한을 주어, 다양한 분야에서 여러분이 전에 했던 것보다
자신감을 가지고 프로그래밍 할 수 있도록 해줍니다.

예를 들어, 메모리 관리, 데이터 표현, 그리고 동시성에 대한 저수준의 디테일을
다루는 “시스템 레벨”의 일을 해보세요. 전통적으로, 이 프로그래밍 영역은 신비로운
것으로 보이고, 이 영역의 악명높은 함정에 빠지지 않기 위해 필요한 수 년의 시간을
배우는데 헌신한 몇몇의 선택받은 자들만이 접근할 수 있는 것으로 여겨졌습니다.
그리고 이 분야를 연마해온 그들조차도 그들의 코드가 이용당하거나, 망가지거나,
붕괴되지 않도록 조심스럽게 작업을 합니다.

러스트는 여러분이 길을 잃지 않도록 하기 위해, 오래된 함정들을 제거하고
친근하면서도 세련된 도구 세트를 제공함으로써 이 장벽들을 부숩니다. 저수준의
제어에 “살짝만 발을 담글” 필요가 있는 프로그래머들은, 변덕스러운 툴체인의
미세한 지점들을 학습할 필요없이 러스트를 통해 그렇게 할 수 있습니다. 그
정도가 아니라, 이 언어는 속도와 메모리 사용 측면에서 효율적이면서도
안정적인 코드를 작성해 나갈 수 있도록 여러분들을 자연스럽게 안내하도록
설계되었습니다.

이미 저수준의 코드를 가지고 일하고 있는 프로그래머들은 러스트를 사용하여 그들의
야망을 더 키울 수 있습니다. 예를 들면, 러스트에서 소개하는 병렬성은 상대적으로
저위험성 연산입니다: 컴파일러가 여러분을 위해 고전적인 실수를 잡아줄 것입니다.
그리고 여러분은 뜻하지 않게 프로그램이 망가지거나 악용되지 않으리라는 자신감을 가지고
여러분의 코드에 대하여 더 공격적인 최적화에 몰두할 수 있습니다.

하지만 러스트는 저수준의 시스템 프로그래밍에 한정되지 않습니다. 이 언어는 CLI 앱,
웹 서버, 그리고 작성하기에 꽤나 즐거운 종류의 다른 코드들을 만들기에 충분할 정도로
표현력이 풍부하고 인간 공학적입니다 - 여러분은 이 책의 뒷 부분에서 이에 대한 단순한
예제들을 보게될 것입니다. 러스트로 일하는 것은 여러분이 어떤 영역에서 또다른 영역으로
옮기는 기술을 만들수 있게 해줍니다; 여러분은 웹 앱을 작성하는 것으로 러스트를 배울 수
있고, 그 다음 여러분의 라즈베리 파이를 대상으로 동일한 기술을 적용할 수 있습니다.

이 책은 러스트 사용자에게 권한을 주기 위해 러스트의 잠재력을 모두 담아내었습니다. 이 책은
러스트에 대한 여러분의 지식을 향상시키는 것 뿐만 아니라, 일반적인 프로그래머로서의 도약과
자신감을 향상시키는 것을 돕기 위한 의도로 친절하고 이해하기 쉬운 텍스트로 되어있습니다.
그러니 뛰어 들어서 배울 준비를 하세요-러스트 커뮤니티에 오신 것을 환영합니다!

- Nicholas Matsakis와 Aaron Turon