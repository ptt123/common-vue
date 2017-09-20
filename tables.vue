<!-- 测试表格和搜索组件，勿删 -->
<template>
  <div class="tables">
    <div class="tablesbox">
      <search-group 
      :box-info="boxInfo" 
      :select-info="selectInfo" 
      :btn-group="btnGroup" 
      :show-time-search="showTimeSearch" 
      :end="endtimespan" 
      :start="starttimespan"
      @add="add()" 
      @del="del()" 
      @edit="edit()" 
      @search="search()" 
      @clear="clear()" 
      @download="download()" 
      :btn-group-class="btnGroupClass" 
      :box-info-class="boxInfoClass" 
      :select-info-class="selectInfoClass" 
      @stimechange="stimechange" 
      @etimechange="etimechange" 
      :time-group-class="timeGroupClass">
      </search-group>
      <my-table 
      :columns="gridColumns" 
      :data="gridData" 
      :even-li="bgWhite" 
      :odd-li="bgGray" 
      :thead-style="theadstyle" 
      :select-all="selectAll" 
      :a="a" :all="all"
      @choose="choose" 
      @totalchoose="totalchoose" 
      :show-photo="showPhoto" 
      :photo-class="photoClass">
      </my-table>
    </div>
  </div>
</template>
<script>
  import myTable from '@/childpage/table.vue'
  import searchGroup from '@/childpage/searchGroup.vue'
  export default{
    name: 'tables',
    components: {
      myTable,
      searchGroup
    },
    data () {
      return {
        bgWhite: 'bg-white p1',
        bgGray: 'bg-gray p1',
        theadstyle: 'theadstyle p1 clearfix',
        btnGroupClass: 'btnGroup',
        boxInfoClass: 'box-info',
        selectInfoClass: 'select-info',
        // 是否显示全选按钮
        selectAll: true,
        a: -1,
        shopid: -1,
        // 全选
        all: false,
        // 是否在第一列显示图片
        showPhoto: true,
        photoClass: 'photo',
        timeGroupClass: 'times',
        gridColumns: [
          {
            text: '',
            width: '10%',
            attribute: 'selectRadio',
            height: '42px',
            class: 'choice'
          },
          {
            text: '名字',
            attribute: 'name',
            width: '15%',
            height: '42px',
            class: 'nameColum'
          }, {
            text: '性别',
            attribute: 'sex',
            width: '15%',
            height: '42px',
            class: 'sexColum'
          }, {
            text: '年龄',
            attribute: 'age',
            width: '20%',
            height: '42px',
            class: 'ageColum'
          }, {
            text: '体重',
            attribute: 'weight',
            width: '20%',
            height: '42px',
            class: 'weightColum'
          }, {
            text: '操作',
            attribute: 'operate',
            width: '20%',
            height: '42px',
            class: 'operateColum'
          }
        ],
        // 接口请求的数据
        gridData: [
          {
            selectRadio: {
              class: 'chooce'
            },
            name: '张三去买包子的路上遇到狗子',
            sex: '男',
            age: '20',
            weight: '50',
            operate: [
              {
                text: '编辑',
                class: 'add'
              }, {
                text: '删除',
                class: 'del'
              }
            ]
          }, {
            selectRadio: {
              class: 'chooce'
            },
            name: '张三去买包子的路上遇到狗子',
            sex: '男',
            age: '20',
            weight: '50',
            operate: [
              {
                text: '编辑',
                class: 'add'
              }, {
                text: '删除',
                class: 'del'
              }
            ]
          }
        ],
        boxInfo: {
          sort: {
            text: '分类',
            value: '',
            class: 'inputbox'
          },
          brand: {
            text: '品牌',
            value: '',
            class: 'inputbox'
          }
        },
        selectInfo: {
          sort: {
            text: '性别',
            class: 'selectbox',
            id: 'sex',
            value: [
              {
                desc: '男',
                value: 1
              }, {
                desc: '女',
                value: 0
              }
            ]
          },
          operate: {
            text: '操作',
            class: 'selectbox',
            id: 'operate',
            value: [
              {
                desc: '同意',
                value: 1
              }, {
                desc: '不同意',
                value: 0
              }
            ]
          }
        },
        btnGroup: [
          {
            text: '搜索',
            class: 'search'
          }, {
            text: '清空条件',
            class: 'clear'
          }, {
            text: '导出',
            class: 'download'
          }, {
            text: '+新增商品',
            class: 'add'
          }
        ],
        showTimeSearch: true,
        endtimespan: '到',
        starttimespan: '下单时间',
        stime: '',
        etime: ''
      }
    },
    methods: {
      clear () {
        this.boxInfo.sort.value = ''
        this.boxInfo.brand.value = ''
        document.getElementById('sex').value = ''
        document.getElementById('operate').value = ''
      },
      search () {
        alert('search')
        console.log(this.stime)
        console.log(this.etime)
      },
      add () {
        alert('add')
      },
      del () {
        alert('del')
      },
      edit () {
        alert('edit')
      },
      download () {
        alert('download')
      },
      stimechange (stime) {
        let date = new Date(stime)
        this.stime = date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate()
      },
      etimechange (etime) {
        let date = new Date(etime)
        this.etime = date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate()
      },
      // 单选的选择
      // choose (data) {
      //   console.log(data)
      //   if (data.item.id === this.a) {
      //     this.shopid = data.index
      //   }
      //   // this.user_id = item.user_id
      // },
      totalchoose () {
        var that = this
        if (this.all === true) {
          this.count.list.forEach(function (item, index, arr) {
            that.ids.push(item.guid)
            item.check = true
          })
          this.multi = true
        } else {
          this.count.list.forEach(function (item, index, arr) {
            item.check = false
          })
          that.ids = []
          this.multi = false
        }
      },
      // 多选的选择
      choose (item, index) {
        var length = this.count.list.length
        var store = this.count.list[index]
        this.ids.push(item.guid)
        this.chooselength = store.check ? this.chooselength + 1 : this.chooselength - 1
        /* console.log('chooselength',this.chooselength) */
        if (this.chooselength === length) {
          this.all = true
        } else {
          this.all = false
        }

        if (this.chooselength > 1) {
          this.multi = true
        } else {
          this.multi = false
        }
      }
    }
  }
</script>

<style lang="less">
@import "../assets/reset.less";
@import "../assets/page.css";

.tables{
  width: 90%;
  padding-top: 60px;
  margin-left: 180px;
  min-width: 980px;
  background: @bg-gray;
}

.tablesbox {
  width: 98.5%;
  margin: 20px 0 0 1%;
  box-shadow: 3px 3px 10px #eeeeee;   
  min-width: 911px;
  background: #ffffff;
  .fs14;
}
.name {
  width: 25%;
}
.sex {
  width: 25%;
}
.age {
  width: 25%;
}
.weight {
  widht: 25%;
}
.theadstyle {
  background: #eeeeee;
  height: 42px;
  line-height: 42px;
}
.bg-white {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #eeeeee;
  .clearfix;
}
.bg-gray{
  background: #ffffff;
  border-bottom: 1px solid #eeeeee;
  display: flex;
  align-items: center;
  .clearfix;
}
.theadstyle {
  height: 42px;
  line-height: 42px;
}
.clearfix:after {
  content: "";
  display: block;
  clear: both;
  visibility: hidden;
  line-height: 0;
  font-size: 0;
  height: 0;
}
.search {
  display: inline-block;
  text-align: center;
  height: 30px;
  line-height: 30px;
  width: 84px;
  color: #ffffff;
  background: #5a95f1;
  margin-right: 22px;
  border-radius: 15px;
}
.clear {
  height: 28px;
  line-height: 28px;
  width: 84px;
  border-radius: 15px;
  border: 1px solid #5a95f1;
  font-size: 12px;
  text-align: center;
  color: #5a95f1;
  display: inline-block;
}
.download {
  height: 28px;
  line-height: 28px;
  width: 84px;
  border-radius: 15px;
  border: 1px solid #5a95f1;
  font-size: 12px;
  text-align: center;
  color: #5a95f1;
  display: inline-block;
}
.add {
  height: 30px;
  line-height: 30px;
  text-align: center;
  color: #ffffff;
  width: 94px;
  border-color: #ffab53;
  background: #ffab53;
  border-radius: 15px;
  display: inline-block;
  float: right;
}
.del {
  height: 30px;
  line-height: 30px;
  text-align: center;
  color: #ffffff;
  width: 94px;
  border-color: #ffab53;
  background: #ff0000;
  border-radius: 15px;
  display: inline-block;
  float: right;
}
.inputbox {
  height: 30px;
  width: 55%;
  border: 1px solid #e5e5e5;
}
.selectbox {
  height: 32px;
  border: 1px solid #e5e5e5;
}
.btnGroup {
  width: 100%;
}
.box-info {
  width: 10%;
  min-width: 100px;
  float: left;
}
.select-info {
  width: 10%;
  min-width: 120px;
  float: left;
}
.operateColum {
  text-align: center;
}
.choice{
  display: flex !important;
  align-items: center;
  // -webkit-appearance: none; 
  // display: block;
  // outline: none;
  width: 18px;
  height: 18px;
  border-radius: 10px;
  // cursor: pointer;
  // vertical-align: middle;
  background-image: url('../assets/image/bg-radio.png') no-repeat;
}
.chooce {
  .clearfix;
  display: flex;
  align-items: center;
  justify-content: center;
}
.times {
  width: 20%;
  min-width: 500px;
}
.photo{
  display: flex;
  align-items:center;
  margin-top: 10%;
  margin-bottom: 10%;
  width: 80%;
  height: 100px;
  margin-left: 10%;
  justify-content: center;
}
.photo img {
  max-width: 85%;
  max-height: 95%;
}
</style>