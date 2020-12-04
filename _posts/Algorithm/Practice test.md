---
title: "프로그래머스-LEVEL1-모의고사"
date: 2020-12-01 20:42:00 +0900
categories: Algorithm
---
이번에도 생각이 안나서 프로그래머스에서 제일 상단에 있는 코드를 가져왔다.

<pre><code>
class Solution {
	public static void main(String[] args) {
		int[] problem = { 1, 2, 3, 4, 5 };
		Solution solution = new Solution();
		solution.solution(problem);
	}
    public int[] solution(int[] answer) {
        int[] a = {1, 2, 3, 4, 5};
        int[] b = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] c = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
        int[] score = new int[3];
        for(int i=0; i<answer.length; i++) {
        	// 정답과 찍은답을 비교하여 동일할경우 ++
            if(answer[i] == a[i%a.length]) {score[0]++;}
            if(answer[i] == b[i%b.length]) {score[1]++;}
            if(answer[i] == c[i%c.length]) {score[2]++;}
        }

        // 최대값 구하기
        int maxScore = Math.max(score[0], Math.max(score[1], score[2]));
        ArrayList<Integer> list = new ArrayList<>();

        // 최대값이 같은것만 리스트에 넣기
        if(maxScore == score[0]) {list.add(1);}
        if(maxScore == score[1]) {list.add(2);}
        if(maxScore == score[2]) {list.add(3);}
        
        return list.stream().mapToInt(Integer::intValue).toArray();
    }
}
</code></pre>