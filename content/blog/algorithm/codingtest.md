---
title: codingtest
date: 2019-05-19 23:05:92
category: algorithm
---

### 프로그래밍 1

문제 설명
폭탄 던지기 게임을 하려고 합니다. 1부터 N의 번호를 가진 사람들이 원형 탁자에 시계방향으로 앉아있습니다. 처음에는 1번 사람이 폭탄을 가지고 있습니다. 1번 사람은 폭탄을 다른 사람에게 던집니다. 폭탄을 받은 사람은 다른 사람에게 다시 폭탄을 던집니다. 폭탄을 던지는 방식은 폭탄을 받은 사람이 폭탄을 받은 횟수가 짝수 번이면 현재 자신을 기준으로 오른쪽으로 K 번째 있는 사람에게 폭탄을 던지고, 홀수 번이면 현재 자신을 기준으로 왼쪽으로 K 번째 있는 사람에게 폭탄을 던집니다. 단, 폭탄을 받은 사람이 폭탄을 M 번 받았으면 폭탄이 터지고 게임이 종료됩니다.
매개변수로 N, M, K가 주어질 때, 게임이 종료될 때까지 폭탄이 몇 번 던져지는지를 return 하도록 solution 함수를 완성해 주세요.

제한사항
N : 2 이상 2000 이하의 자연수
M : 2000 이하의 자연수
K : N-1 이하의 자연수
입출력 예
N M K answer
3 3 2 6
입출력 예 설명
입출력 예 #1
처음에는 1번 사람이 폭탄을 가지고 있습니다.

1번 사람은 폭탄을 한번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 왼쪽으로 2번째인 3번 사람에게 폭탄을 던집니다.
3번 사람은 폭탄을 한번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 왼쪽으로 2번째인 2번 사람에게 폭탄을 던집니다.
2번 사람은 폭탄을 한번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 왼쪽으로 2번째인 1번 사람에게 폭탄을 던집니다.
1번 사람은 폭탄을 두번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 오른쪽으로 2번째인 2번 사람에게 폭탄을 던집니다.
2번 사람은 폭탄을 두번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 오른쪽으로 2번째인 3번 사람에게 폭탄을 던집니다.
3번 사람은 폭탄을 두번 받았기 때문에 홀수 번이므로 현재 자신을 기준으로 오른쪽으로 2번째인 1번 사람에게 폭탄을 던집니다.
1번 사람은 폭탄을 세번 받았기 때문에 게임이 종료됩니다.
이때, 게임이 종료될 때까지 폭탄을 6번 던졌으므로 6을 return 하면 됩니다.

```
function solution(n, m, k) {
  let boomCount = 0;
  let target = 1;
  let personCounts = {
    [target]: 1
  };
  while(true) {
    const personCount = personCounts[target];
    if(personCount % 2) {
      target = (target + k) % n;
      target = target === 0 ? n : target;
    } else {
      target -= k;
      target = target < 1 ? n + target : target;
    }
    personCounts[target] = personCounts[target] ? personCounts[target] + 1 : 1;
    boomCount++;
    if(personCounts[target] === m) {
      break;
    }
  }
  return boomCount;
}

solution(3, 3, 2);
```

### 프로그래밍 3

문제 설명
n 개의 '(' 와 m 개의 ')' 를 이용해 문자열을 만들려고 합니다. 이때, 완성된 문자열이 반드시 올바른 괄호 문자열일 필요는 없으며, 반드시 모든 문자를 사용해야 합니다. '(' 의 개수 n과 ')'의 개수 m이 매개변수로 주어질 때, n개의 '('와 m개의 ')'를 모두 사용해서 만들 수 있는 문자열의 개수를 return 하도록 solution 함수를 완성해주세요.

제한사항
n은 1이상 16이하의 자연수입니다.
m은 1이상 16이하의 자연수입니다.
정답은 231 - 1 이하의 자연수입니다.
입출력 예
n m result
1 1 2
1 2 3
입출력 예 설명
입출력 예 #1
(), )( 의 2가지 문자열을 만들 수 있습니다.

입출력 예 #2
()), )(), ))( 의 3가지 문자열을 만들 수 있습니다.

```js
function factorial(num) {
  if (num == 0) return 1
  else return num * factorial(num - 1)
}
function solution(n, m) {
  const all = factorial(n + m)
  const nFilter = factorial(n)
  const mFilter = factorial(m)
  return all / (nFilter * mFilter)
}
```
