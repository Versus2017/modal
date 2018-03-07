<template>
  <transition
    :name="transition"
    mode="in-out"
    appear
    :appear-active-class="enterClass"
    :enter-active-class="enterClass"
    :leave-active-class="leaveClass"
    @beforeEnter="beforeEnter"
    @afterEnter="afterEnter"
    @beforeLeave="beforeLeave"
    @afterLeave="afterLeave"
  >
    <div :class="classes" v-if="show">
      <div class="modal-background" @click="!removeDeactiveAction && deactive"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">{{ title }}</p>
          <button class="delete" v-if="!removeDeactiveAction" @click="deactive"></button>
        </header>
        <section class="modal-card-body">
          <slot></slot>
        </section>
        <footer class="modal-card-foot">
          <a class="button is-primary" @click="ok">{{ okText }}</a>
          <a class="button" v-if="!hideCancelButton" @click="cancel">{{ cancelText }}</a>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import BaseModal from './BaseModal'

export default {
  mixins: [BaseModal],

  props: {
    title: {
      type: String
    },
    okText: {
      type: String,
      default: 'Ok'
    },
    cancelText: {
      type: String,
      default: 'Cancel'
    },
    hideCancelButton: {
      tyre: Boolean,
      default: false,
    },
    // hide close button and background tap action
    removeDeactiveAction: {
      tyre: Boolean,
      default: false,
    }
  },

  computed: {
    classes () {
      return ['modal', 'animated', 'is-active']
    }
  },

  methods: {
    ok () {
      this.$emit('ok')
    },

    cancel () {
      this.$emit('cancel')
    },
  }
}
</script>
