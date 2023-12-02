## 테스트 코드 로직모음

### 공통인자가 필요할 때는 @BeforeEach() 활용

```
private GameResult gameResult;

@BeforeEach
void setUp() {
    gameResult = GameResult.byDefault();
}
```

### 한 개의 값을 간단히 테스트 할 때

```
@DisplayName("테스트 이름")
@Test
void 메소드_이름() {
  assertThat();
}
```

### 여러 개의 값을 테스트 할 때

- 한가지 값을 여러개 테스트 할때 : valueSource 활용

```
@DisplayName("유효하지 않은 값이 들어오면 예외 테스트")
@ParameterizedTest
@ValueSource(strings = {"A", "B", "재시작", "12312"})
void 유효하지않은_입력_검증(String input) {
    assertThatThrownBy(() -> GameAction.from(input))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessage(ERROR_GAME_COMMAND.getMessage());
}
```

- 여러 종류의 값을 테스트 할때 : CsvSource 활용

```
@DisplayName("숫자가 입력되면 해당하는 심볼이 반환되는지 테스트")
@ParameterizedTest
@CsvSource({
        "1, U",
        "0, D"
})
void 숫자를_위치로_반환_검증(int inputNumber, String expected) {
    assertThat(BridgePosition.makeBridgeSpace(inputNumber)).isEqualTo(expected);
}
```

### input에 대한 검증

```
class InputValidatorTest {

    @Nested
    class InvalidInput {
        @DisplayName("입력크기를 벗어나면 예외 테스트")
        @ParameterizedTest
        @ValueSource(strings = {"223232934839448394893434934893493", "1890273490312390218920139201213890"})
        void 초과_크기_검증(String input) {
            assertThatThrownBy(() -> InputValidator.validateUserNumber(input))
                    .isInstanceOf(IllegalArgumentException.class)
                    .hasMessage(INVALID_NUMERIC_INPUT.getMessage());
        }

        @DisplayName("입력이 세자리 아닌경우 예외 테스트")
        @ParameterizedTest
        @ValueSource(strings = {"12", "7891"})
        void 세자리_검증(String input) {
            assertThatThrownBy(() -> InputValidator.validateUserNumber(input))
                    .isInstanceOf(IllegalArgumentException.class)
                    .hasMessage(INVALID_NUMBER_LENGTH.getMessage());
        }

        @DisplayName("입력이 유효한 범위가 아니면 예외 테스트")
        @ParameterizedTest
        @ValueSource(strings = {"012", "804", "430"})
        void 범위내_숫자검증(String input) {
            assertThatThrownBy(() -> InputValidator.validateUserNumber(input))
                    .isInstanceOf(IllegalArgumentException.class)
                    .hasMessage(INVALID_NUMBER_RANGE.getMessage());
        }
    }

    @Nested
    class ValidInput {
        @ParameterizedTest
        @ValueSource(strings = {"123", "459", "928", "281"})
        void 정상_입력_검증(String input) {
            assertThatCode(() -> InputValidator.validateUserNumber(input))
                    .doesNotThrowAnyException();
        }
    }
}
```
