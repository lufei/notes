# Layui

## 获取select选择的值

```javascript
form.on('select(filter)', function(data){
    console.log(data.elem); //得到select原始DOM对象
    console.log(data.value); //得到被选中的值
    console.log(data.othis); //得到美化后的DOM对象
    console.log(data.elem[data.elem.selectedIndex].text); // 得到选中的文本内容
});      
```