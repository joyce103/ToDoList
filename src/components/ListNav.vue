<template>
  <ul class="nav nav-tabs" id="myTab" role="tablist">
    <li
      class="nav-item"
      v-for="tab in tabs"
      :key="tab"
      :class="['tab-button', { active: currentTab === tab }]"
      @click="TabSwitch(tab)"
    >
      <button class="nav-link">{{ tab }}</button>
    </li>
  </ul>
</template>
<script>
export default {
  name: "ListNav",
  props: ["nowtab"],
  data() {
    return {
      currentTab: this.nowtab,
      tabs: ["ALL", "DONE", "TODO"],
    };
  },
  methods: {
    TabSwitch(i) {
      this.currentTab = i;
      this.$emit("TabSwitch", this.currentTab);
    },
  },
};
</script>
<style scope>
.nav-tabs,
.nav-tabs {
  color: #ffffff !important;
}
.nav-link:focus,
.nav-link:hover {
  background-color: #ffffff !important;
  color: #547b68 !important;
}
</style>
