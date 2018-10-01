##### 오버플로우와 언더플로우

Overflow - 자료형 크기보다 큰 값을 선언해서 최소값부터 다시 시작

Underflow - 자료형 크기보다 작은 값을 선언해서 최대값부터 다시 시작

```c
char num1 = 128; // -128 오버플로우 발생 
unsigned char num2 = 256 // 0 오버플로우 발생 
char num3 = -128 // 127 언더플로우 발생 
```



##### 자료형 크기 구하기

sizeof 표현식

sizeof(자료형)

sizeof(표현식)

> 표현식은 변수, 상수, 배열 등 프로그래머가 만들어낸 요소를 뜻함

```c
#include <stdio.h>
int main()
{
    int num1 = 0;
    int size;
    
    size = sizeof num1; // size = 4 변수 num1의 자료형 크기를 구함
    
    printf("num1의 크기 : %d\n", size); // num1의 크기 : 4
    
    return 0;
}
```



```c
#include <stdio.h>

int main()
{
    printf("char: %d, short: %d, int: %d, long: %d, long long: %d\n",
        sizeof(char),        // 1: sizeof로 char 자료형의 크기를 구함
        sizeof(short),       // 2: sizeof로 short 자료형의 크기를 구함
        sizeof(int),         // 4: sizeof로 int 자료형의 크기를 구함
        sizeof(long),        // 4: sizeof로 long 자료형의 크기를 구함
        sizeof(long long)    // 8: sizeof로 long long 자료형의 크기를 구함
    );

    return 0;
}
```



##### 헤더파일(*h)

stdio.h에 printf가 정의되어 있고 printf 함수를 사용하기 위해서 #include <stdio.h>를 사용하는 것이다. 사용자가 원하는 기능을 가진 헤더파일을 정의하고 사용할 수 있다.

##### #include

#include <stdio.h> 컴파일 하기전에 stdio.h를 포함해라 전처리기 기능을 담당



##### 최소값과 최대값을 표현방법

```c
#include <stdio.h>
#include <limits.h>    // 자료형의 최대값과 최소값이 정의된 헤더 파일

int main()
{
    char num1 = CHAR_MIN;          // char의 최소값
    short num2 = SHRT_MIN;         // short의 최소값
    int num3 = INT_MIN;            // int의 최소값
    long num4 = LONG_MIN;          // long의 최소값
    long long num5 = LLONG_MIN;    // long long의 최소값

    // char, short, int는 %d로 출력하고 long은 %ld로 출력, long long은 %lld로 출력
    printf("%d %d %d %ld %lld\n", num1, num2, num3, num4, num5);
    // -128 -32768 -2147483648 -2147483648 -9223372036854775808

    return 0;
}
```



| 자료형             | 최솟값    | 최댓값     |
| ------------------ | --------- | ---------- |
| char               | CHAR_MIN  | CHAR_MAX   |
| short              | SHRT_MIN  | SHRT_MAX   |
| int                | INT_MIN   | INT_MAX    |
| long               | LONG_MIN  | LONG_MAX   |
| long long          | LLONG_MIN | LLONG_MAX  |
| unsigned char      | 0         | UCHAR_MAX  |
| unsigned short     | 0         | USHRT_MAX  |
| unsigned int       | 0         | UINT_MAX   |
| unsigned long      | 0         | ULONG_MAX  |
| unsigned long long | 0         | ULLONG_MAX |



##### 크기가 표시된 정수형 자료형 사용하기

stdint.h 는 크기가 표시된 정수 자료형으로 변수를 선언하는 방법

```c
#include <stdio.h>
#include <stdint.h>    // 크기별로 정수 자료형이 정의된 헤더 파일

int main()
{
    int8_t num1 = -128;                    // 8비트(1바이트) 크기의 부호 있는 정수형 변수 선언
    int16_t num2 = 32767;                  // 16비트(2바이트) 크기의 부호 있는 정수형 변수 선언 
    int32_t num3 = 2147483647;             // 32비트(4바이트) 크기의 부호 있는 정수형 변수 선언
    int64_t num4 = 9223372036854775807;    // 64비트(8바이트) 크기의 부호 있는 정수형 변수 선언

    // int8_t, int16_t, int32_t는 %d로 출력하고 int64_t는 %lld로 출력
    printf("%d %d %d %lld\n", num1, num2, num3, num4); // -128 32767 2147483647 9223372036854775807

    uint8_t num5 = 255;                      // 8비트(1바이트) 크기의 부호 없는 정수형 변수 선언
    uint16_t num6 = 65535;                   // 16비트(2바이트) 크기의 부호 없는 정수형 변수 선언
    uint32_t num7 = 4294967295;              // 32비트(4바이트) 크기의 부호 없는 정수형 변수 선언
    uint64_t num8 = 18446744073709551615;    // 64비트(8바이트) 크기의 부호 없는 정수형 변수 선언

    // uint8_t, uint16_t, uint32_t는 %u로 출력하고 uint64_t는 %llu로 출력
    printf("%u %u %u %llu\n", num5, num6, num7, num8); // 255 65535 4294967295 18446744073709551615

    return 0;
}
```

stdint의 최소, 최대값은 stdint.h 헤더 파일 안에 정의되어 있으므로 limits.h 헤더 파일을 사용하지 않아도 됩니다. 자료형과 마찬가지로 최소, 최댓값도 비트 단위로 크기가 표시되어 있으므로 간편하게 사용할 수 있습니다.

- 부호 있는 정수(signed) 최소값: INT8_MIN, INT16_MIN, INT32_MIN, INT64_MIN
- 부호 있는 정수 최대값: INT8_MAX, INT16_MAX, INT32_MAX, INT64_MAX
- 부호 없는 정수(unsigned) 최소값: 0
- 부호 없는 정수 최대값: UINT8_MAX, UINT16_MAX, UINT32_MAX, UINT64_MAX

##### 실수형 자료형

```c
#include <stdio.h>

int main()
{
    float num1 = 0.1f;               // 단정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // float는 숫자 뒤에 f를 붙임

    double num2 = 3867.215820;       // 배정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // double은 숫자 뒤에 아무것도 붙이지 않음

    long double num3 = 9.327513l;    // 배정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // long double은 숫자 뒤에 l을 붙임

    // float와 double은 %f로 출력, long double은 %Lf로 출력
    printf("%f %f %Lf\n", num1, num2, num3);    // 0.100000 3867.215820 9.327513

    return 0;
}
```

실수형 자료형 지수표기법

```c
#include <stdio.h>

int main()
{
    float num1 = 3.e5f;             // 지수 표기법으로 300000을 표기
                                    // float는 숫자 뒤에 f를 붙임
 
    double num2 = -1.3827e-2;       // 지수 표기법으로 -0.013827을 표기
                                    // double은 숫자 뒤에 아무것도 붙이지 않음

    long double num3 = 5.21e+9l;    // 지수 표기법으로 5210000000을 표기
                                    // long double은 숫자 뒤에 l을 붙임

    // float와 double은 %f로 출력, long double은 %Lf로 출력
    printf("%f %f %Lf\n", num1, num2, num3); // 300000.000000 -0.013827 5210000000.000000

    // 지수 표기법으로 출력할 때는 float와 double은 %e로 출력, long double은 %Le로 출력
    printf("%e %e %Le\n", num1, num2, num3); // 3.000000e+05 -1.382700e-02 5.210000e+09

    return 0;
}
```

> 지수 표기법으로 표기할 때는 정수 부분은 한 자릿수만 적고, 소수자릿수 뒤에 e와 지수를 표기합니다. 마찬가지로 변수 크기에 맞게 마지막에 f 또는 l을 붙여줍니다. e 뒤에 지수가 양수이면 소수점 기준으로 자릿수가 왼쪽으로 이동하며 음수이면 오른쪽으로 이동합니다. 지수가 양수일 때는 +를 생략할 수 있습니다.
>
> printf 함수는 실수를 지수 표기법으로 출력할 수도 있습니다. float와 double은 **%e**로, long double은 **%Le**로 출력하면 됩니다.

실수 자료형 크기 구하기

```c
#include <stdio.h>

int main()
{
    float num1 = 0.0f;
    double num2 = 0.0;
    long double num3 = 0.0l;

    printf("float: %d, double: %d, long double: %d\n",
        sizeof(num1),     // 4: sizeof로 float 변수의 자료형 크기를 구함
        sizeof(num2),     // 8: sizeof로 double 변수의 자료형 크기를 구함
        sizeof(num3)      // 8: sizeof로 long double 변수의 자료형 크기를 구함
    );

    return 0;
}
// 출력값 float: 4, double: 8, long double: 8
```



실수 자료형 양수 최대값과 최소값

```c
#include <stdio.h>
#include <float.h>    // 실수 자료형의 양수 최솟값, 최댓값이 정의된 헤더 파일

int main()
{
    float num1 = FLT_MIN;           // float의 양수 최솟값
    float num2 = FLT_MAX;           // float의 양수 최댓값
    double num3 = DBL_MIN;          // dobule의 양수 최솟값
    double num4 = DBL_MAX;          // double의 양수 최댓값
    long double num5 = LDBL_MIN;    // long double의 양수 최솟값
    long double num6 = LDBL_MAX;    // long double의 양수 최댓값

    printf("%.40f %.2f\n", num1, num2);    // 0.0000000000000000000000000000000000000118
                                           // 340282346638528859811704183484516925440.00

    printf("%e %e\n", num3, num4);         // 2.225074e-308 1.797693e+308
    printf("%Le %Le\n", num5, num6);       // 2.225074e-308 1.797693e+308
 
    return 0;
}

```



##### 문자 자료형

char에 문자를 저장할 때는 문자 자체를 저장하는 것이 아니라 문자에 해다하는 정수값을 저장하게 됩니다. 다음은 각 정수값이 어떤 문자에 해당되는지 표로 나타낸 것이며 이 규칙을 아스키(ASCII)코드라고 부릅니다.

```c
#include <stdio.h>
 
int main()
{
    char c1 = 'a';    // 문자 변수를 선언하고 문자 a를 저장
    char c2 = 'b';    // 문자 변수를 선언하고 문자 b를 저장
 
    // char를 %c로 출력하면 문자가 출력되고, %d로 출력하면 정숫값이 출력됨
    printf("%c, %d\n", c1, c1);    // a, 97: a의 ASCII 코드값은 97
    printf("%c, %d\n", c2, c2);    // b, 98: b의 ASCII 코드값은 98
 
    char c1 = 97;    // a의 ASCII 코드값 97 저장
    char c2 = 98;    // b의 ASCII 코드값 98 저장

    // char를 %c로 출력하면 문자가 출력되고, %d로 출력하면 정숫값이 출력됨
    printf("%c, %d\n", c1, c1); // a, 97
    printf("%c, %d\n", c2, c2); // b, 98
    
    char c1 = 0x61;    // a의 ASCII 코드값 0x61 할당
    char c2 = 0x62;    // b의 ASCII 코드값 0x62 할당

    // char를 %c로 출력하면 문자가 출력되고, %d로 출력하면 정수 값이 출력됨
    // %x로 출력하면 16진수로 출력됨
    printf("%c, %d, 0x%x\n", c1, c1, c1);    // a, 97, 0x61
    printf("%c, %d, 0x%x\n", c2, c2, c2);    // b, 98, 0x62
    
    return 0;
}
```



##### 상수 사용하기

```c
//         ↓ 상수
const int con1 = 10;
//               ↑ 리터럴
```

```c
#include <stdio.h>

int main()
{
    const int con1 = 1;         // 상수. 선언과 동시에 초기화
    const float con2 = 0.1f;    // 상수. 선언과 동시에 초기화
    const char con3 = 'a';      // 상수. 선언과 동시에 초기화

    printf("%d %f %c\n", con1, con2, con3);    // 1 0.100000 a

    return 0;
}
```

상수는 반드시 선언과 동시에 값을 할당하여 초기화해주어야 하며 초기화를 하지 않으면 컴파일 에러가 발생합니다. 물론 상수도 변수처럼 printf에서 상수 이름을 사용하여 저장된 값을 출력할 수 있습니다. 상수에 값을 할당한 뒤 컴파일해보면 컴파일 에러가 발생합니다. 즉, const를 붙여서 상수가 되면 더 이상 값을 할당할 수 없습니다. 완전 고정된 상태죠. 다른 값을 사용하려면 새 상수를 선언해야 합니다.

const의 위치  const 자료형  상수이름 = 값; ex) const int  con1 = 1;

리터럴(literal)은 "문자 그대로"라는 뜻인데 C언어에서는 값 그 자체를 뜻합니다. 그리고 상수(constant)는 변수처럼 리터럴이 저장되는 공간입니다.

```c
#include <stdio.h>

int main()
{
    printf("%d\n", 10);                 // 10: 정수 리터럴
    printf("%f\n", 0.1f);               // 0.100000: 실수 리터럴
    printf("%c\n", 'a');                // a: 문자 리터럴
    printf("%s\n", "Hello, world!");    // Hello, world!: 문자열 리터럴
    
    printf("%d\n", 19);        // 19: 10진 정수 리터럴
    printf("0%o\n", 017);      // 017: 8진 정수 리터럴
    printf("0x%X\n", 0x1F);    // 0x1F: 16진 정수 리터럴


    return 0;
}
```

10진수는 숫자 그대로 표기하면 되고, 8진수는 숫자 앞에 0을 붙이고, 16진수는 0x를 붙입니다. 이때 printf에서 8진수를 출력하려면 서식 지정자로 %o를 사용합니다. 여기서 %o로는 8진수 숫자만 출력되므로 10진수와 구분하기 힘듭니다. 그래서 보통 %o앞에 숫자 0을 붙여서 017형태로 출력합니다.

##### 입력 값을 변수에  저장하기

 정수 입력받기

- scanf(서식, 변수의주소);
  - int scanf(char const \* const _Format, ...);
  - 성공하면 가져온 값의 개수를 반환, 실패하면 EOF(-1)를 반환

scanf 함수는 표준 입력을 받아서 변수에 값을 저장하는 함수입니다.  scanf 함수의 첫 번째 인수에는 큰따옴표 안에 서식 지정자를 넣어서 입력받을 값의 형태를 설정합니다. 그리고 두 번째 인수에는 입력 값을 저장할 변수를 넣습니다. 여기서 주의할 점은 &num1처럼 변수 앞에 &를 붙여주어야 한다는 점입니다.

```c
//     ↓ 첫 번째 인수
scanf("%d", &num1);    // 표준 입력을 받아서 변수에 저장
//            ↑ 두 번째 인수
```

```c
#define _CRT_SECURE_NO_WARNINGS // scanf 보안경고로 인한 컴파일 에러 방지 (Visual Studio에서만 삽입)
#include <stdio.h>
# 정수 1개 입력 받기
int main()
{
    int num1;

    printf("정수를 입력하세요: ");
    scanf("%d", &num1);    // 표준 입력을 받아서 변수에 저장

    printf("%d\n", num1);    // 변수의 내용을 출력

    return 0;
}
```

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
# 정수 2개 입력받기
int main()
{
    int num1, num2;

    printf("정수를 두 개 입력하세요: ");
    scanf("%d %d", &num1, &num2);    // 값을 두 개 입력받아서 변수 두 개에 저장

    printf("%d %d\n", num1, num2);    // 변수의 내용을 출력

    return 0;
}
```




