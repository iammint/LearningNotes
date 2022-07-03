# DAY37 Hexadecimal Numbers Conversion
## From decimal to binary
```js
function decimalToBinary(n) {
  let ans = ""
  while(n > 0) {
    ans = (n%2).toString() + ans
    n = n/2
  }
  return ans
}
```

## From binary to decimal
```js
function binToDec(num) {
    let ans = 0
    for(let i of num) {
        ans = ans*2 + Number(i)
    }
    return ans
}
console.log(binToDec("1101"))
```

## From hexadecimal to decimal
```js
function hexaToDecimal(n) {
  let ans = 0
  let numberMap = {
    0: "0",
    1: "1",
    2: "2",
    3: "3",
    4: "4",
    5: "5",
    6: "6",
    7: "7",
    8: "8",
    9: "9",
    10: "a",
    11: "b",
    12: "c",
    13: "d",
    14: "e",
    15: "f",
  }
  for(let i of n) {
    ans = ans*16 + numberMap[i.toLowerCase()]
  }
  return ans
}
```

## From decimal to hexadecimal
```js
function decimalToHexa(n) {
  let ans = ""
  let numberMap = {
    0: "0",
    1: "1",
    2: "2",
    3: "3",
    4: "4",
    5: "5",
    6: "6",
    7: "7",
    8: "8",
    9: "9",
    10: "a",
    11: "b",
    12: "c",
    13: "d",
    14: "e",
    15: "f",
  }
  while(n > 0) {
    ans = numberMap[(n%16)] + ans
    n = Math.floor(n/16)
  }
  return ans
}
//数组方法
let ans = []
let numberMap = {...}
while(n > 0) {
  ans = ans.unshift(numberMap[n%16])
  n = Math.floor(n/16)
}
return ans.join("")
```

