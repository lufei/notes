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