<template>
  <div 
    :class="classObj"
    v-show="show">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    header: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    badge: {
      type: [String, Number]
    },
    prefixCls: {
      type: String,
      default: 'n3'
    }
  },
  data () {
    return {
      index: 0,
      show: false
    }
  },
  computed: {
    classObj () {
      let {prefixCls, show} = this
      let klass = {}

      klass[prefixCls + '-tab-pane'] = true
      klass[prefixCls + '-tab-hide'] = !show

      return klass
    },
    show () {
      return (this.$parent.activeIndex == this.index)
    }
  },
  created () {
    this.$parent.renderData.push({
      header: this.header,
      disabled: this.disabled,
      badge: this.badge
    })
  },
  ready () {
    for (var c in this.$parent.$children) {
      if (this.$parent.$children[c].$el == this.$el) {
        this.index = c
        break
      }
    }
  }
}
</script>
