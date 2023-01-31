## 컬렉션 API 개선

자바에서는 적은 요소를 포함하는 리스트를 어떻게 만들까?

휴가를 함께 보내려는 친구 이름을 포함하는 그룹을 만들려 한다.

```java
List<String> friends = new ArrayList<>();
friends.add("Raphael");
friends.add("Olivia");
friends.add("Thibaut");
```

<br/>

새 문자열을 저장하는데도 많은 코드가 필요하다.

다음처럼 Arrays.asList() 팩토리 메서드를 이용하면 코드를 간단하게 줄일 수 있다.

<br/>

고정 크기의 리스트를 만들었으므로 요소를 갱신할 순 있지만 

새 요소를 추가하거나 요소를 삭제할 순 없다.

```java
List<String> friends = Arrays.asList("Raphael", "Olivia", "Thibaut");
```

<br/><br/>

## 맵 처리

## forEach 메서드

맵에서 키와 값을 반복하면서 확인하는 작업은 잘 알려진 귀찮은 작업 중 하나다.

```java
for(Map.Entry<String, Integer> entry : ageOfFriends.entrySet()) {
		String friend = entry.getKey();
		Integer age = entry.getValue();
		System.out.println(friend + " is " + age + " years old");
}
```

<br/>

자바 8서부터 Map 인터페이스는 BiConsumer(키와 값을 인수로 받음)를 인수로 받는 forEach 메서드를 

지원하므로 코드를 조금 더 간단하게 구현할 수 있다.

```java
ageOfFriends.forEach((friend, age) -> System.out.println(friend + " is " + age + " years old"));
```

<br/><br/>

## 정렬 메서드

다음 두 개의 새로운 유틸리티를 이용하면 맵의 항목을 값 또는 키를 기준으로 정렬할 수 있다.

- Entry.comparingByValue
- Entry.comparingByKey

<br/>

바꾸기 전 코드.

```java
Map<String, String> favouriteMovies = 
											Map.ofEntries(entry("Raphael", "Star Wars"),
											entry("Cristina", "Matrix"),
											entry("Olivia", "James Bond"));
```

<br/>

변경된 코드

```java
favouriteMovies
			.entrySet()
			.stream()
			.sorted(Entry.comparingByKey())
			.forEachOrdered(System.out::println);
```

<br/>

실행 결과 : 

```
Cristina=Matrix
Olivia=James Bond
Raphael=Star Wars
```

<br/><br/>

>**Reference** 
> <br/> [모던 자바 인 액션](http://www.yes24.com/Product/Goods/77125987)