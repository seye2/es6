# ES6

##nodejs es3~5 => es6 compile
1. nodejs 설치 - https://nodejs.org/ko/
2. yarn 설치
 - npm install -g yarn
 - yarn add package_name

    ### 설치/삭제 옵션
    - yarn add to add to Dependencies
    - yarn add --dev to add to devDependencies
    - yarn add --peer to add to peerDependencies
    - yarn add --optional to add to optionalDependencies
    - yarn upgrade to add to Dependencies
    - yarn remove package_name

3. babel-cli설치
 - yarn add babel-cli

4. build 방법
 - package.json 수정
```
    {
       "name": "my-project",
       "version": "1.0.0",
       "scripts": {
           "build": "babel src -d dist"
        },
        "devDependencies": {
            "babel-cli": "^6.0.0"
        }
    }
```

 - npm run build
   = ./node_modules/.bin/babel src -d dist

5. es2015설치

 - .babelrc생성 및 presets설정
```
    {
        "presets": ["es2015"]
    }
```

6. 실행 방법
 - node dist/file_name.js

7. es2015? es6? stage?
일반적으로 ES2015라고 하면 2015년 6월에 Allen Wirfs-Brock를 에디터로 하여 공식적으로 발표된
ECMAScript의 표준 ECMA-262의 6번째 에디션을 의미합니다.
ES6이라고 칭해졌던 것들은 기본적으로 ES2015와 같으며, 매년 에디션을 내자는 움직임이 있어 ES6에서 연도를
반영하는 형태의 ES2015로 변경되었습니다. 이에 따라 ES7이라 불려지던 것은 대부분 ES2016이 되겠지만,
모든 현재의 proposal이 표준이 된다는 법은 없으므로, 그냥 "ES 제안서" 정도로 표현하면 될 것 같습니다.
물론 아직 인터넷에는 수많은 용어들이 딱히 명확한 구분 없이 사용되고 있는 상황입니다.

ECMAScript 표준 제안 단계에는 stage가 있다는 것입니다.
Babel에서는 언어 명세의 stage에 맞춰 기능을 사용할 수 있게 설정할 수 있는 옵션을 제공하며,
stage 0 제안 단계의 언어 명세에 대해서는 semver를 고려하지 않는다고 밝혔으므로
(즉 API가 한 순간 바뀔 수 있습니다), 사용한다면 shrinkwrap 기능 등을 이용하여 업데이트를 보수적으로
해야 할 필요가 있습니다.

구현체 별 언어 명세 지원 테이블은 http://kangax.github.io/compat-table/es6/를 참고하도록 합시다.

8. es6 문법
 - Modules
    - Modules은 다른 파일에 존재하는 value,function,class들을 import하는 것

```
    export function exampleFunction() {
      console.log('I\'m an example. #TrueStory');
    }

    import { exampleFunction } from './example-function';
    import BaseController from './base-controller';

    export default class ExampleController extends BaseController {
      constructor() {
        super();

        exampleFunction();
      }

      doSomething() {
        console.log('What should I do? Change the DOM? Print a dancing shark to the console?');
      }
    }
```
 - Template Strings
    - Template strings는 변수

 - Class
    - constructor
    - extends
    - static

* 참고 URL
- https://babeljs.io/docs/setup/#installation
- https://yarnpkg.com/en/docs/managing-dependencies
- https://code.facebook.com/posts/1840075619545360
- http://webframeworks.kr/tutorials/react/es2015-react/#tocAnchor-1-2
- https://developers.google.com/web/shows/ttt/series-2/es2015

