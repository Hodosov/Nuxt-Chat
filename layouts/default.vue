<template>
 <v-app app dark>
  <v-navigation-drawer app v-model="drawer" mobile-break-point='540'>
      <v-card app>
    <v-list subheader>
      <v-subheader>Собеседники</v-subheader>
      <div
        v-for="u in users"
        :key="u.name + 2"
        @click.prevent
         class="mx-auto"
          min-width="600">
        <div class="mes-card">
          <div>{{u.name}}</div>
           <div>
          <v-icon :color="u.id === user.id ? 'primary' : 'grey'">chat_bubble</v-icon>
        </div>
        </div>
      </div>
    </v-list>
  </v-card>
          </v-navigation-drawer>
          <v-toolbar app>
          <v-toolbar-side-icon @click="drawer = !drawer"></v-toolbar-side-icon>
          <v-btn icon @click="exit">
          <v-icon>arrow_back</v-icon>
          </v-btn>
          <v-toolbar-title>Чат комната {{user.room}}</v-toolbar-title>
  </v-toolbar>
  <v-content>
    <div style="height: 100%">
      <nuxt />
    </div>
  </v-content>
</v-app>
</template>

<script>
import {mapState, mapMutations} from 'vuex'
export default {
  data: () => ({
    drawer: true,
  }),
  computed: mapState(['user', 'users']),
  methods: {
    ...mapMutations(['clearData']),
    exit() {
      this.$socket.emit('userLeft', this.user.id, () => {
          this.$router.push('/?message=leftChat')
          this.clearData()
      })
    }
  }
}
</script>

<style scoped>
  .mes-card {
    display: flex;
    flex-direction: row;
    padding: 10px 20px;
    justify-content: space-between;
  }
  
  .mx-auto :hover {
    background: #303030;
    cursor: pointer;
  }
</style>
