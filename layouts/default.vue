<template>
  <div >
    <TheHeader @sidenavToggle="displaySidenav = !displaySidenav"/>
    <TheSideNav
        :show="displaySidenav"
        @close="displaySidenav = false" />
    <nuxt class="default" />
    <Footer />
  </div>
</template>

<script>
  import TheHeader from '@/components/Navigation/TheHeader'
  import TheSideNav from '@/components/Navigation/TheSideNav'
  import Footer from '@/components/Footer/Footer'
  

export default {
  data() {
    return {
      displaySidenav: false
    }
  },
  components:{
    TheHeader,
    TheSideNav,
    Footer
  },
  // middleware: 'log',
}
</script>


<style>

</style>
