<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import { getUsers, selectUser, currentUser } from '@/models/users'

const users = getUsers()
const navbarBurgerActive = ref(false)
const loginDropdownActive = ref(false)
</script>

<template>
  <nav class="navbar is-warning" role="navigation">
    <div class="container">
      <div class="navbar-brand">
        <a class="navbar-item" href="/">
          <img class="logo" src="@/assets/newlogo.svg" width="40" />
        </a>

        <a
          role="button"
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          :class="{ 'is-active': navbarBurgerActive }"
          @click="navbarBurgerActive = !navbarBurgerActive"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu" :class="{ 'is-active': navbarBurgerActive }">
        <div class="navbar-start">
          <RouterLink to="/my-activity" class="navbar-item pr-3 pl-4"
            ><span class="icon"><i class="fa-solid fa-person"></i></span>My Activity</RouterLink
          >
          <RouterLink to="/" class="navbar-item pr-3"
            ><span class="icon"><i class="fa-solid fa-people-group"></i></span>Friends'
            Activity</RouterLink
          >
          <RouterLink to="/" class="navbar-item pr-3"
            ><span class="icon"><i class="fa-solid fa-chart-area"></i></span>Statistics</RouterLink
          >
          <RouterLink to="/" class="navbar-item pr-3"
            ><span class="icon"><i class="fa-solid fa-magnifying-glass"></i></span
            >Search</RouterLink
          >
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div v-if="currentUser">
              <span>
                <span><i class="fa-solid fa-user pr-2"></i></span> {{ currentUser.name }}
                <button class="pl-2" @click="selectUser(null)"><u>Log out</u></button>
              </span>
            </div>
            <div v-else class="buttons">
              <a
                class="button is-link dropdown"
                :class="{ 'is-active': loginDropdownActive }"
                @click="loginDropdownActive = !loginDropdownActive"
              >
                <div class="dropdown-trigger">
                  <span><i class="fa-regular fa-user pr-2"></i></span> Log in
                  <span class="pl-2"><i class="fas fa-angle-down"></i></span>
                </div>
                <div class="dropdown-menu" role="menu">
                  <div class="dropdown-content">
                    <a
                      v-for="user in users"
                      :key="user.id"
                      class="dropdown-item"
                      @click="(selectUser(user), console.log(currentUser.name))"
                    >
                      {{ user.name }}
                    </a>
                  </div>
                </div>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped></style>
