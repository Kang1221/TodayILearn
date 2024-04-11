# JPA Repository

### Spring Data repository abstraction
> The goal of Spring Data repository abstraction
> - significantly reducing the amount of boilerplate code required to implement data access layers for various persistence stores.

Spring Data repository abstraction의 목표는 무엇이냐. <br>
데이터 저장소에 대한 엑세스 계층을 구현하는데 필요한 boilerplate code(최소한의 변경으로 여러곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드)의 양을 크게 줄이는 것!


### What is JPA Repository
> Java Persistence API


### Core Concept
> The central interface in the Spring Data repository abstraction is `Repository`. <br>
> It takes the domain class to manage as well as the identifier type of the domain class as type arguments.<br> 
> This interface acts primarily as a marker interface to capture the types to work with and to help you to discover interfaces that extend this one.





### Super interfaces
- CrudRepository<T,ID>
- ListCrudRepository<T,ID>
- ListPagingAndSortingRepository<T,ID>
- PagingAndSortingRepository<T,ID>
- QueryByExampleExecutor<T>
- Repository<T,ID>

<br>

`CrudRepository`

```java
public interface CrudRepository<T, ID extends Serializable>
    extends Repository<T, ID> {
                                                                                                                       (1)
    <S extends T> S save(S entity);
                                                                                                                       (2)
    T findOne(ID primaryKey);
                                                                                                                       (3)
    Iterable<T> findAll();

    Long count();
                                                                                                                       (4)
    void delete(T entity);
                                                                                                                       (5)
    boolean exists(ID primaryKey);
                                                                                                                       (6)
    // … more functionality omitted.
}
```
1. Saves the given entity.
2. Returns the entity identified by the given id.
3. Returns all entities.
4. Returns the number of entities.
5. Deletes the given entity.
6. Indicates whether an entity with the given id exists.

➡️  기본적인 CRUD 기능 제공

<br>

📍 우리가 보통 JPARepository를 상속받아 구현해 findAll 메소드를 사용하면 리턴타입이  `List`임!

그런데 이 CrudRepository의 findAll 리턴타입은 `Iterable`임을 확인할 수 있음.

우리가 편하게 JPARepository의 List 리턴타입의 findAll을 쓸 수 있는 이유는 JPARepository가 ListCrudRepository를 상속받기 때문!

> `ListCrudRepository` <br>
It offers equivalent methods, 
but they return List where the CrudRepository methods return an Iterable.



<br><br>

`PagingAndSortingRepository`

On top of the CrudRepository there is a PagingAndSortingRepository.
It adds additional methods to ease paginated access to entities

CrudRepository를 상속하여 페이징 처리 기능을 추가함

```java
public interface PagingAndSortingRepository<T, ID extends Serializable> 
  extends CrudRepository<T, ID> {

  Iterable<T> findAll(Sort sort);

  Page<T> findAll(Pageable pageable);
}
```
➡️  Paging 기능, sorting 제공



<br>

> `ListPagingAndSortingRepository`
> <br>
It offers equivalent methods, but returns a List where the PagingAndSortingRepository methods return an Iterable
> <br><br>
> ➡️ 같은 기능이지만 리턴타입이 `List` 이도록! 

<br>

In addition to query methods, query derivation for both count and delete queries is available. 
The following list shows the interface definition for a derived count query:
- count query
```java
interface UserRepository extends CrudRepository<User, Long> {

long countByLastname(String lastname);
}
```

- delete query
```java
interface UserRepository extends CrudRepository<User, Long> {

  long deleteByLastname(String lastname);

  List<User> removeByLastname(String lastname);
}
```


<br>
<br>


---

### Reference
https://docs.spring.io/spring-data/jpa/reference/jpa.html
https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html
