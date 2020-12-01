---
title: "프로그래머스-LEVEL1-완주하지 못한 선수"
date: 2020-12-01 10:06:00 +0900
categories: Algorithm
---
풀지못하여 구글링하였다

HashMap의 getOrDefalut(Object key, V defaultValue)는 
지정된 키가 매핑되는 값을 반환하거나 키에 대한 매핑이없는 경우 defaultValue를 반환합니다.

사용한 이유는 참가중에 동명이인이 있을 수 있으므로 사용


<pre><code>
	public String solution(String[] participant, String[] completion) {
		String answer = "";
		HashMap<String, Integer> hm = new HashMap<>();

		// getOrDefault를 사용하여 해쉬맵에 참가자가 없으면 0 + 1 동명이인이 있으면 그 키에 대한 값 + 1
		for (String player : participant)
			hm.put(player, hm.getOrDefault(player, 0) + 1);

		// 완주한 인원으로 기존 해쉬맵에 참가자 있는 사람은 -1
		for (String player : completion)
			hm.put(player, hm.get(player) - 1);

		// 참가하지 못한 사람은 1이상이므로 
		for (String key : hm.keySet()) {
			if (hm.get(key) != 0) {
				answer = key;
				break;
			}
		}
		return answer;
	}
</code></pre>