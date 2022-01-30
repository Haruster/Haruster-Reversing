- 오늘은 Reversing 워게임 사이트인 Codeengn의 Basic RCE L05라는 문제를 한번 풀어보도록 하겠습니다.

- 제일 먼저 문제를 보면 해당 프로그램의 등록키를 찾는 문제라는 것을 알 수 있습니다. 

![](https://images.velog.io/images/dsph9245/post/f13b36ab-ce70-4982-8881-e1e436eb903e/1.png)

- .7z 파일을 다운로드 할 수 있으며, 해당 압축을 풀어보면?

![](https://images.velog.io/images/dsph9245/post/fc4d2865-52eb-4c90-8a12-0c1de0d91d0b/2.png)

- 05.exe 파일이 있는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/5aebd2c0-ba32-40fd-a9b2-319407309758/3.png)

- 제일 먼저 05.exe 파일을 한번 실행해보도록 하겠습니다.

- 프로그램 실행 화면을 확인해보면 id(?)란에 Unregistered...라는 문자열이 들어가 있고, key(?)란에는 754-GFX-IER-954라는 문자열이 들어가 있는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/3ecd17c8-b208-4acf-835e-31274f47d663/4.png)

- 여기서 Register now ! 버튼을 누르면 Wrong Serial, try again!이라는 문자열과 함께 틀렸다는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/3a4ca3c5-15d9-4ca2-b164-86941581f17b/5.png)

- 그럼 일단 올리디버거를 실행하기 전에 Exeinfope를 이용해서 언패킹이 되어있는지 확인하겠습니다.

- UPX 0.89 즉, 언패킹이 되어있네요....

![](https://images.velog.io/images/dsph9245/post/a66c9ff1-58bd-4229-991a-ca66d0d531b8/6.png)

- 언패킹 툴을 이용해서 (upx -d 05.exe) 해당 파일을 언패킹 해줍니다.

![](https://images.velog.io/images/dsph9245/post/09aeb3b8-5984-4552-8a6c-60d86c1d22e7/7.png)

- EP(Entry Point)에서 Search for -> All referenced text strings에 들어가서 해당 프로그램에 존재하는 모든 문자열을 확인해보면 Congrats! You cracked this CrackMe!라는 문자열이 존재하는 것을 확인할 수 있습니다.

- 해당 문자열의 위치로 이동해주겠습니다.

![](https://images.velog.io/images/dsph9245/post/2ebf03f5-deae-49e7-a54e-d5732e9575a0/8.png)

- 해당 지점으로 이동해서 살펴보면 Regitered User 뒤에 JNZ ..... 0440F8C라고 해서 0440F8C지점으로 점프를 하는 것을 확인할 수 있습니다. 


![](https://images.velog.io/images/dsph9245/post/1bb3722b-8aa9-4c08-9138-edc02edb1766/9.png)

- 그리고 0440F8C 지점에서는 PUSH 0 즉, 0을 스택 최상단에 위치하는 것이다.(스택 최상단에 0이라는 값을 밀어 넣음)

![](https://images.velog.io/images/dsph9245/post/98011250-cf3a-4598-9c77-4de037af23d6/10.png)

- 또한 GFX-754-IER-954라는 문자열이 실행되고 나서도 마찬가지로 JNZ 0440F72라고 해서 0440F72 지점으로 점프하는 것을 확인할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/b38137bb-a3df-4911-8b68-80e869d18c79/11.png)

- 그리고 0440F72 지점 또한 PUSH 0 즉, 0을 스택 최상단에 위치하는 하게 하는 것을 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/568bb8a4-d193-44b1-a53d-78aa31fcd611/12.png)

- 즉, 해당 문자열이 실행되고 난 후에 JNZ로 인해 스택 최상단에 0이라는 값이 위치하게 되기 때문에, 두 문자열이 ID(?)와 Key(?)라고 의심할 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/95f33923-c5ca-43bd-9ada-bb2d9c6d3d87/13.png)

- 그래서 해당 두 문자열을 각각 ID(?), Key(?) 박스에 넣고 Register
now ! 버튼을 누르면 정상적으로 인증이 되는 것을 알 수 있습니다.
![](https://images.velog.io/images/dsph9245/post/30f4efc3-55c9-404e-bce9-c40904681cd6/14.png)
