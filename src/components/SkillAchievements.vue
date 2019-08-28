<template>

  <v-container class="container">

    <v-snackbar v-model="snackbar">
      {{ text }}
      <v-btn
        color="pink"
        text
        @click="snackbar = false"
      >
        <v-icon>mdi-close-circle</v-icon>
      </v-btn>
    </v-snackbar>

    <v-hover  v-for="(item, i) in items" v-bind:key="item.title" v-slot:default="{ hover }">
      <v-card max-width="1000" min-width="330" class="mx-auto card">
        <div class="title">{{item.title}}</div>
        <div class="subtile">
          {{item.text}}
        </div>
        <v-divider color="white"></v-divider>
        <v-progress-linear
          v-model="score.data[i]"
          height="20"
          color="light-green lighten-2"
          class="progress-skill mx-auto"
          reactive
          striped
        >
          <template v-slot="{ value }">
            <strong>{{ Math.ceil(value) }}%</strong>
          </template>
        </v-progress-linear>
    
        <v-list >
          <v-list-item-group>

            <template v-for="achievement in item.achievements">
              <v-list-item  class="tile" active="false" :key="achievement.name">

                <v-avatar tile class="image">
                  <img v-if="achievement.achieve == false" class="false-img" v-bind:src="achievement.img">
                  <img v-if="achievement.achieve == true" class="true-img" v-bind:src="achievement.img">
                </v-avatar>

                <v-list-item-content @click="openSnackbar(achievement.description)">
                  <v-list-item-title v-if="achievement.achieve == false"  class="false-text bold" v-text="achievement.name"></v-list-item-title>
                  <v-list-item-subtitle v-if="achievement.achieve == false" class="false-text" v-text="achievement.description"></v-list-item-subtitle>
                  <v-list-item-title v-if="achievement.achieve == true"  class=" bold blue-text" v-text="achievement.name"></v-list-item-title>
                  <v-list-item-subtitle v-if="achievement.achieve == true" class="black-text" v-text="achievement.description"></v-list-item-subtitle>
                </v-list-item-content>

                <v-list-item-action @click="if(achievement.achieve == true){
                achievement.achieve = false}else{achievement.achieve = true}">
                  <v-icon v-if="achievement.achieve == true" color="green">mdi-check-bold</v-icon>
                  <v-icon v-if="achievement.achieve == false" color="grey">mdi-radiobox-blank</v-icon>
                </v-list-item-action>
            
              </v-list-item>
            </template>

          </v-list-item-group>
        </v-list>
      </v-card>
    </v-hover>

  </v-container>
    
</template>

<script>
export default {
  computed:{
    score(){
      const data = this.calcul();
      return {data} 
    }
  },
  methods:{
  calcul(){
      const data = [];
      const result = [];
      for (let i=0; i < this.items.length; i++){
        data.push({true: 0, total: this.items[i].achievements.length})
        for( let x=0; x < this.items[i].achievements.length; x++){
          if (this.items[i].achievements[x].achieve == true){
            data[i].true=data[i].true+1
          }
        }
        result.push((data[i].true/data[i].total)*100)
      }
      return result
  },
  openSnackbar(text){
    this.text = text;
    this.snackbar =true;
  }
  },
 
  data: () => ({
    snackbar: false,
    text:"",
    items:[
      {
        title:"Front-End",
        text:"Développer la partie front-end d'une application web en intégrant les recommandations de sécurité",
        achievements:[ 
          {
            name:"Maître de l'art du maquettage",
            description:"Maquetter une application",
            img:"https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Maquette_centre_ville_Saint-L%C3%A9onard.jpg/3264px-Maquette_centre_ville_Saint-L%C3%A9onard.jpg",
            achieve:true
          },
          {
            name:"Interface",
            description:"Réaliser une interface web statique et adaptable",
            img:"https://production-gameflipusercontent.fingershock.com/us-east-1:db514ae5-9998-4151-8c66-cb3b27b2e87e/cbb14b78-3484-4d2f-b2b2-7c2afcfb173b/c7062b30-6784-4308-b0bf-d8c47e7280c0",
            achieve:true
          },
          {
            name:"Super Interface",
            description:"Développer une interface utilsateur dynamique",
            img:"https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/dd6bc5b5-932d-4de0-ab20-1d12c006edef/dcv8di5-296e5caa-3f67-491e-b6ff-c9a15ce04472.png/v1/fill/w_854,h_936,strp/red_yoshi_in_super_smash_bros_ultimate_by_armimason_dcv8di5-pre.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7ImhlaWdodCI6Ijw9MTIwNSIsInBhdGgiOiJcL2ZcL2RkNmJjNWI1LTkzMmQtNGRlMC1hYjIwLTFkMTJjMDA2ZWRlZlwvZGN2OGRpNS0yOTZlNWNhYS0zZjY3LTQ5MWUtYjZmZi1jOWExNWNlMDQ0NzIucG5nIiwid2lkdGgiOiI8PTExMDAifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6aW1hZ2Uub3BlcmF0aW9ucyJdfQ.UgKwD2IotJQFptwv-BxlroE8MOtIVfjY2aDEXawZWls",
            achieve:true
          },
          {
            name:"Super Interface 2",
            description:"Réaliser une interface utilisateur avec une solution de gestion de contenu ou e-commerce",
            img:"https://vignette.wikia.nocookie.net/vsbattles/images/3/3a/3DS_MetroidSamusReturns_char_01_50.png/revision/latest?cb=20170622030710",
            achieve:true
          },
        ]
      },
      {
        title:"Back-End",
        text:"Développer la partie back-end d'une application web en intégrant les recommandations de sécurité",
        achievements:[ 
          {
            name:"BDD",
            description:"Créer une base de données",
            img:"https://gamepedia.cursecdn.com/minecraft_fr_gamepedia/thumb/f/f6/Gardien.png/220px-Gardien.png?version=76dfdac84576411e2163c8c1f4c1cc37",
            achieve:true
          },
          {
            name:"Connexion !!!",
            description:"Développer les composants d'accès aux données",
            img:"https://i.pinimg.com/originals/fd/b2/e1/fdb2e140edf63239022674fd217ccff8.jpg",
            achieve:true
          },
          {
            name:"Back end",
            description:"Développer la partie back-end d'une application web ou web mobile",
            img:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSFj-mWgjxjIqLvP5nyVYf4H4HX6yBSB8PC5t3Dv2PiFOW1WEfF",
            achieve:true
          },
          {
            name:"Voila voila",
            description:"Elaborer et mettre en oeuvre des composants dans une appilcation de gestion de contenu ou e-commerce",
            img:"https://scontent-atl3-1.cdninstagram.com/vp/6d958cc8ed02ea4d3289622f411145c2/5DF433CA/t51.2885-15/e35/c0.73.583.583/s480x480/50751466_250987435819779_2974596966509900466_n.jpg?_nc_ht=scontent-atl3-1.cdninstagram.com",
            achieve:true
          },
        ]
      },
      {
        title:"Annexe",
        achievements:[ 
          {
            name:"Anglais",
            description:"You speak english but not complétement",
            img:"https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/Flag_of_Belgium.svg/1200px-Flag_of_Belgium.svg.png",
            achieve:true
          },
          {
            name:"TRE",
            description:"Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque.",
            img:"https://assets.pokemon.com/assets/cms2/img/pokedex/full/083.png",
            achieve:false
          }
        ]
      },
    ]
  }),
    
}
</script>

<style>

.card {
  background-color:white!important ;
  border: double 6px rgba(92, 111, 153, 0.801);
  margin: 20px;
  padding: 30px;
  border-radius: 10px;
  max-width: 900px;
}
.subtile{
  margin-bottom: 20px;
}
.image{
  margin: 10px 25px 10px 0px;
}
.tile {
  background-color: rgba(102, 102, 102, 0.062);
  margin: 5px;
  border-radius: 10px;
  border: double 3px rgb(255, 255, 255);
}
.v-list {
  background: rgba(73, 73, 73, 0) !important;
}
.black-text{
  color: rgb(0, 0, 0)!important;
}
.blue-text{
  color: rgb(79, 79, 172);
}
.false-img{
  filter: grayscale(1);
  -webkit-filter: grayscale(1);
  -moz-filter: grayscale(1);
  -o-filter: grayscale(1);
  -ms-filter: grayscale(1);
  border: double rgb(172, 172, 172);
  border-radius: 7px !important;
  }
.true-img{
  border: double rgb(78, 121, 161);
  border-radius: 7px !important;
}
.bold{
  font-weight: bold !important;
}
.false-text {
  color: rgb(158, 158, 158) !important;
}
.progress-skill{
  margin: 20px 0px 10px 10px;
  border-radius: 7px;
  max-width: 500px;
  border: solid rgb(255, 255, 255) 1px;
}
.container .card:last-of-type{
  margin-bottom: 150px;
}
  
</style>
