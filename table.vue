<template>
  <div class="tablebox">
    <ul class="tablehead" :class="theadStyle">
      <li v-for="key in columns" :style="{'width': key.width, 'height': key.height, 'line-height':key.height}" :class="key.class">
        <div v-if="key.attribute == 'selectRadio' && selectAll">
          <input type="checkbox" :class="key.class" v-model="myAll" @change="totalchoose">
        </div>
        <span v-else> {{key.text}}</span>        
      </li>
    </ul>
    <ul class="tablelist">
      <li v-for="(item, index) in data" class="clearfix" :class="(index % 2==0) ? evenLi : oddLi">
       <!--  <div v-for="key in columns" :style="{'width': key.width, 'height': key.height, 'line-height':key.height}" class="ellipsis" :class="item[key.attribute].class"> -->
       <div v-for="key in columns" :style="{'width': key.width}" class="ellipsis" :class="item[key.attribute].class">
       <div v-if="key.attribute == 'selectRadio'" class="imgbox">
          <input type="radio" v-if="!selectAll" @change="choose(item,index)" name="shop" v-model="item.id" :value="a">
          <input type="checkbox" v-if="selectAll" v-model="item.check" @change="choose(item,index)">
          <div :class="photoClass" v-if="showPhoto">
            <img v-bind:src="'http://img.sanliandan.com/img/20170919_59c0d6443bb9a.jpg'" alt="图片信息">
          </div>
        </div>
          <div v-if="key.attribute == 'operate'" class="btnGroup">
            <div v-for="subitem in item[key.attribute]" :style="{'height': key.height}" style="display: flex;align-items: center">
              <span :class="subitem.class">{{subitem.text}}</span>
            </div>
          </div>
          <span v-if="key.attribute != 'operate' && key.attribute != 'selectRadio'">{{item[key.attribute]}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'table',
  props: {
    columns: Array,
    data: Array,
    theadStyle: String,
    evenLi: String,
    oddLi: String,
    selectAll: Boolean,
    a: Number,
    // 全选
    all: Boolean,
    // 是否在第一列显示图片
    showPhoto: Boolean,
    // 图片样式
    photoClass: String
  },
  data () {
    return {
      myAll: this.all
    }
  },
  methods: {
    choose (item, index) {
      let obj = {
        item: item,
        index: index
      }
      this.$emit('choose', obj)
    },
    totalchoose () {
      this.$emit('totalchoose')
    }
  }
}
</script>
<style lang="less" scoped>
.clearfix:after {
  content: "";
  display: block;
  clear: both;
  visibility: hidden;
  line-height: 0;
  font-size: 0;
  height: 0;
}
.tablehead li {
  float: left;
}
// .tablelist li div {
//   float: left;
// }
/*--内容超出省略--*/
.ellipsis {
  display: inline-block;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.btnGroup {
  display: flex;
  justify-content: center;
}  
.choose{
    padding-top: 12px;
    position: relative;
    width: 12.6%;
    min-width: 174px;
  }
  .choose input{
    margin-left: 22px;
  }
  .imgbox {
    display: flex;
    align-items: center;
    justify-content:center;
  }
</style>
