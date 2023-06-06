## 📣 들어가며

이번 포스팅에선 PEG.js 의 설치 및 사용법에 대해 다룬다.

## PEG.js 란?

## PEG.js 사용법

예제를 통해 PEG.js 사용법에 대해 알아보자.

아래에서 설명하는 예제는 [공식 웹 컨버터](https://pegjs.org/online)로 직접 테스트해볼 수 있다.

PEG.js로 문장에서 사용된 단어의 개수를 도출해보자.

예를 들어. 'My name is Doozi' 라는 문장이 있다면, 4가 반환되면 되는 것이다.

Wordcounter.pegjs 파일을 하나 생성하고, 아래와 같이 입력해보자.

```
wordCounter = word*
```

`wordCounter` 라고 규칙의 이름을 선언해줬다.

`wordCounter` 말고 다른 이름을 지어줘도 상관 없다.

변수의 이름을 짓듯이 규칙의 이름을 지어주는 것이다.

우측엔 그에 해당하는 규칙을 정의해주면 된다.

나는 `word*` 라고 정의해줬는데,

정규 표현식을 알고 있다면 읽기 쉬울 것이다.

`*` 는 정규표현식에서 0번 이상 반복된다는 뜻이다.

즉, word가 0번이상 반복된다는 것. 

input에 0번 이상 반복된 단어를 입력하면 input이 규칙에 적절하다는 결과가 떠야한다. 

그런데 word를 따로 정의해 주지 않아서 'Rule "word" is not defined.' 에러가 발생한다.

word 규칙도 정의해보자.

```
wordCounter = word*

word = letter+
```

`+` 는 정규표현식에서 1번 이상 반복된다는 뜻이다. 

`word`는 `letter` 가 1번 이상 반복된 규칙을 의미한다. 

`letter` 역시 정의해 주지 않아 'Rule "letter" is not defined.' 에러가 발생할 것이다. 

`letter` 도 같은 방식으로 정의해주자.

```
wordCounter = word*

word = letter+

letter = [a-zA-Z0-9]
```

 `[a-zA-Z0-9]` 은 영문 대소문자와 숫자 범위 내의 문자 중 하나를 의미한다.
 
이제 input에 영문 또는 숫자 조합의 단어를 나열하면 

'Input parsed successfully.' 라며 파싱을 성공했다는 문구가 뜰 것이다.

그런데 우리가 원했던 'My name is Doozi' 따위의 띄어쓰기가 들어간 문장을 입력하면,

'Expected [a-zA-Z0-9] or end of input but " " found.' 에러가 발생한다. 

빈칸에 대한 규칙이 정의되지 않았기 때문이다.

빈칸 규칙도 정의해주자.

```
wordCounter = word* space

word = letter+

letter = [a-zA-Z0-9]

space = " "
```

`space` 라고 규칙 이름을 짓고 " " 라고 정의해줬다.

그리고 `wordCounter` 규칙에 붙여봤다.

하지만 이러면 여전히 에러를 뱉는다.

이유는, `word* space` 규칙이

빈칸 없이 여러 단어가 반복되다가 마지막에만 space 가 붙는 규칙이기 때문이다.

단어 사이사이, 또는 단어 앞/뒤에 빈칸이 있거나 없어도 되는 규칙을 정의해줘야한다.

이를 위해선 괄호와 `?` 정규 표현식을 적절히 활용해주면 된다.

`?` 는 앞에 오는 문자가 0번 또는 1번 존재할 수 있음을 의미한다.

일단 공백이 있어도 되고 없어도 된다는 뜻으로 `space` 뒤에 `?` 를 붙여준다. (또는 `*`을 붙여준다. )

```
wordCounter = word* space?
```

하지만 이러면 여전히 공백이 마지막에 있는지 여부만 검사한다.

단어 사이사이에 공백이 있게 하려면, 단어와 공백이 함께 여러번 반복되게하면 된다. 

즉, `*`규칙을 `word` 와 `space` 에 함께 묶어 사용하면 되는 것이다.

```
wordCounter = (word space?)*
```

이러면 이제 'My name is Doozi' 따위의 문장 input 에 대해 'Input parsed successfully.' 문구를 반환할 것이다.

추가적으로, 문장 앞 뒤에도 공백을 허용하고 싶다면 아래와 같이 해줄 수 있겠다.

```
wordCounter = space? (word space?)*
```

자 이제 input에 대한 유효성 검사는 대충 되는 듯 하니, 

이제 단어를 세는 로직을 추가해보자.

원하는 값을 반환 받고 싶다면 아래와 같이 javascript 를 활용하면 된다.

```
wordCounter = space? (word space?)* { return 1 }
```

위 코드는 무조건적으로 1을 반환하게 하는 로직이다.

우린 1 대신 단어이 개수를 세서 반환하면 된다.

즉, `word` 가 몇 개인지만 세면 되는데, 아주 쉽다.

공식 웹 컨버터의 Output 부분을 보면 알 수 있듯이, 
각각의 규칙이 기본적으로 배열로 반환되는 걸 알 수 있다.

예를 들어, 지금 까지 구현한 규칙에 대해 'My name is Doozi' input을 입력하면 아래와 같은 Output을 반환한다.

```
[
   null, // space?
   [
      [ 
        [ 
            "M", // letter+ 
            "y" // letter+
        ], // word 
            " " // space?
      ], // wordCounter
      [ [ "n", "a", "m", "e" ], " " ],
      [ [ "i", "s" ], " " ],
      [ [ "D", "o", "o", "z", "i" ], " " ]
   ]
]
```

이해를 돕기 위해 주석을 달아봤다. 

`word` 도 결국 배열이라는 뜻이다. `word.length` 만 반환하면 되는 것이다.

하지만 PEG.js의 javascript scope 에 규칙을 바로 입력할 수 없다.

변수명을 정의해주듯이, 규칙에 jacascript 용 이름을 붙여 사용해야햔다.

나는 `word` 라는 규칙에 `w`라는 이름을 붙여주겠다. 

정확히는 바로 `word` 에 이름을 붙여주는 게 아니라, 

빈칸으로 구분된 단어를 세어줘야하기 때문에 괄호친 부분에 대해 이름을 지어주겠다. 

```
wordCounter = space? w:(word space?)* { return w.length }
```

이러면 4를 성공적으로 4를  반환하는 걸 볼 수 있다! 🥳

좀 더 나아가서, 

유저가 문장의 앞에 'wc:' 를 입력하면 단어의 개수를 반환하고,

문장 앞에 'lc:'를 입력하면 문자의 개수를 반환하는 로직을 짜보자.

예를 들어, 'wc: Hello World' 라는 input이 들어오면 2를 반환하고,

'lc: Hello World'를 입력하면 10을 반환하면 된다.

```
textWork = 
    "wc:" wc:wordCounter { return wc }
    / "lc:" lc:letterCounter { return lc }
```

나는 `textWork` 라는 규칙을 새로 생성해줬다.

여기서 `/` 는 '또는' 이라는 뜻이다.

첫번째 규칙이 일치하는지 확인하고, 일치하지 않다면 `/` 뒤 규칙이 맞는치 확인한다.

첫번쨰 규칙은 기존의 wordCounter 를 그대로 응용했다. 

추가된 letterCounter를 구현해보자.

```
letterCounter = 
    space* w:() 
```



## PEG.js 와 Peggy의 차이
