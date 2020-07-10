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