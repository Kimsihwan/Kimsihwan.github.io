---
title: "프로그래머스-LEVEL1-두개 뽑아서 더하기"
date: 2020-12-01 20:55:00 +0900
categories: Algorithm
---

내가 생각한 식
<pre><code>
	public int[] solution(int[] numbers) {
		int[] answer = {};
		
		// 결과에 중복제를 위한 HasSet
		Set<Integer> set = new HashSet<Integer>();
		for (int i = 0; i < numbers.length; i++) {
			for (int j = 1; j < numbers.length; j++) {
				if (i != j)
					set.add(numbers[i] + numbers[j]);
			}
		}
		
		// 값을 넣고 스트림을 이용하여 정렬 및 매핑하여 array에 담기
		return set.stream().sorted().mapToInt(Integer::intValue).toArray();
	}
</code></pre> 
	다른분 꺼
	 2중 for문에 안에 for문을 초기값을 1을 먼저 더해놓으면 위에 if문으로 numbers의 원소값이 같은지 비교를 안해도됨
<pre><code>
		public int[] solution(int[] numbers) {
		Set<Integer> set = new HashSet<>();

		for (int i = 0; i < numbers.length; i++) {
			for (int j = i + 1; j < numbers.length; j++) {
				set.add(numbers[i] + numbers[j]);
			}
		}

		return set.stream().sorted().mapToInt(Integer::intValue).toArray();
	}
    </code></pre> 