<template>
  <div class="game-box-header">
    <!-- WeGame 图标 -->
    <div class="icon"></div>
    <!-- 盒子标题文字 -->
    <div class="title">我的游戏</div>
    <!-- 右侧操作栏 -->
    <div class="action-bar">
      <div class="action-one"
           v-for="(item, index) in actionsList" :key="index"
           :style="item.itemStyle"
           @click="handleClick(item.action)">
        <img :src="item.img" v-if="item.showType !== 'word'" :style="item.imgStyle"/>
        <span class="word" v-if="item.showType !== 'img'">{{item.word}}</span>
      </div>
      <!-- 时间单独处理 -->
      <div class="action-one" style="width: 20px">
        <span class="word" >{{time}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "gameBoxHeader",
  data () {
    return {
      /**
       * 顶部操作项数据源
       * showType：detail(图文) / img（仅图） / word（仅文）
       * action：预定义好的函数名称 如：setting / close
       */
      actionsList: [
        { sort: 1 ,name: 'user', itemStyle: 'width: 150px', img: require('../../public/static/icon/avatar.png'), imgStyle: 'width: 25px;margin-right: 10px', word: this.getUsername(), showType: 'detail', action: null },
        { sort: 2 ,name: 'setting', itemStyle: '', img: require('../../public/static/icon/setting.png'), imgStyle: 'width: 18px', word: '设置', showType: 'img', action: 'setting' },
        { sort: 3 ,name: 'close', itemStyle: '', img: require('../../public/static/icon/close.png'), imgStyle: 'width: 20px', word: '关闭', showType: 'img', action: 'close' }
      ],
      // 时间
      time: null,
      // 计时器句柄
      timer: 0
    }
  },
  mounted() {
    // 启动计时器刷新时钟
    this.getTime()
    this.timer = setInterval(this.getTime, 1000)
  },
  beforeDestroy() {
    // 清除计时器
    clearInterval(this.timer)
  },
  methods: {
    // 处理顶部操作栏的点击事件
    handleClick (funcName) {
      if (funcName === 'close') {
        this.handleClose()
      } else if (funcName === 'setting') {
        this.handleSetting()
      }
    },
    // 点击关闭按钮
    handleClose() {
      console.log('close')
    },
    // 点击设置按钮
    handleSetting() {
      console.log('setting')
    },
    // 获取用户信息
    getUsername () {
      return 'harlan'
    },
    // 获取时间
    getTime () {
      const date = new Date()
      let time = ''
      let h = date.getHours()
      let m = date.getMinutes()
      if (h >= 10) {
        time += h + ":"
      } else time += "0" + h + ":"
      if (m >= 10) {
        time += m
      }else time += "0" + m
      this.time = time
    }
  }
}
</script>

<style scoped lang="stylus">
// 引入公共样式
@import '../../src/styles/commen.styl'
// 顶部区域
.game-box-header {
  margin 0 auto
  width 90%
  height 65px
  border-bottom: 1px solid rgba(255, 255, 255, 0.12)
  .icon {
    position absolute
    top 15px
    left 15px
    background url("~../../public/static/icon/wegame.png")
    background-size cover
    width 35px
    height 35px
  }
  .title {
    position absolute
    top 18px
    left 60px
    color $titleFontColor
    font-size 20px
    font-family $fontFamily
    font-weight $fontWeight
  }
  .action-bar {
    float right
    display flex
    justify-content flex-start
    height 65px
    align-items center
    align-content center
    .action-one {
      display flex
      align-items center
      color $normalFontColor
      margin-right 30px
      .word {
        color $titleFontColor
        font-family $fontFamily
        font-weight $fontWeight
        margin-left 5px
        margin-right 5px
      }
    }
  }
}
</style>