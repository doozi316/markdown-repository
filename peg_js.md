## 📣 들어가며

이번 포스팅에선 PEG.js 의 설치 및 사용법에 대해 다룬다.

## PEG.js 란?

PEG.js 는 Parsing Expression Grammer(PEG) 를 기반으로 하는 자바스크립트 파싱 라이브러리이다.

PEG.js 를 사용하면 문자열이 특정 문법 규칙을 따르는지 검사하거나, 구문을 분석하여 구조화 데이터로 변환하는 작업을 수행할 수 있다.

## PEG.js 설치 및 사용 방법

### PEG.js 설치

PEG.js 는 어떤 변환하는 작업을 수행하는 컨버터이다.

`pegjs` 라는 명령어로 `.pegjs` 라는 확장자 명을 가진 파일을 javascript 로 변환 시킬 수 있다.

또는, 프로젝트 내에서 pegjs 를 주입하여 런타임 중 변환을 시킬 수도 있다.

`pegjs` 명령어를 통해 변환을 시키려면 `pegjs` 를 글로벌하게 설치해야한다.
`-g` 옵션을 붙여 글로벌하게 사용하자.

```
npm install -g pegjs
```

프로젝트 내에서 주입하려면 프로젝트 `node_modules` 에 설치해주면 된다.

```
npm install pegjs
```

### PEG.js 변환 방법

PEG.js 를 설치했다면, PEG 문법을 활용하여 `.pegjs` 파일을 만든다. (문법은 아래에서 설명할 것이다.)

파싱할 각종 규칙을 나열한 `.pegjs` 파일 생성 후,
이 파일을 PEG.js 라이브러리를 통해 javascript 로 변환시킬 수 있다.

글로벌하게 설치했다면 `pegjs` 명령어를 활용한다.

```
peggy test.pegjs
```

`pegjs` 명령어엔 다양한 옵션이 존재하는데,
자세한 건 [공식문서](https://pegjs.org/documentation)에서 확인할 수 있다.

만약 프로젝트 내에 PEG.js 를 주입하고, 런타임 중 변환하길 원한다면, 아래와 같이 구현하면 된다.

```
var peg = require("pegjs");
var parser = peg.generate("start = ('a' / 'b')+");
parser.parse("abba"); // returns ["a", "b", "b", "a"]
```

먼저 `pegjs` 를 주입하고,
`start = ('a' / 'b')+` 라는 파싱 규칙을 등록한다.
이 `generate` 는 글로벌한 명령어로 `.pegjs` 파일을 자바스크립트로 변환시킨 것과 동일한 역할을 한다.
`start = ('a' / 'b')+` 라는 PEG 문법을 자바스크립트로
컨버트 하여 generate(등록) 시키는 것이다.

등록된 파서를 `parse()` 메소드로 파싱시킬 수 있다.
이 과정은 글로벌한 명령어로 javascript 파일을 생성한 경우에도 동일하게 진행하면 된다.
원하는 input 을 인자로 넘기고, 변환된 output 을 반환받을 수 있다.

## PEG.js 문법

예제를 통해 PEG.js 문법에 대해 알아보자.

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

여기까지 PEG.js 전문은 아래와 같다.

```
wordCounter = space? (word space?)*

word = letter+

letter = [a-zA-Z0-9]

space = " "
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

예를 들어, 지금 까지 구현한 규칙에 대해 (return 없는 규칙) 'My name is Doozi' input을 입력하면 아래와 같은 Output을 반환한다.

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

하지만 PEG.js의 javascript 영역에 규칙을 바로 입력할 수 없다.

규칙에 jacascript 용 이름을 붙여 사용해야한다.

나는 `word` 라는 규칙에 `w`라는 이름을 붙여주겠다.

정확히는 바로 `word` 에 이름을 붙여주는 게 아니라,

빈칸으로 구분된 단어를 세어줘야하기 때문에 괄호친 부분에 대해 이름을 지어주겠다.

```
wordCounter = space? w:(word space?)* { return w.length }
```

이러면 4를 성공적으로 4를 반환하는 걸 볼 수 있다! 🥳

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
letterCounter = w:(iw:word space? {return iw;})* {
   var total = 0;
   for (var i = 0; i < w.length; i++) {
       total += w[i].length;
   }
   return total;
 }
```

뭔가 갑자기 for문이 추가되고 코드가 훌쩍 늘어났지만 겁 먹을 필요 없다.

차근차근 해석해보자.

일단 자바스크립트 영역이 두 부분으로 나뉘어 진 것을 볼 수 있을 것이다.

하나는 `{return iw;}` 이고,
하나는

```
{
   var total = 0;
   for (var i = 0; i < w.length; i++) {
       total += w[i].length;
   }
   return total;
 }
```

첫번째 자바스크립트 영역이 무엇을 반환하는지 확인해보자.

```
iw:word space? {return iw;}
```

`word` 규칙에 `iw` 라는 규칙 이름을 붙여줬다.
`word` 뒤엔 `space` 가 있을 수도 있고, 없을 수도 있다.

즉, 아까 구현했던 공백으로 단어를 구분 짓는 코드인 것이다.
`return iw;` 는 공백으로 구분된 단어를 반환한다는 것을 의미한다.

그리고 이 코드는 괄호로 감싸져 `w`라고 이름이 붙여졌다.

```
w:(iw:word space? {return iw;})*
```

가장 뒤에 `*` 가 붙음으로써 `w`는 0번 이상 존재함을 의미한다.

이 `w` 가 어떻게 쓰이는 지는, 두번째 자바스크립트 영역에서 알 수 있다.

```
{
   var total = 0;
   for (var i = 0; i < w.length; i++) {
       total += w[i].length;
   }
   return total;
 }
```

자바스크립트를 읽을 줄 안다면 무슨 소리인지 바로 알 수 있을 것이다.

아까 위에서 언급했듯이 각 규칙은 모두 배열로 반환된다.
즉, 배열 `w`에 대해 반복을 돌고 있다.
`w` 배열의 내용은 각각 공백으로 구분된 단어 `iw` 이다.

예를 들어, input 이 'My name is doozi' 라면,
`w` 는 `[ 'My', 'name', 'is', 'doozi']` 인 것이다.

배열 `w`를 반복 돌면서, total 에 단어의 길이를 더하고 있다.

즉, 문자 하나하나를 세고 있는 것이다.

'lc:My name is doozi' 에 대한 total 값은 13이 된다.

## PEG.js 와 Peggy의 차이

나는 PEG.js 를 SQL 문에 대한 구조화 데이터를 만들 기 위해 사용 했었다.

예를 들어, input 이 `select column1, column2 from table`
이라면 아래와 같은 Object 를 반환하게 하는 것이다.

```
statement: 'select',
columns: ['column1', 'column2'],
table: ['tables']
```

간단한 예시를 들었지만, 실 업무에선 `where`, `join`, `alias` 등을 모두 고려한 꽤나 복잡한 PEG.js 를 구현했다.

처음엔 자바스크립트로 파싱해보려했었으나, 경우의 수도 너무 많고
어떤 사이드 이펙트가 발생할 지 몰라 PEG.js 를 사용했었다.
결론적으로 매우 유용했음!

아무튼 나는 PEG.js 를 구현한 프로젝트가 타입스크립트 환경이었는데,
PEG.js 가 typescript 를 공식적으로 지원하지 않아 난감했었다.

그래서 알아낸 게 **Peggy** 이다.

Peggy 는 PEG.js 를 기반으로 좀 더 최근에 개발된 라이브러리이다.
Peggy 는 PEG.js 에 비해 더 빠른 속도로 파싱이 가능하다.
Peggy 는 PEG.js 가 지원하는 모든 파싱 문법을 지원하지만 일부 기능이 추가되거나 개선되었다.

무엇보다 가장 큰 다른 점은 Peggy 는 공식적으로 Typescript 를 지원한다는 점이다.

`.peggy` 파일을 타입스크립트로 변환하는 `ts-pegjs` 를 플러그인으로 주입시키기만 하면 된다.

```
peggy --plugin ts-pegjs test.peggy
```

ts-pegjs 의 개념과 다른 옵션에 대해선 [공식 문서](https://github.com/metadevpro/ts-pegjs)에서 더 자세히 알 수 있다.
