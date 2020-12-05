# JavaScript

## 表格点击变色再点击取消

```javascript
$('tbody').on('click', function(e) {
    // 点击变色 再次点击取消
    if (!$(e.target).parent('tr').hasClass('bg-primary')) {
        $(e.target).parent('tr').addClass('bg-primary');
    } else {
        $(e.target).parent('tr').removeClass('bg-primary');
    }
    // 点击变色并同时删除其他的
    // $(e.target).parent('tr').addClass('bg-primary').siblings('tr.bg-primary').removeClass('bg-primary');
});
```

## 表格点击变色选中复选框

```javascript
//除了表头（第一行）以外所有的行添加click事件
$('tr').slice(1).click(function (e) {
    // 忽略哪些元素点击
    if (e.target.tagName === 'BUTTON') {
        return false;
    }
    // 切换样式
    if (!$(this).hasClass('layui-table-click')) {
        $(this).addClass('layui-table-click');
    } else {
        $(this).removeClass('layui-table-click');
    }
    // 找到checkbox对象
    var chks = $("input[type='checkbox']", this);
    var tag = $(this).attr('tag');
    if (tag === 'selected') {
        // 之前已选中，设置为未选中
        $(this).attr('tag', '');
        chks.prop('checked', false);
    } else {
        // 之前未选中，设置为选中
        $(this).attr('tag', 'selected');
        chks.prop('checked', true);
    }
});
```

## 登录超时后跳出iframe

```javascript
if (top.location !== self.location) {
    top.location = self.location;
}
```

!> 加在登录页面中。
