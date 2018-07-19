# Notes

### CSS

1、flex布局中justify-content: space-between方法的排版问题

Q:当最后一行不满三个时，因为是两端布局，所以会出现问题。

A：使用after伪元素来解决该布局bug

```
父亲元素:after{
	content:'',
	width:子元素宽度，
}
```
