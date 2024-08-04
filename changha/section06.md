# JDBC와 JPA 차이점 
## JDBC
- JDBC는 자바 데이터베이스 연결을 위한 API
- JDBC는 SQL을 사용하여 데이터베이스와 통신함
- JDBC는 데이터베이스의 종류와 상관없이 똑같은 코드로 데이터베이스와 통신함

## JPA
- JPA는 자바 ORM 기술로, 객체와 관계형 데이터베이스의 매핑을 처리함
- JPA는 SQL을 직접 사용하지 않고, 객체를 사용하여 데이터베이스와 통신함
- JPA는 데이터베이스의 종류와 상관없이 똑같은 코드로 데이터베이스와 통신함

## 차이점
- JPA는 데이터베이스와 객체를 매핑하는 기술일 뿐, 내부적으로는 DB와 통신을 위해 JDBC를 사용함 
- JPA도 인터페이스이므로 구현체가 필요한데, 대표적으로 Hibernate가 있다.이 Hibernate 내부에는 JDBC가 사용됨

# JDBC Template 와 JDBC Client 차이점
## JDBC Template
- JDBC Template는 JDBC를 사용하여 데이터베이스와 통신하는 클래스
- JDBC Template는 데이터베이스와 통신하는 반복적인 코드를 간결하게 작성할 수 있도록 도와줌

## JDBC Client
- JDBC Client는 스프링 6에 도입된 새로운 DB 접근 API, 더욱 현대적이고 간편한 인터페이스 제공 

```java
// jdbc template
 public User findUserById(Long id) {
    String sql = "SELECT * FROM users WHERE id = ?";
    return jdbcTemplate.queryForObject(sql, new Object[]{id}, (rs, rowNum) -> {
        User user = new User();
        user.setId(rs.getLong("id"));
        user.setUsername(rs.getString("username"));
        user.setPassword(rs.getString("password"));
        return user;
    });
}

// jdbc client
public User findUserById(Long id) {
    String sql = "SELECT * FROM users WHERE id = ?";
    return jdbcClient.sql(sql)
            .param(id)
            .queryForObject((rs, rowNum) -> {
                User user = new User();
                user.setId(rs.getLong("id"));
                user.setUsername(rs.getString("username"));
                user.setPassword(rs.getString("password"));
                return user;
            });
}
```


# 메타데이터란 

## 정의
- 스프링 컨테이너에게 빈을 등록할 때 사용하는 정보
- 어노테이션 기반 or XML 기반으로 메타데이터를 작성할 수 있음
- 함께 xml과 어노테이션을 사용할 수 있음 


# 트랜잭션 프록시
## 정의
- 기존 서비스 코드를 건들지 않고 트랜잭션을 적용할 수 있도록 도와주는 프록시
- 프록시는 일종의 대리인으로, 클라이언트의 요청을 받아 실제 서비스 객체에게 전달함
- 트랜잭션 프록시는 트랜잭션을 적용하는 역할을 함

```java 
public class OrderServiceTxProxy implements OrderService {
    private final OrderService target;
    private final PlatformTransactionManager transactionManager;

    public OrderServiceTxProxy(OrderService target, PlatformTransactionManager transactionManager) {
        this.target = target;
        this.transactionManager = transactionManager;
    }

    @Override
    public Order createOrder(String no, BigDecimal total) {
        return new TransactionTemplate(transactionManager).execute(status ->
                target.createOrder(no, total)
        );
    }

    @Override
    public List<Order> createOrders(List<OrderReq> reqs) {
        return new TransactionTemplate(transactionManager).execute(status ->
                target.createOrders(reqs)
        );
    }
}
```