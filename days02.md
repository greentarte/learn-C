##### 실수 입력받기

```c
 #define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    float num1;

    printf("실수를 입력하세요: ");
    scanf("%f", &num1);    // 실수를 입력받아서 변수에 저장

    printf("%f\n", num1);    // 변수의 내용을 출력

    return 0;
}
```

```c
double num1;
scanf("%lf", &num1);    // 자료형이 double일 때는 %lf

long double num2;
scanf("%Lf", &num2);    // 자료형이 long double일 때는 %Lf
```



##### 문자 입력받기

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    char c1;

    printf("문자를 입력하세요: ");
    scanf("%c", &c1);    // 문자를 입력받아서 변수에 저장

    printf("%c\n", c1);    // 변수의 내용을 출력

    return 0;
}
```

scanf 함수 대신 getchar 함수를 사용해도 문자를 입력받을 수 있습니다.

```c
#include <stdio.h>

int main()
{
    char c1 = getchar();    // 문자 하나를 입력받음
    					  //만약 문자 여러 개를 입력해도 첫 번째 문자만 반환됩니다.

    printf("%c\n", c1);

    return 0;
}
```

getchar 함수에 대응하는 함수로 putchar가 있는데 이 함수는 문자 하나를 화면에 출력합니다.

```c
#include <stdio.h>

int main()
{
    char c1 = 'a';

    putchar(c1);

    return 0;
}
```

>  getchar, putchar 함수 모두 stdio.h 헤더 파일에 선언되어 있습니다.



##### 덧셈, 뺄셈

정수 덧셈, 뺄셈

```c
#include <stdio.h>

int main()
{
    int num1;
    int num2;

    num1 = 1 + 2;    // 1에 2를 더해서 num1에 저장
    num2 = 1 - 2;    // 1에서 2를 빼서 num2에 저장

    printf("%d\n", num1);    //  3
    printf("%d\n", num2);    // -1

    return 0;
}
```

실수 덧셈,뺄셈

```c
#include <stdio.h>

int main()
{
    float num1;
    float num2;

    num1 = 1.0f + 0.456789f;    // 1.0에 0.456789를 더해서 num1에 저장
    num2 = 1.0f - 0.456789f;    // 1.0에서 0.456789를 빼서 num2에 저장

    printf("%f\n", num1);    // 1.456789
    printf("%f\n", num2);    // 0.543211

    return 0;
}
```

```c
#include <stdio.h>

int main()
{
    int num1 = 1;
    int num2 = 1;

    num1 += 2;    // num1에 2를 더한 뒤 다시 num1에 저장(2를 증가시킴)
    num2 -= 2;    // num2에서 2를 뺀 뒤 다시 num2에 저장(2를 감소시킴)

    printf("%d\n", num1);    //  3
    printf("%d\n", num2);    // -1

    return 0;
}
```



##### 증가, 감소 연산자

증가 연산은 ++ 연산자를 사용하며 변수 앞과 뒤에 붙일 수 있습니다.

- 변수++;
- ++변수;

```c
#include <stdio.h>

int main()
{
    int num1 = 1;

    num1++;    // 정수형 변수의 값을 1 증가시킴

    printf("%d\n", num1);    // 2

    return 0;
}
```

알파벳 소문자 b가 들어있는 변수에 ++, -- 연산자를 사용하였습니다. 문자 자료형도 실제로는 정수이므로 증감 연산자를 사용하면 1을 증가시키거나, 감소시킵니다. 따라서 b를 1 증가시키면 ASCII 코드대로 c가 되고, 1 감소시키면 a가 됩니다.

```c
#include <stdio.h>

int main()
{
    char c1 = 'b';
    char c2 = 'b';

    c1++;    // 문자 자료형 변수의 값을 1 증가시킴, 'c'로 바뀜
    c2--;    // 문자 자료형 변수의 값을 1 감소시킴, 'a'로 바뀜

    printf("%c %c\n", c1, c2);    // c a: b에서 1 증가시켰으므로 c, b에서 1 감소시켰으므로 a

    return 0;
}
```



##### 곱셈, 나눗셈

먼저 정수의 곱셈과 나눗셈입니다. 다음과 같이 곱셈은 * 연산자, 나눗셈은 / 연산자를 사용합니다.

```c
#include <stdio.h>

int main()
{
    int num1;
    int num2;

    num1 = 2 * 3;    // 2에 3를 곱해서 num1에 저장
    num2 = 7 / 2;    // 7에서 2를 나누어서 num2에 저장

    printf("%d\n", num1);    // 6
    printf("%d\n", num2);    // 3: 소수점을 사용하지 않고 최대한 나눌 수 있는 값이 3

    return 0;
}
```

```c
#include <stdio.h>

int main()
{
    int num1 = 1;
    int num2 = 0;
    int num3;
    
    num3 = num1 / num2;    // 1을 0으로 나눔. 실행 에러 발생

    printf("%d\n", num3);

    return 0;
}

//0x00AB1690에(div_zero_integer_error.exe의) 처리되지 않은 예외가 있습니다. 0xC0000094: Integer division by zero.
```



실수 곱셈, 나눗셈

```c
#include <stdio.h>

int main()
{
    float num1;
    float num2;

    num1 = 2.73f * 3.81f;    // 2.73에 3.81f을 곱해서 num1에 저장
    num2 = 7.0f / 2.0f;      // 7.0에서 2.0을 나누어서 num2에 저장

    printf("%f\n", num1);    // 10.401299
    printf("%f\n", num2);    // 3.500000

    return 0;
}
```

실수도 소스 코드에서 0으로 직접 나누면 컴파일 에러가 발생합니다.

```c
num1 = 1.0f / 0.0f;   // 1.0을 0.0으로 나눔. 컴파일 에러 발생
//mul_div_real_number.c(8): error C2124: 0으로 나누기 또는 나머지 연산을 수행했습니다.
```

하지만 다음과 같이 변수에 실수와 0.0을 저장해서 나누면 결과가 정수와는 조금 다르게 나옵니다.

```c
#include <stdio.h>

int main()
{
    float num1 = 1.0f;
    float num2 = 0.0f;
    float num3;

    num3 = num1 / num2;

    printf("%f\n", num3);    // inf: 무한대

    return 0;
}
```

곱셈과 나눗셈도 변수를 두 번 입력하지 않도록 곱셈 후 할당 *=, 나눗셈 후 할당 /= 연산자를 제공합니다.

- 변수 \*= 값
- 변수 /= 값

```c
#include <stdio.h>

int main()
{
    int num1 = 2;
    int num2 = 7;

    num1 *= 3;    // num1에 3을 곱한 뒤 다시 num1에 저장
    num2 /= 2;    // num2에서 2를 나눈 뒤 다시 num2에 저장

    printf("%d\n", num1);    // 6
    printf("%d\n", num2);    // 3

    return 0;
}
```



##### 나머지 연산

나머지 연산은 % 연산자를 사용하며 정수 a에서 b를 나눈 뒤 나머지를 구합니다. 

- a % b

```c
#include <stdio.h>

int main()
{
    printf("%d\n", 1 % 3);    // 1: 1을 3으로 나누면 몫은 0 나머지는 1
    printf("%d\n", 2 % 3);    // 2: 2를 3으로 나누면 몫은 0 나머지는 2
    printf("%d\n", 3 % 3);    // 0: 3을 3으로 나누면 몫은 1 나머지는 0
    printf("%d\n", 4 % 3);    // 1: 4를 3으로 나누면 몫은 1 나머지는 1
    printf("%d\n", 5 % 3);    // 2: 5를 3으로 나누면 몫은 1 나머지는 2
    printf("%d\n", 6 % 3);    // 0: 6을 3으로 나누면 몫은 2 나머지는 0

    return 0;
}
```

> 실수의 나머지 구하기
>
> 실수끼리 나누었을 때 나머지는 math.h 헤더 파일의 fmod, fmodf, fmodl 함수로 구할 수 있습니다. 여기서 fmod 함수는 double형 실수, fmodf는 float형 실수, fmodl은 long double형 실수일 때 사용합니다.
>
> - fmod(나누어지는수, 나누는수);
>
> - - double fmod(double _X, double _Y);
>
> - fmodf(나누어지는수, 나누는수);
>
> - - float fmodf(float _X, float _Y);
>
> - fmodl(나누어지는수, 나누는수);
>
> - - long double fmodl(long double _X, long double _Y);
>
> ```c
> #include <stdio.h>
> #include <math.h>    // fmod 함수가 선언된 헤더 파일
> 
> int main()
> {
>     // 실수의 나머지 연산은 fmod, fmodf, fmodl 함수를 사용
> 
>     double num1 = 10.843;
>     double num2 = 3.79;
>     printf("%f\n", fmod(num1, num2));    // 3.263000
> 
>     float num3 = 10.843f;
>     float num4 = 3.79f;
>     printf("%f\n", fmodf(num3, num4));    // 3.263000
> 
>     long double num5 = 10.843l;
>     long double num6 = 3.79l;
>     printf("%Lf\n", fmodl(num5, num6));    // 3.263000
> 
>     return 0;
> }
> ```

```c
int num1 = 7;
int num2 = 2;

num1 %= num2;
num1 = num1 % num2;
```

> 음수의 나머지 연산
>
> 음수를 나머지 연산했을 때 결과는 어떻게 될까요? 결과가 음수가 나올지 양수가 나올지 좀 헷갈립니다.
>
> ```c
> printf("%d\n", 5 % (-3));       // 2
> printf("%d\n", (-5) % 3);       // -2
> printf("%d\n", (-5) % (-3));    // -2
> ```
>
> C99 표준에서 나머지 연산자는 a == (a / b) * b + a % b로 정의하고 있습니다. 따라서 이 식에 앞의 값들을 대입해보면 왜 그런지 알 수 있습니다.
>
> - 5 == 5 / (-3) * (-3) + 5 % (-3)
>
> - - 5 == (-1) * (-3) + 2
>   - 5 == 3 + 2
>
> - -5 == (-5) / 3 * 3 + (-5) % 3
>
> - - -5 == (-1) * 3 + (-2)
>   - -5 == (-3) + (-2)
>
> - -5 == (-5) / (-3) * (-3) + (-5) % (-3)
>
> - - -5 == 1 * (-3) + (-2)
>   - -5 == (-3) + (-2)
>
> 결론적으로 a % b를 연산하면 결과는 a의 부호를 따릅니다(b의 부호는 무시).



##### 자료형의 확장과 축소

정수와 실수를 함께 연산했을 때의 자료형의 확장을 알아보겠습니다.

```c
#include <stdio.h>
 
int main()
{
    int num1 = 11;
    float num2 = 4.4f;
 
    printf("%f\n", num1 + num2);    // 15.400000: 정수와 실수 덧셈. 정수는 실수로 변환됨
    printf("%f\n", num1 - num2);    // 6.600000: 정수와 실수 뺄셈. 정수는 실수로 변환됨
    printf("%f\n", num1 * num2);    // 48.400002: 정수와 실수 곱셈. 정수는 실수로 변환됨
    printf("%f\n", num1 / num2);    // 2.500000: 정수와 실수 나눗셈. 정수는 실수로 변환됨
 
    return 0;
}
```

C 언어에서는 자료형을 섞어서 쓰면 컴파일러에서 암시적 형 변환(implicit type conversion)을 하게 되는데 자료형의 크기가 큰 쪽, 표현 범위가 넓은 쪽으로 자동 변환됩니다. 이를 형 확장(type promotion)이라고 하며 값이 버려지지 않고 그대로 보전됩니다.



실수에서 정수로 표현 범위가 좁은 쪽으로 변환하게 되면 값의 손실이 생깁니다.

```c
#include <stdio.h>
 
int main()
{
    float num1 = 11.0f;
    float num2 = 5.0f;
 
    int num3 = num1 / num2;    // 실수에서 실수를 나누어 2.2가 나왔지만 
                               // 정수 자료형에는 2만 저장되고 0.2는 버려짐
 
    printf("%d\n", num3);    // 2
 
    return 0;
}
```

형 축소가 일어나면 컴파일할 때 다음과 같이 값의 손실이 일어날 수 있다고 경고가 나옵니다. C 언어에서 자료형을 섞어 쓸 때 이 부분을 항상 주의해야 하며 예상치 못한 버그가 발생하기 쉽습니다.

> ```
> type_demotion_float_to_int.c(8): warning C4244: '초기화 중': 'float'에서 'int'(으)로 변환하면서 데이터가 손실될 수 있습니다.
> ```

컴파일 경고가 나오지 않게 하려면 형 변환(type conversion, type casting, 타입 캐스팅)을 해야 합니다. 보통 형 변환은 자료의 손실을 감안하여 구현하거나, 자료형을 숨기고 싶을 때 등 다양한 방식으로 활용합니다.

```c
#include <stdio.h>
 
int main()
{
    char num1 = 28;
    int num2 = 1000000002;
 
    char num3 = num1 + num2;    // char보다 큰 숫자는 저장할 수 없음
                                // 28 + 2만 남고 앞 자릿수는 버려짐
 
    printf("%d\n", num3);    // 30
  
    return 0;
}
```

![img](https://dojang.io/pluginfile.php/163/mod_page/content/24/unit16-3.png)

오른쪽으로 갈수록 크기가 크고 표현 범위가 넓은 자료형입니다. 그리고 같은 자료형 안에서도 숫자가 높을수록 크기가 큽니다.



##### 조건문

if 조건문은 괄호 안에 조건식을 지정하여 사용합니다.

```c
if (조건식)
{
    코드
}
```

```c
#include <stdio.h>
 
int main()
{
    int num1 = 10;
 
    if (num1 == 10)    // num1이 10이면
    {
        printf("10입니다.\n");    // "10입니다."를 출력
    }
 
    return 0;
}
```

if 조건문에서 실행할 코드가 한 줄이라면 다음과 같이 중괄호를 생략할 수 있습니다.

```c
#include <stdio.h>
 
int main()
{
    int num1 = 10;
 
    if (num1 == 10)
        printf("10입니다.\n");    // 실행할 코드가 한 줄이라면 중괄호 생략
 
    return 0;
}
```



실수와 문자 비교하기

```c
#include <stdio.h>
 
int main()
{
    float num1 = 0.1f;
    char c1 = 'a';
 
    if (num1 == 0.1f)  // 실수 비교
        printf("0.1입니다.\n");
 
    if (c1 == 'a')     // 문자 비교
        printf("a입니다.\n");
 
    if (c1 == 97)      // 문자를 ASCII 코드로 비교
        printf("a입니다.\n");
 
    return 0;
}
```



```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
 
int main()
{
    int num1;

    scanf("%d", &num1);    // 입력받은 값을 변수에 저장
 
    if (num1 == 10)             // num1이 10이면
    {
        printf("10입니다.\n");  // "10입니다."를 출력
    }
 
    if (num1 == 20)             // num1이 20이면
    {
        printf("20입니다.\n");  // "20입니다."를 출력
    }
 
    return 0;
}
```



else는 if 조건문 뒤에 오며 단독으로 사용할 수 없습니다.

```c
if (조건식)
{
    코드1
}
else
{
    코드2
}
```

```c
#include <stdio.h>
 
int main()
{
    int num1 = 5;
 
    if (num1 == 10)
    {	// if로 실행할 코드가 두 줄 이상이라면 중괄호로 묶어줌
        printf("if 조건문\n");
        printf("10입니다.\n");
    }
    else    // if의 조건식이 만족하지 않을 때 코드를 실행
    {	// else로 실행할 코드가 두 줄 이상이라면 중괄호로 묶어줌
        printf("else\n");
        printf("10이 아닙니다.\n");    // num1은 10이 아니므로 "10이 아닙니다."가 출력됨
    }
 
    return 0;
}
```

else도 if와 마찬가지로 실행할 코드가 한 줄이면 중괄호를 생략할 수 있습니다.

```c
#include <stdio.h>
 
int main()
{
    int num1 = 10;
 
    if (num1 == 10)
        printf("10입니다.\n");
    else
        printf("10이 아닙니다.\n");    // 실행할 코드가 한 줄이라면 중괄호 생략
 
    return 0;
}
```

C 언어에서 if는 0일 때 거짓, 0이 아닐 때 참으로 동작합니다. 

```c
#include <stdio.h>
 
int main()
{
    if (2)    // 0이 아니므로 참
        printf("참\n");
    else
        printf("거짓\n");
 
    return 0;
}
```

```c
#include <stdio.h>
 
int main()
{
    if (0)    // 0이므로 거짓
        printf("참\n");
    else
        printf("거짓\n");
 
    return 0;
}
```



&&와 ||를 사용하여 여러개의 조건식을 사용 

```c
#include <stdio.h>

int main()
{
    int num1 = 10;
    int num2 = 20;

    if (num1 == 10 && num2 == 20)    // num1이 10이면서 num2이 20일 때
        printf("참\n");
    else
        printf("거짓\n");

    return 0;
}
```



else if 사용하기

```c
if (조건식)
{
    코드1
}
else if (조건식)
{
    코드2
}
```

```c
#include <stdio.h>

int main()
{
    int num1 = 20;

    if (num1 == 10)
        printf("10입니다.\n");
    else if (num1 == 20)    // else인 상태에서 조건식 지정
        printf("20입니다.\n");

    return 0;
}
```

```c
#include <stdio.h>

int main()
{
    int num1 = 30;

    if (num1 == 10)        // num1이 10일 때
        printf("10입니다.\n");
    else if (num1 == 20)   // num1이 20일 때
        printf("20입니다.\n");
    else                   // 앞의 조건식에 모두 만족하지 않을 때
        printf("10도 20도 아닙니다.\n");

    return 0;
}
```



##### 비교연산자와 삼항연산자

비교연산자

```c
#include <stdio.h>
 
int main()
{
    int num1 = 10;
	//false면 0 true면  1 
    printf("%d\n", num1 == 10);    // 1: num1이 10과 같은지
    printf("%d\n", num1 != 5);     // 1: num1이 5와 다른지
 
    printf("%d\n", num1 > 10);     // 0: num1이 10보다 큰지
    printf("%d\n", num1 < 10);     // 0: num1이 10보다 작은지
 
    printf("%d\n", num1 >= 10);    // 1: num1이 10보다 크거나 같은지
    printf("%d\n", num1 <= 10);    // 1: num1이 10보다 작거나 같은지
 
    return 0;
}
```

삼항연산자

```c
#include <stdio.h> 

int main()
{
    int num1 = 5;
    int num2;
 
    num2 = num1 ? 100 : 200;    // num1이 참이면 num2에 100을 할당, 거짓이면 num2에 200을 할당
 
    printf("%d\n", num2);    // 100: num1이 5이므로 참. num2에는 100이 할당됨
 
    return 0;
}
```

![img](https://dojang.io/pluginfile.php/202/mod_page/content/19/unit20-2.png)

> 가독성을 해치지 않으면서 코드가 간결해지는 경우에만 삼항 연산자를 써야 합니다. 대부분의 경우에는 if 조건문을 사용하여 여러 줄로 작성하는 것이 좋습니다. 코드를 암호처럼 복잡하게 만드는 것이 실력이 아닙니다. 나와 다른 사람이 알아보기 쉽게 만드는 것이 진짜 실력임을 잊지 마세요.



논리연산자

| 연산자 | 설명                                   |
| ------ | -------------------------------------- |
| &&     | AND(논리곱), 양쪽 모두 참일 때 참      |
| \|\|   | OR(논리합), 양쪽 중 한쪽만 참이라도 참 |
| !      | NOT(논리 부정), 참과 거짓을 뒤집음     |

```c
#include <stdio.h>
 
int main()
{
    printf("%d\n", 1 && 1);    // 1: 1 AND 1은 참
    printf("%d\n", 1 && 0);    // 0: 1 AND 0은 거짓
    printf("%d\n", 0 && 1);    // 0: 0 AND 1은 거짓
    printf("%d\n", 0 && 0);    // 0: 0 AND 0은 거짓
 
    printf("%d\n", 2 && 3);    // 1: 2 AND 3은 참
 	printf("%d\n", 0 && 1);    // 첫 번째 값 0이 거짓이므로 두 번째 값 1은 확인하지 않고 거짓으로 결정
    return 0;
}
```

```c
#include <stdio.h>
 
int main()
{
    printf("%d\n", 1 || 1);    // 1: 1 OR 1은 참
    printf("%d\n", 1 || 0);    // 1: 1 OR 0은 참
    printf("%d\n", 0 || 1);    // 1: 0 OR 1은 참
    printf("%d\n", 0 || 0);    // 0: 0 OR 0은 거짓
    printf("%d\n", 2 || 3);    // 1: 2 OR 3은 참
    
    printf("%d\n", 1 || 1);    // 첫 번째 값 1이 참이므로 두 번째 값 1은 확인하지 않고 참으로 결정
	printf("%d\n", 1 || 0);    // 첫 번째 값 1이 참이므로 두 번째 값 0은 확인하지 않고 참으로 결정
	printf("%d\n", 2 || 3);    // 첫 번째 값 2가 참이므로 두 번째 값 3은 확인하지 않고 참으로 결정
    return 0;
}
```

```c
#include <stdio.h>
 
int main()
{
    printf("%d\n", !1);    // 0: NOT 1은 거짓
    printf("%d\n", !0);    // 1: NOT 0은 참
 
    printf("%d\n", !3);    // 0: NOT 3은 거짓
 
    return 0;
}
```



##### 논리 자료형 사용하기

boolean 자료형은 논리 자료형이라고도 하며 참과 거짓을 나타냅니다.

지금까지는 C언어는 0을 거짓으로, 0이 아닌 숫자를 참으로 사용하지만 stdbool.h 헤더파일을 사용하면 true를 참으로, false를 거짓으로 나타낼 수 있습니다.

```c
#include <stdio.h>
#include <stdbool.h>    // bool, true, false가 정의된 헤더 파일
 
int main()
{
    bool b1 = true;  
 
    if (b1 == true)        // b1이 true인지 검사
        printf("참\n");    // b1이 true이므로 참이 출력됨
    else
        printf("거짓\n");
 
    return 0;
}
```

bool 자료형의 크기

```c
#include <stdio.h>
#include <stdbool.h>    // bool, true, false가 정의된 헤더 파일
 
int main()
{
    printf("int의 크기: %d\n", sizeof(int));      // int의 크기: 4: int의 크기는 4바이트
    printf("bool의 크기: %d\n", sizeof(bool));    // bool의 크기: 1: bool의 크기는 1바이트
 
    return 0;
}
```

```c
#include <stdio.h>
#include <stdbool.h>    // bool, true, false가 정의된 헤더 파일
 
int main()
{
    printf("%d\n", true && true);      // 1: true AND true는 1
    printf("%d\n", true && false);     // 0: true AND false는 0
    printf("%d\n", false && true);     // 0: false AND true는 0
    printf("%d\n", false && false);    // 0: false AND false는 0
 
    printf("%d\n", true || true);      // 1: true OR true는 1
    printf("%d\n", true || false);     // 1: true OR false는 1
    printf("%d\n", false || true);     // 1: false OR true는 1
    printf("%d\n", false || false);    // 0: false OR false는 0

    return 0;
}
//printf로 결과를 출력할 때는 정수를 출력하는 것처럼 서식 지정자로 %d를 사용합니다.
```



##### 비트연산자 사용하기

| 연산자 | 설명                               |
| ------ | ---------------------------------- |
| &      | 비트 AND                           |
| \|     | 비트 OR                            |
| ^      | 비트 XOR(배타적 OR, Exclusive OR)  |
| ~      | 비트 NOT                           |
| <<     | 비트를 왼쪽으로 시프트             |
| >>     | 비트를 오른쪽으로 시프트           |
| &=     | 비트 AND 연산 후 할당              |
| !=     | 비트 OR 연산 후 할당               |
| ^=     | 비트 XOR 연산 후 할당              |
| <<=    | 비트를 왼쪽으로 시프트한 후 할당   |
| >>=    | 비트를 오른쪽으로 시프트한 후 할당 |

> 비트 연산자는 비트로 옵션을 설정할 때 주로 사용하며 저장 공간을 아낄 수 있는 장점이 있습니다. 특히 이런 방식을 플래그(flag)라고 부릅니다.

```c
#include <stdio.h>
 
int main()
{
    unsigned char num1 = 1;    // 0000 0001
    unsigned char num2 = 3;    // 0000 0011
 
    printf("%d\n", num1 & num2);    // 0000 0001: 01과 11을 비트 AND하면 01이 됨
    printf("%d\n", num1 | num2);    // 0000 0011: 01과 11을 비트 OR하면 11이 됨
    printf("%d\n", num1 ^ num2);    // 0000 0010: 01과 11을 비트 XOR하면 10이 됨
 
    return 0;
}
```

NOT 연산자

~ 연산자는 비트 NOT 연산자입니다. 간단하게 0은 1로 1은 0으로 바꾸며 "비트를 뒤집는다" 또는 "비트 반전"이라고 말합니다.

```c
#include <stdio.h>

int main()
{
    unsigned char num1 = 162;    // 162: 1010 0010
    unsigned char num2;

    num2 = ~num1;

    printf("%u\n", num2);    // 93: 0101 1101: num1의 비트 값을 뒤집음

    return 0;
}
```



시프트 연산자

```c
#include <stdio.h>
 
int main()
{
    unsigned char num1 = 3;     //  3: 0000 0011
    unsigned char num2 = 24;    // 24: 0001 1000
 
    printf("%u\n", num1 << 3);  // 24: 0001 1000: num1의 비트 값을 왼쪽으로 3번 이동
    printf("%u\n", num2 >> 2);  //  6: 0000 0110: num2의 비트 값을 오른쪽으로 2번 이동
 
    return 0;
}
```



시프트 연산자 응용

부호가 없는 자료형

```c
#include <stdio.h>
 
int main()
{
    unsigned char num1 = 1;    //   1: 0000 0001
 
    printf("%u\n", num1 << 1);    //   2: 0000 0010: 2
    printf("%u\n", num1 << 2);    //   4: 0000 0100: 2^2
    printf("%u\n", num1 << 3);    //   8: 0000 1000: 2^3
    printf("%u\n", num1 << 4);    //  16: 0001 0000: 2^4
    printf("%u\n", num1 << 5);    //  32: 0010 0000: 2^5
    printf("%u\n", num1 << 6);    //  64: 0100 0000: 2^6
    printf("%u\n", num1 << 7);    // 128: 1000 0000: 2^7

    return 0;
}
```

```c
#include <stdio.h>
 
int main()
{
    unsigned char num1 = 240;    // 240: 1111 0000
    unsigned char num2 = 15;     //  15: 0000 1111
 
    unsigned char num3, num4;
 
    num3 = num1 << 2;    // num1의 비트 값을 왼쪽으로 2번 이동
    num4 = num2 >> 2;    // num2의 비트 값을 오른쪽으로 2번 이동
 
    printf("%u\n", num3);    // 192: 1100 0000: 맨 앞의 11이 사라져서 11000000이 됨
    printf("%u\n", num4);    //   3: 0000 0011: 맨 뒤의 11이 사라져서 00000011이 됨
 
    return 0;
}
```



부호가 있는 자료형

```c
#include <stdio.h>
 
int main()
{
    unsigned char num1 = 131;    //  131: 1000 0011
    char num2 = -125;            // -125: 1000 0011
 
    unsigned char num3;
    char num4;
 
    num3 = num1 >> 5;    // num1의 비트 값을 오른쪽으로 5번 이동
    num4 = num2 >> 5;    // num2의 비트 값을 오른쪽으로 5번 이동
 
    printf("%u\n", num3);    //  4: 0000 0100: 맨 뒤의 11은 사라지고 0000 0100이 됨
    printf("%d\n", num4);    // -4: 1111 1100: 모자라는 공간은 부호 비트의 값인 1로  
                             // 채워지므로 1111 1100이 됨
 
    return 0;
}
```

![](https://dojang.io/pluginfile.php/246/mod_page/content/22/unit24-2.png)

이 비트들을 오른쪽으로 5번 이동시키면 모자라는 공간은 모두 부호 비트의 값으로 채워지기 때문에 1111 1100(-4)가 됩니다. 하지만 부호 없는 자료형은 비트를 오른쪽으로 이동해도 모자라는 공간은 모두 0으로 채워집니다. 즉, 비트 연산자는 부호 있는 자료형과 부호 없는 자료형이 다르게 동작합니다.

![](https://dojang.io/pluginfile.php/246/mod_page/content/22/unit24-3.png)



```c
#include <stdio.h>
 
int main()
{
    char num1 = 67;    // 67: 0100 0011
    char num2;
 
    num2 = num1 >> 5;    // num1의 비트 값을 오른쪽으로 5번 이동
 
    printf("%d\n", num2);    // 2: 0000 0010: 모자라는 공간은 부호 비트의 값인 0으로 채워지므로 
                             // 0000 0010이 됨
 
    return 0;
}
```

```c
#include <stdio.h>
 
int main()
{
    char num1 = 113;    //  113: 0111 0001
    char num2 = -15;    //  -15: 1111 0001
    char num3, num4, num5, num6;
 
    num3 = num1 << 2;    // num1의 비트 값을 왼쪽으로 2번 이동
    num4 = num2 << 2;    // num2의 비트 값을 왼쪽으로 2번 이동
 
    num5 = num1 << 4;    // num1의 비트 값을 왼쪽으로 4번 이동
    num6 = num2 << 4;    // num1의 비트 값을 왼쪽으로 4번 이동
 
    printf("%d\n", num3);    // -60: 1100 0100: 부호 비트를 덮어쓰게 되므로 양수에서 음수가 됨
    printf("%d\n", num4);    // -60: 1100 0100: 이미 음수인 수는 계속 음수가 됨
 
    printf("%d\n", num5);    // 16: 0001 0000: 이미 양수인 수는 계속 양수가 됨
    printf("%d\n", num6);    // 16: 0001 0000: 부호 비트를 덮어쓰게 되므로 음수에서 양수가 됨
 
    return 0;
}
```

부호 있는 자료형에서 비트를 왼쪽으로 이동시켰을 때는 부호 비트에 위치한 숫자에 따라 양수, 음수가 결정됩니다. 따라서 부호 있는 자료형에 시프트 연산을 할 때는 의도치 않은 결과가 나올 수 있으므로 항상 부호 비트를 생각해야 합니다.



비트 연산자로 플래그 처리하기

정수의 비트에 활용하는 건데 비트가 1이면 on, 0이면 off를 나타냅니다.

```java
0100 0001    // 두 번째 비트와 여덟 번째 비트가 켜진 상태(on)
```

>  플래그를 사용하는 곳은?
>
> 그냥 int형 변수 8개를 선언하여 각각 상태를 저장하면 간단할 텐데 플래그를 사용하는 이유는 무엇일까요? 플래그는 적은 공간에 정보를 저장해야 하고, 빠른 속도가 필요할 때 사용합니다. 가장 대표적인 장치가 CPU인데요. CPU는 내부 저장 공간이 매우 작기 때문에 각종 상태를 비트로 저장합니다.

특정 비트를 켜는 방법

- **플래그 |= 마스크**

```c
#include <stdio.h>
 
int main()
{
    unsigned char flag = 0;
 
    flag |= 1;    // 0000 0001 마스크와 비트 OR로 여덟 번째 비트를 켬
    flag |= 2;    // 0000 0010 마스크와 비트 OR로 일곱 번째 비트를 켬
    flag |= 4;    // 0000 0100 마스크와 비트 OR로 여섯 번째 비트를 켬
 
    printf("%u\n", flag);    // 7: 0000 0111
 
    if (flag & 1)    // & 연산자로 0000 0001 비트가 켜져 있는지 확인
        printf("0000 0001은 켜져 있음\n");
    else
        printf("0000 0001은 꺼져 있음\n");
    
    if (flag & 2)    // & 연산자로 0000 0010 비트가 켜져 있는지 확인
        printf("0000 0010은 켜져 있음\n");
    else
        printf("0000 0010은 꺼져 있음\n");
 
    if (flag & 4)    // & 연산자로 0000 0100 비트가 켜져 있는지 확인
        printf("0000 0100은 켜져 있음\n");
    else
        printf("0000 0100은 꺼져 있음\n");
 
    return 0;
}
```

플래그의 비트 켜기

![](https://dojang.io/pluginfile.php/247/mod_page/content/32/unit24-9.png)

플래그의 특정 비트가 켜져 있는지 검사하려면 & 연산자를 사용

```c
if (flag & 4)    // & 연산자로 0000 0100 비트가 켜져 있는지 확인
    printf("0000 0100은 켜져 있음\n");
else
    printf("0000 0100은 꺼져 있음\n");
```

& 연산자는 두 비트가 모두 1이라야 1입니다. 따라서 flag에 저장된 0000 0111과 마스크 값 0000 0100(4)를 &로 연산하면 여섯 번째 비트가 1이 됩니다. 연산 결과가 마스크 값이 나오면 비트가 켜져 있는 것이고, 0이 나오면 꺼져있는 것이죠.



플래그의 비트를 끄기

마스크 값을 ~ 연산자로 비트를 뒤집은 뒤 &= 연산자를 사용하여 특정 비트를 끕니다.

- **플래그 &= ~마스크**

```c
#include <stdio.h>
 
int main()
{
    unsigned char flag = 7;    // 7: 0000 0111
 
    flag &= ~2;    // 1111 1101 마스크 값 2의 비트를 뒤집은 뒤 비트 AND로 일곱 번째 비트를 끔
 
    printf("%u\n", flag);    // 5: 0000 0101
 
    if (flag & 1)    // & 연산자로 0000 0001 비트가 켜져 있는지 확인
        printf("0000 0001은 켜져 있음\n");
    else
        printf("0000 0001은 꺼져 있음\n");
 
    if (flag & 2)    // & 연산자로 0000 0010 비트가 켜져 있는지 확인
        printf("0000 0010은 켜져 있음\n");
    else
        printf("0000 0010은 꺼져 있음\n");
 
    if (flag & 4)    // & 연산자로 0000 0100 비트가 켜져 있는지 확인
        printf("0000 0100은 켜져 있음\n");
    else
        printf("0000 0100은 꺼져 있음\n");
 
    return 0;
}
```

![](https://dojang.io/pluginfile.php/247/mod_page/content/32/unit24-10.png)



비트가 켜져 있다면 끄고, 꺼져있다면 켜는 방법, 다른 말로는 토글(toggle)

- **플래그 ^= 마스크**

```c
#include <stdio.h>
 
int main()
{
    unsigned char flag = 7;    // 7: 0000 0111
 
    flag ^= 2;    // 0000 0010 마스크와 비트 XOR로 일곱 번째 비트를 토글
    flag ^= 8;    // 0000 1000 마스크와 비트 XOR로 다섯 번째 비트를 토글
 
    printf("%u\n", flag);    // 13: 0000 1101
 
    if (flag & 1)    // & 연산자로 0000 0001 비트가 켜져 있는지 확인
        printf("0000 0001은 켜져 있음\n");
    else
        printf("0000 0001은 꺼져 있음\n");
 
    if (flag & 2)    // & 연산자로 0000 0010 비트가 켜져 있는지 확인
        printf("0000 0010은 켜져 있음\n");
    else
        printf("0000 0010은 꺼져 있음\n");
 
    if (flag & 4)    // & 연산자로 0000 0100 비트가 켜져 있는지 확인
        printf("0000 0100은 켜져 있음\n");
    else
        printf("0000 0100은 꺼져 있음\n");
 
    if (flag & 8)    // & 연산자로 0000 1000 비트가 켜져 있는지 확인
        printf("0000 1000은 켜져 있음\n");
    else
        printf("0000 1000은 꺼져 있음\n");
 
    return 0;
}
```

![](https://dojang.io/pluginfile.php/247/mod_page/content/32/unit24-11.png)



#####  swtich문

![](https://dojang.io/pluginfile.php/259/mod_page/content/20/unit26-1.png)

switch 문법

```c
switch (변수)
{
case 숫자1:
    코드1
    break;
case 숫자2:
    코드2
    break;
default:
    코드3;
    break;
}
```

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    int num1;

    scanf("%d", &num1);    // 값을 입력받음

    switch (num1)   // num1의 값에 따라 분기
    {
    case 1:         // 1일 때
        printf("1입니다.\n");
        break;
    case 2:         // 2일 때
        printf("2입니다.\n");
        break;
    default:        // 아무 case에도 해당되지 않을 때
        printf("default\n");
        break;
    }

    return 0;
}
```

조건식이 바뀌지 않고 값만 바뀔 때는 switch가 적합하며, 값과 조건식이 모두 바뀔 때는 else if가 적합합니다.

case에서 break를 생략하는 상황은 버그 같지만 실제로는 많이 사용되는 방식

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    int num1;

    scanf("%d", &num1);    // 값을 입력받음

    switch (num1)
    {
    case 1:    // 1 또는
    case 2:    // 2일 때 코드 실행
        printf("1 또는 2입니다.\n");
        break;
    case 3:    // 3 또는
    case 4:    // 4일 때 코드 실행
        printf("3 또는 4입니다.\n");
        break;
    default:
        printf("default\n");
    }

    return 0;
}
```

switch 같은 조건을 가진 if 형식

```c
if (num1 == 1 || num1 == 2)
    printf("1 또는 2입니다.\n");
else if (num1 == 3 || num1 == 4)
    printf("3 또는 4입니다.\n");
else
    printf("default\n");
```

case에서 변수를 선언하려면 다음과 같이 { } (중괄호)로 묶어주면 됩니다.

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    int num1;

    scanf("%d", &num1);    // 값을 입력받음

    switch (num1)    // num1의 값에 따라 분기
    {
    case 1:
    {   // case에서 변수를 선언하려면 중괄호로 묶어줌
        int num2 = num1;
        printf("%d입니다.\n", num2);
        break;
    }
    case 2:
        printf("2입니다.\n");
        break;
    default:
        printf("default\n");
        break;
    }

    return 0;
}
```



##### 반복문

for 문법

```c
for (초기식; 조건식; 변화식) // ← 루프 선언문(loop statement)
{
    반복할 코드
}
// ↑ 루프 본체(loop body)
```

```c
#include <stdio.h>

int main()
{
    for (int i = 0; i < 100; i++)    // 0부터 99까지 증가하면서 100번 반복
    {
        printf("Hello, world!\n");
    }

    return 0;
}
```

![](https://dojang.io/pluginfile.php/269/mod_page/content/26/unit27-2.png)



scanf 함수로 입력 값을 받아서 count 변수에 저장한 뒤 for 반복문의 초깃값 부분에서 count를 i에 할당하였습니다. 그리고 조건식은 i > 0, 변화식은 i--로 지정하여 반복문이 실행될 때마다 i를 감소시키고 i가 0이 되면 반복문을 끝내도록 만들었습니다.

i를 따로 선언하지 않고, count를 그대로 사용할 수도 있습니다.

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    int count;

    scanf("%d", &count);    // 값을 입력받음

    for (; count > 0; count--)    // 초깃값 없이 scanf에서 사용한 변수를 감소시켜서 반복
    {
        printf("Hello, world! %d\n", count);
    }

    return 0;
}
```

for의 초기식 부분이 비어있습니다. 즉, for 반복문에 사용할 변수와 초깃값이 준비되어 있으면 초깃값 부분을 생략할 수 있습니다. 그리고 조건식과 변화식 모두 count > 0, count--처럼 count 변수를 기준으로 만들면 됩니다.

> 사실은 이렇게 초기식 부분에서 scanf 함수를 호출하는 방식으로도 작성할 수 있습니다.
>
> ```c
> for (scanf("%d", &count); count > 0; count--)
> ```

반복문에 변수 2개 사용 및 변수의 증가 폭을 다르게 설정

```c
#include <stdio.h>

int main()
{
    for (int i = 0, j = 0; i < 10; i++, j += 2)    // i는 1씩 증가, j는 2씩 증가
    {
        printf("i: %d, j: %d\n", i, j);
    }

    return 0;
}
// 실행결과
// i: 0, j: 0
// i: 1, j: 2
// i: 2, j: 4
// i: 3, j: 6
// i: 4, j: 8
// i: 5, j: 10
// i: 6, j: 12
// i: 7, j: 14
// i: 8, j: 16
// i: 9, j: 18
```

for 무한루프 

```c
#include <stdio.h>

int main()
{
    for (;;)    // 초깃값, 조건식, 변화식을 모두 생략하면 무한 루프
    {
        printf("Hello, world!\n");
    }

    return 0;
}
```



##### while

while문법

```c
초기식
while (조건식) // ← 루프 선언문(loop statement)
{
    반복할 코드
    변화식
}
// ↑ 루프 본체(loop body) 및 변화식
```

```c
#include <stdio.h>

int main()
{
    int i = 0;
    while (i < 100)    // i가 100보다 작을 때 반복. 0에서 99까지 증가하면서 100번 반복
    {
        printf("Hello, world!\n");
        i++;           // i를 1씩 증가시킴
    }

    return 0;
}
```

![](https://dojang.io/pluginfile.php/282/mod_page/content/19/unit28-2.png)

```c
#include <stdio.h>
#include <stdlib.h>    // srand, rand 함수가 선언된 헤더 파일
#include <time.h>      // time 함수가 선언된 헤더 파일

int main()
{
    srand(time(NULL));    // 현재 시간값으로 시드 설정

    int i = 0;
    while (i != 3)         // 3이 아닐 때 계속 반복
    {
        i = rand() % 10;   // rand 함수를 사용하여 무작위로 정수를 생성한 뒤 10 미만의 숫자로 만듦
        printf("%d\n", i);
    }

    return 0;
}
```

먼저 무작위로 정수를 생성하려면 srand, rand, time 함수가 필요합니다(무작위로 정수를 생성하는 행동을 난수 생성 또는 랜덤이라고도 합니다).

- srand: 난수를 발생시킬 초깃값인 시드(seed)를 설정합니다. 보통 현재 시간값을 사용합니다.
- rand: 난수를 발생시킵니다.
- time: 정수 형태로 된 현재 시간값을 반환합니다.

**while 반복문은 반복 횟수가 정해져 있지 않을 때 유용합니다.**

```c
#include <stdio.h>

int main()
{
    while (1)    // while에 1을 지정하면 무한 루프
    {
        printf("Hello, world!\n");
    }

    return 0;
}
```





