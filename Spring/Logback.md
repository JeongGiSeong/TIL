- [Logback이란?](#logback이란)
  - [왜 Logging이 필요한가?](#왜-logging이-필요한가)
  - [왜 Logback을 사용하는가?](#왜-logback을-사용하는가)
  - [Log Level](#log-level)
  - [Log Pattern](#log-pattern)
  - [logback-spring.xml](#logback-springxml)


# Logback이란?

Java 기반 Logging Framework 중 하나로 SLF4J 의 구현체  
Spring Boot에서 기본 로깅 시스템으로 사용되는데, logback-spring.xml 파일을 통해 설정

## 왜 Logging이 필요한가?
1. 디버깅: 프로그램이 정상적으로 동작하지 않을 때, 문제를 찾기 위해 사용  
2. 모니터링: 프로그램이 동작하는 상태를 확인하기 위해 사용
3. 보안
4. 사용자 행동 분석

## 왜 Logback을 사용하는가?
1. 성능: 빠르고 적은 메모리 사용  
2. 기능: 자동 리로딩, 조건에 따른 로깅, 로그 파일 분할/압축/롤링 등


## Log Level
- TRACE : 디버깅용 로그
- DEBUG : 디버깅용 로그
- INFO : 정보성 로그
- WARN : 경고성 로그
- ERROR : 에러 로그

## Log Pattern
- %-5level : 로그 레벨, -5는 출력의 고정폭 값(5글자)
- %msg : - 로그 메시지 (=%message)
- ${PID:-} : 프로세스 아이디
- %d : 로그 기록시간
- %p : 로깅 레벨
- %F : 로깅이 발생한 프로그램 파일명
- %M : 로깅일 발생한 메소드의 명
- %l : 로깅이 발생한 호출지의 정보
- %L : 로깅이 발생한 호출지의 라인 수
- %thread : 현재 Thread 명
- %t : 로깅이 발생한 Thread 명
- %c : 로깅이 발생한 카테고리
- %C : 로깅이 발생한 클래스 명
- %m : 로그 메시지
- %n : 줄바꿈(new line)
- %% : %를 출력
- %r : 애플리케이션 시작 이후부터 로깅이 발생한 시점까지의 시간(ms)



## logback-spring.xml
    ERROR 레벨이 안찍히던 이유 : filter 설정만 하고, root level에 ERROR를 추가하지 않았음

``` xml
<configuration scan="true" scanPeriod="30 second">
<!--    30초마다 로그 갱신 -->

<!-- 콘솔 환경 로그 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss SSS} %highlight(%-5level) %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 파일로 로그 저장 -->
        <file>logs/application.log</file>
        <encoder>
            <pattern>%d{MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
            <!-- [시간][로그레벨][thread이름] logger이름 메시지 \n -->
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>logs/application.%d{yyyy-MM-dd}.log</fileNamePattern>
            <!-- 로그 파일의 이름 패턴 -->
            <!-- logs/application.2024-06-20.log -->
            <maxHistory>7</maxHistory>
            <!-- 7일간 유효 -->
            <totalSizeCap>50MB</totalSizeCap>
            <!-- 로그 파일 최대 보관 크기. 최대 크기를 초과하면 가장 오래된 로그 자동 제거 -->
        </rollingPolicy>
    </appender>

    <appender name="ERROR_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>logs/error.log</file>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>error</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <encoder>
            <pattern>%d{MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>logs/error.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
            <totalSizeCap>50MB</totalSizeCap>
        </rollingPolicy>
    </appender>


    <root level="INFO">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
        <appender-ref ref="ERROR_FILE" />
    </root>
</configuration>
```