---
layout: post
title: Spring 프로젝트 Local 환경에서 실행시키기
tags: [NHN, 신입사원, Spring]
color: rgb(229, 64, 54)
excerpt_seperator: <!--more-->
---



NHN Basecamp가 끝나고 부서 배치를 받았다. 부서 배치를 받고 가장 처음 받은 과제는 스프링 프로젝트를 로컬 환경에서 실행시키는 것이었다. SpringBoot만 실컷 쓰다가 갑자기 Spring이 나와서 어리둥절 했다. 삽질을 좀 했기에 안 까먹으려고 정리해둔다.



> 참고로 -
>
> Community Edition에서 더이상 진행이 안돼서 Ultimate Edition으로 진행했으며, brew로 tomcat을 설치했으나 폴더 구조 등의 문제가 발생해서 공식 홈페이지에서 zip 파일로 다운로드함



1. `account-api` 프로젝트를 불러오고 JDK 버전 설정 (1.8로 안 바꾸면 bind 어쩌고 오류남)
  <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/01.png?raw=true">
2. `target` 폴더나 그 안에 `generated-sources` 파일이 없다? 그러면 프로젝트 루트 폴더에서 마우스 오른쪽 - `Maven` - `Reload Project` & `Generate Sources and Update Folders` 해주기
   <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/02.png?raw=true">
3. 해주면 이렇게 생김
  <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/03.png?raw=true">
4. 이제 오른쪽에서 war:war 가능
  <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/04.png?raw=true">
5. `Command` + `;` 누르면 프로젝트 정보를 볼 수 있음
6. `Modules`에서 Web 있는지 확인. 없으면 만들어도 된다. 이거 때문에 Ultimate 필요했음. Artifact 없다고 뜨는데 `Create Arifact` 클릭
  <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/05.png?raw=true">
7. Put into /WEB-INF/lib 해서 싹 다 넣어준다.
  <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/06.png?raw=true">
8. 환경에 따른 프로필은 여기서 바꿔줄 수 있는 듯 하다. (어떻게 하는거지? 신입교육할 때는 각 환경마다 다르게 세팅하긴 했는데 이렇게 안 생겼던 것 같은데.. 나중에 알아볼 것.)
   <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/07.png?raw=true">
9. 이제 톰캣으로 Build를 하도록 설정해보자. 위에 요거 클릭
   <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/08.png?raw=true">
10. `Template` - `Tomcat Server` - `Local` 선택. 이거 때문에도 Ultimate가 필요했음.
    <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/09.png?raw=true">
11. `Application Server` 옆에 `Configure` 누르고 톰캣 경로 찾아주기
    <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/10.png?raw=true">
12. 오른쪽 위쪽에 `Create configuration` 클릭하면 오른쪽 아래에 Artifacts가 없다고 `Fix`가 뜨는데 
    <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/11.png?raw=true">
13. 클릭해서 `account-api:war`로 바꿔주고 접근하게 편하게 Application context는 `/`로~
    <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/12.png?raw=true">
14. 방금 만든 tomcat으로 설정하고 `run`하면
    <img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/13.png?raw=true">



## 성공!
<img src="https://github.com/rachel-kwak/rachel-kwak.github.io/blob/master/assets/img/2021-03-31/14.png?raw=true">



## 시행착오

1. http-8080 핸들러 어쩌고 오류나면 이미 8080 포트가 쓰이는 중인 것.
   => 8080 찾아서 꺼주면 해결됨

2. `catalina.sh` 권한이 없다고 뜨면?

   ```bash
   $ chmod +x ${TOMCAT_HOME}/bin/catalina.sh
   ```

   해서 실행 권한을 추가해준다.



## References

- https://freehoon.tistory.com/147