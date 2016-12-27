1 JPA

JPA Java Persistence API

2 新的知识

2.1 Spring Data jpa1.10 new

3 依赖

Maven pom依赖

```
<dependencies>

<dependency>

<groupId>org.springframework.data</groupId>

<artifactId>spring-data-jpa</artifactId>

</dependency>

<dependencies>

```

当前的Spring Data Module 需要至少Spring Framework 4.2.9 RELEASE版，推荐使用最新版

4 使用Spring Data Repository工作



Spring Data repository 的目标就是极大的减少数据库上数据访问层的代码量。



4.1 核心概念

Spring Data repository的核心接口就是Reposity。这个Repository接口是把entity class以及和此entity相关联的主键Id作为接口泛型参数。其中CrudReposity接口提供了entity class实体类的crud操作(增删改查操作)。

```java
public interface CrudRepository<T, ID extends Serializable>
extends Repository<T, ID> {
<S extends T> S save(S entity); ①
T findOne(ID primaryKey); ②
Iterable<T> findAll(); ③
Long count(); ④
void delete(T entity); ⑤
boolean exists(ID primaryKey); ⑥
// … more functionality omitted.
}
```

这个是CrudRepository接口里包含的方法。可以看到其参数是T 和与T关联的ID；可以看到上面6个方法：1，保存一个实体，2，根据主键ID获取一个实体，3，获取所有的实体对象并且返回一个可迭代的集合，4获取实体总数量，5，删除一个实体，6，根据主键ID判断一个实体是否存在。

Note:Spring Boot推荐我们使用一些特定的接口如JpaRepository以及MongoRepository，这两个接口都继承CrudRepository，并且扩展了相应的功能。

PagingAndSortingRepository

这个接口比较有意思，我们开发Web应用时少不了用到分页技术，其中这个接口就是专门用于分页的。

```java
public interface PagingAndSortingRepository<T, ID extends Serializable>
extends CrudRepository<T, ID> {
Iterable<T> findAll(Sort sort);
Page<T> findAll(Pageable pageable);
}
```

下面举个例子：

比如我们有一个实体类 User，现在我们要获取20个作为第一页，你可以用下面这段代码

```java
PagingAndSortingRepository<User, Long> repository = // … get access to a bean
Page<User> users = repository.findAll(new PageRequest(1, 20));
```



CountQuery

```java
public interface UserRepository extends CrudRepository<User, Long> {
Long countByLastname(String lastname);
}
```



DeleteQuery

```java
public interface UserRepository extends CrudRepository<User, Long> {
Long deleteByLastname(String lastname);
List<User> removeByLastname(String lastname);
}
```