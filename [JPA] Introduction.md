# JPA Introduction
## 기본 기능
* EntityManagerFactory 생성
* EntityManager 생성

```java

public class JpaMain {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();
        tx.begin();

        try {
            /** 등록 */
            Member member = new Member();
            member.setId(1L);
            member.setName("seomoon");
            em.persist(member);

            /** 조희              */
            Member findMember = em.find(Member.class, 1L);
            System.out.println("findMember = " + findMember.getId() + ", name: " + findMember.getName());
            /** 수정 */
            findMember.setName("eveningStar");
            /** 삭제 */
            em.remove(findMember);
            
            tx.commit();
        } catch (Exception e) {
            tx.rollback();
        } finally {
            em.close();
        }
        emf.close();
    }
}
```
## 주의점
* EntityManagerFactory는 하나만 생성해서 application 전체에서 공유한다.
* entityManager는 쓰레드간 공유하지 않는다.
* JPA의 모든 데이터 변경은 transaction 안에서 실행한다.
* 
