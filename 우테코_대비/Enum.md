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
}
```

- 숫자일 경우 == 로 비교
