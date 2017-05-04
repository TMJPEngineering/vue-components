<template>
  <div id="app">
    <button :class="computedClass" v-text="button" @click="toggle()"></button>

    <div class="modal" :class="{ 'is-active' : active }">
      <div class="modal-background"></div>
      <div class="modal-card">
        <slot name="content"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'card-modal',

    props: {
        button: { required: true, type: String },
        className: { required: true, type: String }
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
