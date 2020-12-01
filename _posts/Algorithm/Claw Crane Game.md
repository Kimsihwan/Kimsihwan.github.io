---
title: "프로그래머스-LEVEL1-크레인 인형 뽑기 게임 "
date: 2020-11-30 23:56:00 +0900
categories: Algorithm
---

<pre><code>
	public int solution(int[][] board, int[] moves) {
		int answer = 0;
		Stack<Integer> stack = new Stack<>();
		for (int move : moves) {
			// j가 높이 조절
			// move가 깊이 조절
			for (int j = 0; j < board.length; j++) {
				// 인형이 있을때
				if (board[j][move - 1] != 0) {
					// 장바구니가 비어있을 경우
					if (stack.isEmpty()) {
						// 장바구니에 추가
						stack.push(board[j][move - 1]);
						// 인형을 뺀 곳에 0으로 설정
						board[j][move - 1] = 0;

						// 제일 가까운 for문 탈출
						break;
					}

					// 제일 마지막에 추가된 인형과 현재 빼려고하는 인형이 같을경우
					if (board[j][move - 1] == stack.peek()) {

						// 제일 최근에 추가된(Top) 데이터 삭제
						stack.pop();

						// 같은 인형이 2개닌깐 +2
						answer += 2;
					} else

						// 아니면 장바구니에 넣기
						stack.push(board[j][move - 1]);

					// 인형을 뺀 곳에 0으로 설
					board[j][move - 1] = 0;
					break;
				}
			}
		}
		return answer;
	}
</code></pre>