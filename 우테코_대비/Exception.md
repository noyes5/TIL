## Exception

- 관련된 에러메시지를 모아 클래스를 만듬
- 만약 한 개만 필요할 것 같으면 ExceptionMessage, 여러개면 \*\*\*Exception으로 작성

### 1번 방식

```
public enum ExceptionMessage {
    INVALID_BALL_AMOUNT("볼의 갯수는 3개여야 합니다."),
    INVALID_NUMERIC_INPUT("숫자만 입력이 가능합니다."),
    INVALID_NUMBER_LENGTH("숫자는 세자리만 입력이 가능합니다."),
    INVALID_NUMBER_RANGE("1부터 9까지의 숫자만 입력 가능합니다."),
    INVALID_GAME_COMMAND("1 또는 2를 입력해야 합니다.");

    private String message;

    ExceptionMessage(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
```

### 2번 방식

```
public enum ExceptionMessage {
    CANNOT_REMOVE_STATION("역의 갯수가 작아 삭제할 수 없습니다."),
    NO_SUCH_COMMAND("선택할 수 없는 기능입니다."),
    DUPLICATED_STATION_MESSAGE("이미 등록된 역입니다."),
    DUPLICATION_LINE_MESSAGE("이미 등록된 노선입니다."),
    ALREADY_REGISTERED_IN_LINE("이미 노선에 역이 등록되어 있습니다."),
    INVALID_SECTION_INDEX("구간 값을 제대로 입력해주세요."),
    INVALID_LINE_NAME("존재하지 않는 노선 이름입니다."),
    INVALID_NUMERIC_INPUT("입력값은 숫자만 입력가능합니다."),
    INVALID_STATION_NAME("존재하지 않는 역 이름입니다."),
    INVALID_STATION_NAME_LENGTH("역 이름은 두 글자 이상 입력해야 합니다."),
    MIN_LINE_NAME_LENGTH("노선 이름은 2글자 이상이어야 합니다."),
    STATION_DELETE_NOT_ALLOWED("노선에 등록된 역은 삭제할 수 없습니다.");

    private String message;
    private static final String BASE_MESSAGE = "[ERROR] %s";

    ExceptionMessage(String message) {
        this.message = String.format(BASE_MESSAGE, message);
    }

    public String getMessage() {
        return message;
    }
}

```
