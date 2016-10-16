# ES6

##nodejs es3~5 => es6 compile
1. nodejs 설치 - https://nodejs.org/ko/
2. yarn 설치
 - npm install -g yarn
 - yarn add package_name

 * 설치/삭제 옵션

 yarn add to add to Dependencies

 yarn add --dev to add to devDependencies

 yarn add --peer to add to peerDependencies

 yarn add --optional to add to optionalDependencies

 yarn remove package_name

3. babel-cli설치
 - yarn add babel-cli

4. build 방법
 - package.json 수정
    tell code
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
    end code

 - npm run build
   = ./node_modules/.bin/babel src -d dist

5. es2015설치

 - .babelrc생성 및 presets설정
    tell code
    {
        "presets": ["es2015"]
    }
    end code

6. 실행 방법
 - node dist/file_name.js

* 참고 URL

https://babeljs.io/docs/setup/#installation

https://yarnpkg.com/en/docs/managing-dependencies

https://code.facebook.com/posts/1840075619545360


