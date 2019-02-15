## ES6 문법정리

이 문서는 https://jsdev.kr/t/es6/2944 를 바탕으로 공부하기 위해 작성한 것입니다.

### 소개
ECMAScript 2015로도 알려저 있는 ECMAScript 6
ECMAScript 표준의 가장 최신 버전

### 새로운 기능들
1. arrows
2. classes
3. enhanced object literals
4. template strings
5. destructuring
6. default + rest + spread
7. let + const
8. iterator + for ... of
9. generators
10. unicode
11. modules
12. module loaders
13. map + set + weakmap + weakset
14. proxies
15. symbols
16. subclassable built-ins
17. promises
18. math + number + string + array + object APIs
19. binary and octal literals
20. reflect api
21. tail calls

### Arrows
Arrow 함수는 => 문법을 사용하는 축약형 함수

#### 기능 
1. 표현식의 결과 값을 반환하는 표현식 본문(expression bodies) 지원
```
    var evens = [2, 4, 6, 8];

    //Expression bodies (표현식의 결과가 반환됨)
    var odds = evens.map(v => v + 1); //[3, 5, 7, 9]
    var nums = evens.map((v, i) => v + i) //[2, 5, 8, 11]
    var pairs = evens.map(v => ({even: v, odd: v + 1})); 
```

2. 상태블럭 본문도 지원(블럭 내부를 실행만 하고, 반환을 위해서는 return을 명시)

```
    nums.forEach(v => {
        if( v % 5 === 0)
            fives.push(v);
    })
```

3. 코드의 상위 스코프(lexical scope)를 가리키는 lexical thsi 지원
일반 함수의 자신을 호출하는 객체를 가리키는 dynamic this와 달리 arrow 함수는 lexical this 가리킴

arrow function
```
    var bob = {
        _name: "Bob",
        _friends: ["John, Brian"],
        printFrieds() {
            this._friends.forEach(f =>
            console.log(this._name + " knows " + f));
        }
    }
```

default function
```
    this._friends.forEach(function (f) {
        console.log(this._name +" knows " + f));
    }.bind(this));
```

### Classes

ES6 클래스는 포로토타입 기반 객체지향 패턴을 더 쉽게 사용할 수 있는 대체제
클래스 패턴 생성을 더 쉽고 단순하게 생성할 수 있어서 사용하기도 편하고 상호운용성도 증가

```
    class SkinnedMesh extends THREE.Mesh {
        constructor(geometry, materials) {
            super(geometry, materials);

            this.idMatrix = SkiinedMesh.defaultMatrix();
            this.bones = [];
            this.boneMatrices = [];
            //...
        }
    

        update(camera) {
            //...
            super.update();
        }

        get bonCount() {
            return this.bones.length;
        }

        set matrixType(matrixType) {
            this.idMatrix = SkinnedMesh[matrixType]();
        }

        static defaultMatrix() {
            return new THREE.Matrix4();
        }   
    }
```

### Enhanced Object Literals

ES6에서 객체 리터럴은 선언문에서 프로토타입 설정, foo: foo 선언을 위한 단축 표기법, 메서드 정의, super 클래스 호출 및 동적 속성명을 지원하도록 향상
그에 따라 객체 리터럴 및 클래스 선언이 더 밀접되어져, 객체기반 설계가 편리해짐

```
    var obj = {
        // __proto__
        __proto__ : theProtoObj

        // 'handler': handler의 단축 표기
        handler,

        // Methods
        toString() {

            // Super calls
            return "d " + super.toString();
        },


        // Computed (dynamic) property name
        [ 'prop_' _ (() => 42)() ]: 42
    }
```





