## 📢 들어가며

본 포스팅은 [GeekNews](https://news.hada.io/), [CodeProject](https://www.codeproject.com/script/news/list.aspx) 의 2023년 11월 둘째 주 주요 기사를 요약/정리한 글입니다.

해석/요약엔 ChatGPT, 구글 번역, 파파고를 사용하고 있습니다.

틀린 정보는 댓글 부탁드립니다 ㅎㅎ

## 💡 헤드라인 모아보기

JetBrains, Kotlin 업그레이드 및 K2 컴파일러 베타 버전 출시

일론 머스크의 xAi, 챗봇 AI Grok 발표

마이크로소프트, '과도한' 사용자에게 AI 서비스 제한 경고

ChatGPT, 사용자 정의 버전인 GPTs 공개

OpenAI, DevDay에서 새로운 모델 및 개발자 제품 공개

JetBrains는 CLion Nova라는 새로운 C++ IDE 발표

## 👁️ 기사 요약 모아보기

### JetBrains, Kotlin 업그레이드 및 K2 컴파일러 베타 버전 출시

2023년 10월 31일, JetBrains의 Kotlin 언어 1.9.20 버전이 발표되어 K2 컴파일러가 베타 단계로 업그레이드 됐다.

이 버전에서 K2 컴파일러는 이제 JVM, 네이티브, JavaScript 및 WebAssembly를 포함한 모든 플랫폼에서 베타 버전으로 사용할 수 있게 되었다.

K2 컴파일러는 Kotlin 프로그래밍 언어를 대상 플랫폼으로 컴파일하는 데 사용되는 공식 컴파일러이다.

[원본 기사]([What's new in Kotlin 1.9.20 | Kotlin Documentation](https://kotlinlang.org/docs/whatsnew1920.html))

### 일론 머스크의 x.Ai, 챗봇 AI Grok 발표

2023년 11월 4일, x.Ai 는 챗봇 AI Grok 를 발표했다.

x.Ai 는 일론 머스크가 지난 7월 출범한 AI 스타트업이다.

약간의 재치로 질문에 답하도록 설계 되었으며, 반항적인 성향을 가지고 있다고 한다.

유머를 싫어한다면 사용하지 말라고...ㅋㅋ

X(트위터)를 통해서 전세계에 대한 실시간 지식을 보유하고 있다는 것이 특이한 장점.

ChatGPT-3.5 를 능가하는 LLM(거대언어모델 또는 훈련된 인공지능) "Grok-1" 을 훈련시켰다고 발표했다.

이 모델은 표준 LM(언어모델) 벤치마크에서 LLaMA 2(70B) 기능에 접근하지만 교육 리소스의 절반만 사용했다고 한다.

[원본 기사](https://x.ai/)

### 마이크로소프트, '과도한' 사용자에게 AI 서비스를 제한 경고

2023년 11월 1일, 마이크로소프트는 온라인 서비스의 이용 약관을 변경하여 "과도한" AI 서비스 사용자는 액세스가 제한될 수 있다는 경고를 포함시켰다.

그러나 이 문서는 "과도한 사용"의 기준을 정의하지 않았으며 "일시적" 제한이 얼마 동안 지속될 수 있는지, 또 "제한" 중에 정확히 어떤 일이 발생하는지를 정의하지 않고 있다.

이런 제한이 AI 아키텍처에서 병목 현상을 나타내어 사용자가 덜 뛰어난 서비스를 받게 될 수도 있다는 우려가 나오고 있다.

그러나 한편으로는 비용을 아끼려는 시도로 추측되고 있다.

마이크로소프트는 GitHub의 AI Copilot에서 이미 손실을 보고 있다고 보고했기 때문.

[원본 기사](https://www.theregister.com/2023/11/02/microsoft_generative_ai_throttling/)

### ChatGPT, 사용자 정의 버전인 GPTs 공개

2023년 11월 6일, OpenAI 는 ChatGPT의 사용자 정의 버전인 GPTs를 공개했다.
GPTs는 기존에 있던 맞춤형 지침을 개선하여 매번 동일한 지침을 ChatGPT에 입력하지 않고도 더 많은 제어를 가능하게 한다.
보드게임의 규칙을 배우거나 자녀에게 수학을 가르치는 등 목적에 맞는 채팅 가능하다.
GPT Store가 이번 달 말 출시되어 사용자가 생성한 GPT를 공개적으로 공유할 수 있다.
원하는 GPT를 검색하고, 일반적인 상점처럼 순위표와 추천이 있을 것이고, 이익을 얻을 수 있게할 예정이라고 한다.
내장된 기능뿐만 아니라 외부 API에 GPT를 통합하는 것도 가능하다.
기업 고객은 내부 전용 GPT를 배포할 수 있다.
ChatGPT Enterprise의 커스텀 버전으로 비즈니스에 맞는 GPT를 만들거나, 독점 데이터를 이용한 GPT를 만들기 가능하다.
추가로 ChatGPT Plus는 2023년 4월까지의 데이터로 훈련됐다고 밝혔다.

[원본기사](https://openai.com/blog/introducing-gpts)

### OpenAI, DevDay에서 새로운 모델 및 개발자 제품 공개

2023년 11월 6일, OpenAI 는 DevDay에서 새로운 모델 및 개발자 제품을 공개했다.

아래는 공개된 내용이다.

-   GPT-4 Turbo

    -   128K 문맥 창(Context Window)을 지원하며, 2023년 4월 기준 데이터로 훈련됐다.

    -   GPT-4 대비 입력 토큰은 3배, 출력 토큰은 2배 저렴.

    -   특정 형식으로 응답하는 지침을 더 잘 따르며, JSON 응답이 보장되는 JSON 모드도 있다.

    -   seed 기반으로 재현할 수 있는 출력을 지원하며 출력에 대한 로그 확률을 반환하는 기능을 추가할 예정.

    -   GPT-3.5 Turbo도 같이 업데이트됐다.

-   Assistants API

    -   코드 인터프리터, 검색, 함수 호출 기능을 가진 특수 목적 AI.

    -   스레드 기반으로 상태를 관리하여 무한히 긴 내용도 처리 가능.

    -   코드 인터프리터 - 샌드박스 환경에서 Python 코드를 작성하고 실행할 수 있다.

    -   검색 - 사용자가 제공한 문서 등 모델 외부의 지식으로 내용을 검색하고 응답.

    -   함수 호출 - 사용자가 정의한 함수를 적절하게 호출하고, 응답을 결과에 포함할 수 있다.

-   그 외 신규 API
    -   GPT-4 Turbo에 이미지를 인식하는 기능이 추가됨,
    -   DALL-E 3가 API로 출시되었으며, 이미지 생성당 0.04 달러.
    -   TTS API가 추가됨.
-   모델 커스터마이징
    -   GPT-4 미세 조정 모델이 실험적 액세스로 출시될 예정.
    -   거대 조직을 위해 사용자 정의 모델을 제작하기 위한 맞춤형 모델 서비스 제공.
        -   수십억 토큰 이상의 독점 데이터 세트를 통한 훈련 등.
-   가격 인하
    -   GPT-4 Turbo 128K는 입력 토큰당 0.01 달러, 출력 토큰당 0.03 달러.
        -   기존에 비해 입력 토큰은 3배, 출력 토큰은 2배 저렴해짐.
    -   GPT-3.5 Turbo 16K는 입력 토큰당 0.001 달러, 출력 토큰당 0.002 달러에 제공.
        -   기존에 비해 입력 토큰은 3배, 출력 토큰은 2배 저렴해졌으며, 4K 모델에 비해서도 입력 토큰인 33% 저렴해짐.
    -   GPT-3.5 Turbo의 미세 조정 모델은 입력 토큰당 0.003 달러, 출력 토큰당 0.006 달러에 제공.
        -   기존에 비해 입력 토큰은 4배, 출력 토큰은 2.7배 저렴해짐.

[원본 기사](https://openai.com/blog/new-models-and-developer-products-announced-at-devday)

### JetBrains는 CLion Nova라는 새로운 C++ IDE 발표

2023년 11월 9일, JetBrains는 CLion Nova라는 새로운 C++ IDE를 발표했다.
CLion Nova는 ReSharper C++/Rider C++ 언어 엔진을 사용하여 기존 CLion 엔진 대신 구축되었다.
2024년에 CLion Nova가 CLion에 통합될 예정이며, 그 전까지는 무료로 사용 가능하고 기존 CLion과 병렬로 설치할 수 있다.
CLion Nova는 기존 CLion보다 더 빠르고 반응이 뛰어나며 성능이 향상되었다.

[원본 기사](https://blog.jetbrains.com/clion/2023/11/clion-nova/)