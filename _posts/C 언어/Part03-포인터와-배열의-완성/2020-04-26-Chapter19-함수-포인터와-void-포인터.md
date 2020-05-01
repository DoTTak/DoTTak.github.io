---
layout: post
title: "[C 언어] Chapter19 - 함수 포인터와 void 포인터"
date: 2020-04-26 05:34:23 +0900
categories: 
    - C 언어
tags:
    - C 언어
toc: true
notice: "> 본 글은 '윤성우 저 열혈강의 C 프로그래밍' 교재를 학습 후 정리한 글입니다."
---

<!-- more -->



## 01 함수 포인터와 void 포인터

### 01-1 함수 포인터 변수
- 함수 포인터 변수란 ?
    - 메모리상에 함수의 주소 값을 저장하는 포인터 변수
- 함수의 이름
    - 배열의 이름이 배열의 시작주소를 의미하는 것 처럼, **함수의 이름도 함수가 저장된 메모리 공간의 주소 값을 의미**
- 함수 이름의 포인터 형
    ```c
    int SimpleFunc(int num){...}
    ```
    - 함수이름의 포인터형은 반환형과 매개변수의 선언을 이용
        - 즉, 반환형이 int형이고 매개변로 int형 하나 선언된 포인터형
- 함수 포인터 변수의 선언
    - 함수의 주소값을 저장할 수 있는 포인터 변수
    - `int (*fptr) (int,int)`
        - int `(*ptr)` (int,int): fptr은 포인터
        - `int` (*ptr) (int,int): 반환형이 int
        - int (*ptr) `(int,int)`: 매개변수 선언이 int
    - 예제 코드
        - 함수 포인터 변수 선언
            ```c
            void SimpleAdder(int n1, int n2)
            {
                printf("%d + %d = %d \n", n1, n2, n1+n2);
            }

            void ShowString(char * str)
            {
                printf("%s \n", str);
            }

            int main(void)
            {
                char * str = "Function Pointer";
                int num1=10, num2=20;

                void (*fptr1) (int, int) = SimpleAdder;
                void (*fptr2) (char *) = ShowString; 

                fptr1(num1, num2);
                fptr2(str);

                return 0;
            }
            ```
        - 함수 포인터 변수 인자 전달
            ```c
            int OlderFirst(int n1, int n2)
            {
                if(n1 > n2){
                    return n1;
                }else{
                    return n2;
                }
            }

            int YoungFirst(int n1, int n2)
            {
                if(n1 > n2){
                    return n2;
                }else{
                    return n1;
                }
            }

            int WhoIsFirst(int n1, int n2, int (*first)(int, int))
            {
                return first(n1, n2);
            }


            int main(void)
            {
                int num1=10,num2=20;
                int first;
                
                printf("입장 순서 1 \n");
                first = WhoIsFirst(num1, num2, OlderFirst);
                printf("%d와 %d세중 %d세 먼저 입장 ! \n", num1, num2, first);

                printf("입장 순서 2 \n");
                first = WhoIsFirst(num1, num2, YoungFirst);
                printf("%d와 %d세중 %d세 먼저 입장 ! \n", num1, num2, first);

                return 0;
            }
            ```

### 01-2 형이 존재하지 않는 void 포인터
- void형 포인터 변수
    - `void * ptr;`
        - 무엇이든 담을 수 있는 바구니(?)
        - 즉, 어떠한 변수의 주소 값도 담을 수 있다.(함수의 주소도..)
        - 대신, 단점이 있음
            - **void형 포인터 변수를 가지고 아무런 연산도 못함**
            - **값의 변경이나 참조 불가능**
- 코드
    ```c
    void SoSimpleFunc(void)
    {
        printf("Call Simple Function \n");
    }

    int main(void)
    {
        int num=20;
        void * ptr;

        ptr = &num;             // 변수 num 주소 저장
        printf("%p \n", ptr);

        ptr = SoSimpleFunc;     // 함수의 주소 값 저장
        printf("%p \n", ptr);

        return 0;
    }
    ```

## 02 main 함수로의 인자전달

### 02-1 main 함수
- main 함수의 모양
    - `int main(void){....}`
    - `int main(int argc, char * argv[]){....}`
        - `char * argv[]`
            ```c
            void SimpleFunc(char ** argv){....}
            void SimpleFunc(char * argv[]){....}
            ```
- 코드
    ```c
    int main(int argc, char *argv[])
    {
        int i=0;
        printf("전달된 문자열의 수: %d \n", argc);

        for(i=0; i<argc; i++)
            printf("%d번째 문자열: %s \n", i+1, argv[i]);
        
        return 0;
    }
    ```