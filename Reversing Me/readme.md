- 오늘은 HackCTF의 Reversing 문제인 Reversing Me를 풀어보도록 하겠습니다.

- 추가로 첨부파일도 다운로드 해줍니다.

![](https://images.velog.io/images/dsph9245/post/6cd53f88-ea65-4480-a027-7d9781952e1d/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-09-15%20%EC%98%A4%EC%A0%84%204.32.59.png)

- 먼저 소스코드를 확인해보겠습니다.

```
#include <stdio.h>
#include <string.h>

int main() {
	int i;
	char *serial = "H`cjCUFzhdy^stcbers^D1_x0t_jn1w^r2vdrre^3o9hndes1o9>}";
	char enter[54];
	printf("키를 입력하시게 : ");
	scanf("%s", enter);
	if (strlen(enter) == strlen(serial)) {
		for (i = 0; i < strlen(serial) && (enter[i] ^ (i % 2)) == serial[i]; i++);
		if (i - 1 == strlen(enter))
			printf("정답일세!\n");
	}
	else
		printf("그건 아닐세...\n");
		exit(0);
	
}
```

- Serial 값과 사용자 값을 입력한 enter값을 변조한 결과를 비교해서 모든 조건을 통과했을 때 "정갑일세"라는 문구가 나오게 되는 코드입니다.



- 여기서 문제 풀이의 핵심이 되는 부분이 바로 enter[i] ^ (i % 2)) == serial[i] 이 부분이다. 

- 해당 소스를 해석해보면 enter값 사용자 값을 i를 2로 나눈 나머지 값 즉, 0또는 1의 값으로 xor한 값이 serial값과 일치하면 정답이라는 문구가 나오게 될 것입니다.

- 그렇기 때문에 즉, 해당 연산을 코드로 작성해주면 되는 문제입니다.

```
serial = "H`cjCUFzhdy^stcbers^D1_x0t_jn1w^r2vdrre^3o9hndes1o9>}"

for i in range(len(serial)):
    
    if (i % 2 == 0):

        print(serial[i])

    else:

        print(chr(ord(serial[i])^1))


```

- 해당 코드를 실행하면 다음과 같은 플래그가 나오는 것을 확인할 수 있습니다.

- HackCTF{hey_success_D0_y0u_kn0w_r3verse_3n9ineer1n9?}

![](https://images.velog.io/images/dsph9245/post/6c8161de-c4f7-4aee-9f22-1888233d1dd5/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-09-15%20%EC%98%A4%EC%A0%84%204.52.33.png)


