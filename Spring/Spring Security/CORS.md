- [CORS (Cross-Origin Resource Sharing)](#cors-cross-origin-resource-sharing)
  - [배경](#배경)
  - [원인](#원인)
  - [해결](#해결)
    - [참고](#참고)


### CORS (Cross-Origin Resource Sharing)
브라우저는 기본적으로 SOP 정책을 따르고 있다. 

그래서 개발을 할 때 발생하는 SOP의 불편함을 해소하면서, 보안을 지키기 위해 등장한 것이 CORS(Cross-Origin Resource Sharing)이다.

"CORS를 지키면, '다른 출처'에서도 데이터를 불러올 수 있게 해줄게!"

즉, CORS란 도메인이 다른 서버끼리 리소스를 주고 받을 때 보안을 위해 설정된 정책

그렇다면 같은 출처와 다른 출처는 어떻게 구분할까?

![image](https://github.com/JeongGiSeong/TIL/assets/80134129/96770155-1370-48fd-bf67-0eb351cb1779)


#### 배경
AWS EC2로 백엔드 서버를 열었음.   
나(localhost:8080)는 잘 되는데 프론트엔드(localhost:5173)에서 CORS 오류가 발생.

<br>

1. Spring Security에서 CORS 비활성화 > 그래도 안 됨.

``` java
.csrf(AbstractHttpConfigurer::disable)
.cors(AbstractHttpConfigurer::disable)
```

<br>

2. AWS EC2 보안그룹 인바운드 규칙에서 프론트엔드 포트(5173) 오픈 > 그래도 안 됨
   
<br>

#### 원인
  CORS를 비활성화한다는 것은 서버가 다른 도메인에서 오는 요청을 허용하지 않겠다는 의미.   
  반대로 CORS를 활성화한다는 것은 서버가 다른 도메인에서 오는 요청을 허용하겠다는 의미.

<br>

#### 해결
```java
.cors(cors -> cors
  .configurationSource(request -> {
      var corsConfiguration = new org.springframework.web.cors.CorsConfiguration();
      corsConfiguration.setAllowedOrigins(List.of("*"));
      corsConfiguration.setAllowedMethods(List.of("*"));
      corsConfiguration.setAllowedHeaders(List.of("*"));
      return corsConfiguration.applyPermitDefaultValues();
  }));
```


##### 참고
https://velog.io/@effirin/CORS%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
