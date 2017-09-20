<template>
  <div class="popWindow" id="popWindow">
    <div class="popTitle">提示</div>
    <div class="popBox">
      <div class="tipMessage">
        <svg :class="iconStyle" aria-hidden="true">
          <use :xlink:href="xxx"></use>
        </svg>
        <div class="message">{{message}}</div>
      </div>
      <div class="btn-grounp">
        <div class="sure" @click="sure">确定</div>
        <div class="bg-white-btn" @click="jump">{{btnMessage}}</div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'popWindow',
    props: {
      xxx: '',
      message: '',
      btnMessage: '',
      iconStyle: ''
    },
    data () {
      return {

      }
    },
    methods: {
      sure () {
        this.$emit('closepop')
      },
      jump () {
        this.$emit('jump')
      }
    }
  }
</script>
<style lang="less" scoped>
@import "../assets/reset.less";
  .popWindow {
    width: 23%;
    height: 190px;
    background-color: #fff;
    border-radius: 6px;
    margin: 20% auto;
    font-size: 14px;
  }
  .popTitle {
    height: 54px;
    line-height: 54px;
    padding-left: 7%;
    border-bottom: 1px solid #e5e5e5;
  }
  .chenggong {
    width: 30px; 
    height: 30px;
    vertical-align: -0.15em;
    fill: #72d540;
    overflow: hidden;
    margin-left: 7%;
    margin-top: 25px;
  }
  .warn {
    width: 30px; 
    height: 30px;
    vertical-align: -0.15em;
    fill: #ff0000;
    overflow: hidden;
    margin-left: 7%;
    margin-top: 25px;
  }
  .tipMessage {
    display: flex;
  }
  .message {

    margin-top: 30px;
    margin-left: 11px;
  }
  .btn-grounp {
    margin-top: 15px;
    display: flex;
    justify-content: center;
  }
  .bg-white-btn,
  .sure {
    border-radius: 6px;
    height: 36px;
    line-height: 36px;
    width: 26%;
    text-align: center;
  }
  .sure {
    background: #5a96f1;
    color: #fff;
    height: 38px;
    line-height: 38px;
  }
  .bg-white-btn {
    background: #fff;
    color: #5a96f1;
    border: 1px solid;
    margin-left: 20px;
  }
</style>