<template>
  <div class="tabsboxs" id="tabs">
    <!-- <div class="tabs" v-for="(item,index) in myTablist"  @click="go(item,index)" :class="{'bg-white':index===myActive}"> -->
    <div class="tabs" v-for="(item,index) in myTablist">
      <router-link :to="item.paths">{{item.name}}
        <!-- <div class="texts" :class="{'blue-border':index===myActive}">{{item.name}}</div> -->
      </router-link>        
    </div>     
  </div>
</template>

<script>
  export default{
    name: 'tabs',
    props: {
      tablist: Array,
      active: 0
    },
    data () {
      return {
        myTablist: this.tablist,
        myActive: this.active
      }
    },
    methods: {
      go (item, index) {
        this.myActive = index
        console.log(this.myActive)
        console.log(index)
      }
    }
  }
</script>

<style lang="less">
@import "../assets/reset.less";
#tabs{
  width: 98.5%;
  margin: 20px 0 0 1%;
  display: flex;
  .fs14
}

.tabs{
  height: 33px;
  line-height: 33px;
  margin-right: 20px;  
}

.tabs a{
  color: @text-black
}
.texts{
  padding: 0 4px;
}
.router-link-active {
  .blue-border;
  .bg-white;
  padding: 0 20px;
} 
a {
  display: block;
}
</style>