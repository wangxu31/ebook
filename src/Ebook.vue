<template>
<div class="ebook">
  <div class="title-wrapper" v-show="ifTitleAndMenuShow">
    <div class="left">
      <span class="ion-arrow-left-a icon"></span>
    </div>
    <div class="right">
      <div class="icon-wrapper">
        <span class="ion-ios-cart icon"></span>
      </div>
      <div class="icon-wrapper">
        <span class="ion-person icon"></span>
      </div>
      <div class="icon-wrapper">
        <span class="ion-android-more-vertical icon"></span>
      </div>
    </div>
  </div>
  <div class="read-wrapper">
    <div id="read"></div>
    <div class="mask">
      <div class="left" @click="prevPage()"></div>
      <div class="center" @click="toggleTitleAndMenu()"></div>
      <div class="right" @click="nextPage()"></div>
    </div>
  </div>
  <div class="menu-wrapper" v-show="ifTitleAndMenuShow">
    <div class="icon-wrapper">
      <span class="ion-android-menu icon"></span>
    </div>
    <div class="icon-wrapper">
      <span class="ion-ios-circle-filled icon"></span>
    </div>
    <div class="icon-wrapper">
      <span class="ion-android-sunny icon"></span>
    </div>
    <div class="icon-wrapper">
      <span class="ion-edit icon"></span>
    </div>
  </div>
</div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '../static/book.epub'
global.ePub = Epub
export default {
  data () {
    return {
      ifTitleAndMenuShow: false
    }
  },
  methods: {
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
    },
    prevPage () {
      //Rendition prev
      if (this.rendition) {
        this.rendition.prev();
      }
    },
    nextPage () {
      //Rendition next
      if (this.rendition) {
        this.rendition.next();
      }
    },
    toggleTitleAndMenu () {
      this.ifTitleAndMenuShow = !this.ifTitleAndMenuShow;
    }
  },
  // 构造函数
  mounted () {
    console.log('mounted ebook')
    this.showEpub()
  },
  created () {
    console.log('created ebook')
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
  .menu-wrapper {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    z-index: 101;
    display: flex;
    height: px2rem(48);
    background: white;
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, 0.15);
    .icon-wrapper {
      flex: 1;
      @include center;
    }
  }
}
</style>
