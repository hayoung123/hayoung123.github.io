---
title: "[Python] 순열과 조합 구하기"
subtitle: "PYTHON에서 dfs와 itertools 라이브러리를 이용한 순열과 조합 구하기"
categories: algorithm
tags: [python, 알고리즘, dfs, 순열, 조합]
---

# DFS와 itertools라이브러리를 이용한 순열,조합

Python의 itertools 라이브러리를 이용해 순열과 조합을 간단하게 구할 수 있다.
하지만, 복잡한 조건이 붙거나 라이브러리를 사용 못하는 환경에 대비해 DFS를 이용해 구하는 방법을 익혀보자.

---

## \*1~n까지 자연수 중 m개를 뽑은 순열 구하기

LEVEL의 값이 `m`이 됐을 때 출력하는 방식으로 해결한다.

조합과 순열을 DFS로 구할 때 `res`라는 결과값이 되는 LIST를 이용한다.

## 1. 순열 구하기

## DFS를 이용한 순열 구하기

```
def dfs(L):
    if L == m:
        for x in res:
            print(x, end=' ')
    else:
        for i in range(1, n+1):
            if ch[i] == 0:
                ch[i] = 1
                res[L] = i
                dfs(L+1)
                ch[i] = 0


if __name__ == "__main__":
    n, m = map(int, input().split())

    ch = [0]*(n+1)
    res = [0]*m
    cnt = 0
    dfs(0)
```

- checkList `ch` 를 이용해 그 수가 사용 됐는지 확인 후에 답안list `res` 에 추가한다.
- dfs가 끝나게 될 때 `ch`를 0으로 체크 해제 해준다.

```
결과
1 2
1 3
1 4
2 1
2 3
2 4
3 1
3 2
3 4
4 1
4 2
4 3
```

## itertools를 이용한 순열 구하기

itertools의 permutations 메소드를 이용해 해결한다.

```
import itertools as it

n, m = map(int, input().split())
a=list(range(1,n+1))

for tmp in it.permutations(a,m):
	print(tmp)

#결과
#위의 결과에 ()가 붙어 있습니다.
```

## 2. 조합 구하기

## DFS를 이용한 조합 구하기

```
def dfs(L, s):
    if L == m:
        for x in res:
            print(x, end=' ')
        print()
    else:
        for i in range(s, n+1):
            res[L] = i
            dfs(L+1, i+1)


if __name__ == "__main__":
    n, m = map(int, input().split())
    res = [0]*m
    dfs(0, 1)

#결과 아래 결과에 ()가 제거돼 있습니다.
```

#### DFS의 두번째 인자를 설정해 주어서 해결했다.

DFS 구조를 그린 것.

![DFS구조](https://user-images.githubusercontent.com/67357426/91832466-66082400-ec80-11ea-8086-a771fc988356.png)

- `s`는 `res[0]` 즉, res의 첫번 째 값인 i 값 +1 로 설정해 주어서 중복을 피해준다.

※ `res[0]`이 4일때는 s가 5가 되기 때문에 for문을 돌지 않는다.

## itertools를 이용한 조합 구하기

itertools의 combinations 메소드를 이용해 해결한다.

```
import itertools as it

n, m = map(int, input().split())
a = list(range(1, n+1))

for tmp in it.combinations(a, m):
    print(tmp)

'''
결과
(1, 2)
(1, 3)
(1, 4)
(2, 3)
(2, 4)
(3, 4)
'''
```
