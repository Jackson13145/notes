# Notes

## 目录

* [CSS](#CSS)
  * [flex布局排版](#flex布局排版问题)
* [JS](#JS)
  * [每秒copy目标数组中的一个值到新数组中](#每秒copy目标数组中的一个值到新数组中)
  * [数组随机选取](#数组中随机选取某项元素)
  * [数组去重](#数组去重)
  * [数组重组](#数组重组)
  
## CSS

### flex布局排版问题

Q：justify-content:space-between方法，当最后一行不满三个时，因为是两端布局，所以会出现问题。

A：使用after伪元素来解决该布局bug

```css
父亲元素:after{
  content:'',
  width:子元素宽度，
}
```
## JS
### 每秒copy目标数组中的一个值到新数组中

```js
let targetArr = [1,2,3,4,5]
let currentArr = []

const copyTargetArr = (arr) => {
  let tmp = arr.slice()  //浅拷贝targetArr
  let getFrist = setInterval(()=>{
    if (tmp[0]) {
      currentArr.push(tmp.shift())
      //删除tmp第一个元素，并返回该元素的值
    }else{
      clearInterval(getFrist);
    }
  },1000);
}

copyTargetArr(targetArr)
```
### 数组中随机选取某项元素

(1)随机选取1项

```js
const randomSelectOne = (arr) => {
  return  arr[Math.floor(Math.random() * arr.length)]
}
```
(2)随机选取N项

```js
const randomSelect = (arr, num) => {
  return arr.sort(() =>
    0.5 - Math.random()
  ).slice(0, num)
}
```
### 数组去重

(1)基本数组

[1]利用ES6的Array.from()/扩展运算符 以及 Set

```js
function unique(arr){
  return Array.from(new Set(arr));
}
```

```js
function unique(arr){
  return [...new Set(arr)];
}
```
[2]利用indexOf判断是否存在于新数组中

```js
var newArr = [];
for(var i in arr) {
 if(newArr.indexOf(arr[i]) === -1) {
 	newArr.push(arr[i])
 }
}
 return newArr;
}

```
(2)对象数组

[1]利用对象的键名不能重复的特点

```js
unique(arr){
  let unique = {};
   arr.forEach((item) => {
     unique[JSON.stringify(item)]=item;//键名不会重复
   })
   arr = Object.keys(unique).map(function(u){ 

     return JSON.parse(u);
   })
   return arr;
}
```
[2]利用对象其中一个键名不能重复的特点（顺序:前者为尊）

```js
funticon unique(arr){
  let result = {};
  let finalResult=[];
  let item

  arr.forEach((item) => {
    result[JSON.stringify(item.id)]=item;//键名id不会重复
  })
  for(item in result){
    finalResult.push(result[item]);
  }

  return finalResult;
}
```
[3]利用对象其中一个键名不能重复的特点（顺序:后来居上）

```js
funticon unique(arr){
  const result = {}
  const finalResult = []
  const keys = []

  arr.forEach(item => {
    result[item.id] = item // 键名id不会重复
    keys.push(item.id)
    if (keys.indexOf(item.id) !== keys.lastIndexOf(item.id)) {
      keys.splice(keys.indexOf(item.id), 1)
    }
  })

  keys.forEach(item => {
    finalResult.push(result[item])
  })

  return finalResult
}
```
### 数组重组

(1)将数组中key相同的对象组成新的数组

```js
const formatGiftDetail = (data) => {
  const newData = {}

  data.forEach(obj => {
    const array = newData[obj.sameKey] || []

    array.push(obj)
    newData[obj.sameKey] = array
  })

  return newData
}
```