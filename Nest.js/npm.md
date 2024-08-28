- [npm (Node Package Manager)](#npm-node-package-manager)
  - [Global, Local](#global-local)
    - [Global](#global)
    - [Local](#local)
    - [참조 우선순위](#참조-우선순위)
  - [명령어](#명령어)
    - [npm 버전 확인](#npm-버전-확인)
    - [init](#init)
    - [install/unistall](#installunistall)
    - [list](#list)
    - [outdated](#outdated)
    - [version](#version)
    - [info](#info)


# npm (Node Package Manager)
https://npmjs.com

## Global, Local
### Global
전역 설치된 패키지는 시스템 전체에서 사용할 수 있으며, 명령줄에서 실행할 수 있다.

### Local
로컬 설치된 패키지는 프로젝트 내에서만 사용할 수 있으며, 프로젝트 디렉토리 내 node_modules에 설치된다.

### 참조 우선순위
1. Local
2. Global

## 명령어
### npm 버전 확인
``` bash
npm -v
```

### init
package.json 생성
``` bash
npm init
npm init -y # 기본값으로 생성
```

### install/unistall
``` bash
npm install <package>
npm install -g <package> # 전역 설치

npm uninstall <package>
npm uninstall -g <package> # 전역 삭제
```

### list
``` bash
npm list
npm list -g # 전역 패키지 목록
```

### outdated
업데이트가 필요한 패키지 확인
``` bash
npm outdated
```

### version
패키지 버전 변경
``` bash
npm version <version>
```
### info
패키지 정보 확인
``` bash
npm info <package>
```
