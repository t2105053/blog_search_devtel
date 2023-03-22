# 블로그 검색 서비스
### Description
검색어로 카카오, 네이버 오픈 API를 이용하여 "블로그 검색 서비스"를 만들려고 합니다.

<br>

## 개발환경
- JAVA11
- Spring-boot
- Gradle
- H2, JPA
- Redis

## API 명세서 링크

## JAR 다운 링크

## 구현항목 
- [블로그 검색] 키워드를 통해 블로그를 검색할 수 있어야 합니다.
  - 카카오 블로그 검색 API를 Default로 사용했습니다.
  - vender 구분값을 추가해 원하는 API 를 사용하도록 하였습니다
  - 검색 키워드를 JPA를 활용하여 h2 디비에 저장하였습니다.
- [블로그 검색] 검색 결과에서 Sorting(정확도순, 최신순) 기능을 지원해야 합니다.
- [블로그 검색] 검색 결과는 Pagination 형태로 제공해야 합니다.
  - 카카오,네이버 API의 페이징 값이 상이함을 인지하고 구현하였습니다.
- [블로그 검색] 추후 카카오 API 이외에 새로운 검색 소스가 추가될 수 있음을 고려해야 합니다.
  - Sort상수 Vender상수 등 Enum 으로 상수를 관리해 카카오 및 네이버 등 관리에 용의하게 구현했습니다.
  - Interface 통해 유연, 확장에 용의하게 구현했습니다.
- [인기검색어 목록] 사용자들이 많이 검색한 순서대로, 최대 10개의 검색 키워드를 제공합니다.
- [인기검색어 목록] 검색어 별로 검색된 횟수도 함께 표기해 주세요.
- [추가] 멀티 모듈 구성 및 모듈간 의존성 제약
  - boot-blog [어플리케이션 모듈], boot-api [API 모듈] , data-blog [DATA 모듈] 로 모듈을 나눠 의존성 제약을 두고 의존도를 낮춰 개발하였습니다.
- [추가] 동시성 이슈가 발생할 수 있는 부분을 염두에 둔 구현 (예시. 키워드 별로 검색된 횟수의 정확도)
  - 동시성을 제어하기 위해 싱글스레드인 Redis 를 이용하였스며 Redis 의 내부적으로 synchronizer.invoke() 하는 increment 를 사용했습니다.
  - 아쉬운 점은 Redis 데이트럴 backup 및 동기화 관리를 완성못해 아쉽게나 검색어 조회시 log성 데이터가 DB에 저장되도록 구현했습니다..
- [추가] 카카오 블로그 검색 API에 장애가 발생한 경우, 네이버 블로그 검색 API를 통해 데이터 제공

## 추가 라이브러리
- WEBFLUX
  - WebClient 사용을 위해 추가했습니다.
- Redis
  - 동시성 제어를 위해 추가했습니다.