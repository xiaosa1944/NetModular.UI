<template>
  <section class="nm-menus">
    <el-scrollbar>
      <el-menu :default-active="active" :unique-opened="uniqueOpened" :collapse="collapse" :collapse-transition="false">
        <template v-for="item in menus">
          <menu-item v-if="item.show" :key="item.id" :menu="item" />
        </template>
      </el-menu>
    </el-scrollbar>
  </section>
</template>
<script>
import MenuItem from './item'
import { mapState } from 'vuex'
export default {
  components: { MenuItem },
  computed: {
    ...mapState('app/account', ['menus', 'routeMenus']),
    ...mapState('app/system', { uniqueOpened: s => s.config.component.menu.uniqueOpened }),
    ...mapState('app/page', ['current']),
    ...mapState('app/skins/pretty/sidebar', ['collapse']),
    active: {
      get() {
        if (this.current.name && this.routeMenus) {
          let routeMenu = this.routeMenus.get(this.current.name)

          if (routeMenu) {
            return routeMenu.menu.id
          }
        }
        return '-1'
      },
      set() {}
    }
  }
}
</script>
