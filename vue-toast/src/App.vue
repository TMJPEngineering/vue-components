<template>
  <div id="app">
    <section class="section">
      <div class="container">
        <div class="notification">
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Message</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <input class="input" type="input" v-model="message" placeholder="Input your message">
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Number of Toast</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <input class="input" type="number" placeholder="Max" min="0" v-model="max">
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">CSS Position</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <span class="select is-fullwidth">
                    <select v-model="position">
                      <option value="top left">Top Left</option>
                      <option value="top right">Top Right</option>
                      <option value="bottom left">Bottom Left</option>
                      <option value="bottom right">Bottom Right</option>
                    </select>
                  </span>
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Class Name</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <span class="select is-fullwidth">
                    <select v-model="className">
                      <option value="tag is-white">White</option>
                      <option value="tag is-light">Light</option>
                      <option value="tag is-primary">Primary</option>
                      <option value="tag is-info">Info</option>
                      <option value="tag is-success">Success</option>
                      <option value="tag is-warning">Warning</option>
                      <option value="tag is-danger">Danger</option>
                      <option value="tag is-dark">Dark</option>
                      <option value="tag is-black">Black</option>
                    </select>
                  </span>
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Size</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <span class="select is-fullwidth">
                    <select v-model="size">
                      <option value="is-small">Small</option>
                      <option value="is-medium">Medium</option>
                      <option value="is-large">Large</option>
                    </select>
                  </span>
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Timeout (in seconds)</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <input class="input" type="number" placeholder="Timeout" min="1" v-model="timeout" :disabled="disableTimeout">
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label is-normal">
              <label class="label">Closable</label>
            </div>
            <div class="field-body">
              <div class="field is-grouped">
                <p class="control is-expanded">
                  <input type="checkbox" v-model="closable" v-change="close(closable)">
                </p>
              </div>
            </div>
          </div>
          <div class="field is-horizontal">
            <div class="field-label"></div>
            <div class="field-body">
              <div class="field">
                <div class="control">
                  <button class="button is-info" @click="show">
                    Show Toast
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <vue-toast-manager ref="toast"></vue-toast-manager>
    </section>
  </div>
</template>

<script>
import VueToastManager from './components/ToastManager'

export default {
    name: 'Toast',

    data() {
        // Default value on load
        return {
            max: 6,
            position: 'top right',
            className: 'tag is-dark',
            size: 'is-medium',
            timeout: 3000,
            closable: false,
            disableTimeout: false
        }
    },

    watch: {
        max: 'reset',
        position: 'reset'
    },

    mounted() {
        this.reset()
    },

    methods: {
        close(closable) {
            this.disableTimeout = closable
        },

        reset() {
            this.$refs.toast.init({
                max: this.max,
                position: this.position
            })
        },

        show() {
            if (this.message) {
                this.toast(this.message, {
                    className: `${this.className} ${this.size}`,
                    timeout: this.timeout,
                    closable: this.closable
                })

                return
            }

            // If message is empty
            this.toast('Please input your message')
        },

        toast(message, options = {}) {
            this.$refs.toast.showToast(message, options)
        }
    },

    components: {
        'vue-toast-manager': VueToastManager
    }
}
</script>
