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
                <v-btn flat small color="#45cb85">
                  <v-icon small> mdi-plus </v-icon>
                </v-btn>
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
              <section>
                <v-tabs v-model="tabs" color="#45cb85" grow center-active>
                  <v-tab key="chats" value="chats">Chats</v-tab>
                  <v-tab key="contacts" value="contacts">Contacts</v-tab>
                </v-tabs>
                <v-window class="overflow-y-hidden" v-model="tabs">
                  <v-window-item value="contacts">
                    <v-list density="compact">
                      <v-list-subheader>Create new Message</v-list-subheader>

                      <v-list-item
                        v-for="(item, i) in chatContacts"
                        :key="i"
                        :value="item"
                        active-color="#4b38b3"
                      >
                        <template v-slot:prepend>
                          <v-avatar color="grey-lighten-1">
                            {{ item.user.split("")[0].toUpperCase() }}
                          </v-avatar>
                        </template>

                        <v-list-item-title
                          v-text="item.user"
                        ></v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-window-item>
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
                <v-card-title>Alireza</v-card-title>
                <v-card-subtitle>Online</v-card-subtitle>
              </div>
            </div>
            <div class="chat-background"></div>
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
</script>

<style scoped>
.main-chat__wrapper {
  height: 100%;
}
.chat-background {
  max-height: 350px;
  background: url("https://img.freepik.com/free-vector/white-gray-geometric-pattern-background-vector_53876-136510.jpg?w=826&t=st=1667240679~exp=1667241279~hmac=f2be032aa4d110430831b44c3e3badcd2e8df985b0ddabbcc44ae1923d451fac");
  background-size: cover;
  background-attachment: scroll;
  background-position: center;
  height: 325px;
  background-color: #cccc;
  overflow-y: auto;
}
:deep() .v-input__details {
  display: none;
}
</style>
