<template>
<div>
    <nav class="boot-nav">
        <ul class="pagination boot-page">
            <li>
                <a href="javascript:void(0)"  @click="wholePrevClick()" class="oval-btn">
                    <span aria-hidden="true">首页</span>
                </a>
            </li>
            <li>
                <a href="javascript:void(0)" aria-label="Previous" @click="onPrevClick()">
                    <span aria-hidden="true">&laquo;</span>
                </a>
            </li>
            <li v-for="(page, index) in pages" >
                <a href="javascript:void(0)" v-text="page" @click="onPageClick(index)" :class="activeNum === index ? 'active' : ''"></a>
            </li>
            <li>
                <a href="javascript:void(0)" aria-label="Next" @click="onNextClick()">
                    <span aria-hidden="true">&raquo;</span>
                </a>
            </li>
            <li>
                <a href="javascript:void(0)"  @click="wholeNextClick()" class="oval-btn">
                    <span aria-hidden="true">尾页</span>
                </a>
            </li>
        </ul>
        <div class="page-total">
           共 <span v-text="pageTotal"></span> 页
       </div>
    </nav>
    <div class="popbox" v-if="showLoading">
      <loading></loading>
    </div>
</div>    
</template>

<script>
  import loading from '@/childpage/loading.vue'
  export default {
    components: {
      loading
    },
    props: {

      // 每页显示个数
      // len: {
      //   type: Number,
      //   default: 2
      // },
      // 表格数据（数组）
      data: {
        type: Array,
        default: function () {
          return []
        }
      },
      // AJAX地址
      url: {
        type: String,
        default: ''
      },
      // 当前页的字段
      currentPage: {
        type: String,
        default: ''
      },
      totalName: {
        type: String,
        default: ''
      },
      // 显示页数
      pageLen: {
        type: Number,
        default: 5
      },

      // 参数内容
      param: {
        type: Object,
        default: function () {
          return {}
        }
      },
      // method
      method: {
        type: String,
        default: 'get'
      }
    },
    data () {
      return {
        // 页码
        pages: {
          type: Array,
          default: function () {
            return [1]
          }
        },
        // 总页数
        pageTotal: {
          type: Number
        },
        activeNum: 0,
        first: -1,
        last: -1,
        showLoading: false
      }
    },
    created () {
      this.getData()
      this.getPages()
    },
    watch: {
      '$store': function () {
        console.log(this.$store.state.a.renderData)
        // if (this.$store.state.a.renderData) {

        // }
      }
    },
    methods: {
      // 第一页
      wholePrevClick: function () {
        this.first = 1
        var newPages = []
        for (let i = 0; i < this.pages.length; i++) {
          newPages[i] = i + 1
        }
        this.pages = newPages
        this.activeNum = 0
        this.getData()
      },
      // 最后一页
      wholeNextClick: function () {
        this.last = this.pageTotal
        var newPages = []
        for (let i = 0; i < this.pages.length; i++) {
          newPages[this.pages.length - i - 1] = this.pageTotal - i
        }
        this.pages = newPages
        this.activeNum = this.pages.length - 1
        this.getData()
      },
      pageMake: function (index) {
        let newPages = []
        let len2 = parseInt(this.pages.length / 2)
        if (this.pages[index] <= len2 || this.pageTotal <= this.pageLen || this.pages[index] > this.pageTotal - len2) {
          for (let i = 0; i < this.pages.length; i++) {
            newPages[i] = this.pages[i]
          }
          this.activeNum = index
        } else if (this.pages[index] <= this.pageTotal - len2) {
          for (let i = 0; i < this.pages.length; i++) {
            newPages[i] = this.pages[index] - len2 + i
          }
          this.activeNum = len2
        }
        this.pages = newPages
        this.getData()
      },
      // 点击页码刷新数据
      onPageClick (index) {
        this.pageMake(index)
      },
      // 上一页
      onPrevClick () {
        // 当前页是否为当前最小页码
        if (this.activeNum > 0) {
          // this.activeNum = this.activeNum - 1;
          let index = this.activeNum - 1
          this.pageMake(index)
        } else {
          if (this.pages[0] !== 1) {
            let newPages = []
            for (let i = 0; i < this.pages.length; i++) {
              newPages[i] = this.pages[i] - 1
            }
            this.pages = newPages
            this.getData()
          }
        }
      },
      // 下一页
      onNextClick () {
        // 当前页是否为当前最大页码
        if (this.activeNum < this.pages.length - 1) {
          // this.activeNum = this.activeNum + 1
          let index = this.activeNum + 1
          this.pageMake(index)
        } else {
          if (this.pages[this.pages.length - 1] < this.pageTotal) {
            let newPages = []

            for (let i = 0; i < this.pages.length; i++) {
              newPages[i] = this.pages[i] + 1
            }
            this.pages = newPages
            this.getData()
          }
        }
      },
      // 获取页码
      getPages () {
        this.pages = []
        // 比较总页码和显示页数
        if (this.pageTotal <= this.pageLen) {
          // console.log(this.pageTotal+"....."+this.pageLen)
          for (let i = 1; i <= this.pageTotal; i++) {
            this.pages.push(i)
          }
        } else {
          for (let i = 1; i <= this.pageLen; i++) {
            this.pages.push(i)
          }
        }
      },
      // 页码变化获取数据
      getData () {
        // Hub.$emit('change')
        this.showLoading = true
        // var _self = this
        this.param[this.currentPage] = this.pages[this.activeNum]
        if (this.first !== -1) {
          this.param[this.currentPage] = this.first
          this.first = -1
        } else if (this.last !== -1) {
          this.param[this.currentPage] = this.last
          this.last = -1
        }
        this.$nextTick(function () {
          // var _self = this
          var param = this.param
          this.$http.post(this.url, param).then(function (res) {
            this.showLoading = false
            if (res.data.code === 0) {
              var data = res.data.data
              let total = res.data.data.page
              // if (typeof (res.data.data.page) !== 'string') {
              //   total = res.data.data.count
              // } else {
              //   total = res.data.data.page
              // }
              // if (!res.data.data.hasOwnProperty('page')) {
              //   total = res.data.data.count
              // }
              this.pageTotal = Math.ceil(total / param.listrows)
              if (this.pages.length !== this.pageLen || this.pageTotal < this.pageLen) {
                this.getPages()
              }
              this.$store.commit('changeRenderData', {data})
            } else if (res.data.msg === 'token\u9a8c\u8bc1\u5931\u8d25') {
              this.$ls.clear()
              alert('您已下线!请重新登录!')
              this.$router.push('Hello')
              window.location.reload()
            }
          }, (response) => {
            this.showLoading = false
            alert('服务器出错，请联系管理员')
          })
        })
      },
      refresh () {
        this.pages = [1]
        this.activeNum = 0
        this.getData()
      }
    }
  }
</script>

<style lang= "less" scoped>
@import "../assets/reset.less";

a{
    text-decoration: none;
    color: #000;
    background-color: #eeeeee;
    color: #000;
    display: inline-block;
    width: 30px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    border-radius: 50%;
}
.active {
    color: #fff;
    background-color: #90d072;
}
a:hover {
    color: #fff;
    background-color: #90d072;
}
.oval-btn{
    width: 86px;
    height: 28px;
    line-height: 28px;
    border-radius: 12px;
}
li {
    display: inline;
    margin-right: 18px;
    color: #fff;
}
.boot-select {
    float: left;
    width: 80px;
}

.boot-nav {
    float: right;
}

.boot-page {
    display: inline-block;
    margin: 2px 10px 0 20px;
    vertical-align: middle;
}

.page-total {
    display: inline-block;
    vertical-align: middle;
}
</style>