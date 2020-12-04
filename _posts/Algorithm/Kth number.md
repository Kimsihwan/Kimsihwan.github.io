---
title: "프로그래머스-LEVEL1-K번째 수"
date: 2020-12-01 21:40:00 +0900
categories: Algorithm
---
내가 짠 코드
<pre><code>
class Solution {

	public static void main(String[] args) {
		int[] array = { 1, 5, 2, 6, 3, 7, 4 };
		int[][] commands = { { 2, 5, 3 }, { 4, 4, 1 }, { 1, 7, 3 } };
		Solution solution = new Solution();
		int[] solution2 = solution.solution(array, commands);
		System.out.println(Arrays.toString(solution2));
	}

	public int[] solution(int[] array, int[][] commands) {
		int[] answer = {};
		ArrayList<Integer> rsList = new ArrayList<Integer>();

		for (int i = 0; i < commands.length; i++) {

            // i번째 숫자
			int start = commands[i][0];
            // j번째 숫자
			int end = commands[i][1];
            // 구하려는 숫자
			int num = commands[i][2];

			ArrayList<Integer> list = new ArrayList<Integer>();

            // i번째부터 j번째까지 배열 뽑아내기
			for (int j = start - 1; j < end; j++) {
				list.add(array[j]);
			}

            // 뽑은 배열 오름차순으로 정렬하기
			int[] array2 = list.stream().sorted().mapToInt(Integer::intValue).toArray();

            // 정렬한 배열 중에 구하려는 숫자 넣기
			Integer integer = array2[num - 1];
			rsList.add(integer);
		}

        // Integer => int로 변경하기
		return rsList.stream().mapToInt(Integer::intValue).toArray();
	}
}
</code></pre>

제일 상단에 있는 코드 중 라이브러리 사용한 코드

Arrays.copyOfRange(원본 배열, 복사할 배열인덱스 시작인덱스, 복사할 끝인텍스)
<pre><code>
	public int[] solution(int[] array, int[][] commands) {
		int[] answer = new int[commands.length];

		for (int i = 0; i < commands.length; i++) {
			int[] temp = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
			Arrays.sort(temp);
			answer[i] = temp[commands[i][2] - 1];
		}

		return answer;
	}
</code></pre>

제일 상단에 있는 코드 중 라이브러리 사용하지 않은 코드
<pre><code>
    public int[] solution(int[] array, int[][] commands) {
        int n = 0;
        int[] ret = new int[commands.length];

        while(n < commands.length){

            // 잘라서 넣을 공간을 미리 확보하기 위한 공식
            int m = commands[n][1] - commands[n][0] + 1;

            // 자른값이 1개면 
            if(m == 1){
                ret[n] = array[commands[n++][0]-1];
                continue;
            }

            int[] a = new int[m];
            int j = 0;
            for(int i = commands[n][0]-1; i < commands[n][1]; i++)
                a[j++] = array[i];

            sort(a, 0, m-1);

            ret[n] = a[commands[n++][2]-1];
        }

        return ret;
    }

    void sort(int[] a, int left, int right){
        int pl = left;
        int pr = right;
        int x = a[(pl+pr)/2];

        do{
            while(a[pl] < x) pl++;
            while(a[pr] > x) pr--;
            if(pl <= pr){
                int temp = a[pl];
                a[pl] = a[pr];
                a[pr] = temp;
                pl++;
                pr--;
            }
        }while(pl <= pr);

        if(left < pr) sort(a, left, pr);
        if(right > pl) sort(a, pl, right);
    }
</code></pre>