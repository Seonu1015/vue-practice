<script setup lang="ts">
import { ref } from "vue";
import { RouterView } from "vue-router";
import { useTheme } from "vuetify";

const notification = [
  {
    title: "Message from A",
    icon: "mdi-email",
    color: "blue",
  },
  {
    title: "Message from B",
    icon: "mdi-email",
    color: "green",
  },
  {
    title: "Message from B",
    icon: "mdi-email",
    color: "red",
  },
  {
    title: "Message from D",
    icon: "mdi-email",
    color: "yellow",
  },
  {
    title: "Message from E",
    icon: "mdi-email",
    color: "purple",
  },
  {
    title: "Message from F",
    icon: "mdi-email",
    color: "orange",
  },
];

const darkTheme = ref(true);
const theme = useTheme();

function changeTheme() {
  darkTheme.value = !darkTheme.value;
  theme.global.name.value = darkTheme.value ? "dark" : "light";
}
</script>

<template>
  <v-app>
    <v-toolbar density="compact">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>
        <RouterLink to="/"> Vuetify </RouterLink>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon @click="changeTheme">
        <v-icon :icon="darkTheme ? 'mdi-weather-sunny' : 'mdi-weather-night'">
        </v-icon
      ></v-btn>

      <v-menu transition="scale-transition">
        <template v-slot:activator="{ props }">
          <v-btn icon v-bind="props">
            <v-badge color="red-darken-2" content="6" size="small">
              <v-icon icon="mdi-bell" color="blue-darken-4"></v-icon
            ></v-badge>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in notification"
            :key="index"
            :value="index"
          >
            <v-list-item-title>
              <v-icon :icon="item.icon" :color="item.color"></v-icon>
              {{ item.title }}</v-list-item-title
            >
          </v-list-item>
        </v-list>
      </v-menu>

      <v-btn to="/login" size="small" text="Login" variant="outlined"> </v-btn>
    </v-toolbar>

    <v-main>
      <v-fade-transition>
        <RouterView />
      </v-fade-transition>
    </v-main>
  </v-app>
</template>
