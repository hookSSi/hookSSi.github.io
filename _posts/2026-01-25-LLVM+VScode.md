---
layout: post
categories: [Family]
use_math: true
---

# About Clang

C, C++ 등을 위한 컴파일러 프론트엔드이며, LLVM을 백엔드로 사용하여 크로스플랫폼 빌드가 가능합니다.

프론트엔드: 외부로 직접 노출되는 인터페이스 ex) 명령줄
백엔드: 내부 구현/비즈니스 로직 등 ex) 정보의 저장

# LLVM

![](assets/images/llvm.webp)

1. 소스 코드를 LLVM IR로 컴파일 .bc(LLVM Bitcode) 형식으로 출력
2. .bc 타겟 아키텍처의 어셈블리 코드 생성 즉 .o(목적 파일) 생성
3. 링크하여 실행 파일 생성

# 설치(윈도우 기준)

1. [LLVM](https://github.com/llvm/llvm-project/releases) 설치
2. 시스템 환경 변수 설정
3. [Visual Studio Build Tools](https://visualstudio.microsoft.com/en/visual-cpp-build-tools/) 설치
4. Build Tools를 실행하여 C++를 사용한 데스크톱 개발로 들어가서 MSVC, Windows 11 SDK 체크하여 설치
5. "Hello, World!" 빌드 확인

```c
#include<stdio.h>

int main()
{
    printf("Hello World\n");
    return 0;
}
```

```shell
clang -o main.exe main.c
```