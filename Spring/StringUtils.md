- [String.isEmpty()](#stringisempty--)
- [(deprecated)StringUtils.isEmpty()](#-deprecated-stringutilsisempty--)
- [StringUtils](#stringutils)
  * [hasLength()](#haslength--)
  * [hasText()](#hastext--)

<hr>

### String.isEmpty()

Java에서 제공하는 String 클래스의 isEmpty()
length가 0인지만 체크하기 때문에 null 체크가 안되어, String이 null 일 경우에는 NullPointerException(NPE)이 발생
```java
    /**
     * Returns {@code true} if, and only if, {@link #length()} is {@code 0}.
     *
     * @return {@code true} if {@link #length()} is {@code 0}, otherwise
     * {@code false}
     *
     * @since 1.6
     */
    @Override
    public boolean isEmpty() {
        return value.length == 0;
    }
```


### (deprecated)StringUtils.isEmpty()
null 또는 공백("")인지 체크. 문자열이 " "인 경우엔 False가 반환됨.
```java
    /** @deprecated */
    @Deprecated
    public static boolean isEmpty(@Nullable Object str) {
        return str == null || "".equals(str);
    }
```


### StringUtils

#### hasLength()
null 체크 후 String 클래스의 isEmpty()를 호출하여 길이까지 체크.
``` java
StringUtils.hasLength(null) = false
StringUtils.hasLength("") = false
StringUtils.hasLength(" ") = true

public static boolean hasLength(@Nullable String str) {
        return str != null && !str.isEmpty();
    }
```

#### hasText()
null 체크 후 " " 같이 공백 문자만 들어있는 경우도 체크
```java
StringUtils.hasLength(null) = false
StringUtils.hasLength("") = false
StringUtils.hasLength(" ") = false
public static boolean hasText(@Nullable String str) {
        return str != null && !str.isBlank();
    }
```

