<template>
  <div>
    <div class="tabs is-fullwidth is-toggle">
      <ul >
        <li v-for="tab in tabs" :class="{ 'is-active': tab.isActive }">
          <a :href="tab.href" v-text="tab.name" @click="selectTab(tab)"></a>
        </li>
      </ul>
    </div>
    
    <slot></slot>
  </div>
</template>

<script>
export default {
    name: 'tabs',

    data() {
        return { tabs: [] }
    },

    created() {
        this.tabs = this.$children
    },

    methods: {
        selectTab(selectedTab) {
            this.tabs.forEach((tab) => {
                tab.isActive = (tab.name === selectedTab.name)
            })
        }
    }
}
</script>

<style>
  
</style>
