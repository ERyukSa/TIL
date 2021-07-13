# Project1 - BMI 계산기

<br>

## 정리

<br>

### ● 데이터 타입
코틀린에서는 모든 데이터가 객체로 분류된다. 따라서 각 타입에 정의된 함수와 프로퍼티를 사용할 수 있다. 코틀린의 기본 데이터 타입으로는 크게 numbers, booleans, characters, strings, arrays가 있다.

<br>

1. **Any**: 코틀린의 데이터 타입 최상위 클래스로, 모든 데이터 타입을 의미한다.
   
2. **Numbers** 
   1. **정수**: Byte, Short, Int, Long이 있다. Long에는 끝에 L을 붙인다. ex) 213L
   
        | Type    | Size(bits) | Value range
        | :-----: | :------:   | :------
        |  Byte   |    8       | -128 ~ 127
        |  Short  |    16      | -32768 ~ 32767
        |  Int    |    32      | -2^31 ~ (2^31 - 1)
        |  Long   |    64      | -2^63 ~ (2^63 - 1)

   2. **실수**: Float과 Double이 있으며, Double이 기본형이다. Float형을 사용할 떄는 뒤에 f나 F를 붙인다. ex) 123.4f
        
        | Type     | Size(bits) | Significant bits | Exponent bits | Decimal digits
        | :-----:  | :------:   |   :------:       | :---:         | :---:
        |  Float   |    32      | 24               | 8             | 6-7
        |  Double  |    64      | 53               | 11            | 15-16

3. **Booleans**: true와 false를 값으로 갖으며, Booleans? 타입은 null도 될 수 있다. 논리 연산자로는 ||(or), &&(and), !(not)이 있다.
   
4. **Char**: 문자를 의미하며, char형 값은 작은따옴표로 나타낸다. ex) val aChar: Char = **'a'**

5. **Strings**: 문자열이며 쌍따옴표로 나타낸다. 쌍따옴표 3개(""")로 나타내는 raw strings도 있는데, 차이점은 "\n"과 같은 escape code도 문자 그대로 보여준다. **ex) println("""\n"""), 출력: \n**

<br>

### ● 반복문

1. **for문**
   
   - 1 **..** 5 (5포함)
   - 1 **until** 5 (5 미포함)
   - **downTo** , **step**

        ```kotlin
        for(i in 6 downTo 0 step 2){
            println(i)
        } // 6 4 2 0
        ```
   - 이터레이터 반복
    
        ```kotlin
        val numberList = listOf(100, 200, 300)
        for (number in numberList){
            println(number)
        } // 100, 200, 300

2. **while문**: while / do while 
   
    ```kotlin
    var y = 0
    do {
        print(y)
        y--
    } while(y > 0)
    // 0

<br>

### ● 조건문 
if와 when이 있으며, 대입문에서 조건문을 사용할 수 있다.

- **if**
    
    **예제)**
    
    ```kotlin
    var max: Int
    if (a > b) {
        max = a
    } else{
        max = b
    }

    // 조건문을 사용하는 대입문
    val max = if (a > b){
        a
    }else{
        b
    }
    ```

- **when**
  
    **예제1)**

    ```kotlin
    when(x) {
        1 -> print("x == 1")
        2 -> print("x == 2")
        else -> {
            print("x is neither 1 nor 2")
        }
    }
    ```

    **예제2**

    ```kotlin
    when(x){
        0, 1 -> print("x == 0 or x == 1")
        else -> print("otherwise")
    }

    **예제3**

    ```kotlin
    when(x){
        in 1..10 -> print("x는 1부터 10까지")
        !in 1..20 -> print("x는 10부터 20 범위 안에 없음")
        else -> print("otherwise")
    }
    ```

    **예제4**

    ```kotlin
    when(x){
        is Int -> print("x는 정수형")
        else -> print("x는 정수가 아님")
    }
    ```

<br>

### ● Nullable vs Null-safe
코틀린의 가장 큰 특징 중 하나는 **Null-safe 형식을 제공하기 때문에 null 참조의 위험에서 자유로운** 코드를 작성할 수 있다는 것이다.

**예시)**

```kotlin
val a: Int? = 100 // ?를 사용해서 nullable value임을 명시
val b: Int = 100 // 그냥 선언할 경우 non-nullable

a?.sum() // a가 null 값일 경우, 뒤에 함수는 호출되지 않는다. a는 nullable이므로 반드시 뒤에 !!(non-null)나 ?를 붙여줘야 한다.
b.sum() // b는 non-null이므로 null 처리를 할 필요가 없다. 
```

<br>

### ● Scope Function(apply, with, let, also, run)
특정 객체의 context를 대상으로 블록 내 코드를 실행하는 함수들이다. 함수마다 전통적인 쓰임새가 있으며, 코드를 읽기 쉽게 만들기 위해 사용한다.

1. Apply

    객체의 확장 함수 형식으로 사용하며, 수신 객체를 반환한다. 주로 **주로 객체를 초기화 할 때 사용한다.**

    ex)
    ```kotlin
    val adam = Person("Adam").apply {
        age = 32
        city = "London"        
    }
    println(adam)
    ```

2. Also

    **객체의 프로퍼티나 함수가 아닌 객체 자체에 접근하는 용도로 사용하며, 주로 디버깅 등 객체를 확인하는 용도로 쓴다.**
    객체의 확장 함수 형식으로 사용하며 수신 객체를 반환한다. 

    ex)
    ```kotlin
    val numbers = mutableListOf("one", "two", "three")
    numbers
        .also { println("The list elements before adding new one: $it") }
        .add("four")
    ```
    
3. Let

    **Nullable 객체가 null이 아닐 때만 코드를 실행시켜야 하는 경우에** 사용한다. 즉, ?와 함께 사용하는 경우가 많으며, 마지막 줄의 수행 결과가 반환된다.

    ex)
    ```kotlin
    val str: String? = "Hello"   
    
    val length = str?.let { 
        println("let() called on $it")        
        processNonNullString(it) // ?안의 it은 null이 아님
        it.length
    }
    ```
4. With

    **주로 Non-nullale 객체에 수행 결과가 필요하지 않을 때 사용한다.**
    확장함수 형식으로 사용하지 않으며, 람다의 마지막 수행 결과를 반환한다. 

    ex)
    ```kotlin
    val numbers = mutableListOf("one", "two", "three")
    with(numbers) {
        println("'with' is called with argument $this")
        println("It contains $size elements")
    }
    ```

5. Run

    **초기화와 연산을 모두 하는 경우처럼 여러 처리를 할 때 사용한다.**
    확장함수 형식으로 사용하거나 그냥 사용할 수도 있으며, 람다의 마지막 수행 결과를 반환한다. 그냥 사용할 때는 변수 범위를 블록 내로 제한해서 특정 연산을 하는 용도로 사용한다.

    ex)
    ```kotlin
    val hexNumberRegex = run {
        val digits = "0-9"
        val hexDigits = "A-Fa-f"
        val sign = "+-"

        Regex("[$sign]?[$digits$hexDigits]+")
    }
    ```

<br>

### ● Data class
데이터 저장 목적의 클래스로, Java의 긴 코드에 비해 한줄로 생성이 가능하다.
getter, setter, copy, toString, hashCode, equal 함수 등이 자동으로 만들어진다.

<br>

### ● lateinit, lazy init
1. lateinit

    **변수를 선언하는 순간이 아닌, 이후에 초기화하기 위해 사용한다.** 지역 변수에 는 사용할 수 없다.

    ex)
    ```kotlin
    private lateinit var txt: TextView
    ```

2. lazy (by lazy)

    이 문법을 사용하면 변수를 사용하기 전까지 변수에 지정한 값이 할당되지 않는다.

    ex)
    ```kotlin
    private val numberPicker: NumberPicker by lazy{
        findViewById(R.id.numberPicker)
    }
    ```

<br>

### ● Manifest 파일
**안드로이드 OS에 앱이 어떤 구조로 되어있는지 설명해주는 파일이다.** 코드 실행 과정에서 안드로이드 OS가 매니패스트 파일을 참조하여 요청을 수행한다.

ex) Intent로 특정 액티비티를 실행시킬 때, 매니패스트 파일에 액티비티를 등록하지 않을 경우 OS가 해당 액티비티를 찾지 못해 에러가 발생한다.