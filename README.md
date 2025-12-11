```markdown
# 🛠️ Mini CLI Tool Project

Linux 환경에서 C 기반 Mini CLI 프로그램을 제작하고,  
Docker 컨테이너로 패키징한 뒤 GitHub 버전관리를 수행한 프로젝트입니다.  
프로그램 자체는 간단하지만, 오픈소스 개발 workflow를 직접 경험하는 것을 목표로 합니다.

---

## 📁 프로젝트 구조

```

mini-cli/
├─ src/
│   └─ mini.c
├─ Dockerfile
├─ README.md
├─ LICENSE
└─ docs/
└─ images/
├─ linux_run.png
└─ docker_run.png

```

---

## 🚀 1. Mini 프로그램

### ✔ 코드 (`src/mini.c`)

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    printf("Hello from Mini CLI Tool!\n");
    printf("You passed %d arguments.\n", argc - 1);

    for (int i = 1; i < argc; i++) {
        printf("arg %d: %s\n", i, argv[i]);
    }

    return 0;
}
```

---

## 🧪 2. Linux 실행 결과 (WSL Ubuntu)

프로젝트는 Windows 환경의 **WSL2 Ubuntu** 터미널에서 실행 및 테스트했습니다.

### ✔ 실행 명령어

```bash
sudo apt update
sudo apt install -y gcc

cd ~/mini-cli
gcc src/mini.c -o mini
./mini
./mini hello world
```

### ✔ 실행 화면 캡처

![Linux 실행 화면](docs/images/linux_run.png)

---

## 🐳 3. Dockerfile 및 실행 결과

### ✔ Dockerfile

```Dockerfile
FROM docker.io/library/gcc:13

WORKDIR /app

COPY src/mini.c .

RUN gcc mini.c -o mini && \
    rm mini.c

CMD ["./mini", "from", "docker"]
```

---

### ✔ Docker 이미지 빌드

```bash
cd ~/mini-cli
docker build -t localhost/mini-cli:latest .
```

### ✔ Docker 실행

```bash
docker run --rm localhost/mini-cli:latest
```

### ✔ 실행 화면 캡처

![Docker 실행 화면](docs/images/docker_run.png)

---

## 🔧 4. GitHub 버전관리 내역

프로젝트는 아래 조건을 만족하도록 Git workflow를 구성했습니다:

### ✔ 체크리스트

* [x] Commit 5회 이상
* [x] Branch 생성(feature/docs)
* [x] Branch → main Merge
* [x] 의미 있는 Commit 메시지 작성

### ✔ 설명

1. main 브랜치에 기본 구조, mini.c, Dockerfile을 커밋
2. feature/docs 브랜치를 생성하여 README 보완 및 이미지 추가 작업 수행
3. 작업 완료 후 main 브랜치로 merge 진행

예시 커밋 메시지:

```
Add initial project structure and documentation
Add mini CLI tool C source code
Add Dockerfile for building CLI tool
Improve README with Linux and Docker execution steps
Add Linux and Docker execution screenshots
```

---

## 📄 5. LICENSE

본 프로젝트는 **MIT License**를 적용합니다.

```
MIT License

Copyright (c) 2025 정현준

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

(이하 생략 — LICENSE 파일에 전체 전문 포함)
```

---

## 📝 6. 고찰

* WSL 기반 Linux 환경에서 gcc 설치부터 컴파일까지 전체 흐름을 직접 경험했다.
* Docker가 podman을 에뮬레이션하는 환경이라 이미지 빌드 시 short-name 오류 등이 발생했는데,
  레지스트리 풀 경로(`docker.io/library/gcc:13`)를 지정함으로써 해결할 수 있었다.
* Git에서 브랜치 생성 및 merge 과정을 직접 사용해보면서
  협업 시 버전 관리 흐름을 이해할 수 있었다.
* 앞으로는 자동화된 테스트나 GitHub Actions 등을 활용해
  컨테이너 빌드 자동화를 적용해보고 싶다.

---

## 📚 7. 참고 자료

* [https://docs.docker.com/](https://docs.docker.com/)
* [https://gcc.gnu.org/](https://gcc.gnu.org/)
* [https://learn.microsoft.com/windows/wsl/](https://learn.microsoft.com/windows/wsl/)
* [https://choosealicense.com/](https://choosealicense.com/)

```

---

