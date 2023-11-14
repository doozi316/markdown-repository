## 📢 들어가며

본 포스팅은 [GeekNews](https://news.hada.io/), [CodeProject](https://www.codeproject.com/script/news/list.aspx) 의 2023년 11월 둘째 주 주요 기사를 요약/정리한 글입니다.

## 💡 헤드라인 모아보기

📰 Google Play의 새로운 개인 개발자는 앱 출시에 20명 이상의 테스터가 2주이상 앱을 테스트해줘야 배포 가능해진다.

📰 Microsoft의 GitHub, 회사의 개인 코드에 대해 배울 수 있는 Copilot 도우미 발표

📰 Humane, OpenAI 기반 웨어러블 AI Pin 공식 출시

📰 Intel, 다운폴(Downfall) CPU 취약점에 대해 알고 있었지만 5년 동안 아무 조치도 취하지 않았다는 이유로 집단 소송 당해

📰 Microsoft, Windows Server 2022로 전환할 수 있도록 Windows Server 2012 수명선을 확장

📰 Angular.dev 및 Angular 17 버전 출시

## 👁️ 기사 요약 모아보기

### Google Play의 새로운 개인 개발자는 앱 출시에 20명 이상의 테스터가 2주이상 앱을 테스트해줘야 배포 가능해진다.

https://news.hada.io/topic?id=11813

[원본 기사](https://support.google.com/googleplay/android-developer/answer/14151465?hl=ko)

### Copilot이 GitHub을 AI기반 개발자 플랫폼으로 만들 것이라고 발표

"GitHub가 Git을 기반으로 설립되었듯이, 오늘 우리는 Copilot을 기반으로 다시 설립되었음"
GitHub Copilot Chat은 2023년 12월에 정식 출시
GPT-4 모델로 더 정확한 제안과 설명
당신의 코드를 컨텍스트로 사용하여 복잡한 컨셉을 설명하거나 열린 파일 기반으로 코드를 제안, 보안 취약점 감지를 도와주거나 에러를 찾는 것을 도와줌
인라인 Copilot Chat 으로 특정 라인에 대해서 채팅 가능
슬래시 명령을 도입 : /fix 로 코드를 수정, /tests 로 테스트를 생성
클릭 한번으로 AI의 강력한 기능을 적용
JetBrains 기반 IDE들에도 Copilot Chat 적용(프리뷰 오늘부터 시작)
GitHub Copilot Chat이 깃헙 웹사이트와 모바일앱에도 도입
웹에서도 코드, 풀 리퀘스트, 문서 및 일반적인 코딩 관련 질문에 대해 제안, 요약, 분석 및 답변을 제공
고급 코드 검색 기능과 결합하여 Copilot Chat이 인기 있는 오픈 소스 프로젝트의 최신 변경 사항을 이해하고 지원할 수 있도록 도와줌
iPhone 및 Android 기기에서 자연어로 모든 프로그래밍 질문을 할 수 있고, 앱에서 보고 있는 리포지토리, 파일 또는 문서에 대한 답변을 얻을 수 있음
GitHub Copilot Enterprise 공개 : 조직에 맞게 맞춤화된 Copilot
에디터에 그치지 않고 전체 코드베이스의 전체 컨텍스트에 맞춰 개인화 됨
개발자 팀이 코드베이스를 빠르게 파악하고, 문서를 검색 및 작성하고, 내부 및 비공개 코드를 기반으로 제안을 받고, 풀 리퀘스트를 빠르게 검토할 수 있음
2024년 2월에 사용자당 월 39달러에 정식 출시될 예정
GitHub Copilot 파트너 프로그램을 통한 Copilot 기반 에코시스템 육성
타사 개발자 도구, 온라인 서비스 및 GitHub 외부의 지식과 통합하여 GitHub Copilot을 더욱 강화할 것
GitHub Copilot 파트너 프로그램은 새로운 네트워크와 독창성이 GitHub Copilot에 주입될 수 있는 생태계를 조성하여 개발자가 AI로 달성할 수 있는 범위를 넓힐 것
Datastax, LaunchDarkly, Postman, Hashicorp, Datadog 등 25개 이상의 데뷔 파트너와 함께 이 프로그램의 첫 번째 단계를 시작
GitHub Advanced Security에서 사용할 수 있는 새로운 AI 기반 보안 기능
현재 GitHub Copilot은 안전하지 않은 코딩 패턴을 실시간으로 차단하는 LLM 기반 취약성 방지 시스템을 적용하여 GitHub Copilot의 제안을 더욱 안전하게 만듦
이 모델은 하드코딩된 자격 증명, SQL 삽입, 경로 삽입 등 가장 일반적인 취약한 코딩 패턴을 대상으로 함
또한 GitHub Copilot Chat은 IDE의 보안 취약점을 식별하고, 자연어 기능을 통해 취약점의 메커니즘을 설명하며, 강조 표시된 코드에 대한 구체적인 수정 사항을 제안할 수 있음
이제 코드의 취약점과 비밀을 감지하고 수정하도록 설계된 새로운 "AI 기반 애플리케이션 보안 테스트 기능"을 GitHub Advanced Security에 추가
"코드 스캔 자동 수정" 으로 풀 리퀘스트에서 직접 JavaScript 및 TypeScript용 CodeQL을 사용하여 AI가 생성한 수정 사항을 제안하여 개발자가 문제를 더 빠르게 해결하고 코드베이스에 새로운 취약점이 도입되는 것을 줄임
또한 일반 시크릿에 대한 AI 시크릿 스캔과 사용자 지정 패턴에 대한 새로운 정규식 생성기를 통해 낮은 오탐률로 유출된 시크릿을 더 쉽게 찾을 수 있음
GitHub Copilot Workspace 출시 예정
개발자에게 가장 큰 장벽은 아이디어를 코드로 전환하고 풀 리퀘스트에 이르는 데 필요한 계획을 생성하는 것부터 시작되는 경우가 많음
많은 아이디어와 버그는 GitHub 이슈에서 시작됨
이슈의 세부 사항과 코드베이스에 대한 지식, GPT-4의 추론 기능을 결합하여 모든 개발자가 아이디어를 코드로 전환하는 장벽을 넘을 수 있도록 지원하는 AI 기반 브릿지를 개발
Copilot 워크스페이스에서 이슈를 열면 의도한 변경 사항을 구현하는 방법에 대한 계획이 자동으로 제안됨
워크스페이스는 완전히 편집할 수 있으므로 이슈의 의도와 전체 코드베이스를 이해하는 AI의 이점을 활용하면서 원하는 방향으로 AI를 정확하게 조정할 수 있음
변경 사항이 예상대로 작동하는지 검증하기 위해 Copilot Workspace를 사용하면 코드를 빌드, 실행 및 테스트할 수 있음
또한 오류가 발생하면 자동으로 오류를 수정할 수 있음
Copilot Workspace는 프로젝트의 모든 부분을 잘 알고 있는 파트너와의 페어 프로그래밍 세션과 같으며, AI의 강력한 기능을 통해 이슈부터 풀 리퀘스트까지 리포지토리 전반을 변경할 수 있도록 리드를 따를 수 있음
2024년에 Copilot Workspace가 제공되면 개발자가 AI를 제2의 두뇌로 사용하여 자연어를 통해 몇 분 만에 창의력을 발휘할 수 있는 시대로 한 단계 더 도약하게 될 것
AI 기반 개발자 플랫폼에서 모든 것을 하나로 모으기
인간과 인공 지능의 교차점은 플랫폼 전반에 걸쳐 미래 세대의 GitHub Copilot을 계속 정의할 것
우리가 발표하는 모든 것은 개발자가 무엇을 구축하든 상관없이 개발자에게 총체적이고 생산적이며 원활한 AI 기반 개발자 플랫폼을 제공한다는 한 가지에 초점을 맞추고 있음
모바일 앱을 전 세계에 출시하기 위해 GitHub Actions를 사용하는 5명의 스타트업이든, 수천 명의 개발자로 구성된 대기업이 내부 소스 협업을 개선하기 위해 GitHub Enterprise 및 GitHub 코드스페이스로 마이그레이션하든, 오픈 소스 개발자 그룹이 GitHub에서 다음 디지털 인프라를 공유하든, 우리는 지구상의 모든 개발자가 인류의 발전을 가속화할 수 있도록 혁신하고 있음
Git의 도입과 GitHub의 탄생이 그랬던 것처럼, 이 다음 시대는 GitHub Copilot의 토대 위에 구축될 것. 그리고 이제 시작에 불과함.

[원본 기사1](https://www.cnbc.com/2023/11/08/microsoft-launches-github-copilot-enterprise-to-help-with-private-code.html)
[원본 기사2](https://github.blog/2023-11-08-universe-2023-copilot-transforms-github-into-the-ai-powered-developer-platform/)

### Humane, OpenAI 기반 웨어러블 AI Pin 공식 출시

[원본 기사](https://www.theverge.com/2023/11/9/23953901/humane-ai-pin-launch-date-price-openai)

### Intel, 다운폴(Downfall) CPU 취약점에 대해 알고 있었지만 5년 동안 아무 조치도 취하지 않았다는 이유로 집단 소송 당해

인텔 프로세서의 보안 취약점 중 하나인 "다운폴(Downfall)"은 2018년에 발견되었으나 인텔은 이를 숨기고 취약 제품을 판매한 것으로 주장되는 새로운 집단 소송이 미국 캘리포니아 주 샌호세의 연방 법원에 제기되었습니다.

다운폴(Downfall)은 6세대부터 11세대까지의 소비자용 칩과 1세대부터 4세대까지의 제온 인텔 x86-64 CPU에 영향을 미치는 보안 취약점으로, 모던 인텔 CPU에 존재하는 고급 벡터 익스텐션(Advanced Vector Extensions, AVX) 명령에 영향을 받습니다. 이 취약점은 공격자가 추론적 실행 동안 내부 벡터 레지스터 파일의 내용을 노출시킬 수 있는데, 이를 통해 비밀 사용자 데이터가 노출될 수 있습니다.

이 소송의 원고들은 2018년에 두 차례에 걸쳐 다운폴 취약점에 대한 보고서를 인텔에 알렸다고 주장하며, 그 당시 인텔은 스펙터(Spectre)와 멜트다운(Meltdown) 취약점을 다루느라 바빴기 때문에 AVX 명령의 다운폴 취약점을 놓쳤다고 주장합니다. 나중에 인텔이 릴리스한 마이크로코드 업데이트로 인해 특정 "보통의 컴퓨팅 작업"에서 CPU 성능이 최대 50%까지 감소한다고 소송에서 주장하고 있습니다.

현재 많은 사람들이 사용하는 인텔 CPU는 이 다운폴 취약점 때문에 공격에 취약하거나 다운폴 취약점을 해결하기 위해 성능이 눈에 띄게 감소한 제품이 되었다고 주장하고 있습니다. 이러한 제품은 소송에서 주장하는 바에 따르면 소유자가 구매한 제품과는 "다르게 작동"하며 가치가 현저히 낮아졌다고 주장하고 있습니다.

인텔은 다운폴을 해결하지 않은 채로 x86 칩의 세 세대에 걸쳐 문제를 해결하지 않았으며, 이로 인해 포토 및 비디오 편집, 게임 및 암호화 소프트웨어를 사용하는 고객들이 인텔의 태만한 태도의 대가로 지금까지 지불해야 하게 되었다고 주장하고 있습니다. 소송은 또한 인텔이 AVX 결함 명령과 관련된 몇 가지 "비밀 버퍼"를 구현했지만 이 존재를 공개하지 않았다고 주장하고 있습니다. 이러한 비밀 버퍼는 인텔 CPU에서 백도어로 작용했을 것이며, 공격자가 RAM에 저장된 민감한 정보를 얻을 수 있었을 것입니다. 현재까지 인텔은 이 소송에 대한 댓글을 거부하고 있습니다.

[원본 기사](https://www.techspot.com/news/100814-intel-knew-about-downfall-cpu-vulnerability-but-did.html)

### Microsoft, Windows Server 2022로 전환할 수 있도록 Windows Server 2012 수명선을 확장

[원본 기사](https://www.windowscentral.com/software-apps/microsoft-end-support-for-windows-server-2012)

### Angular.dev 및 Angular 17 버전 출시

[원본 기사](https://www.telerik.com/blogs/angular-dev-version-17-told-you-renaissance-here)
