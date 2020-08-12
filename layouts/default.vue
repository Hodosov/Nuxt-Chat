<template>
 <v-app app dark>
  <v-navigation-drawer app v-model="drawer" mobile-break-point='540'>
      <v-card app>
    <v-list subheader>
      <v-subheader>Собеседники</v-subheader>
      <div
        v-for="item in items"
        :key="item.title"
        @click.prevent
         class="mx-auto"
          min-width="600">
        <div class="mes-card">
          <div v-text="item.title"></div>
           <div>
          <v-icon :color="item.id === 2 ? 'deep-purple accent-4' : 'grey'">chat_bubble</v-icon>
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
     items: [
        { active: true, title: 'Jason Oner', id: 1},
        { active: true, title: 'Ranee Carlson', id: 2},
      ],
  }),
  computed: mapState(['user']),
  methods: {
    ...mapMutations(['clearData']),
    exit() {
      this.$router.push('/?message=leftChat')
      this.clearData()
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
