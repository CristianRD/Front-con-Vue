<template>
  <div id="app">
    <nav>
      <ul>
        <li>
          <router-link to="/users">Usuarios</router-link>
        </li>
        <li>
          <router-link to="/">Mascotas</router-link>
        </li>
      </ul>
    </nav>
    <hr>
    <router-view></router-view>
  </div>
</template>

<script>
import pets from './components/Pets'
import users from './components/Users'

export default {
  name: 'App',
  components: {
    pets,
    users
  }
}
</script>

<style>
 * {
   box-sizing: border-box;
 }
</style>
