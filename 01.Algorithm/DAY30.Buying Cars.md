# DAY30 Buying Cars
在一定数目的预算内，最多能买多少辆车
```js
    function buyingCars(budget, prices) {
      let ans = 0
      prices.sort((a, b) => a-b)
      for(const num of prices) {
        if(budget >= num) {
          ans += 1
          budget -= num
        }
        else break
      }
      return ans
    }
    console.log(buyingCars(200, [50, 30, 30, 80, 90, 100]))
```

