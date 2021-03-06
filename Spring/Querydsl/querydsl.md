### 프로젝션과 결과 DTO로 반환

1. 프로퍼티 접근

   ```java
   List<MemberDto> result = queryFactory.select(Projections.bean(MemberDto.class,
   member.username,
   member.age)) .from(member)
   .fetch();
   ```

2. 필드 직접 접근

   ```java
   List<MemberDto> result = queryFactory.select(Projections.fields(MemberDto.class,
   member.username,
   member.age)) .from(member)
   .fetch();
   ```

   * 프로퍼티나, 필드 접근 생성 방식에서 이름이 다를 때 해결 방안 
   * ExpressionUtils.as(source,alias) : 필드나, 서브 쿼리에 별칭 적용 
   * username.as("memberName") : 필드에 별칭 적용

   ```java
    List<UserDto> fetch = queryFactory.select(Projections.fields(UserDto.class,
   member.username.as("name"), ExpressionUtils.as(
   ) ).from(member)
   .fetch();
   ```

   

3. 생성자 사용

   ```java
   @Getter
   @Setter
   @NoArgsConstructor
   @AllArgsConstructor
   public class MenuResponseDto {
       private BigInteger id;
       private String name;
       private int price;
   }
   ```

   

   ```java
   ㅉ		@Override
       public List<MenuResponseDto> findMenuResponseDto(Long restaurantId) {
           return queryFactory
                   .select(Projections.constructor(MenuResponseDto.class, menu.id, menu.name, menu.price ))
                   .from(menu)
                   .where(menu.restaurant.id.eq(restaurantId))
                   .fetch();
       }
   
   ```

   

### 페이징 적용하기

컨트롤러

* http://localhost:8080/api/v1/post?size=5&page=0

````java
@ApiOperation(value = "식당 정보 수정 요청 조회", notes = "식당 정보 수정 요청을 조회합니다.")
@GetMapping("/api/v1/post")
public ResponseEntity<?> getPost(Pageable pageable){
  Page<PostResponseDto> posts = postService.getPost(pageable);
	ApiResponse response = new ApiResponse(true, "식당 정보 수정 요청 조회 완료");
	response.putData("posts", posts);
  return ResponseEntity.ok(response);
}
````



리포지토리

```java
@Override
public Page<PostResponseDto> findAllPostResponseDto(Pageable pageable) {
	List<PostResponseDto> content = queryFactory
                .select(Projections.fields(PostResponseDto.class, post.id, 
                                           post.restaurant.id.as("restaurantId"), post.imageUrl, post.claim))
                .from(post)
                .offset(pageable.getOffset())
                .limit(pageable.getPageSize())
                .fetch();

  JPAQuery<Post> countQuery = queryFactory
                .select(post)
                .from(post);

  return PageableExecutionUtils.getPage(content, pageable, countQuery::fetchCount);
}
```



### SQL function 호출

* 사용하는 방언에 함수가 등록되어 있는지 확인하기

```java
public class MySQLDialect extends Dialect {
...
	public MySQLDialect() {
		super();
		registerFunction( "ascii", new StandardSQLFunction( "ascii", StandardBasicTypes.INTEGER ) );
		registerFunction( "bin", new StandardSQLFunction( "bin", StandardBasicTypes.STRING ) );
		registerFunction( "char_length", new StandardSQLFunction( "char_length", StandardBasicTypes.LONG ) );
  	registerFunction( "rand", new NoArgSQLFunction( "rand", StandardBasicTypes.DOUBLE ) );
		...
	}
}		
```

* 사용하기

```java
// group_concat() 사용하기
Expressions.stringTemplate("group_concat({0})",menu.name).as("menu"))
```

```java
//rand() 사용하기
Expressions.numberTemplate(Double.class, "rand()").asc()
```



### 랜덤 정렬하기

```
.orderBy(Expressions.numberTemplate(Double.class, "rand()").asc())
```



### 별칭으로 정렬하기

```java
 NumberPath<Long> aliasLike = Expressions.numberPath(Long.class, "like");
 List<Tuple> tuples = queryFactory
                .select(restaurant, userLiking.id.count().as(aliasLike))
                .from(restaurant)
                .leftJoin(restaurant.userLikings, userLiking)
                .where( longitudeBetween(condition.getLongitude(), condition.getRadius()),
                        latitudeBetween(condition.getLatitude(), condition.getRadius()),
                        nameLike(condition.getName()))
                .groupBy(restaurant.id)
                .orderBy(aliasLike.asc())
                .fetch();
```

