### 스키마/타입(schema/type)

데이터베이스 스키마(schema)를 작성할 때의 경험을 SQL 쿼리 작성으로 비유한다면, `gql` 스키마를 작성할 때의 경험은 `C`, `C++`의 헤더파일 작성에 비유할 수 있다.

```graphql
type Character {
  name: String!
  appearsIn: [Episode!]!
}
```

- 오브젝트 타입 : `Character`
- 필드 : `name`, `appearsIn`
- 스칼라 타입 : `String`, `ID`, `Int` 등
- 느낌표(!) : `필수 값을 의미(non-nullable)`
- 대괄호([, ]) : `배열을 의미(array)`
