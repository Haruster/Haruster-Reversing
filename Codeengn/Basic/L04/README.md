- 오늘은 Reversing 워게임 사이트인 Codeengn의 문제인 Basic RCE L04를 한번 풀어보도록 하겠습니다.

- 일단 문제를 보면 디버거를 탐지하는 기능을 가지고 있는 프로그램에서 디버거를 탐지하는 함수의 이름을 찾으면 될 것 같습니다. 

- 문제를 다운로드 해줍니다.

![](https://images.velog.io/images/dsph9245/post/045bfea4-22fa-45d9-85e6-eceba38312e5/1.png)

- .7z 파일이네요.

![](https://images.velog.io/images/dsph9245/post/49baac75-8935-456d-b325-26b2b96e2253/2.png)

- 당연하게도 안에는 04.exe 파일이 있습니다.

![](https://images.velog.io/images/dsph9245/post/083f94c7-594d-4dea-8168-10130680da16/3.png)

![](https://images.velog.io/images/dsph9245/post/80f8d88c-5ff8-407e-88fb-6bae02026b6a/4.png)

- 일단 디버거를 이용하지 않고 그냥 파일을 실행했을 때에는 정상이라는 문구가 계속 반복되면서 출력되는 것을 볼 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/30188983-4a9a-4989-8c3f-9b25f48036b2/5.png)

- 여기서부터는 윈도우 xp로 진행하도록 하겠습니다.

- 윈도우 xp에서도 마찬가지로 디버거를 사용하지 않은 상태에서는 정상이라는 문구가 계속 반복해서 뜨는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/65beddf2-234a-47a4-a420-e1d20b8664a6/1.PNG)

- 그러면 올리디버거를 사용해서 분석을 시작해보도록 하겠습니다.

- 제일 먼저 EP(Entry Point)에서 F9 단축키를 눌러서 프로그램을 실행해보겠습니다.

- 그러면 아까와는 다르게 디버깅 당함이라는 문자열이 반복해서 출력되는 것을 확인할 수 있습니다. 

- 이 문제의 핵심은 이러한 문자열이 출력되게 만드는 함수의 이름을 찾는 것입니다.

![](https://images.velog.io/images/dsph9245/post/9be46fc0-81fb-4328-b496-f7b1951eb04c/2.PNG)

- Search for -> Allintermodular calls에 들어가서 해당 프로그램에서 사용된 함수들의 목록을 보겠습니다.

![](https://images.velog.io/images/dsph9245/post/7d7852ad-05a9-47d3-995b-e9b432d3efc8/3.PNG)

- 함수들의 목록을 보면 IsDebuggerPresent 즉, 디버거가 있음을 나타내는 이름의 함수가 있음을 볼 수 있습니다. 즉, 이것이 디버깅을 탐지하는 함수라는 것을 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/76797673-82ec-4bb9-8ea1-c9d85cbacecb/4.PNG)

- 추가로 해당 부분을 0으로 리턴해주면 정상이라는 문구를 출력할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/bbcc9fcb-2860-49fe-947b-ece079a96148/5-1.PNG)

- C언어에서 return 0;로 반환을 하듯이 MOV EAX, 0을 통해 EAX에 0을 대입합니다. (레지스터를 0으로 만드는 명령입니다.)

![](https://images.velog.io/images/dsph9245/post/1418d2c4-a68c-497b-a407-c79b33d1e8ce/5-2.PNG)

- 그러면 디버깅 탐지 없이 정상이라는 문구가 출력되는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/51cc9f21-3eab-4431-b969-27b43fbea640/6.PNG)
