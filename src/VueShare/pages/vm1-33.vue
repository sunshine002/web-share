<template>
  <div>
    <pre>

      组件特性demo:
    </pre>
    <pre>is</pre>
    <div id="dynamic-component-demo" class="demo">
      <button
        v-for="tab in tabs"
        v-bind:key="tab"
        class="dynamic-component-demo-tab-button"
        v-bind:class="{ 'dynamic-component-demo-tab-button-active': tab === currentTab }"
        v-on:click="currentTab = tab"
      >
      {{ tab }}
      </button>
      <component v-bind:is="currentTabComponent" class="dynamic-component-demo-tab"></component>
    </div>

  </div>
</template>

<script>
import Vue from "vue";

export default {
  data() {
    return {
      currentTab: "Home",
      tabs: ["Home", "Posts", "Archive"]
    };
  },
  computed: {
    currentTabComponent: function() {
      return "tab-" + this.currentTab.toLowerCase();
    }
  }
};

Vue.component("tab-home", { template: "<div>Home component</div>" });
Vue.component("tab-posts", { template: "<div>Posts component</div>" });
Vue.component("tab-archive", { template: "<div>Archive component</div>" });
</script>

<style>
.dynamic-component-demo-tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
}
.dynamic-component-demo-tab-button:hover {
  background: #e0e0e0;
}
.dynamic-component-demo-tab-button-active {
  background: #e0e0e0;
}
.dynamic-component-demo-tab {
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
