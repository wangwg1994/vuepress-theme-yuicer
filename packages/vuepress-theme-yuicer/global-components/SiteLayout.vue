<template>
  <div class="theme-container" :class="pageClasses">
    <Navbar v-if="shouldShowNavbar" />
    <div class="wrapper">
      <slot />
    </div>
  </div>
</template>

<script>
import Navbar from '@theme/components/Navbar.vue'
export default {
  components: { Navbar },
  computed: {
    shouldShowNavbar() {
      const { themeConfig } = this.$site
      const { frontmatter } = this.$page
      if (frontmatter.navbar === false || themeConfig.navbar === false) {
        return false
      }
      return (
        this.$title ||
        themeConfig.logo ||
        themeConfig.repo ||
        themeConfig.nav ||
        this.$themeLocaleConfig.nav
      )
    },
    pageClasses() {
      const userPageClass = this.$page.frontmatter.pageClass
      return [
        {
          'no-navbar': !this.shouldShowNavbar
        },
        userPageClass
      ]
    }
  }
}
</script>
<style src="prismjs/themes/prism-tomorrow.css"></style>
<style lang="stylus" scoped>
@require '../styles/wrapper.styl'
.wrapper
  @extend $wrapper
</style>
