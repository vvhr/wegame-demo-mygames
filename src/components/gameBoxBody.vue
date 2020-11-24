<template>
    <div class="game-box-body" id="box" @mousedown="bindMouseEvents">
      <!-- 卡片列表容器 -->
      <div id="game-list" class="game-list">
        <!-- 卡片 -->
        <section
            class="game-item"
            v-for="(item, index) in source"
            :key="index"
            :id="'item-' +  index">
          <div @mouseenter="handleEnter(item)"
               :class="getGameCardClass(item)"
               :style="{backgroundImage: 'url(' + item.photo + ')' }">
            <!-- 默认标题 -->
            <div class="title">
              <div class="title-container">
                <div class="name">{{item.name}}</div>
                <div class="icon"></div>
              </div>
            </div>
            <!-- 激活时标题-->
            <div class="active-title"
                 @click="onClickPlay(item)">
              <div class="title-container">
                <div class="icon"></div>
                <div class="text">启动游戏</div>
              </div>
            </div>
          </div>
          <!-- 激活时卡片下方显示游戏名称 -->
          <div class="game-name"
               v-if="hoverItem && hoverItem.name === item.name">
            {{item.name}}
          </div>
        </section>
      </div>
    </div>
</template>

<script>
import source from "@/utils/source";

export default {
  name: "gameBoxBody",
  data() {
    return {
      // 获取焦点的卡片
      hoverItem: null,
      // dom树
      box: null,
      ulList: null,
      // 游戏数据源
      source
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    // 初始化
    init() {
      // 获取dom元素
      this.box = document.querySelector(`#box`);
      this.ulList = this.box.querySelector('#game-list');
      // 动态计算总宽度
      document.getElementById('game-list').style["width"]=source.length * 170 + 'px';
      // 绑定鼠标事件
      this.bindMouseEvents()
    },
    // 绑定鼠标事件
    bindMouseEvents() {
      // 鼠标按下时记录鼠标相对于game-list的坐标listX
      this.ulList.onmousedown = (e) => {
        // e.layerX获取到的是鼠标相对于game-list(最近的有绝对定位的元素)的坐标
        let listX = e.layerX
        // 鼠标移动时获取mousemove事件
        document.onmousemove = e => {
          // 计算滚动条滚动距离 = 移动前盒子离浏览器左边的距离（box.offsetLeft） - 盒子离浏览器左边的距离（e.clientX - listX）+ 边距偏移补偿
          this.box.scrollLeft = this.box.offsetLeft - (e.clientX - listX) + 55
        }
        // 鼠标弹起时清除移动监听
        document.onmouseup = () => {
          document.onmousemove = null
        }
        // 取消默认行为
        if (e.preventDefault) {
          e.preventDefault()
        } else return false
      }
    },
    // 点击开始游戏
    onClickPlay (item) {
      this.$emit('openModal', item)
    },
    // 鼠标进入卡片触发mouseenter事件
    handleEnter (item) {
      this.hoverItem = item
      this.$emit('changeHover', item)
    },
    // 根据当前是否被选中获取游戏卡片的样式类
    getGameCardClass (item) {
      if (this.hoverItem) {
        if (this.hoverItem.name === item.name) {
          return 'game-card-active'
        } else return 'game-card'
      } else return 'game-card'
    }
  }
}
</script>

<style lang="stylus">
// 引入公共样式
@import '../../src/styles/commen.styl'
// 中部区域
.game-box-body {
  margin-left 40px
  padding-top 80px
  padding-bottom 50px
  width: 1040px;
  height 100%
  overflow hidden
  position: relative;
  .game-list {
    position absolute
    width 1700px
    height 500px
    display flex
    justify-content flex-start
    .game-item {
        width 170px
        margin-right 5px
        margin-left 3px
        .game-name {
          text-align left
          font-size 20px
          color $titleFontColor
          font-family $fontFamily
          font-weight $fontWeight
          transition: all 0.5s linear
        }
        .game-card {
          display: inline-block
          z-index: 3
          margin 10px
          width 150px
          height 200px
          border-radius 15px 0 15px 0
          background-size cover
          position relative
          box-shadow 0 0 2px black
          cursor pointer
          transition: all 0.2s linear
          &:hover {
            margin 0
            z-index 999
            width 170px
            height 220px
            border: 3px solid #ffd400
            box-shadow: inset 0 0 6px #ffe66b
            .title {
              display none
            }
            .active-title {
              display block
            }
          }
          .title {
            border-radius 0 0 15px 0
            position absolute
            bottom 0
            background: rgba(31, 31, 31, 0.75)
            width 100%
            text-align left
            transition: all 0.5s linear
            .title-container {
              display flex
              justify-content space-between
              align-items center
              .name {
                margin 3px
                color $normalFontColor
                font-family $fontFamily
                font-weight $fontWeight
                font-size 14px
              }
              .icon {
                margin 3px
                width 15px
                height 15px
                background url("~../../public/static/icon/game.png") no-repeat
                background-size cover
              }
            }
          }
          .active-title {
            display none
            position absolute
            bottom 5px
            right 10px
            transition: all 0.5s linear
            .title-container {
              display flex
              background-color orange
              align-items center
              justify-content center
              width 80px
              border-radius 6px
              .icon {
                margin 3px
                width 15px
                height 15px
                background url("~../../public/static/icon/game-black.png") no-repeat
                background-size cover
              }
              .text {
                font-size 12px
                color #1f1f1f
              }
            }
          }
        }
        .game-card-active {
          display: inline-block
          border-radius 15px 0 15px 0
          background-size cover
          position relative
          cursor pointer
          transition: all 0.2s linear;
          margin 0
          z-index 999
          width 170px
          height 220px
          border: 3px solid #ffd400;
          box-shadow: inset 0px 0px 6px #ffe66b
          .title {
            display none
            border-radius 0 0 15px 0
            position absolute
            bottom 0
            background: rgba(31, 31, 31, 0.75)
            width 100%
            text-align left
            transition: all 0.5s linear
            .title-container {
              display flex
              justify-content space-between
              align-items center
              .name {
                margin 3px
                color $normalFontColor
                font-family $fontFamily
                font-weight $fontWeight
              }
              .icon {
                margin 3px
                width 15px
                height 15px
                background url("~../../public/static/icon/game.png") no-repeat
                background-size cover
              }
            }
          }
          .active-title {
            display block
            position absolute
            bottom 5px
            right 10px
            transition: all 0.5s linear;
            .title-container {
              display flex
              background-color orange
              align-items center
              justify-content center
              width 80px
              border-radius 6px
              .icon {
                margin 3px
                width 15px
                height 15px
                background url("~../../public/static/icon/game-black.png") no-repeat
                background-size cover
              }
              .text {
                font-size 12px
                color #1f1f1f
                font-family $fontFamily
                font-weight $fontWeight
              }
            }
          }
        }
      }
  }
}
</style>