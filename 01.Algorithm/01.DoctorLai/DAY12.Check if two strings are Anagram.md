# DAY12 Check if two strings are Anagram
## 异位词
> 组成字符串的字母出现的次数一样，只是顺序不一样
> 
> eg: eat/tea
```js
    function isAnagram(str1, str2) {
      if(str1.length !== str2.length) {
        return false
      }
      //需要计算每个字母出现的次数，
      //利用对象的key-value属性
      //由于对象的属性是有顺序区分的，因此需要先sort
      str1 = str1.split("").sort().join("")
      str2 = str2.split("").sort().join("")
      let countStr1 = {}
      for(let i of str1) {
        if(countStr1[i]) {
          countStr1[i] += 1
        }
        else {
          countStr1[i] = 1
        }
      }
      let countStr2 = {}
      for(let i of str2) {
        if(countStr2[i]) {
          countStr2[i] += 1
        }
        else {
          countStr2[i] = 1
        }
      }
    // check if two objects are equal
    function isEqual(obj1, obj2) {
      const obj1Keys = Object.keys(obj1)
      const obj2Keys = Object.keys(obj2)
      if(obj1Keys.length !== obj2Keys.length) {
        return false
      }
      for(const i of obj1Keys) {
        if(obj1Keys[i] !== obj2Keys[i]) {
          return false
        }
      }
      return true
    }
      return isEqual(countStr1, countStr2) 
    }

    console.log(isAnagram("tea", "eat")) 
```
![wenhao.png](https://media.haochen.me/wenhao.png)
```js
function checkAnagram(str1, str2) {
  str1 = str1.split("").sort().join("")
  str2 = str2.split("").sort().join("")
  return str1 === str2
}
console.log(checkAnagram("happy", "phpay"))//true
```
