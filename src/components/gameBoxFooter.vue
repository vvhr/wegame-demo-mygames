<template>
  <div class="game-box-footer">
    <div class="play-btn" @click="handleShowModal(hoverItem)">
      <div class="game-icon">
        <div class="icon">
          <i class="iconfont iconiconfontyouxihudong"></i>
        </div>
      </div>
      <span class="text">进入游戏</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "gameBoxFooter",
  props: {
    hoverItem: {
      type: Object,
      default: null
    }
  },
  methods: {
    handleShowModal(item) {
      if (item) {
        this.$emit('openModal', item)
      }
    }
  }
}
</script>

<style scoped lang="stylus">
// 引入公共样式
@import '../../src/styles/commen.styl'
// 尾部区域
.game-box-footer {
  position absolute
  width 100%
  bottom 0
  .play-btn {
    float right
    z-index 999
    margin-right 50px
    margin-bottom 50px
    display flex
    cursor pointer
    padding: 3px
    border-radius 6px
    &:hover {
      .text {
        color orange
      }
      .game-icon {
        border 1px solid orange
        .icon {
          color orange
        }
      }
    }
    .game-icon {
      border 1px solid white
      border-radius 25px
      padding 3px
      width 15px
      height 15px
      margin-right 5px
      .icon {
        color white
      }
    }
    .text {
      font-size 15px
      color $titleFontColor
      font-family $fontFamily
      font-weight $fontWeight
    }
  }
}
</style>