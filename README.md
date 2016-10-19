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

 - export
    - export문은 지정된 파일(또는 모듈)에서 함수 또는 오브젝트, 원시 타입들을 export 하는데 사용됩니다.(내보낼 식별자 이름 (import를 통해 다른 스크립트에서 가져올 수 있습니다.))
    - named exports

        ```
        // module "my-module.js"
        export function cube(x) {
          return x * x * x;
        }
        const foo = Math.PI + Math.SQRT2;
        export { foo };
        ```

        ```
        이 방법으로 우리는 다른 스크립트에서 사용할 수 있습니다
        import { cube, foo } from 'my-module.js';
        console.log(cube(3)); // 27
        console.log(foo);    // 4.555806215962888
        ```

    - default export 사용하기

        ```
        // module "my-module.js"
        let cube = function cube(x) {
          return x * x * x;
        }
        export default cube;
        ```

        ```
        // module "my-module.js"
        import myFunction from 'my-module';
        console.log(myFunction(3)); // 27
        ```

 - Template Strings
    - Template strings는 문자를 변수,클래스,함수로 치환하는걸 허용한다

    ```
    // Simple string substitution
    var name = "Brendan";
    console.log('Yo, ${name}!');

    // =&gt; "Yo, Brendan!"
    ```

    ```
    // Simple string substitution
    var a = 10;
    var b = 10;
    console.log('a+b = ${a+b}.');
    //=&gt; a+b = 20.
    ```

    ```
    function fn() { return "I am a result. Rarr"; }
    console.log('foo ${fn()} bar');
    //=&gt; foo I am a result. Rarr bar.
    ```

 - Class
    - class란?
        - Class는 사실 함수이다. 함수를 함수 표현식과 함수 선언으로 정의할 수 있듯이 class 문법도 class 표현식과 class 선언 두가지 방법을 제공한다.

        ```
        class Polygon {
          constructor(height, width) {
            this.height = height;
            this.width = width;
          }
        }
        ```

        * Hoisting
            - 함수 선언 과 클래스 선언의 중요한 차이점은 함수 선언의 경우 호이스팅이 일어나지만 클래스 선언은 그렇지 않다는 것이다. 클래스를 사용하기 위해서는 클래스를 먼저 선언 해야 하며 그렇지 않으면 다음과 같은 코드는 ReferenceError를 던질 것이다:

            ```
            var p = new Polygon(); // ReferenceError
            class Polygon {}
            ```

    - Class 표현식
        - class 표현식은 class를 정의 하는 또 다른 방법이다 . Class 표현식은 이름을 가질 수도 있고 안가질 수도 있다. 이름을 가진 class 표현식의 클래스 이름은 해당 클래스의 body에 대해 local scope에 한해 유효하다.

        ```
        // unnamed
        var Polygon = class {
          constructor(height, width) {
            this.height = height;
            this.width = width;
          }
        };

        // named
        var Polygon = class Polygon {
          constructor(height, width) {
            this.height = height;
            this.width = width;
          }
        };
        ```

    - constructor
        - constructor 메소드는 class 로 생성된 객체를 생성하고 초기화하기 위한 특수한 메소드이다.  "constructor" 라는 이름을 가진 특수한 메소드는 클래스 안에 한 개만 존재할 수 있다. 만약 클래스가 한 개를 초과하는 constructor 메소드를 포함하면 SyntaxError 가 발생한다.
          constructor 는 부모 클래스의 constructor 를 호출하기 위해 super 키워드를 사용할 수 있다.

        ```
        class Polygon {
          constructor(height, width) {
            this.height = height;
            this.width = width;
          }

          get area() {
            return this.calcArea()
          }

          calcArea() {
            return this.height * this.width;
          }
        }
        ```

    - extends
        - extends 키워드는 클래스 선언이나 클래스 표현식에서 다른 클래스의 자식 클래스를 생성하기 위해 사용된다.

        ```
        class Animal {
          constructor(name) {
            this.name = name;
          }

          speak() {
            console.log(this.name + ' makes a noise.');
          }
        }

        class Dog extends Animal {
          speak() {
            console.log(this.name + ' barks.');
          }
        }
        ```

    - super
        - super 키워드는 객체의 부모가 가지고 있는 함수들을 호출하기 위해 사용된다.

        ```
        class Cat {
          constructor(name) {
            this.name = name;
          }

          speak() {
            console.log(this.name + ' makes a noise.');
          }
        }

        class Lion extends Cat {
          speak() {
            super.speak();
            console.log(this.name + ' roars.');
          }
        }
        ```

    - static method
        - static 키워드는 클래스의 정적(static) 메소드를 정의한다. 정적 메소드는 클래스의 인스턴스화(instantiating) 없이 불리며, 클래스가 인스턴스화 되었다면 부를 수 없다. 정적 메소드는 어플리케이션(application)을 위한 유틸리티(utility) 함수를 생성하는데 주로 사용된다.

        ```
        class Point {
            constructor(x, y) {
                this.x = x;
                this.y = y;
            }

            static distance(a, b) {
                const dx = a.x - b.x;
                const dy = a.y - b.y;

                return Math.sqrt(dx*dx + dy*dy);
            }
        }

        const p1 = new Point(5, 5);
        const p2 = new Point(10, 10);

        console.log(Point.distance(p1, p2));
        ```

    - rest parameter
         - 나머지 매개변수(rest parameter) 구문은 정해지지 않은 수(an indefinite number, 부정수) 인수를 배열로 나타낼 수 있게 합니다.
         - 나머지 매개변수 및 arguments 객체간 차이
            - 나머지 매개변수와 arguments 객체 사이에 세 가지 주요 차이점이 있습니다.
                1. 나머지 매개변수는 개별 이름이 주어지지 않은 유일한 대상이고 arguments 객체는 함수에 전달되는 모든 인수를 포함합니다.
                2. arguments 객체는 실제 배열이 아니고 나머지 매개변수는 Array 인스턴스로, sort, map, forEach 또는 pop 같은 메서드가 바로 인스턴스에 적용될 수 있음을 뜻합니다
                3. 즉 arguments 객체는 자체에 특정 추가 기능이 있습니다 (callee 속성처럼)


        ```
        arguments에서 배열까지

        나머지 매개변수는 인수에 의해 유발된 상용구(boilerplate) 코드를 줄이기 위해 도입되었습니다.

        // 나머지 매개변수 이전에는, 다음을 볼 수 있음:
        function f(a, b){
          var args = Array.prototype.slice.call(arguments, f.length);

          // …
        }

        // 위는 아래와 같음

        function f(a, b, ...args) {

        }
        ```

        ```
        theArgs가 배열이기에, length 속성을 사용하여 그 요소의 수를 얻을 수 있습니다:

        function fun1(...theArgs) {
          console.log(theArgs.length);
        }

        fun1();  // 0
        fun1(5); // 1
        fun1(5, 6, 7); // 3
        ```

        ```
        function multiply(multiplier, ...theArgs) {
          return theArgs.map(function (element) {
            return multiplier * element;
          });
        }

        var arr = multiply(2, 1, 2, 3);
        console.log(arr); // [2, 4, 6]
        ```

        ```
        다음 예는 arguments 객체가 아니라 나머지 매개변수에 Array 메서드를 사용할 수 있음을 보입니다:

        function sortRestArgs(...theArgs) {
          var sortedArgs = theArgs.sort();
          return sortedArgs;
        }

        console.log(sortRestArgs(5,3,7,1)); // 1,3,5,7로 보임

        function sortArguments() {
          var sortedArgs = arguments.sort();
          return sortedArgs; // 이는 결코 일어나지 않음
        }

        // TypeError 발생: arguments.sort는 함수가 아님
        console.log(sortArguments(5,3,7,1));
        ```

    - arrow function
        -화살표 함수 식(arrow function expression)은 function 식에 비해 구문이 짧고 (자신의 this, arguments, super 또는 new.target을 바인딩 하지 않는) this 값을 렉시컬(lexically, 정적) 바인딩 합니다. 화살표 함수는 항상 익명입니다.

        ```
        ES6
        // empty 화살표 함수는 undefined를 반환
        let empty = () => {};

        (() => "foobar")() // "foobar" 반환

        var simple = a => a > 15 ? 15 : a;
        simple(16); // 15
        simple(10); // 10

        let max = (a, b) => a > b ? a : b;

        // 쉬운 배열 필터링, 매핑, ...

        var arr = [5, 6, 13, 0, 1, 18, 23];
        var sum = arr.reduce((a, b) => a + b);  // 66
        var even = arr.filter(v => v % 2 == 0); // [6, 0, 18]
        var double = arr.map(v => v * 2);       // [10, 12, 26, 0, 2, 36, 46]

        // 더 간결한 프로미스 체인
        promise.then(a => {
          // ...
        }).then(b => {
           // ...
        });
        ```

        ```
        ES5
        // empty 화살표 함수는 undefined를 반환
        var empty = function empty() {};

        (function () {
          return "foobar";
        })(); // "foobar" 반환

        var simple = function simple(a) {
          return a > 15 ? 15 : a;
        };
        simple(16); // 15
        simple(10); // 10

        var max = function max(a, b) {
          return a > b ? a : b;
        };

        // 쉬운 배열 필터링, 매핑, ...

        var arr = [5, 6, 13, 0, 1, 18, 23];
        var sum = arr.reduce(function (a, b) {
          return a + b;
        }); // 66
        var even = arr.filter(function (v) {
          return v % 2 == 0;
        }); // [6, 0, 18]
        var double = arr.map(function (v) {
          return v * 2;
        }); // [10, 12, 26, 0, 2, 36, 46]

        // 더 간결한 프로미스 체인
        promise.then(function (a) {
          // ...
        }).then(function (b) {
          // ...
        });
        ```

    - Promise
        - Promise 객체는 비동기 계산을 위해 사용됩니다.

        ```
        new Promise( /* executor */ function(resolve, reject) { ... } );
        ```

        - 상태
            대기중(pending): 초기 상태, 이행 또는 거부되지 않은.
            이행됨(fulfilled): 연산이 성공리에 완료되었음을 뜻합니다.
            거부됨(rejected): 연산이 실패했음을 뜻합니다.

        <img src="https://mdn.mozillademos.org/files/8633/promises.png" />

        - method
            - Promise.all
                반복가능한 변수(배열 등)에 포함된 모든 Promise들이 통과된 경우 결정(resolve)을 하고, 그렇지 못하고 거절(reject)하는 경우 거절하는 첫번째 Promise를 의 거절 원인으로 Promise를 반환합니다.
                Promise.all w는 배열 내 모든 값이 결정(resolve)할 때까지 기다립니다.

            ```
            var p1 = Promise.resolve(3);
            var p2 = 1337;
            var p3 = new Promise(function(resolve, reject) {
              setTimeout(resolve, 100, "foo");
            });

            Promise.all([p1, p2, p3]).then(function(values) {
              console.log(values); // [3, 1337, "foo"]
            });
            ```

            - Promise.race
                프로미스 중 하나가 결정(resolve) 또는 거부하자마자 결정 또는 거부하는 프로미스를 반환합니다,

            ```
            var p3 = new Promise(function(resolve, reject) {
                setTimeout(resolve, 100, "three");
            });
            var p4 = new Promise(function(resolve, reject) {
                setTimeout(reject, 500, "four");
            });

            Promise.race([p3, p4]).then(function(value) {
              console.log(value); // "three"
              // p3이 더 빠르기에 결정함
            }, function(reason) {
              // 호출되지 않음
            });
            ```

            - Promise.reject
                 주어진 이유(reason)로 거부된 Promise 객체를 반환합니다.

            ```
             Promise.reject("Testing static reject").then(function(reason) {
               // 호출되지 않음
             }, function(reason) {
               console.log(reason); // "Testing static reject"
             });

             Promise.reject(new Error("fail")).then(function(error) {
               // 호출되지 않음
             }, function(error) {
               console.log(error); // Stacktrace
             });
            ```

            - Promise.resolve
                주어진 값으로 결정(resolve)되는 Promise.then 객체를 반환합니다. 그 값이 thenable(즉 "then" 메서드가 있음)인 경우, 반환된 프로미스는 그 thenable을 "따르며", 그 최종 상태를 취합니다; 그렇지 않으면 반환된 프로미스는 그 값으로 이행(fulfill)됩니다.

            ```
            // thenable이 콜백 전에 오류 던짐
            // 프로미스 거부
            var thenable = { then: function(resolve) {
              throw new TypeError("Throwing");
              resolve("Resolving");
            }};

            var p2 = Promise.resolve(thenable);
            p2.then(function(v) {
              // 호출되지 않음
            }, function(e) {
              console.log(e); // TypeError: Throwing
            });

            // thenable이 콜백 후에 오류 던짐
            // 프로미스 결정
            var thenable = { then: function(resolve) {
              resolve("Resolving");
              throw new TypeError("Throwing");
            }};

            var p3 = Promise.resolve(thenable);
            p3.then(function(v) {
              console.log(v); // "Resolving"
            }, function(e) {
              // 호출되지 않음
            });
            ```

            - Promise.catch
                Promise 반환하여 거부된 경우만 다룹니다. Promise.prototype.then(undefined, onRejected)를 호출하는 것과 동일하게 행동합니다.

            ```
            var p1 = new Promise(function(resolve, reject) {
              resolve('Success');
            });

            p1.then(function(value) {
              console.log(value); // "Success!"
              throw 'oh, no!';
            }).catch(function(e) {
              console.log(e); // "oh, no!"
            }).then(function(){
              console.log('after a catch the chain is restored');
            }, function () {
              console.log('Not fired due to the catch');
            });

            // 다음은 위와 동일하게 행동
            p1.then(function(value) {
              console.log(value); // "Success!"
              return Promise.reject('oh, no!');
            }).catch(function(e) {
              console.log(e); // "oh, no!"
            }).then(function(){
              console.log('after a catch the chain is restored');
            }, function () {
              console.log('Not fired due to the catch');
            });
            ```

            - Promise.then
                Promise를 리턴하고 두개의 콜백 함수를 인수로 받습니다. 하나는 Promise가 성공(success)했을 때를 위한 콜백 함수이고, 다른 하나는 실패(failure)했을 때를 위한 콜백 함수입니다.

            ```
            var p2 = new Promise(function(resolve, reject) {
              resolve(1);
            });

            p2.then(function(value) {
              console.log(value); // 1
              return value + 1;
            }).then(function(value) {
              console.log(value); // 2
            });

            p2.then(function(value) {
              console.log(value); // 1
            });
            ```

    - Object.assign (객체 복사 = 깊은 복사)
        소스 프로퍼티와 동일한 프로퍼티의 키를 가진 타켓 오브젝트의 프로퍼티들은 소스 오브젝트의 프로퍼티로 덮어쓰기 될 것입니다.

        ```
        Object.assign(target, ...sources)

        target
            타켓 오브젝트
        sources
            하나 이상의 소스 오브젝트

        리턴값
            타겟 오브젝트
        ```

        - 같은 프로퍼티를 가지는 객체 병합

        ```
        var o1 = { a: 1, b: 1, c: 1 };
        var o2 = { b: 2, c: 2 };
        var o3 = { c: 3 };

        var obj = Object.assign({}, o1, o2, o3);
        console.log(obj); // { a: 1, b: 2, c: 3 }
        ```

        - Copying Accessors

        ```
        var obj = {
          foo: 1,
          get bar() {
            return 2;
          }
        };

        var copy = Object.assign({}, obj);
        console.log(copy);
        // { foo: 1, bar: 2 }, the value of copy.bar is obj.bar's getter's return value.

        // This is an assign function that copies full descriptors
        function completeAssign(target, ...sources) {
          sources.forEach(source => {
            let descriptors = Object.keys(source).reduce((descriptors, key) => {
              descriptors[key] = Object.getOwnPropertyDescriptor(source, key);
              return descriptors;
            }, {});
            // by default, Object.assign copies enumerable Symbols too
            Object.getOwnPropertySymbols(source).forEach(sym => {
              let descriptor = Object.getOwnPropertyDescriptor(source, sym);
              if (descriptor.enumerable) {
                descriptors[sym] = descriptor;
              }
            });
            Object.defineProperties(target, descriptors);
          });
          return target;
        }

        var copy = completeAssign({}, obj);
        console.log(copy);
        // { foo:1, get bar() { return 2 } }
        ```

        - Polyfill
        ```
        if (typeof Object.assign != 'function') {
          (function () {
            Object.assign = function (target) {
              'use strict';
              // We must check against these specific cases.
              if (target === undefined || target === null) {
                throw new TypeError('Cannot convert undefined or null to object');
              }

              var output = Object(target);
              for (var index = 1; index < arguments.length; index++) {
                var source = arguments[index];
                if (source !== undefined && source !== null) {
                  for (var nextKey in source) {
                    if (source.hasOwnProperty(nextKey)) {
                      output[nextKey] = source[nextKey];
                    }
                  }
                }
              }
              return output;
            };
          })();
        }
        ```


* 참고 URL
- https://babeljs.io/docs/setup/#installation
- https://yarnpkg.com/en/docs/managing-dependencies
- https://code.facebook.com/posts/1840075619545360
- http://webframeworks.kr/tutorials/react/es2015-react/#tocAnchor-1-2
- https://developers.google.com/web/shows/ttt/series-2/es2015


