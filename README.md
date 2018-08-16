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