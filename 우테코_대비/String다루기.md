## String 다루기

### 빈 줄 추가하기

- 자바에서 제공하는 lineSeparator() 사용

```
 private static final String NEW_LINE = System.lineSeparator();
```

### 앞뒤와 중간에 구분자가 필요한 경우

- StringJoiner 사용

```
public static final String BRIDGE_START = "[ ";
public static final String BRIDGE_SEPARATOR = " | ";
public static final String BRIDGE_END = " ]";

StringJoiner result = new StringJoiner(BRIDGE_SEPARATOR, BRIDGE_START, BRIDGE_END);
```
