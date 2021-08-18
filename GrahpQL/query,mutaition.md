### 쿼리/뮤테이션(query/mutation)

쿼리와 뮤테이션 그리고 응답 내용의 구조는 상당히 직관적 이다. 요청하는 쿼리문의 구조와 응답 내용의 구조는 거의 일치 한다.

> <img src="http://tech.kakao.com/files/graphql-example.png"/>
> GraphQL 쿼리문(좌측)과 응답 데이터 형식(우측)

`gql`에서는 굳이 쿼리와 뮤테이션을 나누는데 내부적으로 들어가면 사실상 이 둘은 별 차이가 없다. 쿼리는 데이터를 읽는데 사용하고, 뮤테이션은 데이터를 변조 하는데 사용한다는 개념 적인 규약을 정해 놓은 것 뿐이다.

```graphql
{
  human(id: "1000") {
    name
    height
  }
}

query HeroNameAndFriends($episode: Episode) {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}
```

일반적인 경우 클라이언트에서 `static`한 쿼리문을 작성하지는 않는다. 주로 정보를 불러올때 `id` 값이나, 다른 인자 값을 가지고 데이터를 불러 온다. `gql`에는 쿼리에 변수라는 개념이 있는데, 이 개념은 이러한 용처를 위해 존재한다. `gql`을 구현한 클라이언트에서는 이 변수에 프로그래밍으로 값을 할당 할 수 있는 함수 인터페이스가 존재한다. `react apollo client`의 경우에는 `variables` 라는 파라미터에 원하는 값을 넣어주면 된다.

```graphql
query getStudentInfomation($studentId: ID){
  personalInfo(studentId: $studentId) {
    name
    address1
    address2
    major
  }
  classInfo(year: 2018, studentId: $studentId) {
    classCode
    className
    teacher {
      name
      major
    }
    classRoom {
      id
      maintainer {
        name
      }
    }
  }
  SATInfo(schoolCode: 0412, studentId: $studentId) {
    totalScore
    dueDate
  }
}
```

오퍼레이션 네임 쿼리는 매우 편리 하다. 굳이 비유하자면 쿼리용 함수 입니다. 데이터베이스 에서의 프로시져(`procedure`) 개념과 유사하다고 생각하면 된다. 오퍼레이션 네임 쿼리는 한번의 인터넷 네트워크 왕복으로 여러분이 원하는 모든 데이터를 가져 올 수 있다.
