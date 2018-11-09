# Notes

### CSS

1、flex布局中justify-content: space-between方法的排版问题

Q：当最后一行不满三个时，因为是两端布局，所以会出现问题。

A：使用after伪元素来解决该布局bug

```
父亲元素:after{
  content:'',
  width:子元素宽度，
}
```
### JS
1、每秒copy目标数组中的一个值到新数组中

```
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
2、数组中随机选取某项元素

(1)随机选取1项

```
const randomSelectOne = (arr) => {
  return  arr[Math.floor(Math.random() * arr.length)]
}
```
(2)随机选取N项

```
const randomSelect = (arr, num) => {
  return arr.sort(() =>
    0.5 - Math.random()
  ).slice(0, num)
}
```
3、数组去重

(1)基本数组

[1]利用ES6的Array.from()/扩展运算符 以及 Set

```
function unique(arr){
  return Array.from(new Set(arr));
}
```

```
function unique(arr){
  return [...new Set(arr)];
}
```
[2]利用indexOf判断是否存在于新数组中

```
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

```
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
[2]利用对象其中一个键名不能重复的特点

```
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