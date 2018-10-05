##### do while 반복문

do while 반복문은 초기식이 반복문 바깥에 있습니다. 그리고 do로 시작하여 중괄호 안에 반복할 코드와 변화식이 함께 들어가며 중괄호가 끝나는 부분에 조건식을 지정

 **do while은 처음 한 번은 실행해야 하며 그 이후에는 조건에 따라 반복해야 하는 코드를 간단하게 표현할 수 있습니다.**

```c
초기식
do // ↓ 루프 본체(loop body) 및 변화식
{
    반복할 코드
    변화식
} while (조건식);
//   ↑ 루프 선언문(loop statement)
```

```c
#include <stdio.h>

int main()
{
    int i = 0;

    do     // 처음 한 번은 아래 코드가 실행됨
    {
        printf("Hello, world! %d\n", i);    // Hello, world!와 i의 값을 함께 출력
        i++;                                // i를 1씩 증가시킴
    } while (i < 100);    // i가 100보다 작을 때 반복. 0부터 99까지 증가하면서 100번 반복

    return 0;
}
// 출력결과 
// Hello, world! 0
// Hello, world! 1
// 99까지 출력됨
```

![](https://dojang.io/pluginfile.php/294/mod_page/content/22/unit29-2.png)



##### break, continue로 반복문 제어

break는 for, while, do while, switch 문법에서 제어흐름을 벗어나기 위해 사용

![](https://dojang.io/pluginfile.php/304/mod_page/content/14/unit30-1.png)

```c
#include <stdio.h>

int main()
{
    int num1 = 0;

    while (1)   // 무한 루프
    {
        num1++;  // num1을 1씩 증가시킴

        printf("%d\n", num1);

        if (num1 == 100)    // num1이 100일 때
            break;          // 반복문을 끝냄. while의 제어흐름을 벗어남
    }

    return 0;
}
```



continue는 제어흐름(반복)을 유지한 상태에서 코드의 실행만 건너뛰는 역할 

![](https://dojang.io/pluginfile.php/306/mod_page/content/21/unit30-3.png)

```c
#include <stdio.h>

int main()
{
    for (int i = 1; i <= 100; i++)    // 1부터 100까지 증가하면서 100번 반복
    {
        if (i % 2 != 0)               // i를 2로 나누었을 때 나머지가 0이 아니면 홀수
            continue;                 // 아래 코드를 실행하지 않고 건너뜀

        printf("%d\n", i);
    }

    return 0;
}
// 짝수면 출력되는 결과가 나옴
```



##### 제어문 goto

보통 프로그램을 작성하다보면 중간의 코드는 무시하고 원하는 부분으로 건너뛰어야 하는 상황이 생기기도 합니다. 이런 경우에 사용하는 제어문이 goto입니다.

![](https://dojang.io/pluginfile.php/320/mod_page/content/15/unit32-1.png)

goto는 레이블을 지정해서 사용합니다. 레이블은 : (콜론)을 붙이며 레이블 이름을 짓는 규칙은 변수와 같습니다.

- **goto 레이블;**
- **레이블:**

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main()
{
    int num1;

    scanf("%d", &num1);

    if (num1 == 1)         // num1이 1이면
        goto ONE;          // 레이블 ONE으로 즉시 이동
    else if (num1 == 2)    // num1이 2이면
        goto TWO;          // 레이블 TWO로 즉시 이동
    else                   // 1도 아니고 2도 아니면
        goto EXIT;         // 레이블 EXIT로 즉시 이동

ONE:    // 레이블 ONE
    printf("1입니다.\n");
    goto EXIT; // 레이블 EXIT로 즉시 이동

TWO:    // 레이블 TWO
    printf("2입니다.\n");
    goto EXIT; // 레이블 EXIT로 즉시 이동

EXIT:    // 레이블 EXIT
    return 0;
}
```



중첩 루프를 빠져 나오려면 추가적인 코드가 더 필요한데 goto를 사용하면 간단하게 빠져나올 수 있습니다.

```c
#include <stdio.h>

int main()
{
    int num1 = 0;

    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            if (num1 == 20)    // num1이 20이라면
                goto EXIT;     // 레이블 EXIT로 즉시 이동

            num1++;
        }
    }

EXIT:    // 레이블 EXIT
    printf("%d\n", num1);    // 20

    return 0;
}
```

goto와 예외처리 패턴

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main()
{
    int gender;      // 성별: 남자 1, 여자 2
    int age;         // 나이
    int isOwner;     // 주택 소유 여부: 자가 1, 전월세 0

    scanf("%d %d %d", &gender, &age, &isOwner);

    printf("안녕하세요.\n");
    printf("문을 연다.\n");

    if (gender == 2)
        goto EXIT;    // 에러가 발생했으므로 EXIT로 이동

    if (age < 30)
        goto EXIT;    // 에러가 발생했으므로 EXIT로 이동

    if (isOwner == 0)
        goto EXIT;    // 에러가 발생했으므로 EXIT로 이동
 
EXIT:
    printf("안녕히계세요.\n");    // 에러 처리 코드를
    printf("문을 닫는다.\n");     // 한 번만 사용함

    return 0;    // 프로그램 종료
}
```



##### 포인터

C 언어에서 메모리 주소는 포인터(pointer) 변수에 저장합니다.

메모리 주소 출력방법

```c
#include <stdio.h>

int main()
{
    int num1 = 10;

    printf("%p\n", &num1);    // 008AF7FC: num1의 메모리 주소를 출력
                              // 컴퓨터마다, 실행할 때마다 달라짐

    return 0;
}
```

변수의 메모리 주소

![](https://dojang.io/pluginfile.php/337/mod_page/content/21/unit34-2.png)

> 32비트, 64비트와 메모리 주소
>
> 다음과 같이 시스템이 32비트인지 64비트인지에 따라 메모리 주소의 범위도 달라집니다.
>
> - 32비트: 16진수 8자리
> - - 0x00000000 ~ 0xFFFFFFFF
>   - 예) 0x008AF7FC
> - 64비트: 16진수 16자리
> - - 0x0000000000000000 ~ 0xFFFFFFFFFFFFFFFF
>   - 예) 0x00000000008AF7FC
>   - 64비트 메모리 주소는 0x00000000`00000000처럼 8자리씩 끊어서 `를 붙이기도 합니다.



포인터 변수는 *를 사용하여 선언합니다(포인터 변수는 포인터로 줄여서 부르기도 합니다).

- **자료형 \*포인터이름;**
- **포인터 = &변수;**

```c
#include <stdio.h>

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // int형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    printf("%p\n", numPtr);    // 0055FC24: 포인터 변수 numPtr의 값 출력
                               // 컴퓨터마다, 실행할 때마다 달라짐
    printf("%p\n", &num1);     // 0055FC24: 변수 num1의 메모리 주소 출력
                               // 컴퓨터마다, 실행할 때마다 달라짐

    return 0;
}
```

```c
int* numPtr;     // 자료형 쪽에 *을 붙임
int * numPtr;    // 자료형과 변수 가운데 *를 넣음
int *numPtr;     // 변수 쪽에 *을 붙임
```

![](https://dojang.io/pluginfile.php/338/mod_page/content/22/unit34-3.png)

![](https://dojang.io/pluginfile.php/338/mod_page/content/22/unit34-4.png)

![](https://dojang.io/pluginfile.php/338/mod_page/content/22/unit34-5.png)

> 32비트와 64비트와 포인터 크기
>
> 다음과 같이 시스템이 32비트인지 64비트인지에 따라 포인터의 크기가 달라집니다.
>
> - 32비트: 16진수 8자리
> - - 0x00000000 ~ 0xFFFFFFFF
> - 64비트: 16진수 16자리
> - - 0x0000000000000000 ~ 0xFFFFFFFFFFFFFFFF
>
> sizeof로 포인터의 크기를 구해보면 32비트에서는 4바이트, 64비트에서는 8바이트가 나옵니다.
>
> - **sizeof(포인터)**
> - **sizeof(자료형 \*)**
>
> 32비트
>
> ```c
> int *numPtr;
> printf("%d\n", sizeof(numPtr));    // 4: 32비트에서 int 포인터는 4바이트
> 
> printf("%d\n", sizeof(char *));    // 4: 32비트에서 char 포인터는 4바이트
> ```
>
> 64비트
>
> ```c
> int *numPtr;
> printf("%d\n", sizeof(numPtr));    // 8: 64비트에서 int 포인터는 8바이트
> 
> printf("%d\n", sizeof(char *));    // 8: 64비트에서 char 포인터는 8바이트
> ```



역참조 연산자 사용하기

포인터 변수에는 메모리 주소가 저장되어 있습니다. 이때 메모리 주소가 있는 곳으로 이동해서 값을 가져오고 싶다면 역참조(dereference) 연산자 *를 사용합니다.

```c
#include <stdio.h>

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // 정수형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    printf("%d\n", *numPtr);    // 10: 역참조 연산자로 num1의 메모리 주소에 접근하여 값을 가져옴

    return 0;
}
```

> 포인터 선언과 역참조?
>
> 포인터를 선언할 때도 *를 사용하고 역참조를 할 때도 *를 사용합니다. 같은 * 기호를 사용해서 헷갈리기 쉽지만 선언과 사용을 구분해서 생각하면 됩니다. 즉, 포인터를 선언할 때 *는 "이 변수가 포인터다"라고 알려주는 역할이고, 포인터에 사용할 때 *는 "포인터의 메모리 주소를 역참조하겠다"라는 뜻입니다.
>
> ```c
> int *numPtr;                // 포인터. 포인터를 선언할 때 *
> printf("%d\n", *numPtr);    // 역참조. 포인터에 사용할 때 *
> ```

포인터 변수에 역참조 연산자를 사용한 뒤 값을 저장(할당)

- ***포인터 = 값;**

```c
#include <stdio.h>

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // 정수형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    *numPtr = 20;     // 역참조 연산자로 메모리 주소에 접근하여 20을 저장

    printf("%d\n", *numPtr);    // 20: 역참조 연산자로 메모리 주소에 접근하여 값을 가져옴
    printf("%d\n", num1);       // 20: 실제 num1의 값도 바뀜

    return 0;
}
```

![](https://dojang.io/pluginfile.php/339/mod_page/content/30/unit34-7.png)

```c
int *numPtr;
int num1;

numPtr = &num1;    // numPtr은 int 포인터형이고, &num1은 int형 변수의 주소이므로 자료형이 일치함
                   // numPtr은 pointer to int, &num1은 address of int이므로 자료형이 일치함
```

pointer to int와 address of int는 자료형이 같습니다.

![](https://dojang.io/pluginfile.php/339/mod_page/content/30/unit34-8.png)

변수, 주소 연산자, 역참조 연산자, 포인터의 차이를 정리

![](https://dojang.io/pluginfile.php/339/mod_page/content/30/unit34-9.png)



디버거에서 포인터 확인

```c
#include <stdio.h>

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // 정수형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    *numPtr = 20;     // 역참조 연산자로 메모리 주소에 접근하여 20을 저장

    printf("%d\n", *numPtr);    // 20: 역참조 연산자로 메모리 주소에 접근하여 값을 가져옴
    printf("%d\n", num1);       // 20: 실제 num1의 값도 바뀜

    return 0;
}
```



다양한 자료형의 포인터 선언

```c
#include <stdio.h>

int main()
{
    long long *numPtr1;    // long long형 포인터 선언
    float *numPtr2;        // float형 포인터 선언
    char *cPtr1;           // char형 포인터 선언

    long long num1 = 10;
    float num2 = 3.5f;
    char c1 = 'a';

    numPtr1 = &num1;    // num1의 메모리 주소 저장
    numPtr2 = &num2;    // num2의 메모리 주소 저장
    cPtr1 = &c1;        // c1의 메모리 주소 저장

    printf("%lld\n", *numPtr1);    // 10
    printf("%f\n", *numPtr2);      // 3.500000
    printf("%c\n", *cPtr1);        // a

    return 0;
}
```

![](https://dojang.io/pluginfile.php/340/mod_page/content/22/unit34-23.png)



void포인터

C 언어에서는 자료형이 정해지지 않은 포인터

void 포인터는 자료형이 정해지지 않은 특성 때문에 어떤 자료형으로 된 포인터든 모두 저장할 수 있습니다. 

- **void \*포인터이름;**

```c
#include <stdio.h>

int main()
{
    int num1 = 10;
    char c1 = 'a';
    int *numPtr1 = &num1;
    char *cPtr1 = &c1;

    void *ptr;        // void 포인터 선언

    // 포인터 자료형이 달라도 컴파일 경고가 발생하지 않음
    ptr = numPtr1;    // void 포인터에 int 포인터 저장
    ptr = cPtr1;      // void 포인터에 char 포인터 저장

    // 포인터 자료형이 달라도 컴파일 경고가 발생하지 않음
    numPtr1 = ptr;    // int 포인터에 void 포인터 저장
    cPtr1 = ptr;      // char 포인터에 void 포인터 저장

    return 0;
}
```

![](https://dojang.io/pluginfile.php/341/mod_page/content/22/unit34-24.png)

void 포인터는 되는 게 별로 없어 보이지만 실제로 C 언어에서 다양한 형태로 사용되고 있습니다. 예를 들자면 함수에서 다양한 자료형을 받아들일 때, 함수의 반환 포인터를 다양한 자료형으로 된 포인터에 저장할 때, 자료형을 숨기고 싶을 때 사용합니다.



이중 포인터 

포인터를 선언할 때 *를 두 번 사용하면 포인터의 포인터(이중 포인터)를 선언합니다.

- **자료형 \**포인터이름;**

```cc
#include <stdio.h>

int main()
{
    int *numPtr1;     // 단일 포인터 선언
    int **numPtr2;    // 이중 포인터 선언
    int num1 = 10;

    numPtr1 = &num1;    // num1의 메모리 주소 저장 

    numPtr2 = &numPtr1; // numPtr1의 메모리 주소 저장

    printf("%d\n", **numPtr2);    // 20: 포인터를 두 번 역참조하여 num1의 메모리 주소에 접근

    return 0;
}
```

![](https://dojang.io/pluginfile.php/342/mod_page/content/18/unit34-25.png)

> 포인터를 선언할 때 *의 개수에 따라서 삼중 포인터, 사중 포인터 그 이상도 만들 수 있습니다. 마찬가지로 역참조를 할 때도 *를 세 번, 네 번 또는 그 이상 사용할 수 있습니다.

만약 실제로 존재하는 메모리 주소라면 포인터에 직접 저장할 수 있습니다.

보통 임베디드 시스템이나 마이크로 프로세서에서 제공하는 메모리 주소를 사용할 때 포인터에 직접 저장하기도 합니다.

```c
int *numPtr = 0x00CCFC2C;    // 실제로 존재하는 메모리 주소라면 저장할 수 있음
```



메모리 사용하기

포인터에 원하는 만큼 메모리 공간을 할당받아 사용하는 방법

메모리는 malloc → 사용 → free 패턴으로 사용합니다.

![](https://dojang.io/pluginfile.php/347/mod_page/content/15/unit35-1.png)



메모리를 사용하려면 malloc 함수로 사용할 메모리 공간을 확보해야 합니다(memory allocation). 이때 필요한 메모리 크기는 바이트 단위로 지정합니다(메모리 할당, 해제 함수는 stdlib.h 헤더 파일에 선언되어 있습니다).

- **포인터 = malloc(크기);**
- - **void \*malloc(size_t _Size);**
  - 성공하면 메모리 주소를 반환, 실패하면 NULL을 반환

```c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int num1 = 20;    // int형 변수 선언
    int *numPtr1;     // int형 포인터 선언

    numPtr1 = &num1;  // num1의 메모리 주소를 구하여 numPtr에 할당

    int *numPtr2;     // int형 포인터 선언

    numPtr2 = malloc(sizeof(int));    // int의 크기 4바이트만큼 동적 메모리 할당

    printf("%p\n", numPtr1);    // 006BFA60: 변수 num1의 메모리 주소 출력
                                // 컴퓨터마다, 실행할 때마다 달라짐

    printf("%p\n", numPtr2);     // 009659F0: 새로 할당된 메모리의 주소 출력
                                // 컴퓨터마다, 실행할 때마다 달라짐

    free(numPtr2);    // 동적으로 할당한 메모리 해제

    return 0;
}
```

원하는 시점에 원하는 만큼 메모리를 할당할 수 있다고 하여 동적 메모리 할당(dynamic memory allocation)이라 부릅니다. 여기서 numPtr1에는 일반 변수의 메모리 주소를 할당했고, numPtr2에는 malloc 함수로 메모리를 할당했습니다. 같은 메모리 주소라도 내부적으로는 약간의 차이가 있습니다. 스택과 힙 두 가지인데 변수는 스택(stack)에 생성되며 malloc 함수는 힙(heap) 부분의 메모리를 사용합니다(스택, 힙의 위치와 커지는 방향은 운영체제 및 플랫폼에 따라 달라질 수 있습니다).

![](https://dojang.io/pluginfile.php/348/mod_page/content/31/unit35-2.png)

스택과 힙의 큰 차이점은 메모리 해제입니다. 스택에 생성된 변수는 사용한 뒤 따로 처리를 해주지 않아도 되지만 malloc 함수를 사용하여 힙에서 할당한 메모리는 반드시 해제를 해주어야 합니다. 따라서 다음과 같이 free 함수로 메모리를 해제합니다.

- **free(포인터);**
- - **void free(void \*_Block);**

```c
free(numPtr2);    // 동적으로 할당한 메모리 해제
```

메모리 해제는 선택이 아닌 필수입니다. 예제는 별로 하는 일이 없는 간단한 프로그램이지만 실무에서는 메모리를 자주, 많이 할당합니다. 따라서 메모리를 할당만 하고 해제를 해주지 않으면 결국에는 시스템의 메모리가 부족해지므로 운영체제가 프로그램을 강제로 종료시키거나 메모리 할당에 실패하게 됩니다. 특히 메모리를 해제하지 않아 메모리 사용량이 계속 증가하는 현상을 메모리 누수(memory leak)라 부릅니다.



메모리에 값 저장하기

```c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int *numPtr;    // int형 포인터 선언

    numPtr = malloc(sizeof(int));    // int의 크기 4바이트만큼 동적 메모리 할당

    *numPtr = 10;   // 포인터를 역참조한 뒤 값 할당

    printf("%d\n", *numPtr);    // 10: 포인터를 역참조하여 메모리에 저장된 값 출력

    free(numPtr);    // 동적 메모리 해제

    return 0;
}
```



메모리내용 한꺼번에 설정

memset 함수를 사용하면 메모리의 내용을 원하는 크기만큼 특정값으로 설정할 수 있으며 함수 이름은 memory set에서 따왔습니다(string.h 헤더 파일에 선언되어 있습니다). 이때 설정하는 크기는 바이트 단위입니다.

- **memset(포인터, 설정할값, 크기);**
- - **void \*memset(void *_Dst, int _Val, size_t _Size);**
  - 값 설정이 끝난 포인터를 반환

```c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일
#include <string.h>    // memset 함수가 선언된 헤더 파일

int main()
{
    long long *numPtr = malloc(sizeof(long long));  // long long의 크기 8바이트만큼 동적 메모리 할당

    memset(numPtr, 0x27, 8);    // numPtr이 가리키는 메모리를 8바이트만큼 0x27로 설정

    printf("0x%llx\n", *numPtr);    // 0x2727272727272727: 27이 8개 들어가 있음

    free(numPtr);    // 동적으로 할당한 메모리 해제

    return 0;
}
```

memset 함수는 주로 다음과 같이 설정할 값을 0으로 지정하여 메모리의 내용을 모두 0으로 만들 때 주로 사용합니다.

```c
emset(numPtr, 0, 8);    // numPtr이 가리키는 메모리를 8바이트만큼 0으로 설정
```

> 자료형의 크기와 포인터의 크기
>
> memset 함수에 설정할 크기를 지정할 때 보통 숫자 대신 sizeof를 사용합니다.
>
> ```c
> long long *numPtr = malloc(sizeof(long long));
> 
> memset(numPtr, 0, sizeof(long long));   
> // numPtr이 가리키는 메모리를 long long 크기만큼 0으로 설정
> ```
>
> 메모리를 sizeof(long long)크기만큼 할당했으므로 설정할 크기도 sizeof(long long)과 같이 지정해야 하며 sizeof(long long *)과 같이 포인터의 크기를 지정하면 안 됩니다.
>
> ```c
> char *cPtr = malloc(sizeof(char));    // char의 크기 1바이트만큼 동적 메모리 할당
> 
> memset(cPtr, 0, sizeof(char));    
> // char의 크기 1바이트만큼 0으로 설정(올바른 방법)
> memset(cPtr, 0, sizeof(char *)); 
> // 32비트: char 포인터의 크기 4바이트만큼 0으로 설정(잘못된 방법)
> // 64비트: char 포인터의 크기 8바이트만큼 0으로 설정(잘못된 방법)
> free(cPtr);
> ```
>
> memset(numPtr, 0, sizeof(char));는 메모리를 1바이트만큼 0으로 설정하니 문제가 없습니다. 하지만 memset(numPtr, 0, sizeof(char *));는 32비트에서 4바이트, 64비트에서 8바이트만큼 0으로 설정하므로 할당받은 메모리 크기를 넘어서게 됩니다.
>
> 다른 예로 32비트에서 sizeof(long long)은 8바이트인데 sizeof(long long *)는 4바이트이므로 할당받은 메모리보다 작은 공간을 설정하게 됩니다(64비트에서 sizeof(long long *)는 8이라 그냥 크기가 일치한 것일 뿐 잘못된 방법입니다).
>
> ```c
> long long *numPtr = malloc(sizeof(long long)); 
> // long long의 크기 8바이트만큼 동적 메모리 할당
> 
> memset(numPtr, 0, sizeof(long long));  
> // long long의 크기 8바이트만큼 0으로 설정(올바른 방법)
> 
> memset(numPtr, 0, sizeof(long long *)); 
> // 32비트: long long 포인터의 크기 4바이트만큼 0으로 설정(잘못된 방법)
> // 64비트: long long 포인터의 크기 8바이트만큼 0으로 설정(잘못된 방법)
> free(numPtr);
> ```
>
> memset 함수에서 sizeof를 사용할 때는 이러한 부분을 주의해야 합니다.



널 포인터 사용하기

```c
#include <stdio.h>

int main()
{
    int *numPtr1 = NULL;    // 포인터에 NULL 저장

    printf("%p\n", numPtr1);    // 00000000

    return 0;
}
```

NULL이 들어있는 포인터를 널 포인터(null pointer)라고 하며 아무것도 가리키지 않는 상태를 뜻합니다. 따라서 역참조는 할 수 없습니다.

실무에서는 다음과 같이 포인터가 NULL인지 확인한 뒤 NULL이면 메모리를 할당하는 패턴을 주로 사용합니다.

```c
if (ptr == NULL)         // ptr이 널 포인터라면
{
    ptr = malloc(1024);   // 1024바이트만큼 메모리 할당
}
```



배열
배열 선언 및 초기화

- **자료형 배열이름[크기];**
- **자료형 배열이름[크기] = { 값, 값, 값 };**

```c
#include <stdio.h>

int main()
{
    int numArr[10] = { 11, 22, 33, 44, 55, 66, 77, 88, 99, 110 };    // 배열을 생성하고 값 할당

    printf("%d\n", numArr[0]);    // 11: 배열의 첫 번째(인덱스 0) 요소 출력
    printf("%d\n", numArr[5]);    // 66: 배열의 여섯 번째(인덱스 5) 요소 출력
    printf("%d\n", numArr[9]);    // 110: 배열의 열 번째(인덱스 9) 요소 출력

    return 0;
}
```



배열 0으로 초기화

```c
#include <stdio.h>

int main()
{
    int numArr[10] = { 0, };      // 배열의 요소를 모두 0으로 초기화

    printf("%d\n", numArr[0]);    // 0: 배열의 첫 번째(인덱스 0) 요소 출력
    printf("%d\n", numArr[5]);    // 0: 배열의 여섯 번째(인덱스 5) 요소 출력
    printf("%d\n", numArr[9]);    // 0: 배열의 열 번째(인덱스 9) 요소 출력

    return 0;
}
```

```c
#include <stdio.h>

int main()
{
    int numArr[10];    // 크기가 10인 배열 선언

    numArr[0] = 11;    // 인덱스가 0인 배열의 요소에 값 할당
    numArr[1] = 22;    // 인덱스가 1인 배열의 요소에 값 할당
    numArr[2] = 33;    // 인덱스가 2인 배열의 요소에 값 할당
    numArr[3] = 44;    // 인덱스가 3인 배열의 요소에 값 할당
    numArr[4] = 55;    // 인덱스가 4인 배열의 요소에 값 할당
    numArr[5] = 66;    // 인덱스가 5인 배열의 요소에 값 할당
    numArr[6] = 77;    // 인덱스가 6인 배열의 요소에 값 할당
    numArr[7] = 88;    // 인덱스가 7인 배열의 요소에 값 할당
    numArr[8] = 99;    // 인덱스가 8인 배열의 요소에 값 할당
    numArr[9] = 110;   // 인덱스가 9인 배열의 요소에 값 할당

    printf("%d\n", numArr[-1]);    // 음수이므로 잘못된 인덱스 쓰레기값 출력
    printf("%d\n", numArr[10]);    // 배열의 범위를 벗어난 인덱스 쓰레기값 출력
    printf("%d\n", numArr[20]);    // 배열의 범위를 벗어난 인덱스 쓰레기값 출력

    return 0;
}
```

배열의 요소에 접근할 때 인덱스로 음수를 지정하거나, 배열의 크기를 벗어난 인덱스를 지정해도 컴파일 에러가 발생하지 않습니다. 하지만 실행을 해보면 쓰레기값이 출력됩니다. 즉, 배열의 범위를 벗어난 인덱스에 접근하면 배열이 아닌 다른 메모리 공간에 접근하게 됩니다. 만약 배열의 범위를 벗어난 접근을 하여 값을 할당해버리면 엉뚱한 메모리에 값을 저장하게 되어 프로그램이 정상적으로 실행되지 않을 수 있으므로 주의해야 합니다.



배열의 크기 구하기

```c
#include <stdio.h>

int main()
{
    int numArr[10] = { 11, 22, 33, 44, 55, 66, 77, 88, 99, 110 };    // 크기가 10인 int형 배열

    printf("%d\n", sizeof(numArr));                  // 40: 4바이트 크기의 요소가 10개이므로 40
    printf("%d\n", sizeof(numArr) / sizeof(int));    // 10: 배열의 크기를 구할 때는
                                                     // 전체 공간을 요소의 크기로 나눠줌

    return 0;
}
```



배열 내용 출력

```c
#include <stdio.h>

int main()
{
    int numArr[10] = { 11, 22, 33, 44, 55, 66, 77, 88, 99, 110 };    // 크기가 10인 int형 배열

    for (int i = 0; i < sizeof(numArr) / sizeof(int); i++)    // 배열의 요소 개수만큼 반복
    {
        printf("%d\n", numArr[i]);    // 배열의 인덱스에 반복문의 변수 i를 지정
    }

    return 0;
}
```



배열을 포인터에 저장

```c
#include <stdio.h>

int main()
{
    int numArr[10] = { 11, 22, 33, 44, 55, 66, 77, 88, 99, 110 };    // 크기가 10인 int형 배열

    int *numPtr = numArr;       // 포인터에 int형 배열을 할당

    printf("%d\n", *numPtr);    // 11: 배열의 주소가 들어있는 포인터를 역참조하면 배열의 
                                // 첫 번째 요소에 접근

    printf("%d\n", *numArr);    // 11: 배열 자체를 역참조해도 배열의 첫 번째 요소에 접근

    printf("%d\n", numPtr[5]);  // 66: 배열의 주소가 들어있는 포인터는 인덱스로 접근할 수 있음

    printf("%d\n", sizeof(numArr));    // 40: sizeof로 배열의 크기를 구하면 배열이 메모리에 
                                       // 차지하는 공간이 출력됨

    printf("%d\n", sizeof(numPtr));    // 4 : sizeof로 배열의 주소가 들어있는 포인터의 크기를 
                                       // 구하면 포인터의 크기가 출력됨(64비트라면 8)

    return 0;
}
```



배열을 활용하여 10진수를 2진수로 변환하기

```c
#include <stdio.h>

int main()
{
    int decimal = 13;
    int binary[20] = { 0, };

    int position = 0;
    while (1)
    {
        binary[position] = decimal % 2;    // 2로 나누었을 때 나머지를 배열에 저장
        decimal = decimal / 2;             // 2로 나눈 몫을 저장

        position++;    // 자릿수 변경

        if (decimal == 0)    // 몫이 0이 되면 반복을 끝냄
            break;
    }

    // 배열의 요소를 역순으로 출력
    for (int i = position - 1; i >= 0; i--)
    {
        printf("%d", binary[i]);
    }

    printf("\n");

    return 0;
}
```



##### 2차원 배열

2차원 배열 출력

```c
#include <stdio.h>

int main()
{
    int numArr[3][4] = {    // 세로 크기 3, 가로 크기 4인 int형 2차원 배열 선언
        { 11, 22, 33, 44 },
        { 55, 66, 77, 88 },
        { 99, 110, 121, 132 }
    };
                       // ↓ 세로 인덱스
    printf("%d\n", numArr[0][0]);    // 11 : 세로 인덱스 0, 가로 인덱스 0인 요소 출력
    printf("%d\n", numArr[1][2]);    // 77 : 세로 인덱스 1, 가로 인덱스 2인 요소 출력
    printf("%d\n", numArr[2][0]);    // 99 : 세로 인덱스 2, 가로 인덱스 0인 요소 출력
    printf("%d\n", numArr[2][3]);    // 132: 세로 인덱스 2, 가로 인덱스 2인 요소 출력
                          // ↑ 가로 인덱스

    return 0;
}
```



2차원 배열 0으로 초기화

```c
#include <stdio.h>

int main()
{
    int numArr[3][4] = { 0, };       // 2차원 배열의 요소를 모두 0으로 초기화

    printf("%d\n", numArr[0][0]);    // 0: 세로 인덱스 0, 가로 인덱스 0인 요소 출력
    printf("%d\n", numArr[1][2]);    // 0: 세로 인덱스 1, 가로 인덱스 2인 요소 출력
    printf("%d\n", numArr[2][0]);    // 0: 세로 인덱스 2, 가로 인덱스 0인 요소 출력
    printf("%d\n", numArr[2][3]);    // 0: 세로 인덱스 2, 가로 인덱스 3인 요소 출력

    return 0;
}
```

> 2차원 배열의 요소에 접근할 때 인덱스로 음수를 지정하거나, 배열의 크기를 벗어난 인덱스를 지정해도 컴파일 에러가 발생하지 않습니다. 하지만 실행을 해보면 쓰레기값이 출력됩니다. 즉, 배열의 범위를 벗어난 인덱스에 접근하면 배열이 아닌 다른 메모리 공간에 접근하게 됩니다



2차원 배열 크기 구하기

```c
#include <stdio.h>

int main()
{
    int numArr[3][4] = {    // 세로 크기 3, 가로 크기 4인 int형 2차원 배열 선언
        { 11, 22, 33, 44 },
        { 55, 66, 77, 88 },
        { 99, 110, 121, 132 }
    };

    printf("%d\n", sizeof(numArr));    // 48: 4바이트 크기의 요소가 12(4*3)개이므로 48

    int col = sizeof(numArr[0]) / sizeof(int);    // 4: 2차원 배열의 가로 크기를 구할 때는 
                                                  // 가로 한 줄의 크기를 요소의 크기로 나눠줌

    int row = sizeof(numArr) / sizeof(numArr[0]); // 3: 2차원 배열의 세로 크기를 구할 때는 
                                    // 배열이 차지하는 전체 공간을 가로 한 줄의 크기로 나눠줌

    printf("%d\n", col);    // 4
    printf("%d\n", row);    // 3

    return 0;
}
```



2차원 배열 출력

```c
#include <stdio.h>

int main()
{
    int numArr[3][4] = {    // 세로 크기 3, 가로 크기 4인 int형 2차원 배열 선언
        { 11, 22, 33, 44 },
        { 55, 66, 77, 88 },
        { 99, 110, 121, 132 }
    };

    int col = sizeof(numArr[0]) / sizeof(int);    // 4: 2차원 배열의 가로 크기를 구할 때는 
                                                  // 가로 한 줄의 크기를 요소의 크기로 나눠줌

    int row = sizeof(numArr) / sizeof(numArr[0]); // 3: 2차원 배열의 세로 크기를 구할 때는 
                                    // 배열이 차지하는 전체 공간을 가로 한 줄의 크기로 나눠줌

    for (int i = 0; i < row; i++)    // 2차원 배열의 세로 크기만큼 반복
    {
        for (int j = 0; j < col; j++)    // 2차원 배열의 가로 크기만큼 반복
        {
            printf("%d ", numArr[i][j]); // 2차원 배열의 인덱스에 반복문의 변수 i, j를 지정
        }
        printf("\n");                // 가로 요소를 출력한 뒤 다음 줄로 넘어감
    }

    return 0;
}
```



2차원 배열 포인터 사용

- **자료형 (\*포인터이름)[가로크기];**

```c
int (*numPtr)[4];
```

```c
#include <stdio.h>

int main()
{
    int numArr[3][4] = {    // 세로 3, 가로 4 크기의 int형 2차원 배열 선언
        { 11, 22, 33, 44 },
        { 55, 66, 77, 88 },
        { 99, 110, 121, 132 }
    };

    int (*numPtr)[4] = numArr;

    printf("%p\n", *numPtr); // 002BFE5C: 2차원 배열 포인터를 역참조하면 세로 첫 번째의 주소가 나옴
                             // 컴퓨터마다, 실행할 때마다 달라짐

    printf("%p\n", *numArr); // 002BFE5C: 2차원 배열을 역참조하면 세로 첫 번째의 주소가 나옴
                             // 컴퓨터마다, 실행할 때마다 달라짐

    printf("%d\n", numPtr[2][1]);    // 110: 2차원 배열 포인터는 인덱스로 접근할 수 있음

    printf("%d\n", sizeof(numArr));  // 48: sizeof로 2차원 배열의 크기를 구하면 배열이 메모리에 
                                     // 차지하는 공간이 출력됨

    printf("%d\n", sizeof(numPtr));  // 4 : sizeof로 2차원 배열 포인터의 크기를 
                                     // 구하면 포인터의 크기가 출력됨(64비트라면 8)

    return 0;
}
```



포인터와 배열 응용하기

```c
#define _CRT_SECURE_NO_WARNING
#include <stdio.h>

int main()
{
    int size;

    scanf("%d", &size);  // 배열의 크기를 입력받음

    int numArr[size];    // GCC에서는 사용 가능, Visual Studio 2015에서는 컴파일 에러

    return 0;
}
```



포인터에 할당된 메모리 배열처럼 사용

포인터를 배열처럼 사용하는 방법은 간단합니다. 포인터에 malloc 함수로 메모리를 할당해주면 됩니다. 

- **자료형 \*포인터이름 = malloc(sizeof(자료형) * 크기);**

```c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int *numPtr = malloc(sizeof(int) * 10);    // int 10개 크기만큼 동적 메모리 할당

    numPtr[0] = 10;    // 배열처럼 인덱스로 접근하여 값 할당
    numPtr[9] = 20;    // 배열처럼 인덱스로 접근하여 값 할당

    printf("%d\n", numPtr[0]);    // 배열처럼 인덱스로 접근하여 값 출력
    printf("%d\n", numPtr[9]);    // 배열처럼 인덱스로 접근하여 값 출력

    free(numPtr);    // 동적으로 할당한 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/381/mod_page/content/23/unit38-1.png)

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int size;

    scanf("%d", &size);

    int *numPtr = malloc(sizeof(int) * size);    // (int 크기 * 입력받은 크기)만큼 동적 메모리 할당

    for (int i = 0; i < size; i++)    // 입력받은 크기만큼 반복
    {
        numPtr[i] = i;                // 인덱스로 접근하여 값 할당
    }

    for (int i = 0; i < size; i++)    // 입력받은 크기만큼 반복
    {
        printf("%d\n", numPtr[i]);    // 인덱스로 접근하여 값 출력
    }

    free(numPtr);    // 동적으로 할당한 메모리 해제

    return 0;
}
```



포인터에 할당된 메모리 2차원 배열처럼 사용

- **자료형 \**포인터이름 = malloc(sizeof(자료형 *) * 세로크기);**와 같이 세로 공간 메모리 할당
- - 반복문으로 반복하면서 **포인터[i] = malloc(sizeof(자료형) \* 가로크기);**와 같이 가로 공간 메모리 할당
  - 반복문으로 반복하면서 **free(포인터[i]);**와 같이 가로 공간 메모리 해제
  - **free(포인터);**와 같이 세로 공간 메모리 해제

```c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int **m = malloc(sizeof(int *) * 3);   // 이중 포인터에 (int 포인터 크기 * 세로 크기)만큼
                                           // 동적 메모리 할당. 배열의 세로

    for (int i = 0; i < 3; i++)            // 세로 크기만큼 반복
    {
        m[i] = malloc(sizeof(int) * 4);    // (int 크기 * 가로 크기)만큼 동적 메모리 할당.
                                           // 배열의 가로
    }

    m[0][0] = 1;    // 세로 인덱스 0, 가로 인덱스 0인 요소에 값 할당
    m[2][0] = 5;    // 세로 인덱스 2, 가로 인덱스 0인 요소에 값 할당
    m[2][3] = 2;    // 세로 인덱스 2, 가로 인덱스 3인 요소에 값 할당

    printf("%d\n", m[0][0]);    // 1: 세로 인덱스 0, 가로 인덱스 0인 요소의 값 출력
    printf("%d\n", m[2][0]);    // 5: 세로 인덱스 2, 가로 인덱스 0인 요소의 값 출력
    printf("%d\n", m[2][3]);    // 2: 세로 인덱스 2, 가로 인덱스 3인 요소의 값 출력

    for (int i = 0; i < 3; i++)    // 세로 크기만큼 반복
    {
        free(m[i]);                // 2차원 배열의 가로 공간 메모리 해제
    }

    free(m);    // 2차원 배열의 세로 공간 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/383/mod_page/content/22/unit38-2.png)

![](https://dojang.io/pluginfile.php/383/mod_page/content/22/unit38-3.png)



