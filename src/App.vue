<template>
  <v-app  >
  
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      app
      overflow
    >
      <v-list-item>
        <v-list-item-avatar tile>
          <v-img :src="github.avatar"></v-img>
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>{{github.user}}</v-list-item-title>
          <v-list-item-subtitle>{{github.name}}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>

        <v-list-item>
          <v-icon color="black">mdi-github-circle</v-icon>
          <div class="title-list">Répértoires</div>
        </v-list-item>

        <v-list-item
          v-for="(repo, i) in github.repos"
          :key="i"
          link
        >
          <v-list-item-content>
            <v-list-item-title><a target="_blank" :href="repo.html_url">{{ repo.full_name }}</a></v-list-item-title>
          </v-list-item-content>
        </v-list-item>

      </v-list>

    </v-navigation-drawer>
     
    <v-app-bar hide-on-scroll class="toolbar" dark color="rgb(79, 79, 172)" :clipped-left="primaryDrawer.clipped" app>
      <v-app-bar-nav-icon @click.stop="primaryDrawer.model = !primaryDrawer.model"></v-app-bar-nav-icon>
      <v-toolbar-title  class="headline text-uppercase">
        <span class="font-weight-light">ARBRE DE COMPETENCE</span>
      </v-toolbar-title>
    </v-app-bar>
    
    
    <v-content class="content">

      <div class="div-nav">
        <v-btn @click="onboarding=0"  class="btn-nav" >
          <v-icon color="orange lighten-2">mdi-star</v-icon>
          Succès
        </v-btn>
        <v-btn @click="onboarding=1" class="btn-nav" >
          <v-icon color="red lighten-1">mdi-cards</v-icon>
          Cartes
        </v-btn>
      </div>

      <v-window v-model="onboarding" >
        <v-window-item>
          <SkillAchievements/>
        </v-window-item>
        <v-window-item>
          <SkillCards/>
        </v-window-item>
      </v-window>

      <v-footer
        padless
      >
        <v-card
          tile
          class="grey darken-3 black--text text-center footer-card"
        >
          <v-card-text class="black--text">
            <v-icon color="white" size="24px">mdi-github-circle</v-icon> <a target="_blank" href="https://github.com/Toohk/achievements">Github</a> 
          </v-card-text>
        </v-card>
      </v-footer>

    </v-content>
    
  </v-app>
  
</template>

<script>
import SkillCards from './components/SkillCards';
import SkillAchievements from './components/SkillAchievements';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SkillCards,
    SkillAchievements
  },

  mounted () {
    const user = "toohk"
    axios.get('https://api.github.com/users/'+user)
    .then(response => {
      this.github.name = response.data.name;
      this.github.user = response.data.login;
      this.github.avatar = response.data.avatar_url;
    })
    .catch(error => {
      // eslint-disable-next-line
      console.log(error)
    })
    axios.get('https://api.github.com/users/'+user+'/repos?type=all')
    .then(response => {
      this.github.repos = response.data
    })
    .catch(error => {
      // eslint-disable-next-line
      console.log(error)
    })
  },

  data: () => ({
    github:{
      user:"",
      name:"",
      avatar:"",
      repos:[]
    },
    primaryDrawer: {
      model: true,
      type: 'Temporary',
    },
    onboarding: 0,
  }),
};
</script>

<style scoped>

.content{
  background: 
  linear-gradient(0deg, rgba(16, 130, 178, 0.58) 0%, rgba(16, 130, 178, 0.58) 13%,rgba(49, 137, 167, 0.58) 13%, rgba(49, 137, 167, 0.58) 42%,rgba(81, 143, 157, 0.58) 42%, rgba(81, 143, 157, 0.58) 49%,rgba(114, 150, 146, 0.58) 49%, rgba(114, 150, 146, 0.58) 58%,rgba(147, 157, 135, 0.58) 58%, rgba(147, 157, 135, 0.58) 69%,rgba(180, 164, 124, 0.58) 69%, rgba(180, 164, 124, 0.58) 74%,rgba(212, 170, 114, 0.58) 74%, rgba(212, 170, 114, 0.58) 78%,rgba(245, 177, 103, 0.58) 78%, rgba(245, 177, 103, 0.58) 100%),linear-gradient(90deg, rgb(180, 56, 238) 0%, rgb(180, 56, 238) 11%,rgb(190, 82, 231) 11%, rgb(190, 82, 231) 22%,rgb(201, 109, 225) 22%, rgb(201, 109, 225) 46%,rgb(211, 135, 218) 46%, rgb(211, 135, 218) 60%,rgb(222, 161, 212) 60%, rgb(222, 161, 212) 65%,rgb(232, 187, 205) 65%, rgb(232, 187, 205) 87%,rgb(243, 214, 199) 87%, rgb(243, 214, 199) 92%,rgb(253, 240, 192) 92%, rgb(253, 240, 192) 100%) !important;
  background-attachment: fixed !important;
  background-position: center !important;
  background-repeat: no-repeat !important;
  background-size: cover !important;
  padding-top: 120px !important;
 
}
.toolbar{
  position: fixed !important;
}
.footer-card{
  width: 100%;
}
.title-list{
  margin-left: 10px;
  font-weight: bold;
}
.div-nav{
  width: 100%;
  display: flex;
  justify-content: center;
}
.btn-nav{
  margin: 10px;
}

</style>
