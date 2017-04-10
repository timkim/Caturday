<template>
  <f7-block>
    <img v-bind:src=message v-bind:style="catImgStyle" />
    <br />
    <f7-buttons>
      <f7-button v-if="!isLiked" icon-f7="heart" v-on:click="like(message)"></f7-button>
      <f7-button v-else icon-f7="heart_fill" v-on:click="unlike(message)"></f7-button>
      <f7-button icon-f7="share" v-on:click="share()"></f7-button>
    </f7-buttons>
  <f7-list form v-if="isShared">
    <f7-list-item>
      <f7-icon slot="media" f7="world"></f7-icon>
      <f7-input type="text" v-model:value=message />
    </f7-list-item>
  </f7-list>
  </f7-block>
</template>

<script>
  export default {
    name: 'Cat',
    props: ['message'],
    data: function () {
      return {
        catImgStyle: {
          margin: '0 auto',
          width: '100%'
        },
        shared: false
      };
    },
    computed: {
      isLiked () {
        return this.$store.getters.findACat(this._props.message);
      },
      isShared () {
        return this.shared;
      }
    },
    methods: {
      like: function (catUrl) {
        if (!this.isLiked) {
          this.$store.commit('addCat', {'src': catUrl});
        }
      },
      unlike: function (catUrl) {
        if (this.isLiked) {
          this.$store.commit('removeCat', {'src': catUrl});
        }
      },
      share: function (target) {
        if (this.shared) {
          this.shared = false;
        } else {
          this.shared = true;
        }
      }
    }
  };
</script>
