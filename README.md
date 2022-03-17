## 가. TDD 개발 방법론의 프로그래밍 순서
1. 실패하는 작은 단위의 테스트를 작성한다.(처음에는 컴파일조차 되지 않을 수 있다.)
2. 테스트를 통과하기 위한 프로덕션 코드를 작성한다.(정답이 아닌 가짜를 구현할 수 있다.)
3. 그 다음의 테스트 코드를 작성한다. 단, 실패 테스트가 없을 경우에만 성공 테스트를 작성한다.
4. 새로운 테스트를 통과하기 위해 프로덕션 코드를 추가 또는 수정한다.
5. 1번~4번 단계를 반복하여 실패/성공의 모든 테스트 케이스를 작성한다.
6. 개발된 코드들에 대해 모든 중복을 제거하며 리팩토링을 진행한다.

## 나. 문제설명
1. 구현 프로그램은 멤버십 적립 서비스
2. 지원하는 멤버십은 네이버, 카카오, 라인 3가지 멤버십이 있으며, 사용자는 원하는 멤버십을 등록할 수 있다.
3. 포인트 적립비율은 결제금액의 1%로 고정, 추후에는 고정금액(1000원)으로 확자 적립이될 수 있어야 한다.
4. 요구사항에 만족하는 REST API를 구현하고, TDD 방식으로 구현

## 다. 기능 요구 사항
1. 멤버십 연결하기, 멤버십 조회, 멤버십 연결끊기, 포인트 적립 API 를 구현
2. 사용자 식별값은 문자열 형태이며, "X-USER-ID" 라는 HTTP Header 로 전달. 이 값은 포인트 적립할 때 바코드 대신 사용된다.
3. Content-type 응답 형태는 application/json(JSON) 형식을 사용
4. 각 기능 및 제약사항에 대한 개발을 TDD, 단위테스트 기반으로 진행

## 라. 요구사항에 따른 상세기술 구현 사항

### 1. 등록 요구사항
- 1-1. 기능
    - 멤버십을 등록
- 1-2. 요청
    - 사용자식별값, 멤버십 이름, 포인트
- 1-3. 응답
    - 멤버십 ID, 멤버십 이름

### 2. 전체조회 요구사항
- 2-1. 기능
    - 모든 멤버십 조회
- 2-2. 요청
    - 사용자식별값
- 2-3. 응답
    - {멤버십 아이디, 멤버십 이름, 포인트, 가입일시}의 멤버십 리스트

### 3. 상세조회 요구사항
- 3-1. 기능
    - 본인의 멤버십 조회
- 3-2. 요청
    - 사용자식별값, 멤버십 아이디
- 3-3. 응답
    - 멤버십 아이디, 멤버십 이름, 포인트, 가입일시

### 4. 삭제 요구사항
- 4-1. 기능
    - 멤버십 삭제
- 4-2. 요청
    - 사용자식별값, 멤버십 번호
- 4-3. 응답
    - 없음

### 5. 포인트 적립
- 5-1. 기능
  - 사용자 멤버십 포인트를 결제 금액의 1% 만큼 적립
- 5-2. 요청
    - 사용자식별값, 멤버십 아이디, 사용금액
- 5-3. 응답
    - 없음
- 5-4. 기타
    - 고정금액 적립 방식으로의 확장이 유연하도록 구현

## 마. 기술 요구 사항
- 언어 : Java 8
- Framework : Spring Boot 2.6
- ORM : JPA
- DB : H2