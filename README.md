# common-vue
table searchGroup loading popWindow tabs pagination
how to use the table component?
<table
// the table head（表头行 Array）
:columns="",
// the table data（表数据 Array）
:data="",
// the table head style（表头行样式 String）
:thead-style="",
// the even row style（表数据偶数行样式 String）
:even-li="",
// the odd row style （表数据基数行样式 String）
:odd-li=""
// need select all btn in table head?（是否显示表头行前面的全选按钮 Boolean）
:select-all="",
// use to change select one status（用于改变每一行的选中状态）
:a="",
// use to check select all yes or no?（判断全选按钮选中 Boolean）
:all="",
// show the photo in the first column(after the choose btn) yes or no?（是否在表数据第一了【选中按钮之后】显示图片 Boolean）
:show-photo="",
// the photo style（图片的样式 String）
:photo-class=""
></table>
