# Select2

## 数据回显

```javascript
$('select2_id').select2({"data":[{"id":1,"text":"111"},{"id":2,"text":"222"}]});
$('#select2_id').val([1,2]).trigger("change");
```

## 从远程获取数据

```javascript
$('#select2_id').select2({
    placeholder: '输入名称',
    ajax: {
        url: "url",
        dataType: 'json',
        delay: 250,
        data: function (params) {
            return {
                search: params.term,
            };
        },
        processResults: function (data) {
            return {
                results: data.data
            };
        },
        cache: true
    },
    minimumInputLength: 1
});
```

## 下拉框不能输入

!> 检查下modal模态窗口中的div中是否有属性`tabindex="-1"`

## 设置宽度

设置宽度需要设置给`span`，即

```css
.select2 span {
    width: 150px;
}
```
