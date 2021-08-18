### 리졸버(resolver)

`gql` 에서는 데이터를 가져오는 구체적인 과정을 직접 구현 해야 한다. `gql` 쿼리문 파싱은 대부분의 `gql` 라이브러리에서 처리를 하지만, `gql`에서 데이터를 가져오는 구체적인 과정은 `resolver(리졸버)`가 담당하고, 이를 직접 구현 해야 한다. 프로그래머는 `resolver`를 직접 구현해야하는 부담은 있지만, 이를 통해서 데이터 `source`의 종류에 상관 없이 구현이 가능 한다.

`gql` 쿼리에서는 각각의 필드마다 함수가 하나씩 존재 한다고 생각하면 된다. 이 함수는 다음 타입을 반환한다. 이러한 각각의 함수를 `리졸버(resolver)`라고 한다. 만약 필드가 스칼라 값(문자열이나 숫자와 같은 `primitive` 타입)인 경우에는 실행이 종료된다. 즉 더 이상의 연쇄적인 리졸버 호출이 일어나지 않는다. 하지만 필드의 타입이 스칼라 타입이 아닌 우리가 정의한 타입이라면 해당 타입의 리졸버를 호출되게 된다.

```graphql
type Query {
  users: [User]
  user(id: ID): User
  limits: [Limit]
  limit(UserId: ID): Limit
  paymentsByUser(userId: ID): [Payment]
}

type User {
  id: ID!
  name: String!
  sex: SEX!
  birthDay: String!
  phoneNumber: String!
}

type Limit {
  id: ID!
  UserId: ID
  max: Int!
  amount: Int
  user: User
}

type Payment {
  id: ID!
  limit: Limit!
  user: User!
  pg: PaymentGateway!
  productName: String!
  amount: Int!
  ref: String
  createdAt: String!
  updatedAt: String!
}
```

> 여기에서는 User와 Limit는 1:1의 관계이고 User와 Payment는 1:n의 관계이다.

```graphql
{
  paymentsByUser(userId: 10) {
    id
    amount
  }
}
```

```graphql
{
  paymentsByUser(userId: 10) {
    id
    amount
    user {
      name
      phoneNumber
    }
  }
}
```

위 두 `gql` 쿼리는 동일한 쿼리명을 가지고 있지만, 호출 되는 리졸버 함수의 갯수는 아래가 더 많다. 각각의 리졸버 함수에는 내부적으로 데이터베이스 쿼리가 존재한다. 이 말인즉, 쿼리에 맞게 필요한 만큼만 최적화하여 호출 할 수 있다는 의미이다. 내부적으로 로직 설계를 어떻게 하느냐에 따라서 달라 질 수 있겠지만, 이러한 재귀형의 리졸버 체인을 잘 활용 한다면, 효율적인 설계가 가능 하다.

```graphql
 Query: {
    paymentsByUser: async (parent, { userId }, context, info) => {
        const limit = await Limit.findOne({ where: { UserId: userId } })
        const payments = await Payment.findAll({ where: { LimitId: limit.id } })
        return payments
    },
  },
  Payment: {
    limit: async (payment, args, context, info) => {
      return await Limit.findOne({ where: { id: payment.LimitId } })
    }
  }
```

리졸버 함수는총 4개의 인자를 받는다.

- 첫번째 인자는 parent로 연쇄적 리졸버 호출에서 부모 리졸버가 리턴한 객체입니다. 이 객체를 활용해서 현재 리졸버가 내보낼 값을 조절 할 수 있다.

- 두번째 인자는 args로 쿼리에서 입력으로 넣은 인자이다.

- 세번째 인자는 context로 모든 리졸버에게 전달이 됩니다. 주로 미들웨어를 통해 입력된 값들이 들어 있다. 로그인 정보 혹은 권한과 같이 주요 컨텍스트 관련 정보를 가지고 있다.

- 네번째 인자는 info로 스키마 정보와 더불어 현재 쿼리의 특정 필드 정보를 가지고 있다. 잘 사용하지 않는 필드이다.
