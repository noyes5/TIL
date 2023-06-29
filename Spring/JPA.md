# JPA(Java Persistance API)

> 자바 진영에서 ORM기술에 대한 API 표준 명세. 자바에서 제공하는 인터페이스.


ORM이란?

Object-Relational Mapping 로서 객체와 DB테이블을 매핑시켜주는 기술

쿼리를 직접 작성하지 않아도 객체를 테이블화하여 DB에 접근이 가능함

## 스프링에서 사용법

gradle인 경우

build.gradle
```
dependency {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
}
```

maven인 경우

pom.xml
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```


application.properties
```
spring.jpa.show-sql=true // 실행시 생성된 sql문을 콘솔에 보여줌
spring.jpa.hibernate.ddl-auto=none // 테이블 또는 행이 없으면 자동 생성해줌을 막아줌
```

hibernate는 JPA 구현체로서 주로 사용함.(다른 JPA 구현체도 있다.)

이 hibernate를 통해 직접 쿼리문을 적지 않아도 콘솔에서 작성된 쿼리문을 볼 수 있다.



----
## 예시 코드
```Java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;

import javax.persistence.EntityManager;
import java.util.List;
import java.util.Optional;

public class JpaMemberRepository implements MemberRepository {

    private final EntityManager em;

    public JpaMemberRepository(EntityManager em) {
        this.em = em;
    }

    @Override
    public Member save(Member member) {
        em.persist(member);
        return member;
    }

    @Override
    public Optional<Member> findById(Long id) {
        Member member = em.find(Member.class, id);
        return Optional.ofNullable(member);
    }

    @Override
    public Optional<Member> findByName(String name) {
        List<Member> result = em.createQuery("select m from Member m where m.name = :name", Member.class)
                .setParameter("name", name)
                .getResultList();

        return result.stream().findAny();
    }

    @Override
    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class).getResultList();
    }
}

```

먼저 EntityManager를 DI 시키고 이 객체를 이용해서 CRUD 할 수 있다.


[메소드]

persist() : 객체를 테이블에 삽입

find(Member.class, id) : 테이블에서 매개변수 값으로 객체 조회

createQuery("select m from Member m", Member.class) : JPQL 문법으로 FROM절에 객체 이름이 들어가며, 해당 객체에 대한 값들 조회

