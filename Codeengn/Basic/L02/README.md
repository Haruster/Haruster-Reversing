- 오늘은 CodeEngn Basic RCE L02를 풀어보도록 하겠습니다.

일단 문제 파일을 다운 받은 후 실행을 해보겠습니다.
![](https://images.velog.io/images/dsph9245/post/d872b8e4-5fc9-4b17-ad57-8156ea6d253c/3.png)

압축 파일을 보니 02.exe 즉, 실행파일이 존재하네요... 한번 실행해보도록 하겠습니다.(원래는 로컬머신이 아닌 가상 머신에서의 실행을 권장합니다.)

- 아 제가 가지고 있는 로컬머신(Windows 11)에서는 돌아가질 않네요... 

![](https://images.velog.io/images/dsph9245/post/b07aa910-1b50-4c70-97de-20cd80beb9c7/2.png)

- 그래서 Vmware로 Windows 8.1을 설치해서 실행을 해보았습니다.

- 실행을 해보니 



- 그럼 먼저 올리디버거로 한번 분석을 해보겠습니다.

- 올리디버거로 해당 실행 파일을 열려고 하니 에러가 납니다.... (열 수 없다고 하네요)

![](https://images.velog.io/images/dsph9245/post/f930e7c7-816e-4106-8b0c-ebdc3e346009/4.png)

- 그럼 다음으로 HXD를 이용해서 분석을 해보도록 해보겠습니다.

![](https://images.velog.io/images/dsph9245/post/f13c392c-4d70-4aa3-a775-2f5b788c2f1c/5.png)

![](https://images.velog.io/images/dsph9245/post/d5cb3750-0ff4-4308-a0d4-bc90ba5c012c/7.png)

- 무언가 문자열 같은 것들도 있고, 굉장히 확인해봐야 할 것들이 많습니다. ㅠㅠ

- 그래서 저는 bintext라는 툴을 이용해서 파일안에 존재하는 String만 추출해보도록 하겠습니다.

![](https://images.velog.io/images/dsph9245/post/a2278c5f-a5ac-44a6-904e-533a3d9d9db1/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202022-01-07%20231550.png)

![](https://images.velog.io/images/dsph9245/post/566e1f56-0a68-4738-8e86-f99288628e5e/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202022-01-07%20231642.png)

![](https://images.velog.io/images/dsph9245/post/9c8118ed-7b29-4cda-9c37-e319b3d059d2/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202022-01-07%20231725.png)

- Crackme #1 밑에 나온 문자열이 바로 플래그임을 알 수 있습니다.
