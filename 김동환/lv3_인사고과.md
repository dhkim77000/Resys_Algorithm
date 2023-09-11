1. 쉬운데 잘 안풀리는 문제
2. 문제를 논리적으로 접근해야할 듯
3. 많이 해맸다.

# code
----
```
def solution(scores):
    answer = 1

    target = scores[0]
    target_score = sum(scores[0])
    scores.sort(key=lambda x: (-x[0], x[1]))

    #sc1을 오름차순으로
    #sc2는 내림차순으로
    
    #
    #3 2
    #3 5
    #2 1
    #2 2
    #1 4
    
    #나보다 큰 사람이 있으면 안됨
    # sc1은 항상 작거나 크다
    # sc2 -> sc1 순서대로 올 때 sc2를 작은 것부터 확인하자
    # sc1이 같다면 뒤에 온 sc2가 더 크므로 a b c 순으로 올 때 a의 sc2에서 걸렸다면 무조건 b의 sc2에도 걸림
    

    threshold = 0
    for score in scores:
        if target[0] < score[0] and target[1] < score[1]:
            return -1
        if threshold <= score[1]:
            if target_score < score[0] + score[1]:
                answer += 1 #나보다 큰 사람만 세면 된다. 동점이든 아니든 
            threshold = score[1]
    return answer
