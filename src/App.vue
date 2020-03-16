<template>
  <v-app id="keep">
    <v-app-bar dark color="#393e46" app clipped-left>
      
      <span class="title ml-3 mr-5">
        Job Order
      </span>
      <v-spacer />
      <v-btn to="Login">
        <span>Log In</span>
      </v-btn>
      <v-btn>
        <span>Register</span>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer
     dark
      v-model="drawer"
      app
      clipped
      permanent
      floating
      color="#393e46"
    >
      <v-list dense>
        <template v-for="(item, i) in items">
          <v-row v-if="item.heading" :key="i" align="center">
            <v-col cols="6">
              <v-subheader v-if="item.heading">{{ item.heading }}</v-subheader>
            </v-col>
            <v-col cols="6" class="text-right">
              <!-- <v-btn small text>edit</v-btn> -->
            </v-col>
          </v-row>
          <v-divider v-else-if="item.divider" :key="i" dark class="my-4" />
          <v-list-item v-else :key="i" link :to="item.route">
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title >{{
                item.text
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </template>
      </v-list>
    </v-navigation-drawer>

    <v-content class="grey darken-4">
      <v-container fluid>
        <v-slide-y-transition mode="out-in" hide-on-leave>
          <router-view class="pt-10"></router-view>
        </v-slide-y-transition>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  props: {
    source: String
  },
  name: "App",
  
  mounted() {
    
  },
  data: () => ({
    drawer: null,
    isLoading: true,
    items: [
      {
        icon: "mdi-order-bool-descending",
        text: "Home",
        route: "Home"
      },
     {divider: true},
     {
        icon: "mdi-table",
        text: "Job Order Table",
        route: "jobordertable"
      },
    ],
  })
};
</script>
<style>
#keep .v-navigation-drawer__border {
  display: none;
}
</style>
