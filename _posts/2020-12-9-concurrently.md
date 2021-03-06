---
layout: post
title: "concurrently package를 이용한 React, Node.js 개발 설정"
subtitle: "React 서버와 Node.js 서버 동시 실행"
date: 2020-12-09 19:26:00
author: "dongjune"
header-img: "img/in_post/pixel_cafe.gif"
catalog: true
tags:
  - Node.js
  - React
--- 

우선 프로젝트의 루트 폴더에서 concurrently package를 설치해줍니다.

```bash
$ npm i -D concurrently
```
-D는 devDependencies에 설치한다는 것을 뜻합니다.  

package.json 파일을 보면 다음과 같이 설치된 것을 확인할 수 있습니다.
<img width="700" alt="스크린샷 2020-12-09 오후 4 12 23" src="https://user-images.githubusercontent.com/53213397/101620216-9cabc280-3a57-11eb-9920-0beaed75bc5c.png">

이제 package.json의 script를 수정해줍시다.

<img width="700" alt="스크린샷 2020-12-09 오후 4 13 57" src="https://user-images.githubusercontent.com/53213397/101620227-a0d7e000-3a57-11eb-8bd9-f8b0e323e984.png">

```json
"scripts": {
    "server":"nodemon server",
    "client":"npm start --prefix client",
    "dev":"concurrently \"npm run server\" \"npm run client\""
}
```
  line 2 : **npm run server** 를 입력하면 **nodemone server**가 실행  
  line 3 : **npm run client** 를 입력하면 **client 폴더로 이동**하여 **npm start** 실행  
  line 4 : **npm run dev**를 입력하면 **npm run server**와 **npm run client**가 **동시**에 실행  

  
이제 실행해봅시다.

```bash
$ npm run dev
```
다음과 같이 react server와 Node.js 서버가 동시에 실행되는것을 확인할 수 있습니다.
<img width="700" alt="스크린샷 2020-12-09 오후 4 18 37" src="https://user-images.githubusercontent.com/53213397/101620233-a1707680-3a57-11eb-8bba-57dc2eff9b9b.png">