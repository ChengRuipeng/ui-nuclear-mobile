<template>
  <div
    :class="prefixCls"
    role="alert"
  >
    <div :class="`${prefixCls}-pic`" :style="imgUrl ? { backgroundImage: `url(${imgUrl})` } : ''">
      <slot name="img"></slot>
    </div>
    <div v-if="title" :class="`${prefixCls}-title`"><slot name="title">{{ title }}</slot></div>
    <div v-if="message" :class="`${prefixCls}-message`"><slot name="message">{{ message }}</slot></div>
    <div v-if="buttonText" :class="`${prefixCls}-button`">
      <Button :type="buttonType" :onClick="buttonClick">{{ buttonText }}</Button>
    </div>
  </div>
</template>
<script>
import Button from '../button'
import Icon from '../icon'
const prefixCls = 'um-result'
export default {
  name: 'Result',
  components: {
    Button,
    Icon
  },
  mounted () {
    if (this.iconClass || this.iconColor) {
      console.warn('\'iconClass\' and \'iconColor\' props has been deprecated, Please use slot instead')
    }
  },
  data () {
    return {
      prefixCls: prefixCls
    }
  },
  props: {
    imgUrl: {
      type: String
    },
    title: {
      type: String
    },
    message: {
      type: String
    },
    buttonText: {
      type: String
    },
    buttonType: {
      type: String
    },
    iconClass: {
      type: String
    },
    iconColor: {
      type: String
    },
    onButtonClick: {
      type: Function
    }
  },
  methods: {
    buttonClick (obj) {
      this.$emit('click')
      this.onButtonClick(obj)
    }
  }
}
</script>

<style lang="less">
@import url('style/index.less');
</style>
