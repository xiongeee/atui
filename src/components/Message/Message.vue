<template>
  <div
    v-show="show"
    v-bind:class="{
      'alert':		true,
      'alert-success':(type == 'success'),
      'alert-warning':(type == 'warning'),
      'alert-info':	(type == 'info'),
      'alert-danger':	(type == 'danger'),
      'alert-help': (type == 'help'),
      'top': 			(placement === 'top'),
      'top-right': 	(placement === 'top-right')
    }"
    transition="fade"
    v-bind:style="{width:width}"
    role="alert">
    <button v-show="dismissable" type="button" class="close"
      @click="show = false">
      <span>&times;</span>
    </button>
    <icon :type="type"></icon>
    <slot></slot>
  </div>
</template>

<script>
import coerceBoolean from '../utils/coerceBoolean.js'

  export default {
    props: {
      type: {
        type: String
      },
      dismissable: {
        type: Boolean,
        coerce: coerceBoolean,
        default: false,
      },
      showIcon: {
        type: Boolean,
        coerce: coerceBoolean,
        default: false,
      },
      show: {
        type: Boolean,
        coerce: coerceBoolean,
        default: true,
        twoWay: true
      },
      duration: {
        type: Number,
        default: 0
      },
      width: {
        type: String
      },
      placement: {
        type: String
      }
    },
    watch: {
      show(val) {
        if (this._timeout) clearTimeout(this._timeout)
        if (val && Boolean(this.duration)) {
          this._timeout = setTimeout(()=> this.show = false, this.duration)
        }
      }
    },
    methods:{
      success() {

      }
    }
  }
</script>

<style>
.fade-transition {
  transition: opacity .3s ease;
}
.fade-enter,
.fade-leave {
  height: 0;
  opacity: 0;
}
.alert.top {
  position: fixed;
  top: 30px;
  margin: 0 auto;
  left: 0;
  right: 0;
  z-index: 2;
}
.alert.top-right {
  position: fixed;
  top: 30px;
  right: 50px;
  z-index: 2;
}
</style>