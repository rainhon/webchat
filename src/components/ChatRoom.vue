<template>
    <div>
      <mt-cell>
        <mt-button size="small" @click="messages=[]" type="danger">清空记录</mt-button>
        <mt-button size="small" v-if="!connected" @click.native="connect" type="primary">点击链接服务器</mt-button>
        <mt-button size="small" v-if="connected" @click.native="disconnect" type="default">断开连接服务器</mt-button>
      </mt-cell>
      <mt-cell v-show="!connected">
        <mt-field label="服务器请求地址" v-model="serverAddress"></mt-field>
      </mt-cell>
      <mt-cell>
        <mt-field v-model="message" ref="post_message"></mt-field>
        <mt-button size="small" type="primary" @click.native="sendMessage">发送消息</mt-button>
      </mt-cell>
      <hr/>
      <mt-cell v-for="message in messages">
        {{message.from}}:{{message.content}}
      </mt-cell>
    </div>
</template>

<script>
  import {Button, Cell, MessageBox, Field, Toast} from "mint-ui";
  let websocket;

  export default {
    components: {
      "mt-button": Button,
      "mt-cell": Cell,
      "message-box": MessageBox,
      "mt-field": Field,
    },
    name: "ChatRoom",
    // props:["serverAddress"],
    data(){
      return {
        messages:[],
        message:'',
        connected: false,
        serverAddress: '',
      }
    },
    methods:{
      connect(){
        let vm = this;
        if(this.serverAddress === ''){
          Toast('请先输入地址')
          return
        }
        console.log(this.serverAddress)
        websocket =new WebSocket(this.serverAddress);

        websocket.onopen = function(){
          console.log('已经连接上服务器')
          vm.connected = true;
        }
        websocket.onmessage = function(event){
          let data = JSON.parse(event.data);
          vm.messages.unshift({from:data.from, content:data.content})
        }
        websocket.onclose = function(event){
          vm.messages.unshift({from:'console', content:'断开连接'})
          vm.connected = false;
        }
        websocket.onerror = function (event) {
          Toast('连接失败')
          vm.connected = false;
        }
      },

      disconnect(){
        websocket.close();
      },

      sendMessage(){
        if(this.message.trim() === ''){
          Toast("请输入内容")
          return;
        }

        websocket.send(this.message);
        this.message = '';
      }
    }
  }
</script>

<style>
  .mint-cell-wrapper{
    background-image:none;
  }
  .mint-field-core{
    background:#eaeaea;
  }
</style>
