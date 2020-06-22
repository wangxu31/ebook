<template>
    <div class="menu-bar">
      <transition name="slide-up">
        <div class="menu-wrapper" :class="{'hide-box-shadow':ifSettingShow || !ifTitleAndMenuShow}" v-show="ifTitleAndMenuShow">
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
            <span class="icon" @click="showSetting">A</span>
          </div>
        </div>
      </transition>
      <transition name="slide-up">
        <div class="setting-wrapper" v-show="ifSettingShow">
          <div class="setting-font-size">
            <div class="preview" :style="{fontSize:fontSizeList[0].fontSize+'px'}">A</div>
            <div class="select">
              <div class="select-wrapper" v-for="(item, index) in fontSizeList" :key="index" @click="setFontSize(item.fontSize)">
                <div class="line"></div>
                <div class="point-wrapper">
                  <div class="point" v-show="defaultFontSize===item.fontSize">
                    <div class="small-point"></div>
                  </div>
                </div>
                <div class="line"></div>
              </div>
            </div>
            <div class="preview" :style="{fontSize:fontSizeList[fontSizeList.length-1].fontSize+'px'}">A</div>
          </div>
        </div>
      </transition>
    </div>

</template>

<script>
export default {
  name: 'MenuBar',
  props: {
    ifTitleAndMenuShow: {
      type: Boolean,
      default: false
    },
    fontSizeList: Array,
    defaultFontSize: Number
  },
  data () {
    return {
      ifSettingShow: false
    }
  },
  methods: {
    showSetting () {
      this.ifSettingShow = true
    },
    hideSetting () {
      this.ifSettingShow = false
    },
    setFontSize(fontSize) {
      // 使用$emit把参数传递到父组件进行处理
      // 子组件调用父组件方法
      this.$emit('setFontSize', fontSize)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/global.scss";
  .menu-bar {
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
      /*&表示hide-box-shadow与menu-wrapper同一级*/
      &.hide-box-shadow {
        box-shadow: none;
      }
      .icon-wrapper {
        flex: 1;
        @include center;
      }
    }
    .setting-wrapper {
      position: absolute;
      bottom: px2rem(48);
      left: 0;
      z-index: 101;
      width: 100%;
      height: px2rem(60);
      background: white;
      box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, 0.15);
      .setting-font-size {
        display: flex;
        height: 100%;
        .preview {
          flex: 0 0 px2rem(40);
          @include center;
        }
        .select {
          display: flex;
          flex: 1;
          .select-wrapper {
            /*flex设置为1表示自动伸缩*/
            flex: 1;
            display: flex;
            align-items: center;
            /*加&，取同级的first-child*/
            &:first-child {
              .line {
                &:first-child {
                  border-top: none;
                }
              }
            }
            &:last-child {
              .line {
                &:last-child {
                  border-top: none;
                }
              }
            }
            .line {
              flex: 1;
              height: 0;
              border-top: px2rem(1) solid #ccc;
            }

            .point-wrapper {
              position: relative;
              flex: 0 0 0;
              width: 0;
              height: px2rem(7);
              border-left: px2rem(1) solid #ccc;
              .point {
                position: absolute;
                top: px2rem(-7);
                left: px2rem(-10);
                height: px2rem(20);
                width: px2rem(20);
                border-radius: 50%;
                background: white;
                border: px2rem(1) solid #ccc;
                box-shadow: 0 px2rem(4) px2rem(4) rgba(0, 0, 0, 0.15);
                @include center;
                .small-point {
                  width: px2rem(5);
                  height: px2rem(5);
                  background: black;
                  border-radius: 50%;
                }
              }
            }
          }
        }
      }
    }
  }
</style>
