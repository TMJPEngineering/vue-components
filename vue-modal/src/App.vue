<template>
  <div id="app">
    <section class="section">
      <div class="container">
        <modal class-name="button is-primary" button="Plain modal">
          <template slot="content">
            <div class="box">
              Any other Bulma elements you want
            </div>
          </template>
        </modal>
      </div>
    </section>
  </div>
</template>

<script>
import Modal from './components/Modal'

export default {
    name: 'app',

    components: {
        Modal
    }
}
</script>

<style>

</style>
