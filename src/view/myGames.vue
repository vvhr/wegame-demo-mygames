<template>
  <div class="app-container">
    <!-- 我的游戏 盒容器-->
    <div class="game-box" :style="getBackgroundStyle">
      <!-- 头部 -->
      <game-box-header/>
      <!-- 中部 -->
      <game-box-body @openModal="handleShowModal" @changeHover="onChangeHoverItem"/>
      <!-- 尾部 -->
      <game-box-footer @openModal="handleShowModal" :hover-item="hoverItem"/>
    </div>
    <!-- 对话框 -->
    <modal
        :visible="visible"
        title="提示"
        :content="'您将要启动游戏 “ ' + (hoverItem ? hoverItem.name : '未知游戏') + ' ” , 是否确认 ?'"
        @close="handleCloseModal">
    </modal>
  </div>
</template>

<script>
  import gameBoxBody from "@/components/gameBoxBody"
  import gameBoxHeader from "@/components/gameBoxHeader"
  import gameBoxFooter from "@/components/gameBoxFooter"
  import modal from "@/components/modal"
  export default {
    name: 'myGames',
    components: {
      gameBoxHeader,
      gameBoxBody,
      gameBoxFooter,
      modal
    },
    data() {
      return {
        // 模态框可视
        visible: false,
        // 当前hover的卡片
        hoverItem: null,
        // 当前选中并启动游戏的卡片
        activeItem: null
      }
    },
    computed: {
      // 根据当前选中项获取背景图
      getBackgroundStyle() {
        if (this.hoverItem) {
          return { background: 'url(' + this.hoverItem.background + ') no-repeat' }
        } else return {}
      }
    },
    methods: {
      // 改变hover时
      onChangeHoverItem (item) {
        this.hoverItem = item
      },
      // 显示模态框
      handleShowModal (item) {
        this.activeItem = item
        this.visible = true
      },
      // 关闭模态框
      handleCloseModal () {
        this.visible = false
      }
    }
  }
</script>

<style lang="stylus" scoped>
  // 引入公共样式
  @import '../styles/commen.styl'
  // 应用容器 灰色背景
  .app-container {
    width 100vw
    height 100vh
    background-color $backgroundColor
    padding 50px
    position relative
    // 我的游戏 盒容器
    .game-box {
      transition: all 0.3s ease 0s;
      position relative
      height 550px
      width 1080px
      background url("~../../public/defaultBg.png") no-repeat
      background-size cover
      border-radius 2px
      box-shadow: 0 1px 8px black
    }
  }

</style>
