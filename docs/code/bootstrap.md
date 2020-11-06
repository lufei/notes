# Bootstrap

## bootstrap-datepicker

```javascript
//只选择年份
$('.datepicker').datepicker({
   format: 'yyyy',
   language: "zh-CN",
   autoclose:true,
   startView: 2,
   minViewMode: 2,
   maxViewMode: 2
});
//选择年月
$('.datepicker').datepicker({
   format: 'yyyy-mm',
   language: "zh-CN",
   autoclose:true,
   startView: 1,
   minViewMode: 1,
   maxViewMode: 1
});
//选择年月日
$('.datepicker').datepicker({
   format: 'yyyy-mm-dd',
   language: "zh-CN",
   autoclose:true,
   startView: 0,
   minViewMode: 0,
   maxViewMode: 0
});
```

## 自定义文件上传

```html
<div class="custom-file mb-3">
  <input onchange="showFilename(this.files[0])" type="file" class="custom-file-input" id="customFile" name="filename">
  <label id="filename_label" class="custom-file-label" for="customFile">选择文件</label>
</div>

<!-- 显示文件名 -->
<script>
function showFilename(file){
    $("#filename_label").html(file.name);
}
</script>
```

### 修改Browse

```css
.custom-file-label::after {
  content: "浏览"!important;
}
```

## 计算分页

```php
/**
 * @param string $url 跳转链接
 * @param int $total 总数
 * @param int $nowPage 当前页
 * @param int $limit 分页个数
 * @param int $rollPage 显示几个链接
 * @return string
 */
function pageShow(string $url, $total = 0, $nowPage = 1, $limit = 20, $rollPage = 5)
{
    if ($total == 0) {
        return '';
    }
    // 计算分页信息
    $totalPages = ceil($total / $limit); //总页数
    $nowPage = $nowPage > 0 ? $nowPage : 1; // 当前页
    if (! empty($totalPages) && $nowPage > $total) {
        $nowPage = $total;
    }

    $parseUrl = parse_url($url);
    $path = [];
    if (isset($parseUrl['query'])) {
        // str转为数组 会处理多个page键名的问题
        parse_str($parseUrl['query'], $path);
    }
    // 当前page设为空
    $path['page'] = '';
    $url = $parseUrl['path'] . '?' . http_build_query($path);

    //计算分页临时变量
    $now_cool_page = $rollPage / 2;
    $now_cool_page_ceil = ceil($now_cool_page);

    //数字链接
    $link_page = '';
    for ($i = 1; $i <= $rollPage; ++$i) {
        if (($nowPage - $now_cool_page) <= 0) {
            $page = $i;
        } elseif (($nowPage + $now_cool_page - 1) >= $total) {
            $page = $total - $rollPage + $i;
        } else {
            $page = $nowPage - $now_cool_page_ceil + $i;
        }
        if ($page > 0) {
            if ($page != $nowPage) {
                if ($page <= $total || $page <= $rollPage) {
                    // 最后禁止点击
                    $end_class = $page > $totalPages ? 'disabled' : '';
                    $link_page .= '<li class="page-item ' . $end_class . '"><a class="page-link" href="' . $url . $page . '">' . $page . '</a></li>';
                } else {
                    break;
                }
            } else {
                $link_page .= '<li class="page-item active"><a class="page-link" href="' . $url . $page . '">' . $page . '</a></li>';
            }
        }
    }

    //上一页
    $up_row = $nowPage - 1;
    $end_class = $up_row > 0 ? '' : 'disabled';
    $up_page = '<li class="page-item ' . $end_class . '"><a class="page-link" title="上一页" href="' . $url . $up_row . '">«</a></li>';
    //下一页
    $down_row = $nowPage + 1;
    $end_class = $down_row > $totalPages ? 'disabled' : '';
    $down_page = '<li class="page-item ' . $end_class . '"><a class="page-link" title="下一页" href="' . $url . $down_row . '">»</a></li>';
    //第一页
    $end_class = $nowPage == 1 ? 'disabled' : '';
    $the_first = '<li class="page-item ' . $end_class . '"><a class="page-link" title="第一页" href="' . $url . '1"><</a></li>';
    //最后一页
    $end_class = $nowPage == $totalPages ? 'disabled' : '';
    $the_end = '<li class="page-item ' . $end_class . '"><a class="page-link" title="最后一页" href="' . $url . $totalPages . '">></a></li>';

    return '<ul class="pagination">' . $the_first . $up_page . $link_page . $down_page . $the_end . '</ul>';
}
```

```php
echo pageShow($_SERVER["REQUEST_URI"], $total, $page);
```

## 导航下拉菜单触发方式改为鼠标浮动触发

```css
.dropdown:hover>.dropdown-menu {
    display: block;
}

.dropdown>.dropdown-toggle:active {
    pointer-events: none;
}
```

## 表格点击变色再点击取消

```javascript
$('table').on('click', function(e) {
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
