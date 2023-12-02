## Util

### 정규식 검증

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

### 일반 유틸 클래스

```
public class Util {
    public static String removeSpace(String input) {
        return input.replaceAll(Regex.SPACE.regex, Regex.NO_SPACE.regex);
    }

    public static String removeDelimiters(String input) {
        return input.replace(Regex.SQUARE_BRACKETS_START.regex, Regex.NO_SPACE.regex)
                .replace(Regex.SQUARE_BRACKETS_END.regex, Regex.NO_SPACE.regex);
    }

    public static List<String> splitByComma(String input) {
        return Arrays.asList(Util.removeSpace(input).split(Regex.COMMA.regex));
    }

    public static List<String> formatProductInfo(String input) {
        return Util.splitByComma(Util.removeDelimiters(Util.removeSpace(input)));
    }

    public static boolean isNumberic(String input) {
      try {
            return Integer.parseInt(input);
        } catch (NumberFormatException exception) {
            throw new IllegalArgumentException(INVALID_NUMERIC_INPUT.getMessage());
        }
    }

    private enum Regex {
        SPACE(" "), NO_SPACE(""),
        SQUARE_BRACKETS_START("["), SQUARE_BRACKETS_END("]"),
        COMMA(",");

        private final String regex;

        Regex(String regex) {
            this.regex = regex;
        }
    }
}
```
