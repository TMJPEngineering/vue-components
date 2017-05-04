<template>
  <div id="app">
    <button :class="computedClass" v-text="button" @click="toggle()"></button>

    <div class="modal" :class="{ 'is-active' : active }">
      <div class="modal-background"></div>
      <div class="modal-content">
        <slot name="content"></slot>
      </div>
      <button class="modal-close" @click="toggle()"></button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'modal',

    props: {
        button: { required: true },
        className: { required: true }
    },

    data() {
        return { active: false }
    },

    methods: {
        toggle() {
            this.active = !this.active
        }
    },

    computed: {
        computedClass() {
            return this.className ? this.className.split(' ') : []
        }
    }
}
</script>

<style>

</style>
