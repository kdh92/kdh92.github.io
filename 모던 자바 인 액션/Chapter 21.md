<h1>결론 그리고 자바의 미래</h1>

<h2>자바 8의 기능 리뷰</h2>
자바 8이 얼마나 실용적이고 유용한 언어인지 다시 확인해보자.
논리적인 언어 설계 방식에 따라 전반적인 기능을 살펴볼 것이다.
또한 자바 8에 추가된 대부분의 새로운 기능은 자바에서 함수형 프로그래밍을 쉽게 적용할 수 있도록 도와준다는 사실을 강조할 것이다.

이러한 두 가지 추세 2가지
- 한 가지 추세는 멀티코어 프로세서의 파워를 충분히 활용해야 한다는 것이다. 무어의 법칙에 따라 실리콘 기술이 발전하면서 개별 CPU 코어의 속도가 빨라지고 있다.
즉, 코드를 병렬로 실행해야 더 빠르게 코드를 실행할 수 있다.
- 데이터 소스를 이용해서 주어진 조건과 일치하는 모든 데이터를 추출하고, 결과에 어떤 연산을 적용하는 등 선언형으로 데이터를 처리하는 방식, 즉 간결하게 데이터 컬렉션을 다루는 추세다.

<h3>동작 파라미터화(람다와 메서드 참조)</h3>
재사용할 수 있는 filter 같은 메서드를 구현하려면 filter 메서드의 인수가 필터링 조건을 받도록 만들어야 한다.
하지만 보통 상당히 복잡한 코드를 구현해야 하며 따라서 유지보수하는 것도 쉽지 않다.

메서드로 전달되는 값은 Function< T, R > , Predicate< T >, BiFunction< T, U, R > 등의 형식을 가지며 메서드를 수신한 코드에서는 applt, test 등의 메서드로 코드를 실행할 수 있다.

<h3>스트림</h3>
자라의 컬렉션 클래스, 반복자, for-each 구문은 오랫동안 사용된 기능이다.
기존의 컬렉션에 람다를 활용한 filter, map 등의 메서드를 추가해서 데이터베이스 질으 같은 기능을 제공하는 비교적 쉬운 방법을 선택할 수 있었다.

컬렉션에서 어떤 문제가 있으며 스트림과 비슷한 점과 다른 점이 무엇일까?
예를 들어 큰 컬렉션에 세 가지 연산을 적용한다고 가정하자.
우선 컬렉션의 필드를 더할 수 있는 객체를 매핑하고, 어떤 조건을 만족하는 합계를 필터링한 다음에, 결과를 정렬해야 한다.
따라서 컬렉션을 각각 세 번 탐색해야 한다.

스트림 API는 이들 연산을 파이프라인이라는 게으른 형식의 연산으로 구성한다.
그리고 한 번의 탐색으로 파이프라인의 모든 연산을 수행한다. 큰 데이터 집합일수록 스트림의 데이터 처리 방식이 효율적이며, 또한 메모리 캐시 등의 관점에서도 커다란 데이터 집합일수록
탐색 횟수를 최소화하는 것이 아주 중요하다.

또한 멀티코어 CPU를 활용해서 병렬로 요소를 처리하는 기능도 매우 중요한 점이다.
스트림의 parallel 메서드는 스트림을 병렬로 처리하도록 지정하는 역할을 한다.
상태 변화는 병렬성의 가장 큰 걸림돌이다.
함수형 개념은 map, filter 등의 연산을 활용하는 스트림의 병렬 처리의 핵심으로 자리 잡는다.

<h3>CompletableFuture 클래스</h3>
Future를 이용하면 여러 작업이 동시에 실행될 수 있도록 다른 스레드나 코어로 작업을 할당할 수 있다.
즉, 멀티코어를 잘 활용할 수 있다.

CompletableFuture는 CompletableFuture와 Future의 관계는 스트림과 컬렉션의 관계와 같다.

- 스트림에서는 파이프라인 연산을 구성할 수 있으므로 map, filter 등으로 동작 파라미터화를 제공한다. 따라서 반복자를 사용했을 때 생기는 불필요한 코드를 피할 수 있다.
- 공통 디자인 패턴을 함수형 프로그래밍으로 간결하게 표현할 수 있도록 thenCompose, thenCombine, allOf 등을 제공한다.
- 명령형에서 발생하는 불필요한 코드를 피할 수 있다.

<h3>Optional 클래스</h3>
T 형식의 값을 반환하거나 아니면 값이 없음을 의미하는 Optional.empty 라는 정적 메서드를 반환할 수 있는 Optional< T > 클래스를 제공한다.
Optional< T > 는 에러가 잘 발생할 수 있는 계산을 수행함년서 값이 없을 떄 에러를 발생시킬 수 있는 null 대신 정해진 데이터 형식을 제공할 수 있다.

스트림 클래스가 제공하는 것과 비슷한 동작으로 계산을 연결할 때 함수형으로 map, filter, ifPresent 등을 사용할 수 있다.
값을 내부적으로 검사하는 것과 외부적으로 검사하는 것은 사용자 코드에서 시스템 라이브러리가 내부 반복을 하느냐 아니면 외부 반복을 하느냐와 같은 의미를 갖는다.

<h3>디폴트 메서드</h3>
인터페이스에 새로운 기능을 추가했을 때 기존의 모든 인터페이스를 구현하는 클래스가 새로 추가된 기능을 구현하지 않을 수 있게 되었다는 점에서
디폴트 메서드는 라이브러리 설계자에서 아주 훌륭한 도구다.

<h3>풍부한 형식의 제네릭</h3>

<h4>구체화된 제네릭</h4>
제네릭은 기존 JVM과 호환성을 유지해야 했다.
결과적으로 ArrayList< String > 이나 ArrayList< Integer > 모두 런타임 표현이 같게 되었다.
이를 제네릭 다형성 삭제 모델이라고 한다.

이 떄문에 약간의 런타임 비용을 지불하게 되었으며 제네릭 형식의 파라미터로 객체만 사용할 수 있게 되었다.

ArrayList 객체를 힙에 할당할 수 있겠지만 ArrayList 컨테이너가 String 같은 객체값을 포함하는 것인지 42 같은 기본형 int값을 포함하는 것인지 알 수 없게 된다.

만일 ArrayList< int > 에서는 기본형 42를 얻을 수 있고, ArrayList< String > 에서는 'abc'라는 문자열 객체를 얻을 수 있다면 왜 ArrayList 컨테이너를 구별할 수 있는지 여부를 걱정해야 
할까? 불행하게도 가비지 컬렉션(GC) 때문이다.
런타임에 ArrayList의 콘텐츠 형식 정보를 확인할 수 없으므로 ArrayList의 13이라는 요소가 Integer 참조인지 아니면 int 기본값인지 분간할 수 없다.

이를 제네릭 다형성 구체화 모델 또는 구체화된 제네릭이라고 부른다.
구체화란 암묵적인 어떤 것을 명시적으로 바꾼다는 의미다.

구체화된 제네릭으로 기본형과 기본형에 대응되는 객체형을 완전하게 통합할 수 있다.

<h3>기본형 특화와 제네릭</h3>
자바의 모든 기본형에는 대응하는 객체형이 존재한다.(ex. int라는 기본형에 대응하는 객체형은 java.lang.Integer다.)
이를 언박스드 타입과 박스드 타입이라고 부른다. 
이와 같은 구분으로 런타임 효율성은 조금 증가했지만 형식은 오히려 혼란스러워한다.
예를 들어 자바 8에서는 왜 Function< Apple, Boolean > 이 아니라 Predicate< Apple > 로 구현해야 할까?
그것은 test 메서드로 Predicate < Apple > 객체형을 호출했을 때 기본형 boolean을 반환하기 때문이다.

반면 모든 제네릭과 마찬가지로 Function도 객체형으로만 파라미터화할 수 있다.
즉, Function< Apple, Boolean > 의 객체형은 기본형 boolean이 아나라 객체형 Boolean이다.

Predicate< Apple > 은 boolean 을 Boolean 으로 박싱할 필요가 없으므로 좀 더 효율적이다.
이런 이유로 자바 언어를 개념적으로 복잡하게 만드는 LongToIntFunction과 BooleanSupplier 같은 인터페이스가 등장했다.

비슷한 문제로 메서드 반환 형식이 아무 값도 없는 것임을 가리키는 void와 값으로 null을 갖는 객체형 Void가 있다.

<h3>값 형식</h3>
기본값과 객체형의 차이점을 살펴보면서 값 형식이 필요한 이유를 설명한다.
객체지향 프로그래밍에 객체가 필요한 것처럼 함수형 프로그래밍에 값 형식이 도움을 준다.







