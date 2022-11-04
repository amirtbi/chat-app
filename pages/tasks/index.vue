<script setup>
definePageMeta({
  layout: false,
});
const filterOptions = reactive({ type: "", status: null, group: null });
</script>

<template>
  <NuxtLayout name="custom">
    <v-container>
      <FilterManager
        :default-filters="filterOptions"
        user-role="admin"
        v-slot="{ filters, setFilter }"
      >
        <TaskManager :filter="filters" v-slot="{ tasks }">
          <v-card min-height="100%" width="600px">
            <v-card-title>Filter tasks</v-card-title>
            <v-card-actions class="d-flex flex-column align-start">
              <div class="d-flex">
                <v-radio-group
                  inline
                  v-model="filterOptions.type"
                  @input="setFilter($event)"
                  class="d-flex"
                >
                  <h4 class="pa-4">Task Type</h4>
                  <v-radio label="sent" value="sent"></v-radio>
                  <v-radio label="received" value="received"></v-radio>
                </v-radio-group>
              </div>
              <div class="filter">
                <v-radio-group
                  inline
                  v-model="filterOptions.status"
                  class="d-flex"
                >
                  <h4 class="pa-4">Task status</h4>
                  <v-radio label="notcompleted" value="notcompleted"></v-radio>
                  <v-radio label="completed" value="completed"></v-radio>
                </v-radio-group>
              </div>
              <div class="filter">
                <v-radio-group
                  inline
                  v-model="filterOptions.group"
                  class="d-flex"
                >
                  <h4 class="pa-4">Task Group</h4>
                  <v-radio label="Group1" value="0"></v-radio>
                  <v-radio label="Group2" value="1"></v-radio>
                </v-radio-group>
              </div>
            </v-card-actions>
          </v-card>
          <v-card class="mt-4" min-height="100%" width="600px">
            <v-list v-for="(item, index) in tasks" Key="index">
              <v-list-item
                >Text:{{ item.text }}<br />
                Type:{{ item.status }}
              </v-list-item>
            </v-list>
          </v-card>
        </TaskManager>
      </FilterManager>
    </v-container>
  </NuxtLayout>
</template>
