<template>
  <div>
    <mt-header class="mint-header" v-bind:title="title"></mt-header>
    <mt-nav-bar v-model="selected">
      <mt-tab-item id="1">服务器聊天
      </mt-tab-item>
      <mt-tab-item id="2">服务器状态查询(未完工)
      </mt-tab-item>
    </mt-nav-bar>
    <mt-tab-container v-model="selected">
      <mt-tab-container-item id="1">
        <chat-room></chat-room>
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
        title: "mc云玩家网页工具",
        selected: "1",
      }
    }
  }
</script>
