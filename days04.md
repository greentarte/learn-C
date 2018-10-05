문자열

C 언어에서는 문자 자료형인 char는 있지만 문자열을 저장하는 자료형은 없습니다. 

문자열은 char 포인터 형식으로 사용합니다.

```c
#include <stdio.h>

int main()
{
    char c1 = 'a';         // 변수에 문자 'a' 저장
    char *s1 = "Hello";    // 포인터에 문자열 "Hello"의 주소 저장

    printf("%c\n", c1);    // a: %c로 문자 출력
    printf("%s\n", s1);    // Hello: %s로 문자열 출력

    return 0;
}
```

![](https://dojang.io/pluginfile.php/392/mod_page/content/33/unit39-1.png)

C 언어의 문자열은 마지막에 항상 널 문자(NULL)가 붙는다는 점입니다. NULL은 0으로도 표현할 수 있으며 문자열의 **끝**을 나타냅니다. 그래서 printf는 문자열을 출력할 때 문자열을 계속 출력하다가 NULL에서 출력을 끝냅니다.

![](https://dojang.io/pluginfile.php/392/mod_page/content/33/unit39-2.png)



문자열 포인터에 인덱스로 문자에 접근

```c
#include <stdio.h>

int main()
{
    char *s1 = "Hello";       // 포인터에 문자열 Hello의 주소 저장

    printf("%c\n", s1[1]);    // e: 인덱스 1(두 번째)의 문자 출력
    printf("%c\n", s1[4]);    // o: 인덱스 4(다섯 번째)의 문자 출력
    printf("%c\n", s1[5]);    // 문자열 맨 뒤의 NULL(\0) 출력. NULL은 화면에 표시되지 않음

    return 0;
}
```

문자열 리터럴이 있는 메모리 주소는 읽기 전용이기 때문입니다. 따라서 문자열 포인터는 인덱스로 접근하여 문자를 할당하면 안 됩니다.



배열형태로 문자열 선언

- **char 배열이름[크기] = "문자열";**

```c
#include <stdio.h>

int main()
{
    char s1[10] = "Hello";  // 크기가 10인 char형 배열을 선언하고 문자열 할당

    printf("%s\n", s1);     // Hello: %s로 문자열 출력

    return 0;
}
```

![](https://dojang.io/pluginfile.php/394/mod_page/content/30/unit39-3.png)

배열에 문자열과 NULL을 저장한 뒤 남는 요소들은 딱히 신경 쓸 필요는 없습니다. 보통 남는 공간에는 모두 NULL이 들어갑니다. 배열로 문자열을 사용할 때 한 가지 주의할 점은 배열을 선언한 즉시 문자열로 초기화해야 한다는 점입니다. 배열을 미리 선언해놓고 문자열을 나중에 할당할 수는 없습니다.



문자열을 배열에 저장할 때 배열의 최소크기

![](https://dojang.io/pluginfile.php/394/mod_page/content/30/unit39-4.png)

다음과 같이 문자 배열을 선언하면서 문자열을 바로 할당할 때는 배열의 크기를 생략할 수 있습니다.

- **char 배열이름[] = "문자열";**

```c
#include <stdio.h>

int main()
{
    char s1[] = "Hello";    // 문자열을 할당할 때 배열의 크기를 생략하는 방법

    printf("%s\n", s1);     // Hello: %s로 문자열 출력

    return 0;
}
```

배열 형태의 문자열은 인덱스로 접근하여 문자를 할당할 수 있습니다.

```c
#include <stdio.h>

int main()
{
    char s1[10] = "Hello";    // 크기가 10인 char형 배열을 선언하고 문자열 할당
                              // 배열에 문자열이 복사됨

    s1[0] = 'A';              // 문자 배열의 인덱스 0에 문자 A를 할당

    printf("%s\n", s1);       // Aello: 바뀐 문자열이 출력됨

    return 0;
}
```



입력값을 문자열에 저장

scanf 함수에서 서식 지정자로 %s를 사용하면 입력 값을 배열 형태의 문자열에 저장할 수 있습니다(stdio.h 헤더 파일에 선언되어 있습니다).

- **scanf("%s", 배열);**

- - **int scanf(char const \* const _Format, ...);**
  - 성공하면 가져온 값의 개수를 반환, 실패하면 EOF(-1)를 반환

```c
#define _CRT_SECURE_NO_WARNINGS // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    char s1[10];    // 크기가 10인 char형 배열을 선언

    printf("문자열을 입력하세요: ");
    scanf("%s", s1);     // 표준 입력을 받아서 배열 형태의 문자열에 저장

    printf("%s\n", s1);  // 문자열의 내용을 출력

    return 0;
}
```

![](https://dojang.io/pluginfile.php/400/mod_page/content/34/unit40-1.png)

scanf에서 서식 지정자 %s로 문자열을 저장할 때 입력된 문자열에 공백이 있다면 배열에는 공백 직전까지만 저장됩니다. 예를 들어 중간에 공백이 있는 Hello, world!를 입력하면 Hello,까지만 저장됩니다.

> 공백까지 포함하여 입력받기
>
> scanf 함수에서 서식 지정자를 아래와 같이 지정하면 공백까지 포함하여 문자열을 입력받을 수 있습니다.
>
> ```c
> char s1[30];
> 
> printf("문자열을 입력하세요: ");
> scanf("%[^\n]s", s1);    // 공백까지 포함하여 문자열 입력받기
> 
> printf("%s\n", s1);
> ```
>
> 실행 결과
>
> ```ㅊ
> 문자열을 입력하세요: Hello, world! (입력)
> Hello, world!
> ```
>
>  
>
> EOF
>
> EOF는 End Of File의 약자인데 더 이상 값을 읽을 수 없는 상태를 나타냅니다(말 그대로 파일의 끝이기도 합니다. 파일의 끝에서는 값을 읽을 수가 없죠). 콘솔(터미널, 명령 프롬프트)에서는 다음 키의 입력을 EOF로 정해놓았습니다.
>
> - Windows: Ctrl+Z
> - 리눅스: Ctrl+D
>
> ```c
> int c1 = getchar();     // 문자를 입력받음
> printf("%d\n", c1);
> printf("%d\n", EOF);    // -1
> ```
>
> 소스를 컴파일하여 실행한 뒤 Ctrl+Z를 입력하면 다음과 같이 출력됩니다.
>
> 실행 결과(Windows)
>
> ```
> ^Z (Ctrl+Z 입력)
> -1
> -1
> ```
>
> EOF는 stdio.h 헤더 파일에 정의되어 있으며 정수 -1입니다. 보통 EOF는 파일 처리 함수가 실패했을 때 반환됩니다.



입력값을 문자열 포인터에 저장

입력 값을 문자열 포인터에 저장하려면 문자열이 들어갈 공간을 따로 마련해야 됩니다. 따라서 다음과 같이 malloc 함수로 메모리를 할당한 뒤 문자열을 저장합니다.

- **scanf("%s", 문자열포인터);**

```c
#define _CRT_SECURE_NO_WARNINGS     // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char *s1 = malloc(sizeof(char) * 10);    // char 10개 크기만큼 동적 메모리 할당

    printf("문자열을 입력하세요: ");
    scanf("%s", s1);      // 표준 입력을 받아서 메모리가 할당된 문자열 포인터에 저장

    printf("%s\n", s1);   // 문자열의 내용을 출력

    free(s1);    // 동적 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/401/mod_page/content/27/unit40-3.png)

scanf에서 서식 지정자 %s로 문자열을 저장할 때 입력된 문자열에 공백이 있다면 문자열 포인터에는 공백 직전까지만 저장됩니다. 예를 들어 중간에 공백이 있는 Hello, world!를 입력하면 Hello,까지만 저장됩니다.



문자열 여러 개 입력받기

공백으로 구분된 문자열 두 개를 입력받아보겠습니다.

- **scanf("%s %s ...", 배열1, 배열2, ...);**
- **scanf("%s %s ...", 문자열포인터1, 문자열포인터2, ...);**

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    char s1[10];    // 크기가 10인 char형 배열을 선언
    char s2[10];    // 크기가 10인 char형 배열을 선언

    printf("문자열을 두 개 입력하세요: ");
    scanf("%s %s", s1, s2);    // 표준 입력에서 공백으로 구분된 문자열 두 개를 입력받음

    printf("%s\n", s1);    // s1의 내용을 출력
    printf("%s\n", s2);    // s2의 내용을 출력

    return 0;
}
```

![](https://dojang.io/pluginfile.php/402/mod_page/content/21/unit40-4.png)



문자열 길이 및 비교

문자열 길이

문자열의 길이는 strlen 함수로 구할 수 있으며 함수 이름은 문자열 길이(string length)에서 따왔습니다(string.h 헤더 파일에 선언되어 있습니다).

- **strlen(문자열포인터);**

- **strlen(문자배열);**

- - **size_t strlen(const \*_Str);**
  - 문자열의 길이를 반환

```c
#include <stdio.h>
#include <string.h>    // strlen 함수가 선언된 헤더 파일

int main()
{
    char *s1 = "Hello";       // 포인터에 문자열 Hello의 주소 저장
    char s2[10] = "Hello";    // 크기가 10인 char형 배열을 선언하고 문자열 할당

    printf("%d\n", strlen(s1));    // 5: strlen 함수로 문자열의 길이를 구함
    printf("%d\n", strlen(s2));    // 5: strlen 함수로 문자열의 길이를 구함

    return 0;
}
```

strlen으로 문자열 길이를 구할 때는 순수하게 문자열의 길이만 구하며 NULL 부분은 포함하지 않습니다.

![](https://dojang.io/pluginfile.php/409/mod_page/content/27/unit41-1.png)



문자열 비교

strcmp 함수를 사용하면 두 문자열이 같은지 비교할 수 있으며 함수 이름은 문자열을 비교하다(string compare)에서 따왔습니다(string.h 헤더 파일에 선언되어 있습니다).

- **strcmp(문자열1, 문자열2);**

- - **int strcmp(const \*_Str1, char const *_Str2);**
  - 문자열 비교 결과를 반환

```c
#include <stdio.h>
#include <string.h>    // strcmp 함수가 선언된 헤더 파일

int main()
{
    char s1[10] = "Hello";
    char *s2 = "Hello";

    int ret = strcmp(s1, s2);    // 두 문자열이 같은지 문자열 비교

    printf("%d\n", ret);         // 0: 두 문자열이 같으면 0

    return 0;
}
```

strcmp(s1, s2);와 같이 strcmp 함수에 비교할 문자열을 넣어주면 결과를 정수로 반환합니다(문자열을 비교할 때 대소문자를 구분함).

- -1: ASCII 코드 기준으로 문자열2(s2)가 클 때
- 0: ASCII 코드 기준으로 두 문자열이 같을 때
- 1: ASCII 코드 기준으로 문자열1(s1)이 클 때

strcmp 함수는 문자열에서 첫 번째 문자부터 차례대로 비교하며 비교 기준은 각 문자의 ASCII 코드입니다. 다음과 같이 a, b, c로 문자열을 만들면 이해하기 쉽습니다.

```c
#include <stdio.h>
#include <string.h>    // strcmp 함수가 선언된 헤더 파일

int main()
{
    // aaa는 ASCII 코드로 97 97 97
    // aab는 ASCII 코드로 97 97 98
    // aac는 ASCII 코드로 97 97 99

    printf("%d\n", strcmp("aaa", "aaa"));    //  0: aaa와 aaa는 같으므로 0
    printf("%d\n", strcmp("aab", "aaa"));    //  1: aab와 aaa 중에서 aab가 크므로 1
    printf("%d\n", strcmp("aab", "aac"));    // -1: aab와 aac 중에서 aac가 크므로 -1

    return 0;
}
```

![](https://dojang.io/pluginfile.php/410/mod_page/content/28/unit41-2.png)



입력된 문자열 비교

```c
#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcmp 함수가 선언된 헤더 파일

int main()
{
    char s1[20];
    char s2[20];

    printf("문자열 두 개를 입력하세요: ");
    scanf("%s %s", s1, s2);

    int ret = strcmp(s1, s2);    // 입력된 문자열 비교

    switch (ret)
    {
    case 0:
        printf("두 문자열이 같음\n");
        break;
    case 1:
        printf("%s보다 %s가 큼\n", s2, s1);
        break;
    case -1:
        printf("%s보다 %s가 큼\n", s1, s2);
        break;
    }

    return 0;
}
```



문자열 복사하기

문자열은 다른 배열이나 포인터(메모리)로 복사할 수 있습니다. strcpy 함수는 문자열을 다른 곳으로 복사하며 함수 이름은 string copy에서 따왔습니다(string.h 헤더 파일에 선언되어 있습니다).

- **strcpy(대상문자열, 원본문자열);**

- - **char \*strcpy(char *_Dest, char const *_Source);**
  - 대상문자열의 포인터를 반환

```c
#define _CRT_SECURE_NO_WARNINGS    // strcpy 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcpy 함수가 선언된 헤더 파일

int main()
{
    char s1[10] = "Hello";    // 크기가 10인 char형 배열을 선언하고 문자열 할당
    char s2[10];              // 크기가 10인 char형 배열을 선언

    strcpy(s2, s1);        // s1의 문자열을 s2로 복사
    
    printf("%s\n", s2);    // Hello

    return 0;
}
```

![](https://dojang.io/pluginfile.php/422/mod_page/content/37/unit42-1.png)

읽기 전용메모리에서는 문자열을 복사할 수 없음(포인터로 저장한 문자열 - 읽기 전용 메모리)

![](https://dojang.io/pluginfile.php/422/mod_page/content/37/unit42-2.png)

> 문자열과 읽기 전용 메모리
>
> char *s1 = "Hello"; char *s2 = "";과 같은 문자열 포인터에 할당된 문자열 리터럴은 왜 읽기 전용일까요?
>
> C 언어 컴파일러는 문자열 포인터에 할당한 문자열 리터럴을 실행 파일의 읽기 전용 데이터 섹션(데이터 세그먼트)에 배치하기 때문입니다. 따라서 실행 파일이 실행된 뒤에는 읽기 전용 메모리가 되며 쓰기를 할 수 없습니다. 다음은 각 운영체제별 읽기 전용 데이터 섹션 이름입니다.
>
> - Windows PE: .rdata
> - 리눅스 ELF: .rodata
> - OS X Mach-O: __TEXT, __cstring

문자열 포인터에 문자열을 복사하려면 문자열이 들어갈 공간을 따로 마련해야 됩니다. 따라서 다음과 같이 malloc 함수로 메모리를 할당한 뒤 문자열을 복사합니다.

```c
#define _CRT_SECURE_NO_WARNINGS    // strcpy 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcpy 함수가 정의된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char *s1 = "hello";                      // 문자열 포인터
    char *s2 = malloc(sizeof(char) * 10);    // char 10개 크기만큼 동적 메모리 할당

    strcpy(s2, s1);        // s1의 문자열을 s2로 복사

    printf("%s\n", s2);    // Hello

    free(s2);    // 동적 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/422/mod_page/content/37/unit42-3.png)



문자열 붙이기

문자열은 strcat 함수를 사용하여 서로 붙일 수 있으며 함수 이름은 문자열을 연결시키다(string concatenate)에서 따왔습니다(string.h 헤더 파일에 선언되어 있습니다).

- **strcat(최종문자열, 붙일문자열);**

- - **char \*strcat(char *_Destination, char const *_Source);**
  - 최종 문자열의 포인터를 반환

```c
#define _CRT_SECURE_NO_WARNINGS    // strcat 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcat 함수가 선언된 헤더 파일

int main()
{
    char s1[10] = "world";
    char s2[20] = "Hello"; // s2 뒤에 붙일 것이므로 배열 크기를 크게 만듦

    strcat(s2, s1);        // s2 뒤에 s1를 붙임

    printf("%s\n", s2);    // Helloworld

    return 0;
}
```

여기서 주의할 부분은 최종 결과가 나올 문자열의 배열 크기입니다. 문자열을 붙이더라도 배열이 모자라지 않도록 크기를 넉넉하게 만듭니다(NULL까지 들어갈 수 있도록).

![](https://dojang.io/pluginfile.php/423/mod_page/content/27/unit42-4.png)

문자열 포인터는 읽기 전용 메모리라서 문자열을 붙일 수 없습니다.

![](https://dojang.io/pluginfile.php/423/mod_page/content/27/unit42-5.png)

```c
#define _CRT_SECURE_NO_WARNINGS    // strcpy 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcat 함수가 선언된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char *s1 = "world";                      // 문자열 포인터
    char *s2 = malloc(sizeof(char) * 20);    // char 20개 크기만큼 동적 메모리 할당

    strcpy(s2, "Hello");   // s2에 Hello 문자열 복사

    strcat(s2, s1);       // s2 뒤에 s1을 붙임

    printf("%s\n", s2);   // Helloworld

    free(s2);    // 동적 메모리 해제

    return 0;
}
```



배열형태의 문자열 포인터에 복사 

```c
#define _CRT_SECURE_NO_WARNINGS    // strcpy 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcpy 함수가 선언된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char s1[10] = "Hello";                   // 크기가 10인 char형 배열을 선언하고 문자열 할당
    char *s2 = malloc(sizeof(char) * 10);    // char 10개 크기만큼 동적 메모리 할당

    strcpy(s2, s1);        // s1의 문자열을 s2로 복사

    printf("%s\n", s2);    // Hello

    free(s2);    // 동적 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/424/mod_page/content/20/unit42-7.png)



배열형태의 문자열을 문자열 포인터에 붙이기

```c
#define _CRT_SECURE_NO_WARNINGS    // strcpy, strcat 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>
#include <string.h>    // strcpy, strcat 함수가 선언된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char s1[10] = "world";                  // 크기가 10인 char형 배열을 선언하고 문자열 할당
    char *s2 = malloc(sizeof(char) * 20);    // char 20개 크기만큼 동적 메모리 할당

    strcpy(s2, "Hello");   // s2에 Hello 문자열 복사

    strcat(s2, s1);        // s2 뒤에 s1을 붙임

    printf("%s\n", s2);    // Helloworld

    free(s2);  // 동적 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/425/mod_page/content/20/unit42-8.png)



문자열 만들기

프로그램에서 문자열이 중요하게 사용되는 만큼 C 언어에서는 다양한 문자열 처리 함수를 제공합니다. 이번에는 printf처럼 서식을 지정해서 문자열을 생성하는 방법을 알아보겠습니다.

sprintf 함수를 사용하면 서식(format)을 지정하여 문자열을 만들 수 있습니다(stdio.h 헤더 파일에 선언되어 있습니다).

- **sprintf(배열, 서식, 값);**

- **sprintf(배열, 서식, 값1, 값2, ...);**

- - **int sprintf(char \* const _Buffer, char const * const _Format, ...);**
  - 성공하면 만든 문자열의 길이를 반환, 실패하면 음수를 반환

```c
#define _CRT_SECURE_NO_WARNINGS    // sprintf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>     // sprintf 함수가 선언된 헤더 파일

int main()
{
    char s1[20];    // 크기가 20인 char형 배열을 선언

    sprintf(s1, "Hello, %s", "world!");    // "Hello, %s"로 서식을 지정하여 s1에 저장

    printf("%s\n", s1);    // Hello, world!: 문자열 s1 출력

    return 0;
}
```

보통 s1과 같이 문자열을 저장할 빈 배열을 **버퍼(buffer)**라고 부릅니다.

![](https://dojang.io/pluginfile.php/416/mod_page/content/48/unit43-1.png)

```c
#define _CRT_SECURE_NO_WARNINGS    // sprintf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>     // sprintf 함수가 선언된 헤더 파일

int main()
{
    char s1[30];    // 크기가 30인 char형 배열을 선언

    sprintf(s1, "%c %d %f %e", 'a', 10, 3.2f, 1.123456e-21f);    // 문자, 정수, 실수를 문자열로 만듦

    printf("%s\n", s1);    // a 10 3.200000 1.123456e-21: 문자열 s1 출력

    return 0;
}
```

![](https://dojang.io/pluginfile.php/416/mod_page/content/48/unit43-2.png)



서식을 지정하여 문자열 포인터에 문자열 만들기

지금까지 배열 형태로 문자열을 만들었습니다. 이번에는 문자열 포인터에 문자열을 만들어보겠습니다. 문자열 포인터를 사용하려면 먼저 malloc 함수로 메모리를 할당한 뒤 sprintf 함수로 문자열을 만들면 됩니다.

- **sprintf(문자열포인터, 서식, 값);**
- **sprintf(문자열포인터, 서식, 값1, 값2, …);**

```c
#define _CRT_SECURE_NO_WARNINGS    // sprintf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>     // sprintf 함수가 선언된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일
    
int main()
{
    char *s1 = malloc(sizeof(char) * 20);  // char 20개 크기만큼 동적 메모리 할당

    sprintf(s1, "Hello, %s", "world!");    // "Hello, %s"로 서식을 지정하여 s1에 저장

    printf("%s\n", s1);    // Hello, world!: 문자열 s1 출력

    free(s1);    // 동적 메모리 해제

    return 0;
}
```

char *s1 = malloc(sizeof(char) * 20);처럼 char 20개 크기만큼 동적으로 메모리를 할당했습니다. 그리고 sprintf 함수에 서식을 지정하여 문자열을 만들면 됩니다. 배열과 마찬가지로 s1과 같이 문자열을 생성할 메모리 공간도 **버퍼**입니다.

![](https://dojang.io/pluginfile.php/417/mod_page/content/27/unit43-3.png)

문자열 사용이 끝났다면 반드시 free 함수로 동적 할당한 메모리를 해제합니다. 즉, 문자열 포인터 사용은 항상 malloc, 사용, free 패턴입니다.

문자열뿐만 아니라 서식 지정자를 사용하여 C 언어의 다양한 값(자료형)도 문자열로 만들 수 있습니다. 이때도 마찬가지로 먼저 malloc 함수로 메모리를 할당합니다.

```c
#define _CRT_SECURE_NO_WARNINGS    // sprintf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>     // sprintf 함수가 선언된 헤더 파일
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char *s1 = malloc(sizeof(char) * 30);    // char 30개 크기만큼 동적 메모리 할당

    sprintf(s1, "%c %d %f %e", 'a', 10, 3.2f, 1.123456e-21f);    // 문자, 정수, 실수를 문자열로 만듦

    printf("%s\n", s1);    // a 10 3.200000 1.123456e-21: 문자열 s1 출력

    free(s1);    // 동적 메모리 해제

    return 0;
}
```

![](https://dojang.io/pluginfile.php/417/mod_page/content/27/unit43-5.png)

