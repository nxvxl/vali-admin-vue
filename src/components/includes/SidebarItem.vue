<template>
  <div>
    <li v-if="!item.children">
      <router-link class="app-menu__item" :to="item.to" active-class="active">
        <i class="app-menu__icon fa" :class="item.icon"></i>
        <span class="app-menu__label">{{ item.label }}</span> 
      </router-link>
    </li>
    <li v-else class="treeview" :class="{ 'is-expanded': isExpanded }" @click="expandMenu">
      <a class="app-menu__item" :class="{ 'active': isExpanded }" href="#">
        <i class="app-menu__icon fa" :class="item.icon"></i>
        <span class="app-menu__label">{{ item.label }}</span> 
        <i v-if="item.children && item.children.length > 0" class="treeview-indicator fa fa-angle-right"></i>
      </a>
      <ul class="treeview-menu" v-if="item.children && item.children.length > 0">
        <li v-for="(child, index) in item.children" :key="index" class="">
          <router-link class="treeview-item" :to="child.to" exact-active-class="active">
            <i class="icon fa fa-circle-o"></i> {{ child.label }}
          </router-link>
        </li>
      </ul>
    </li>
  </div>
</template>

<script>
export default {
  name: 'SidebarItem',
  props: ['item'],
  data() {
    return {
      isExpanded: false,
      isActive: false
    }
  },
  methods: {
    expandMenu() {
      this.isExpanded = !this.isExpanded
    }
  },
  created() {
    if (this.item.children) {
      for (let child of this.item.children) {
        if (this.$route.fullPath.match(child.to)) {
          this.isExpanded = true
          break
        }
      }
    }
  }
}
</script>
