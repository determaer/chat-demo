<script setup>
 
 import FloatFeedChatApp from './components/FloatFeedChatApp.vue';
 import FloatBaseChatApp from './components/FloatBaseChatApp.vue';
import {
  messages, chats,
  userProfiles, templates
} from './data';

// Mock data
const data3 = {
  messages,
  chats,
  userProfiles,
  templates
};

// Define the auth provider
const authProvider = {
  getUserProfile(index) { return data3.userProfiles[index] },
  setUserProfileOnline(index, online){
    if (online){
      data3.userProfiles[index].online = true
      data3.userProfiles[index].status = 'lightgreen'
    }
    else if (!online){
      data3.userProfiles[index].online = false
      data3.userProfiles[index].status = 'gray'
    }
  }
};

// Define the data provider
const dataProvider = {
  setAuth(auth) {
    console.log('auth', auth);
  },
  getFeed(chatId) {
    return data3.messages.filter(m => m.chatId === chatId);
  },
  getTemplates() {
    return data3.templates;
  },
  getChats() {
    return data3.chats;
  },
  addMessage(message) {
    data3.messages.push(message);
    console.log("Добавлено новое сообщение:", message);
  },
};
</script>

<template>
  <div class="container">
    <div class="cell11">
      <FloatFeedChatApp
        :auth-provider="authProvider"
        :data-provider="dataProvider"
        :index="0"
      />
    </div>
    <div class="cell12">
      <FloatFeedChatApp
        :auth-provider="authProvider"
        :data-provider="dataProvider"
        :index="1"
      />
    </div>
    <div class="cell21">
      <FloatFeedChatApp
        :auth-provider="authProvider"
        :data-provider="dataProvider"
        :index="2"
      />
    </div>
    <div class="cell22">
      <FloatBaseChatApp
        :auth-provider="authProvider"
        :data-provider="dataProvider"
        :index="3"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 1300px;
  height: 600px;
  margin: 30px auto;
  display: grid;
  grid-template-columns: 500px 1000px;
  grid-template-rows: 500px 500px;
}

.cell11,.cell12,.cell21,.cell22{
  position: relative;
}
.cell12{
  margin-left: 50px;
}

.cell21{
  margin-top: 50px;
}
.cell22 {
  margin-top: 50px;
  margin-left: 50px;
}
</style>
