## Enum

```
public enum GameAction {
    RETRY("R"),
    QUIT("Q");

    private final String command;

    GameAction(String command) {
        this.command = command;
    }

    public static GameAction from(String input) {
        return Arrays.stream(GameAction.values())
                .filter(command -> command.command.equals(input))
                .findFirst()
                .orElseThrow(() -> new IllegalArgumentException(ERROR_GAME_COMMAND.getMessage()));
    }
    //필요한 경우 사용
    public static List<String> getFormatedList() {
        return Arrays.stream(MainCommand.values())
                .map(it -> String.format("%s. %s", it.command, it.title))
                .collect(Collectors.toList());
    }
}
```

- 숫자일 경우 == 로 비교
