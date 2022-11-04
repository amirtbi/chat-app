<template>
  <NuxtLayout name="custom">
    <container class="gap-1 main-chat__wrapper d-flex">
      <v-row>
        <v-col cols="3">
          <!-- Left chat bar-->
          <v-card min-width="300px" min-height="100%">
            <header class="left-chat__header d-flex flex-column pa-2">
              <div class="ma-4 d-flex justify-space-between">
                <v-card-title>Chats</v-card-title>
                <v-hover>
                  <template v-slot:default="{ isHovering, props }">
                    <v-btn
                      v-bind="props"
                      :color="isHovering ? '#45cb85' : '#ffff'"
                      flat
                      small
                    >
                      <v-icon small> mdi-plus </v-icon>
                    </v-btn>
                  </template>
                </v-hover>
              </div>
              <div class="px-4 mt-2 left-chat__header--searchbar">
                <v-text-field
                  outlined
                  dense
                  label="search..."
                  prepend-inner-icon="mdi-magnify"
                ></v-text-field>
              </div>
            </header>
            <main class="left-chat__main">
              <section class="lef-chat__container">
                <v-tabs v-model="tabs" color="#45cb85" grow center-active>
                  <v-tab key="chats" value="chats">Chats</v-tab>
                  <v-tab key="contacts" value="contacts">Contacts</v-tab>
                </v-tabs>
                <v-window class="window-container" v-model="tabs">
                  <!-- Contacts-->
                  <v-window-item value="contacts">
                    <v-list density="compact">
                      <v-list-subheader>Create new Message</v-list-subheader>

                      <v-list-item
                        v-for="(item, i) in chatContacts"
                        :key="i"
                        :value="item"
                        active-class="tile"
                        @click="displayMessages(item)"
                      >
                        <template v-slot:prepend>
                          <v-badge bottom dot color="success">
                            <v-avatar size="small" color="grey-lighten-1">
                              {{ item.user.split("")[0].toLowerCase() }}
                            </v-avatar>
                          </v-badge>
                        </template>

                        <v-list-item-title
                          class="ml-4"
                          v-text="item.user"
                        ></v-list-item-title>
                      </v-list-item>
                    </v-list>
                    <v-divider> </v-divider>
                    <v-list density="compact">
                      <v-list-subheader>Channels</v-list-subheader>

                      <v-list-item
                        active-class="tile"
                        link
                        v-for="(channel, index) in channelsList"
                        :key="index"
                      >
                        <template v-slot:prepend>
                          <v-chip link>#</v-chip>
                        </template>
                        <v-list-item-title
                          :key="index"
                          :value="channel"
                          link
                          class="ml-4"
                          v-text="channel.title"
                        ></v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-window-item>
                  <!-- Chats tab-->
                  <v-window-item value="chats">
                    <v-list density="compact">
                      <v-list-subheader>Create new Message</v-list-subheader>

                      <v-list-item
                        v-for="(item, i) in chatContacts"
                        :key="i"
                        :value="item"
                        active-color="primary"
                      >
                        <!-- <template v-slot:prepend>
                          <v-icon :icon="item.icon"></v-icon>
                        </template> -->

                        <v-list-item-title
                          v-text="item.user"
                        ></v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-window-item>
                </v-window>
              </section>
            </main>
          </v-card>
        </v-col>
        <v-spacer></v-spacer>
        <v-col cols="8">
          <v-card min-height="100%">
            <div class="user-chat-topbar justify-space-between pa-2">
              <div class="d-flex flex-column">
                <v-card-title>{{ computedActiveUser.username }}</v-card-title>
                <v-card-subtitle>Online</v-card-subtitle>
              </div>
            </div>
            <div class="chat-contents chat-background">
              <div class="chat-conversations">
                <v-list class="chat-lists">
                  <v-list-item
                    class="chat-list"
                    v-for="(message, index) in messages"
                    :key="index"
                    :class="checkMessageSender(message)"
                  >
                    <v-list-item-title
                      v-text="message.text"
                    ></v-list-item-title>
                    <v-list-item-subtitle
                      v-text="message.date"
                    ></v-list-item-subtitle>
                  </v-list-item>
                  <!-- Left chats-->
                  <!-- Received Messages-->

                  <!-- Sent Messages-->
                  <!-- Right chats-->
                </v-list>
              </div>
            </div>
            <div class="chat-input-feedback pa-4 d-flex">
              <v-text-field
                dense
                outlined
                label="type your message"
              ></v-text-field>
              <v-btn class="mx-4 align-self-center" color="success" small
                ><v-icon>mdi-send</v-icon></v-btn
              >
            </div>
          </v-card>
        </v-col>
      </v-row>
    </container>
  </NuxtLayout>
</template>
<script setup>
definePageMeta({
  layout: false,
});

// Constants
const tabs = ref(null);
const chatContacts = ref([
  { user: "ALI", icon: "mdi-account" },
  { user: "HOSEIN", icon: "mdi-account" },
  { user: "JAMSHID", icon: "mdi-account" },
  { user: "RAHIM", icon: "mdi-account" },
  { user: "SADEGHJ", icon: "mdi-account" },
]);

// userInfo
const ActiveUserInfo = ref({ username: "", id: "" });

const computedActiveUser = computed(() => {
  return ActiveUserInfo.value;
});
const channelsList = ref([
  { title: "Group1" },
  { title: "Group2" },
  { title: "Group3" },
  { title: "Group4" },
  { title: "Group4" },
]);

const messages = ref([
  { sender: "ali", id: "1", text: "hi from ali", date: "9:00 am" },
  { sender: "ali", id: "1", text: "hi how are u?", date: "12:00 am" },
  { sender: "hosein", id: "2", text: "Hi, what's up?", date: "13:00 am" },
  { sender: "ali", id: "1", text: "hi from ali", date: "9:00 am" },
  { sender: "ali", id: "1", text: "hi how are u?", date: "12:00 am" },
  { sender: "hosein", id: "2", text: "Hi, what's up?", date: "13:00 am" },
]);
// Functions
function ActiveUser(user) {
  this.username = user.user;
}
const displayMessages = (clickedUser) => {
  const newUser = new ActiveUser(clickedUser);
  newUser.id = "2";
  ActiveUserInfo.value.username = newUser.username;
  ActiveUserInfo.value.id = newUser.id;
};

const checkMessageSender = (message) => {
  const senderId = message.id;
  if (senderId === "2") {
    return "right";
  } else {
    return "left";
  }
};
</script>

<style scoped>
.main-chat__wrapper {
  height: 100%;
}
.lef-chat__container {
  height: 350px;
}
.window-container {
  max-height: 100% !important;
  overflow-y: auto;
  scroll-behavior: smooth;
}
.window-container::-webkit-scrollbar {
  width: 5px;
  height: 50% !important;
}

.window-container::-webkit-scrollbar-thumb {
  background-color: #cbcbcb;

  border: 0.1px solid #b7b7b7;
}
.window-container::-webkit-scrollbar-track {
  max-height: 50%;
  height: 50%;
}
.window-container::-webkit-scrollbar-track-piece {
  background: transparent;
}

.v-chip:hover * {
  cursor: pointer !important;
}
.tile {
  color: white;
  background-color: #4b38b3;
}

/* Chats */
.chat-background {
  max-height: 350px;
  background: url("https://img.freepik.com/free-vector/white-gray-geometric-pattern-background-vector_53876-136510.jpg?w=826&t=st=1667240679~exp=1667241279~hmac=f2be032aa4d110430831b44c3e3badcd2e8df985b0ddabbcc44ae1923d451fac");
  background-size: cover;
  background-attachment: scroll;
  background-position: center;
  height: 325px;

  overflow-y: auto;
}
.chat-background {
  padding: 0.2rem 1.2rem;
  overflow-y: scroll;
}

.chat-background::-webkit-scrollbar {
  width: 5px;
  height: 50% !important;
}

.chat-background::-webkit-scrollbar-thumb {
  background-color: #cbcbcb;

  border: 0.1px solid #b7b7b7;
}
.chat-background:-webkit-scrollbar-track {
  max-height: 50%;
  height: 50%;
}
.chat-background:-webkit-scrollbar-track-piece {
  background: transparent;
}
.chat-lists {
  height: 100%;
  background-color: transparent;
}
.chat-list {
  display: flex;
  flex-direction: row;
  border-radius: 0.25rem;
}
.chat-list .v-list-item-title {
  border-radius: 0.25rem;
}
.chat-list.left {
  justify-content: flex-start;
}
.chat-list.right {
  justify-content: flex-end;
}
.chat-list.left .v-list-item-title {
  background: #ccc;
  color: black;
  padding: 0.75rem;
  margin-bottom: 0.2rem;
}
.chat-list.right .v-list-item-title {
  background: purple;
  color: white;
  padding: 0.75rem;
  margin-bottom: 0.2rem;
}
:deep() .v-input__details {
  display: none;
}
.v-list-item-title {
  font-size: 13.75px;
}
</style>
