# JavaScript bind 함수

bind 함수는 함수가 가리키는 this만 바꾸고 호출하지 않는 것

```
    var obj = {
        string: 'zero'
        yell : function() {
            alert(this.string);
        }
    };

    var obj2 = {
        string : 'what?'
    };

    var yell2 = obj.yell.bind(obj2);

    yell2(); // 'what?'
'''


*obj.yell.bind(obj2)* 를 통해 yell 함수의 this가 obj2로 바뀜
call이나 apply와 비슷하지만 호출은 하지 않고 함수만 반환