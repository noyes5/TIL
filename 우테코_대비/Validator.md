## 검증

### 정규식

- 유효한 숫자 범위에 대한 검증(1~9)

```
public static final Pattern NUMBER_REGEX = Pattern.compile("^[1-9]+$");

private static boolean isNumeric(String input) {
    try {
        Integer.parseInt(input);
        return true;
    } catch (NumberFormatException exception) {
        return false;
    }
}

public static void validateUserNumber(String input) {
    if (!isNumeric(input)) {
        throw new IllegalArgumentException(INVALID_NUMERIC_INPUT.getMessage());
    }
    if (!NUMBER_REGEX.matcher(input).matches()) {
        throw new IllegalArgumentException(INVALID_NUMBER_RANGE.getMessage());
    }
}
```

- 추상 클래스 활용할 경우

```
public class Validator {
    protected static void validateBlank(final String input) {
        if (input == null || input.strip().isEmpty()) {
            throw new IllegalArgumentException(INVALID_INPUT_BLANK.getMessage());
        }
    }
}
```
