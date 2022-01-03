- 오늘은 Codeengn의 Basic RCE L01 문제를 풀어보도록 하겠습니다.


![](https://images.velog.io/images/dsph9245/post/e7f6c783-7253-4fb9-a3c2-26c53b66f0f6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-04%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.28.02.png)

- 일단 문제를 다운로드 받고 실행해주도록 하겠습니다.

![](https://images.velog.io/images/dsph9245/post/6b9780b6-42e1-4f85-b9d1-509bd43d8e79/1.png)

![](https://images.velog.io/images/dsph9245/post/e82da879-b9bf-4239-a144-11027311a92d/2.png)

- 문제를 보아하니 리턴값에 대한 얘기가 나와서 일단 구글링을 통해 return value CD-ROM이라고 검색을 해주겠습니다.

![](https://images.velog.io/images/dsph9245/post/aacd3061-4a2f-4fa4-a1c0-69de09c39c6d/3.png)

- 그 중 가장 상단에 위치한 Microsoft 공식 문서 사이트로 이동해서 자료를 살펴보겠습니다.

![](https://images.velog.io/images/dsph9245/post/b7ab099c-4380-4080-b61f-7702358dbbab/4.png)

- 자료를 살펴본 결과 Drive_CDROM의 리턴값은 5라는 것을 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/2d0ed14f-2654-4b82-8d7a-509c94a53846/5.png)

- 이제 Ollydbg를 이용해서 프로그램을 분석해보도록 하겠습니다.

- 일단, 제 생각에는 제일 먼저 다른 것보다 GetDriveType함수를 위주로 살펴보는 것이 중요할 것 같습니다.

- GetDriveTypeA함수는 분석을 하자마자 찾아볼 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/c90ef640-a1a5-4a1a-8b51-5b0cc8b50fe1/6.png)


```
0040101D  |. 46             INC ESI		;ESI의 값을 1증가
0040101E  |. 48             DEC EAX 		;EAX의 값을 1감소
0040101F  |. EB 00          JMP SHORT 01.00401021
00401021  |> 46             INC ESI 		;ESI의 값을 1증가
00401022  |. 46             INC ESI		;ESI의 값을 1감소
00401023  |. 48             DEC EAX		;EAX의 값을 1감소
00401024  |. 3BC6           CMP EAX,ESI		; EAX와 ESI의 값을 비교


```

여기서 CMP 명령어를 통해 EAX와 ESI를 비교하는 것으로 봐서 EAX와 ESI가 같을 경우 문제가 풀린다는 것을 알 수 있으며, GetDriveTypeA의 값이 5가 된다는 것을 알 수 있습니다. (솔직히 검색만 잘해도 대충 풀 수 있을 것 같습니다.)

정답 : 5



