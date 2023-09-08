# Code
---
def solution(target):
    answer = []
    
    #싱글,불 > 더블,트리플
    
    #던진 다트 횟수 > 다트의 우선 순위
    #횟수는 10의 자리 & 우선 순위는 1의 자리로
    
    #DP?

    #N 일 떄 최적의 수
    # 싱글  -> N- (1~20, 50) + 10
    # 더블 트리플 -> N -(3 x 1-20, 2x1-20) + 11
    
    from collections import defaultdict
    import math
    
    dp = {}
    
    for i in range(1, 21): 
        dp[i] = (1, 0) #총 다트 수 / 그 중 더블,트리플 수
        dp[i*2] = (1, 1) #총 다트 수 / 그 중 더블,트리플 수
        dp[i*3] = (1, 1) #총 다트 수 / 그 중 더블,트리플 수
    dp[50] = (1,0)
    
    for i in range(1, target+1):
        
        if i not in dp: dp[i] = (math.inf, math.inf)
        
        
      
                    
        ## 더블로 해결하는 경우
        for j in range(2,42, 2):
            if i-j in dp:
                if dp[i][0]*10 + dp[i][1] > dp[i-j][0]*10 + dp[i-j][1] + 10:
                    dp[i] = (dp[i-j][0]+1, dp[i-j][1]+1)

        for j in range(3,63, 3):
            if i-j in dp:
                if dp[i][0]*10 + dp[i][1] > dp[i-j][0]*10 + dp[i-j][1] + 10:
                    dp[i] = (dp[i-j][0]+1, dp[i-j][1]+1)
                    
        ## 싱글로 해결하는 경우         
        for j in range(1,21):
            if i-j in dp:
                if dp[i][0]*10 + dp[i][1] > dp[i-j][0]*10 + dp[i-j][1] + 10:
                    dp[i] = (dp[i-j][0]+1, dp[i-j][1])
                    
        if i-50 in dp:
            
            if dp[i][0]*10 + dp[i][1] > dp[i-50][0]*10 + dp[i-50][1] + 10:
                dp[i] = (dp[i-50][0]+1, dp[i-50][1])
                
    
    n_darts, n_double_triple = dp[target]

    return [n_darts, n_darts-n_double_triple]
