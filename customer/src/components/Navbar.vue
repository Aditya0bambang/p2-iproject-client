<script>
import { mapActions, mapWritableState } from "pinia";
import { RouterLink } from "vue-router";
import { useAllStore } from "../stores/allStore";

export default {
  computed: {
    ...mapWritableState(useAllStore, ["isLogin"]),
  },
  methods: {
    ...mapActions(useAllStore, ["logout"]),
  },
  components: {
    RouterLink,
  },
  created() {
    if (localStorage.getItem("access_token")) {
      this.isLogin = true;
    }
  },
};
</script>

<template>
  <nav class="navbar navbar-expand navbar-light bg-light">
    <RouterLink to="/" class="navbar-brand">Movie Cinema</RouterLink>
    <ul class="navbar-nav" style="margin-left: auto">
      <li class="nav-item" v-if="!isLogin">
        <RouterLink to="/register" class="nav-link">Sign Up</RouterLink>
      </li>
      <li class="nav-item" v-if="!isLogin">
        <RouterLink to="/login" class="nav-link">Sign In</RouterLink>
      </li>
      <li class="nav-item" v-if="isLogin">
        <RouterLink to="/ticket" class="nav-link">Your ticket</RouterLink>
      </li>
      <li class="nav-item" v-if="isLogin">
        <RouterLink v-on:click="logout" to="/login" class="nav-link"
          >Logout</RouterLink
        >
      </li>
    </ul>
  </nav>
</template>
