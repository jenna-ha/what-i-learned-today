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

