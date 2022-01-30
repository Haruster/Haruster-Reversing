- 오늘은 Reversing 워게임 사이트인 Codeengn의 Basic RCE L03문제를 한번 풀어보도록 하겠습니다.

- 제일 먼저 문제를 보면 비주얼베이직에서 스트링 비교함수 이름을 찾으라고 하네요 일단은 문제 파일을 먼저 다운로드 해주겠습니다.

![](https://images.velog.io/images/dsph9245/post/8ee6db4c-2f6b-42c8-a2c7-67f34b62eff9/1.png)

- .7z 파일이네요.

![](https://images.velog.io/images/dsph9245/post/fc34a1b9-7c02-440e-acc5-605c3c7f3045/2.png)

- 03.7z 파일을 열어보면 03.exe라는 파일이 있는데 해당 파일을 압축 해제한 후에

![](https://images.velog.io/images/dsph9245/post/d7457a81-ab73-490c-9c4f-33db2656d694/3.png)

![](https://images.velog.io/images/dsph9245/post/341d8dfe-dc67-4b6a-8bcb-b1e47335c7e4/4.png)

- 이를 실행시켜줍니다. 무슨 문자열이 나오지만 영어는 아닌 것 같습니다. 

![](https://images.velog.io/images/dsph9245/post/221645fc-fe5c-4881-8fcf-20c396e6b654/5.png)

- 번역기를 사용해서 이를 번역해주면?

- 독일어로 "이 태그를 제거하거나, 올바른 암호를 찾으십시오."라는 문자열이라는 것을 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/3028448f-79b9-4421-8634-1f92b82735e6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-31%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.22.27.png)

- 그래서 즉, regcode란에 알맞은 암호를 입력해야 됩니다.

![](https://images.velog.io/images/dsph9245/post/567748eb-f045-4c4d-96dd-44f7b6364c67/6.png)

- 만약 틀린 암호를 넣는다면 "Error ! Das Passwort ist falsch !"라는 문자열이 출력되면서 에러가 나는 것을 볼 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/aa0d14d4-bc05-4832-8940-ed6fda8584a9/8.png)

- 올리디버거로 해당 파일을 열어줍니다.

![](https://images.velog.io/images/dsph9245/post/f6edd58d-55e0-4364-845c-ba2073be5ec7/9.png)

![](https://images.velog.io/images/dsph9245/post/156a4589-b00e-40e5-93ef-2da1e17f08ce/10.png)

- EP(Entry Point)에서 Text Strings Referenced로 이동해서 해당 프로그램에 존재하는 문자열들을 확인해줍니다.

![](https://images.velog.io/images/dsph9245/post/8644e6b8-328c-4030-8dd9-d7356ee91994/11.png)

- 문자열들을 확인하다보면 아까 실행한 프로그램에서 출력되었던 문자열을 폴 수 있는데 그 사이에 "2G83G35Hs2"라는 특이한 문자열이 존재하는 것을 볼 수 있습니다. (3개 정도 존재한다.)

![](https://images.velog.io/images/dsph9245/post/659c7f94-4305-4726-b214-87ee8977ee5e/12.png)

- "2G83G35Hs2"라는 특이한 문자열이 처음 나오는 곳을 자세히 살펴보면 vbaStrCmp 즉, 메모리 비교 함수 이름을 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/d7fdbbfc-c0eb-404a-b881-48e885dc0f74/13.png)

- 추가로 Regcode는 "2G83G35Hs2"라는 것도 알 수 있습니다.

![](https://images.velog.io/images/dsph9245/post/f9ee9623-b57e-42e2-8544-45b0408eb2b0/14.png)

