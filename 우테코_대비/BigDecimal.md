## BigDecimal

### 생성

```
BigDecimal THOUSAND = new BigDecimal("1_000");
BigDecimal ZERO = BigDecimal.ZERO;
BigDecimal userTotalMoney = new BigDecimal(String.valueOf(100_000));
```

### 모든 연산은 새로운 BigDecimal에 대입

```
BigDecimal resultRate = new BigDecimal("10");
resultRate = resultRate.add(new BigDecimal("100"));
resultRate = resultRate.subtract(new BigDecimal("100"));
resultRate = resultRate.multiply(new BigDecimal("100"));
resultRate = resultRate.add(new BigDecimal("100"));
```

### 소수 첫번쨰 자리에서 반올림

```
private BigDecimal calculateResultRate(BigDecimal totalPrize, BigDecimal ticketBudget) {
  return totalPrize.multiply(HUNDRED)
          .divide(ticketBudget, 1, RoundingMode.HALF_EVEN);
}
```
