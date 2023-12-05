## String 다루기

- String은 배열대신에 List<String> list = new ArrayList<>(배열);
  과 같이 값이 변경 가능한 것을 활용하자

### 빈 줄 추가하기

- 자바에서 제공하는 lineSeparator() 사용

```
 private static final String NEW_LINE = System.lineSeparator();
```

### 앞뒤와 중간에 구분자가 필요한 경우

- StringJoiner 사용
- 간단하게 사용할 때는 String.join(,,,); 도 가능하다.

```
public static final String BRIDGE_START = "[ ";
public static final String BRIDGE_SEPARATOR = " | ";
public static final String BRIDGE_END = " ]";

StringJoiner result = new StringJoiner(BRIDGE_SEPARATOR, BRIDGE_START, BRIDGE_END);
```

### 빈 칸 검증, 분리하기

```
public class StringUtils {
    public static boolean isBlank(String name) {
        return name == null || name.strip().isEmpty();
    }

    public static String[] splitByDelimiter(String carNames) {
        return carNames.split(",");
    }
}
```
