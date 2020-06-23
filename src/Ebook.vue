<template>
<div class="ebook">
<!--  传递变量到组件-->
  <title-bar :ifTitleAndMenuShow="ifTitleAndMenuShow"></title-bar>
  <div class="read-wrapper">
    <div id="read"></div>
    <div class="mask">
      <div class="left" @click="prevPage()"></div>
      <div class="center" @click="toggleTitleAndMenu()"></div>
      <div class="right" @click="nextPage()"></div>
    </div>
  </div>
<!--  传递变量到组件-->
  <menu-bar :ifTitleAndMenuShow="ifTitleAndMenuShow"
            :fontSizeList="fontSizeList"
            :defaultFontSize="defaultFontSize"
            @setFontSize="setFontSize"
            :themeList="themeList"
            :defaultTheme="defaultTheme"
            @setTheme="setTheme"
            ref="menuBar"></menu-bar>
</div>
</template>

<script>
import TitleBar from './components/TitleBar'
import MenuBar from './components/MenuBar'
import Epub from 'epubjs'
const DOWNLOAD_URL = '../static/book.epub'
global.ePub = Epub
export default {
  components: {
    TitleBar,
    MenuBar
  },
  data () {
    return {
      ifTitleAndMenuShow: false,
      fontSizeList: [
        {fontSize: 12},
        {fontSize: 14},
        {fontSize: 16},
        {fontSize: 18},
        {fontSize: 20},
        {fontSize: 22},
        {fontSize: 24}
      ],
      defaultFontSize: 16,
      themeList: [
        {
          name: 'default',
          style: {
            body: {
              'color': '#000', 'background': '#fff'
            }
          }
        },
        {
          name: 'eye',
          style: {
            body: {
              'color': '#000', 'background': '#ceeaba'
            }
          }
        },
        {
          name: 'night',
          style: {
            body: {
              'color': '#fff', 'background': '#000'
            }
          }
        },

        {
          name: 'gold',
          style: {
            body: {
              'color': '#000', 'background': 'rgb(241, 236, 226)'
            }
          }
        }
      ],
      defaultTheme: 0
    }
  },
  methods: {
    setTheme(index) {
      this.themes.select(this.themeList[index].name)
      this.defaultTheme = index
    },
    registerTheme() {
      this.themeList.forEach(theme => {
        this.themes.register(theme.name, theme.style)
      })
    },
    // 电子书解析和渲染
    showEpub () {
      // 生成book
      this.book = new Epub(DOWNLOAD_URL)
      console.log(this.book)
      // 生成rendition对象
      this.rendition = this.book.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 通过rendition.display渲染电子书
      this.rendition.display()
      // 获取Theme对象，保存在本地一个变量里
      this.themes = this.rendition.themes
      // 设置默认字体
      this.setFontSize(this.defaultFontSize)
      // this.themes.register(name, styles)
      // this.themes.select(name)
      this.registerTheme()
      this.themes.select('default')
      // alert(this.themes.themeList[index])
      this.setTheme(this.defaultTheme)
    },
    prevPage () {
      // Rendition prev
      if (this.rendition) {
        this.rendition.prev()
      }
    },
    nextPage () {
      // Rendition next
      if (this.rendition) {
        this.rendition.next()
      }
    },
    toggleTitleAndMenu () {
      this.ifTitleAndMenuShow = !this.ifTitleAndMenuShow
      if (!this.ifTitleAndMenuShow) {
        // 相当于dom选择器，可以选择dom后调用下面的方法
        this.$refs.menuBar.hideSetting()
      }
    },
    setFontSize(fontSize) {
      this.defaultFontSize = fontSize
      // 接收子组件参数进行处理
      if (this.themes) {
        this.themes.fontSize(fontSize + 'px')
      }
    }
  },
  // 构造函数
  mounted () {
    // console.log('mounted ebook')
    this.showEpub()
  },
  created () {
    // console.log('created ebook')
  }
}
</script>

<style lang="scss" scoped>
@import "assets/styles/global.scss";
.ebook {
  position: relative;
  .title-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 101;
    display: flex;
    height: px2rem(48);
    background: white;
    box-shadow: 0 px2rem(8) px2rem(8) rgba(0, 0, 0, 0.15);
    .left {
      flex: 0 0 px2rem(60);
      @include center;
    }
    .right {
      flex: 1;
      display: flex;
      justify-content: flex-end;
      .icon-wrapper {
        flex: 0 0 px2rem(40);
        @include center;
        .ion-ios-cart {
          font-size: px2rem(21);
        }
      }
    }
  }
  .read-wrapper {
    .mask {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 100;
      display: flex;
      width: 100%;
      height: 100%;
      /*background: yellow;*/
      .left {
        flex: 0 0  px2rem(100);
        /*background: yellow;*/
      }
      .center {
        flex: 1;
        /*background: red;*/
      }
      .right {
        flex: 0 0  px2rem(100);
        /*background: orange;*/
      }
    }
  }
}
</style>
