# 엔티티 매핑

> JPA를 사용할 때 가장 중요한 일은 엔티티와 테이블을 매핑하는 것이다. JPA는 다양한 매핑 어노테이션을 지원하고 객체와 테이블 매핑, 기본 키 매핑, 필드와 컬럼 매핑, 연관관계 매핑 크게 4가지로 분류한 수 있다.  각각 분류마다 대표하는 어노테이션을 알아보자.



## 객체와 테이블 매핑



### @Entity

* JPA를 사용해서 테이블과 매핑할 클래스에 해당 어노테이션을 붙이며 이 클래스를 엔티티라고 부른다.
* 주의사항
  * 기본 생성자 필수
  * final클래스, enum, interface, inner에는 사용할 수 없다.
  * 저장할 필드에 final을 사용하면 안 된다.

**속성**

| 속성 | 설명                    | 기본값      |
| ---- | ----------------------- | ----------- |
| name | 엔티티 이름을 지정한다. | 클래스 이름 |



### @Table

* 엔티티와 매핑할 테이블을 지정한다. 생략하면 엔티티 이름을 테이블 이름으로 사용한다.

**속성**

| 속성              | 설명                                | 기본값      |
| ----------------- | ----------------------------------- | ----------- |
| name              | 테이블 이름을 지정한다.             | 엔티티 이름 |
| uniqueConstraints | DDL 생성 시에 유니크 제약 조건 생성 |             |



## 기본 키 매핑

* 기본키 매핑 방법은 두가지 방법이 있다. ID를 직접 할당하는 직접 할당 방법과 ID를 자동으로 할당하는 자동 생성 방법이 있다.
  * 직접 할당: @Id만 사용
  * 자동 생성: @Id와 @GeneratedValue를 사용

###  @Id

* 엔티티 클래스의 필드를 테이블의 기본 키에 매핑하며 이 필드를 식별자 필드라고 한다.



### @GeneratedValue

* 기본 키를 직접 할당하는 대신에 데이터베이스가 생성해주는 값을 사용한다.
* 데이터베이스 벤더가 지원하는 방식에 맞게 사용한다.

**strategy속성에 사용할 수 있는 전략**

| 사용 가능한 전략 | 설명                                                         |
| ---------------- | ------------------------------------------------------------ |
| IDENTITY         | 데이터베이스에 위임 / MYSQL, Postgresql, SQL Server          |
| SEQUENCE         | 데이터베이스 시퀀스 오브젝트 사용 / ORACLE / @SequenceGenerator 필요 |
| TABLE            | 키 생성용 테이블 사용 / 모든 DB에서 사용 / @TableGenerator 필요 |
| AUTO             | 방언에 따라 자동 지정 / 기본값                               |

**예시**

```java
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
```



**IDENTITY 전략**

- 기본 키 생성을 데이터베이스에 위임한다.
- 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용 한다.
- 먼저 데이터베이스에 값을 저장하고 나서 기본 키를 구할 수 있을 때 사용한다.
- JPA는 보통 트랜잭션 커밋 시점에 INSERT SQL 실행한다.
- AUTO_ INCREMENT는 데이터베이스에 INSERT SQL을 실행한 이후에 ID 값을 알 수 있다
- IDENTITY 전략은 em.persist() 시점에 즉시 INSERT SQL 실행 하고 DB에서 식별자를 조회한다.
  - 따라서 이 전략은 트랙잭션을 지원하는 쓰기 지연이 동작하지 않는다.

**SEQUENCE 전략**

* 데이터베이스 시퀀스는 유일한 값을 순서대로 생성하는 특별한 데이터베이스 오브젝트다.
* 오라클, PostgreSQL, DB2, H2 데이터베이스에서 사용한다.

**TABLE 전략**

* 키 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내 내는 전략이다.
* 모든 데이터베이스에 적용 가능하다는 장점이 있으나 성능이 좋지 못하다는 단점이 있디.



## 필드와 컬럼 매핑

### @Column

* 엔티티의 필드를 테이블의 컬럼에 매핑한다.

| 속성                   | 설명                                                         | 기본값                                                   |
| ---------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| name                   | 필드와 매핑할 테이블의 컬럼 이름                             | 객체의 필드 이름                                         |
| insertable, updatable  | 등록, 변경 가능 여부                                         | TRUE                                                     |
| nullable(DDL)          | null 값의 허용 여부를 설정한다. false로 설정하면 DDL 생성 시에 not null 제약조건이 붙는다. |                                                          |
| unique(DDL)            | @Table의 uniqueConstraints와 같지만 한 컬럼에 간단히 유니크 제 약조건을 걸 때 사용한다. |                                                          |


### @Enumerated

* 자바 enum 타입을 매핑할 때 사용
* EnumType.STRING을 사용하는 것을 권장한다.

| 속성  | 설명                                              | 기본값           |
| ----- | ------------------------------------------------- | ---------------- |
| value | EnumType.ORDINAL: enum 순서를 데이터베이스에 저장 | EnumType.ORDINAL |
| value | EnumType.STRING: enum 이름을 데이터베이스에 저장  | EnumType.ORDINAL |



### @Temporal

* 날짜 타입(java.util.Date, java.util.Calendar)을 매핑할 때 사용

* LocalDate, LocalDateTime을 사용할 때는 생략 가능(최신 하이버네이트 지원)

  

### @Lob

* 데이터베이스 BLOB, CLOB 타입과 매핑
* @Lob에는 지정할 수 있는 속성이 없다.
* 매핑하는 필드 타입이 문자면 CLOB 매핑, 나머지는 BLOB 매핑
  * CLOB: String, char[], java.sql.CLOB 
  * BLOB: byte[], java.sql. BLOB



### @Transient

* 필드 매핑을 하지 않는다.
* 주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을 때 사용



## 데이터베이스 스키마 자동 생성

> JPA는 클래스의 매핑 정보를 가지고 데이터베이스 방언을 사용해서 데이터베이스 스키마를 자동적으로 생성하는 기능을 제공한다. 이 기능을 사용하면 애플리케이션 실행 시점에 데이터베이스 테이블이 자동 생성되므로 개발자의 수고를 덜 수 있다. 하지만 자동 생성된 DDL이 운영 환경에서 사용할 만큼 완벽하지 않기 때문에 개발 용도나 참고용으로 사용하는 것이 좋다.

**특징**

* DDL을 애플리케이션 실행 시점에 자동 생성
* 테이블중심 -> 객체중심
* 데이터베이스 방언을 활용해서 데이터베이스에 맞는 적절한 DDL 생성
* 자동 생성된 DDL은 개발 장비에서만 사용



**hibernate.hbm2ddl.auto**

| 옵션        | 설명                                           |
| ----------- | ---------------------------------------------- |
| create      | 기존테이블 삭제 후 다시 생성 (DROP + CREATE)   |
| create-drop | create와 같으나 종료시점에 테이블 DROP         |
| update      | 변경된 부분만 반영(운영DB에는 사용하지 않는다) |
| validate    | 엔티티와 테이블이 정상 매핑되었는지만 확인     |
| none        | 사용하지 않음                                  |

```properties
#application.properties 예시
spring.jpa.hibernate.ddl-auto = validate
```



**주의사항**

> 운영 장비에는 절대 create, create-drop, update 사용하면 안된다. 개발 초기에는 create 또는 update를 사용하고 테스트 서버는 update 또는 validate를 사용한다. 스테이징과 운영 서버는 validate 또는 none을 사용한다.



**DDL 생성 기능**

> 데이터베이스 스키마 자동 생성 기능으로 DDL을 생성할 때 제약조건을 추가하고 싶다면 DDL 생성 기능을 이용한다. DDL 생성 기능은 DDL을 자동 생성할 때만 사용되고 JPA의 실행 로직에는 영향을 주지 않는다. 따라서 스키마 자동 생성 기능을 사용하지 않는다면 사용할 이유가 없다. 하지만 개발자가 손쉽게 제약조건을 알 수 있다는 장점이 있다.

**예시**

* 제약조건 추가: 회원 이름은 **필수**, 10자 이하
  * `@Column(nullable = false, length = 10)`
* 유니크 제약조건 추가
  * `@Table(uniqueConstraints = {@UniqueConstraint( name = "NAME_AGE_UNIQUE",**  **columnNames = {"NAME", "AGE"} )})`



**출처**

* [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)

