<template>
  <f7-page with-subnavbar>
    <f7-navbar title="Home" sliding />

    <!-- iOS TabBar has icons, Material TabBar does not -->
    <f7-toolbar tabbar :labels="isiOS">
        <f7-link :icon-f7="isiOS ? 'cats' : ''" text="Cats" tab-link="#cats" active></f7-link>
        <f7-link :icon-f7="isiOS ? 'info' : ''" text="About" tab-link="#about"></f7-link>
        <f7-link :icon-f7="isiOS ? 'persons' : ''" text="Services" tab-link="#services"></f7-link>
    </f7-toolbar>

    <f7-tabs >
      <f7-tab id="cats" active>
        <cats-page />
      </f7-tab>
      <f7-tab id="about">
        <about-page />
      </f7-tab>
      <f7-tab id="services">
        <services-page />
      </f7-tab>
    </f7-tabs>

  </f7-page>
</template>

<script>
  import Cats from './Cats';
  import About from './About';
  import Services from './Services';

  export default {
    name: 'Tabs',
    components: {
      'cats-page': Cats,
      'about-page': About,
      'services-page': Services
    },
    computed: {
      isiOS () {
        return window.isiOS;
      },
      isMaterial () {
        return window.isMaterial;
      }
    }
  };
</script>
