---
layout: single
date: 2020-04-14 11:43:00 +0900
title: 그리디 알고리즘
---



## 그리디 알고리즘

**그리디 알고리즘**이란 선택의 순간마다 현재 상황에서 보았을 때 최고의 이익만을 골라서 선택하는 알고리즘을 말한다.

물론 매 순간마다 최고의 선택을 하는 것이 전체적으로 보았을 때, 제일 큰 이득일 가능성도 있지만, 그렇지 않을 때도 있어 언제나 어울리는 최적의 알고리즘은 아니다.



예를 들어 어떤 소비자가 590원짜리 물건을  1000원을 주고 산다고 가정하자.

동전의 종류는 500,170,100,10 원 짜리로 이루어졌다고 하자.(170원 동전은 원래 없지만...)

이 소비자는 거스름돈을 받는것에 그리디 알고리즘을 적용해보자.

 1000-590 =  410 원의 거스름돈을 받아야한다.

현재 500원보다 낮다. 그러므로 500원 짜리동전은 0개이다.

410 - x*170 >= 0 을 만족하는 최대의 x는 2다.

그러므로 사용한 170원 짜리 동전은 2개, 남은 잔돈은 70원이다.

남은 70원을 10원 짜리로 처리해주면 7개로 처리할 수 있다.

정리하면 410원을 170원 짜리 2개, 10원짜리 7개로 줄 수 있다.

하지만, 직관적으로 보았을 때, 우리는 100원짜리 4개, 10원짜리 1개로 주면 더 적은 동전을 사용하며 거스름돈을 줄 수 있다는 것을 안다.

이런점에서 그리디 알고리즘이 최적이 아니다라고 말한다.



## 그리디 알고리즘 예제

이 문제는 해외의 코딩사이트 HackerRank에서 출제된 문제이다.

~~내가 한 번역이 완벽한지는 모르겠다 ㅎㅎ;~~

출처 : [https://www.hackerrank.com/challenges/luck-balance/problem](https://www.hackerrank.com/challenges/luck-balance/problem)



### 1. 문제 설명

레나는 중요한 코딩대회를 준비하고 있다. 이 코딩대회는 여러 테스트를 연속적으로 본다.

그녀는 운이 적립될 수 있다고 믿는다. (대단하다!)

그녀의 운 포인트는 처음엔 0이며, 각 대회의 럭 포인트만큼 질 때는 더해지고, 이기면 럭 포인트만큼 깎인다.

이때, 대회는 중요한 대회와 딱히 안 중요한 대회로 나뉜다. 

중요한 테스트는 1, 그렇지 않은 테스트는 0이다.

만일 레나가 중요한 대회를 k번이하로 진다고 가정할 때, 레나가 이 대회를 마치면서 최종적으로 얻을 운 포인트는 얼마인가?

(값이 마이너스면 잃을 운 포인트는 얼마인가?) 

예를 들어 k = 1 일 때의 예시를 들어보자

---

```tiddlywiki
테스트  럭 포인트 	중요도

1		 5		 1

2	   	 1		 1

3		 4	   	 0
```



---

만약 레나가 모든 대회를 진다면, 그녀의 운 포인트는

5 + 1 + 4 = 10 포인트가 될 것이다.

하지만 그녀는 1번까지만 지는 것이 허용된다.  

그러므로 그녀의 운포인트를 최대로 해주기 위해서는 운 포인트가 제일 적게드는 테스트를 우승하는 것이니, 럭포인트가 1인 2번 테스트를 이기면 5 - 1 + 4 = 9 로 1번까지 지는 것이 허용되었을 때의 최대 포인트를 얻을 수 있다.



### 2. 입력

첫 줄에 대회의 테스트 수, 레나가 질 수 있는 최대의 테스트 수를 정수로 입력받는다.

그 다음 각 테스트에 호응되는 n번째 줄에는 그 대회를 우승하려면 요구되는 운포인트, 중요도를 나타내는 정수 2개를 입력받는다. 



### 3. 출력

레나가 이 대회를 마치고 얻을 수 있는 최대의 운포인트를 출력하라.



### 4. 예시



**sample input**

```wiki
6 3
5 1
2 1
1 1
8 1
10 0
5 0
```



**sample output**

~~~tiddlywiki
29
~~~





## 예제 접근법

먼저 대회의 각 테스트의 운 포인트와 중요도, 그리고 **테스트를 우승했는지 못했는지를 나타내는 변수**를 가지는 클래스 cometition을 만든다.

배열에 입력받음과 동시에 중요도가 1인 테스트의 갯수를 카운트해주는 변수 important_competition_num 를 만들어준다.

또한 입력받을 때, 모든 테스트를 일단 졌다고 표시한다.

( lose_or_win=0 )

이때 이 변수에서 레나가 질 수 있는 최대의 경기수를 빼면 레나가 최소한 이겨야하는 중요한 경기의 수가 구해진다. 이것을 win_count라는 변수에 저장한다.

이제 배열에서 중요도가 1이고 우승하지 못한 테스트들 중에서 운 포인트가 제일 작은 것을 우승했다고 바꿔준다. 최대한 운 포인트가 작은 것을 이겨서 빼야 총 운 포인트는 제일 큰 값을 만들수 있기 때문이다.

우승으로 바꿔주는 패턴을 win_count만큼 반복한다.

이제 배열의 모든 테스트중에서 우승하지 못한 테스트는 그 값을 더해주고, 우승한 경기는 빼준 값을 구하여 출력해준다.



## 내가 구현한 예제의 코드



```java
import java.util.Scanner;

class competition{
    int luck_point;
    int importance;
    int win_or_lose; // 0은 짐, 1은 이김

    public void set(int luck_point,int importance,int win_or_lose){
        this.luck_point=luck_point;
        this.importance=importance;
    }
}

public class Main1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        competition competitions[] = new competition[1000];

        int competition_num = sc.nextInt();
        int max_lose_count = sc.nextInt();
        int important_competition_num=0;
        int luck_point, importance;
        int min_luck_point;


        for (int i = 0; i < competition_num; i++)   // 럭포인트와 중요도 설정
        {
            luck_point = sc.nextInt();
            importance = sc.nextInt();
            competitions[i] = new competition();
            competitions[i].set(luck_point, importance, 0);   // 일단 다 진걸로 설정

            if(importance==1)
                important_competition_num++;   // 중요도가 1인 대회 수만큼으로 설정
        }

        int win_count = important_competition_num - max_lose_count;

        int index=-1;
        for(int i=0;i<win_count;i++)  // 중요도가 1인 대회중 럭포인트가 제일 작은 값들을 '이김' 으로 저장
        {
            for(int j=0;j<competition_num;j++)  // 중요도가 1인 첫번쨰 인덱스 찾기
            {
                if(competitions[j].importance==1)
                {
                    index = j;
                    for(int k=j+1;k<competition_num;k++)
                    {
                        if(competitions[k].importance==1 && competitions[k].win_or_lose==0 && competitions[k].luck_point<competitions[j].luck_point)
                        {
                            j=k;
                        }
                    }
                    competitions[j].win_or_lose=1;  // 이김으로 표시
                    break;
                }
            }
        }

        int sum=0;
        for(int i=0;i<competition_num;i++)
        {
            if(competitions[i].win_or_lose==0)
            {
                sum += competitions[i].luck_point;
            }
            if(competitions[i].win_or_lose==1)
            {
                sum -= competitions[i].luck_point;
            }
        }
        System.out.println(sum);
    }
}
```



다음은 출력창이다.



![](https://user-images.githubusercontent.com/62462277/80302661-49e20b00-87e6-11ea-83fa-26f59d280c78.png)



## 마치며...

이번 컴알수업의 과제를 하며 해외의 여러 코딩사이트를 알게되었으며, 각국의 많은 사람들이 이 코딩사이트에 참여하며 질문, 피드백을 주고받는다는 것을 알게되었다.

앞으로도 이 사이트를 유용하게 써보도록 노력하자.



출처 : [https://www.hackerrank.com/challenges/luck-balance/problem](https://www.hackerrank.com/challenges/luck-balance/problem)