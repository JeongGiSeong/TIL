## UnsupportedOperationException 발생 이슈 정리
### 문제 상황
엔티티 update 테스트 코드 작성 중 UnsupportedOperationException 발생

``` java
java.lang.UnsupportedOperationException
	at java.base/java.util.ImmutableCollections.uoe(ImmutableCollections.java:142)
	at java.base/java.util.ImmutableCollections$AbstractImmutableCollection.clear(ImmutableCollections.java:149)
	at com.demo.travellybe.product.domain.Product.update(Product.java:130)
```
실제 프로젝트 동작 시에는 문제가 없지만, 테스트 코드에서만 이 오류가 발생함.

### 원인 분석
Product 객체 생성 시 사용하는 toList() 메소드가 문제. 이 메소드는 Java 16부터 추가되었으며, 스트림의 요소를 모아서 변경 불가능한 리스트를 반환함. 따라서 이 리스트에 대해 clear(), add(), addAll() 등의 수정 작업을 시도하면 UnsupportedOperationException이 발생함.

``` java
product.tickets = productCreateRequestDto.getTickets().stream()
                .map(ticketDto -> Ticket.of(ticketDto, product))
                .toList();
```

### 해결 방안
toList() 대신 collect(Collectors.toList())를 사용. collect(Collectors.toList())는 변경 가능한 리스트를 반환하므로, 이후에 리스트를 수정하는 작업도 가능함.

``` java
product.tickets = productCreateRequestDto.getTickets().stream()
                .map(ticketDto -> Ticket.of(ticketDto, product))
                .collect(Collectors.toList());
```

### 추가 정보
실제 프로젝트에서는 잘 동작했던 이유는 JPA와 Hibernate가 데이터베이스에서 엔티티를 조회할 때 컬렉션 필드를 자체적으로 감싸서 변경 가능한 컬렉션으로 만들어 주기 때문임.
