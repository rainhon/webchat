<template>
  <div>
    <mt-header class="mint-header" v-bind:title="title"></mt-header>
    <mt-nav-bar v-model="selected">
      <mt-tab-item id="1">彩虹碗
      </mt-tab-item>
      <mt-tab-item id="2">其他
      </mt-tab-item>
    </mt-nav-bar>
    <mt-tab-container v-model="selected">
      <mt-tab-container-item id="1">
        <chat-room  server-address="ws://rainbowl.club:7000"></chat-room>
      </mt-tab-container-item>
      <mt-tab-container-item id="2"></mt-tab-container-item>
    </mt-tab-container>
  </div>
</template>

<script>
  import { Navbar, Header, TabItem, TabContainer, TabContainerItem} from 'mint-ui';
  import ChatRoom from "./components/ChatRoom";
  export default {
    components: {
      ChatRoom,
      'mt-header':Header,
      'mt-nav-bar':Navbar,
      'mt-tab-item':TabItem,
      'mt-tab-container':TabContainer,
      'mt-tab-container-item':TabContainerItem,
    },
    name: 'App',
    data() {
      return {
        title: "test",
        selected: "1",
      }
    }
  }
</script>
