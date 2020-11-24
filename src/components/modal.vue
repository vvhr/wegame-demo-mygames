<template>
  <!-- 模态弹出框 -->
  <div class="dialog-modal" v-if="visible">
    <div class="dialog">
      <div class="header">
        <div class="icon"></div>
        <div class="title">提示</div>
        <div class="close" @click="onClose">×</div>
      </div>
      <div class="body">
        {{ content }}
      </div>
      <div class="footer">
        <div class="button confirm" @click="onClose">确 认</div>
        <div class="button cancel" @click="onClose">取 消</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  props: {
    // 可视
    visible: {
      type: Boolean,
      default: false,
    },
    // 标题
    title: {
      type: String,
      default: '窗口标题',
    },
    // 内容
    content: {
      type: String,
      default: '这是一个模态窗口!'
    }
  },
  methods: {
    onClose() {
      this.$emit('close')
    }
  }
}
</script>

<style scoped lang="stylus">
// 引入公共样式
@import '../../src/styles/commen.styl'
// 模态窗口 外层
.dialog-modal {
  z-index 999
  padding 100px
  position: fixed;
  left: 250px;
  top: 150px;
  margin: auto;
  width 100vw
  height 100vh
  // 窗口 内层
  .dialog {
    z-index 999
    position absolute
    border-radius 4px
    width 400px
    height 200px
    background: #1b1b1b
    box-shadow: 0 0 3px #272727
    .header {
      height 80px
      width 100%
      .icon {
        position absolute
        top 15px
        left 15px
        background url("~../../public/static/icon/wegame.png")
        background-size cover
        width 30px
        height 30px
      }
      .title {
        position absolute
        top 18px
        left 60px
        color $normalFontColor
        font-size 18px
        font-family "微软雅黑 Light"
        font-weight bold
      }
      .close {
        position absolute
        top 10px
        right 20px
        font-size 26px
        color $normalFontColor
        cursor pointer
      }
    }
    .body {
      color $titleFontColor
      font-family "微软雅黑 Light"
      font-weight bold
      font-size 18px
    }
    .footer {
      position absolute
      bottom 0
      height 50px
      right 20px
      .button {
        width 60px
        line-height 25px
        height 25px
        padding 5px
        cursor pointer
        margin-right 10px
        border-radius 4px
        color white
        font-family "微软雅黑 Light"
        font-weight bold
        font-size 14px
      }
      .confirm {
        float left
        background-color orange
      }
      .cancel {
        float right
        background-color #353535
      }
    }
  }
}
</style>