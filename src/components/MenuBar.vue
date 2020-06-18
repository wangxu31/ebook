<template>
    <div class="menu-bar">
      <transition name="slide-up">
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
            <span class="icon" @click="showSetting">A</span>
          </div>
        </div>
      </transition>
      <transition name="slide-up">
        <div class="setting-wrapper" v-show="ifSettingShow">
          <div class="setting-font-size">
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
    }
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
      .icon-wrapper {
        flex: 1;
        @include center;
      }
      /*!*增加&表示和title-wrapper平级*!*/
      /*&.slide-up-enter, &.slide-up-leave-to {*/
      /*  transform: translate3d(0, 100%, 0);*/
      /*}*/
      /*!*增加&表示和title-wrapper平级*!*/
      /*&.slide-up-enter-to, &.slide-up-leave {*/
      /*  transform: translate3d(0, 0, 0);*/
      /*}*/
      /*!*增加&表示和title-wrapper平级*!*/
      /*&.slide-up-enter-active, &.slide-up-leave-active {*/
      /*  transition: all 0.3s linear;*/
      /*}*/
    }
    .setting-wrapper {
      .setting-font-size {
        position: absolute;
        bottom: px2rem(48);
        left: 0;
        width: 100%;
        height: px2rem(60);
        background: white;
        box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, 0.15);
      }
    }
  }
</style>
