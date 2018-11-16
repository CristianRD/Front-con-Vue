<template>
  <div>
    <ul v-for='user in users'>
      <li>
        {{user.first_name}}
      </li>
    </ul>
    me lleva la madre
  </div>
</template>

<script>
export default {
  name: 'Users',
  data () {
    return {
      users: [
        {
          first_name: 'Cristian',
          last_name: 'RD',
          editing: false
        },
        {
        first_name: 'jose',
        last_name: 'machmisaln'
        }]
  }
}
}
</script>

<style scoped>
</style>
