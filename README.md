# common-vue
table searchGroup loading popWindow tabs pagination
# how to use the table component?
# <table
# the table head（表头行 Array）
# :columns="gridColumns"
# the table data（表数据 Array）
# :data=""
# the table head style（表头行样式 String）
# :thead-style=""
# the even row style（表数据偶数行样式 String）
# :even-li=""
# the odd row style （表数据基数行样式 String）
# :odd-li=""
# need select all btn in table head?（是否显示表头行前面的全选按钮 Boolean）
# :select-all=""
# use to change select one status（用于改变每一行的选中状态）
# :a=""
# use to check select all yes or no?（判断全选按钮选中 Boolean）
# :all=""
# show the photo in the first column(after the choose btn) yes or no?（是否在表数据第一了【选中按钮之后】显示图片 Boolean）
# :show-photo=""
# the photo style（图片的样式 String）
# :photo-class=""
# 单选按钮事件
# @choose=""
# 全选按钮事件
# @totalchoose=""
# ></table>


# how to use the searchGroup component?
# <search-group
# input group infomation （input框 Object）
# :box-info=""
# input group style（input组的样式 String）
# :box-info-class=""
# select group infomation （select框 Object）
# :select-info=""
# select group style（select组的样式 String）
# :select-info-class=""
# button group （按钮组 Array）
# :btn-group=""
# btn group style（按钮组的样式 String）
# :btn-group-class=""
# show time box group?（是否显示时间框组件 Boolean）
# :show-time-search=""
# time box start descript（第一个时间框前面的描述字 String）
# :start=""
# time box end descript（第二个时间框前面的描述字 String）
# :end=""
# start time value（开始时间的值 String）
# :stime=""
# end time value（结束时间的值 String）
# :etime=""
# time group style（time组的样式 String）
# :time-group-class=""
# 添加按钮事件
# @add="add()" 
# 删除按钮事件
# @del="del()" 
# 编辑按钮事件
# @edit="edit()" 
# 搜索按钮事件
# @search="search()" 
# 清空按钮事件
# @clear="clear()" 
# 导出按钮事件
# @download="download()
# 父组件取得开始时间事件
# @stimechange="stimechange" 
# 父组件取得结束时间事件
# @etimechange="etimec
# ></search-group>