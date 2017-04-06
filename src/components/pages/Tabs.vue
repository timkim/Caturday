<template>
  <f7-page with-subnavbar>
    <f7-navbar title="Home" sliding />

    <!-- iOS TabBar has icons, Material TabBar does not -->
    <f7-toolbar tabbar :labels="isiOS">
        <f7-link :icon-f7="isiOS ? 'cats' : ''" text="Cats" tab-link="#cats" active></f7-link>
        <f7-link :icon-f7="isiOS ? 'info' : ''" text="Loved" tab-link="#loved"></f7-link>
        <f7-link :icon-f7="isiOS ? 'persons' : ''" text="About" tab-link="#about"></f7-link>
    </f7-toolbar>

    <f7-tabs >
      <f7-tab id="cats" active>
        <cats-page />
      </f7-tab>
      <f7-tab id="loved">
        <loved-page />
      </f7-tab>
      <f7-tab id="about">
        <about-page />
      </f7-tab>
    </f7-tabs>

  </f7-page>
</template>

<script>
  import Cats from './Cats';
  import Loved from './Loved';
  import About from './About';

  export default {
    name: 'Tabs',
    components: {
      'cats-page': Cats,
      'loved-page': Loved,
      'about-page': About
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
