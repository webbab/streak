<template>
  <div class='tabs' v-if='project'>
    <router-link :to='{name: "project-overview"}' :class='{current: isCurrentPage("project-overview")}' class='tab-link'>Overview</router-link>
    <!--router-link :to='{name: "project-discussion"}' :class='{current: isCurrentPage("project-discussion")}' class='tab-link'>Discuss</router-link-->
    <router-link :to='{name: "project-settings"}' :class='{current: isCurrentPage("project-settings")}' class='tab-link' v-if='canEdit'>Settings</router-link>
  </div>
</template>

<script>
export default {
  name: 'ProjectTabs',
  props: ['project'],
  methods: {
    isCurrentPage(page) {
      const currentRoute = this.$route.name;
      if (page === currentRoute) return true;
      if (page === 'project-discussion' && (
        (currentRoute === 'add-comment') || (currentRoute === 'comment-details')
      )) return true;

      // Consider 'add record' as project overview.
      return page === 'project-overview' && currentRoute === 'add-record';
    }
  },
  computed: {
    canEdit() {
      return this.project && this.project.canEdit;
    }
  }
};
</script>

<style lang='stylus'>
@import '../styles/variables.styl';

.tabs {
    position: relative;
    line-height: 32px;
    border-bottom: 1px solid strong-border-color;
    margin-left: -14px;
    margin-right: -14px;
    padding-left: 14px;
    padding-right: 14px;
}
a.tab-link {
    display: inline-block;
    height: 100%;
    padding: 0 14px;
    border: 1px solid transparent;
    color: #999;
}
.tab-link.current {
  border-left: 1px solid strong-border-color;
  border-top: 2px solid action-color;
  border-right: 1px solid strong-border-color;
  background: white;
  top: 1px;
  position: relative;
  color: secondary-text-color;
}
</style>
