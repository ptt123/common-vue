<template>
  <div class="searchGroup">
    <div class="clearfix group">
      <div :class="boxInfoClass" v-for="item in boxInfoArr">
        <span>{{item.text}}</span>
        <input v-model="item.value" :class="item.class">
      </div>
      <div :class="selectInfoClass" v-for="item in selectInfoArr">
        <span>{{item.text}}</span>
          <select type="text" :class="item.class" :id="item.id">
            <option value="">--请选择--</option>
            <option v-for="subitem in item.value" :value="subitem.value">{{subitem.desc}}</option>
          </select>
      </div>
      <div class="fl mr40" v-if="showTimeSearch" :class="timeGroupClass">
        <span>{{start}}</span>
        <div class="start">
          <datepicker placeholder="请选择" language="zh" :format="format" class="time" v-model="mystime" @input="stimechange"></datepicker>
          <span class="iconfont icon-rili"></span>
        </div>
        <span class="ml20 mr20">{{end}}</span>
        <div class="start">
          <datepicker placeholder="请选择" language="zh" :format="format" class="time" v-model="myetime" @input="etimechange"></datepicker>
          <span class="iconfont icon-rili"></span>
        </div>
      </div>
      <div :class="btnGroupClass">
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='search'" @click="search">{{item.text}}</span>
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='clear'" @click="clear">{{item.text}}</span>
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='del'" @click="del">{{item.text}}</span>
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='edit'" @click="edit">{{item.text}}</span>
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='add'" @click="add">{{item.text}}</span>
        <span v-for="item in btnGroup" :class="item.class" v-if="item.class=='download'" @click="download">{{item.text}}</span>
      </div>
    </div>    
  </div>
</template>
<script>
  import Datepicker from 'vuejs-datepicker'
  export default {
    name: 'searchGroup',
    components: {
      Datepicker
    },
    props: {
      boxInfo: Object,
      selectInfo: Object,
      btnGroup: Array,
      showTimeSearch: Boolean,
      start: String,
      end: String,
      stime: String,
      etime: String,
      btnGroupClass: String,
      boxInfoClass: String,
      selectInfoClass: String,
      timeGroupClass: String
    },
    data () {
      return {
        boxInfoArr: [],
        selectInfoArr: [],
        format: 'yyyy-MM-dd',
        mystime: this.stime,
        myetime: this.etime
      }
    },
    mounted () {
      for (let i in this.boxInfo) {
        this.boxInfoArr.push(this.boxInfo[i])
      }
      for (let j in this.selectInfo) {
        this.selectInfoArr.push(this.selectInfo[j])
      }
    },
    methods: {
      add () {
        this.$emit('add')
      },
      del () {
        this.$emit('del')
      },
      edit () {
        this.$emit('edit')
      },
      search () {
        this.$emit('search')
      },
      clear () {
        this.$emit('clear')
      },
      download () {
        this.$emit('download')
      },
      stimechange () {
        this.$emit('stimechange', this.mystime)
      },
      etimechange () {
        this.$emit('etimechange', this.myetime)
      }
    }
  }
</script>
<style lang="less">
.clearfix:after {
  content: "";
  display: block;
  clear: both;
  visibility: hidden;
  line-height: 0;
  font-size: 0;
  height: 0;
}
.start{
  display: inline-block;
  position: relative;
}

.icon-rili{
  position: absolute;
  color: #b3b3b3;
  font-size: 20px;
  right: 5px;
  top: 0;
}
.time input{
  border: 1px solid #e5e5e5 !important;
  width: 164px;
  height: 32px !important;
  line-height: 32px !important;
  border-radius: 2px;
  padding-left: 3px !important;
}
.group {
  display: flex;
  align-items: center;
  height: 50px;
}
</style>