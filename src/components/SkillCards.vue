<template>
  <v-container class="block-content">
        
    <v-dialog
      v-model="dialog"
      min-width="290"
      max-width="600"
      v-bind="description"
    >
      <v-card>
        <v-card-title class="headline"><v-avatar tile class="avatar"><img v-bind:src="description.img"></v-avatar>{{description.title}}</v-card-title>
        <v-card-text>
          <blockquote :cite="description.source">
            <p>{{description.text}}</p>
            <footer><cite> - <a target="_blank" :href="description.source">Wikipedia</a></cite></footer>
          </blockquote>
        </v-card-text>
        <v-card-actions>
          <div class="flex-grow-1"></div>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <div  v-for="card in cards" v-bind:key="card.title">
      <h2>{{card.title}}</h2>
      <v-divider color="white"></v-divider>
      <v-flex class="block-card">

        <v-hover v-slot:default="{ hover }" v-for="skill in card.skills" v-bind:key="skill.name">
          <v-card  :elevation="hover ? 12 : 2" class="card-skill" @click="openSkill(skill)" >
            <div class="name title-card">
              <v-avatar tile size="50" class="avatar">
                <img v-bind:src="skill.avatar">
              </v-avatar>{{skill.name}}
            </div>
            <v-divider color="white"></v-divider>
            <v-rating  color="yellow darken-2" v-model="skill.rank"></v-rating>  
          </v-card>
        </v-hover>

      </v-flex>
    </div>
     
  </v-container>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    description:{
      title:"",
      text:"",
      img:"",
      source:"",
    },
    cards: [
      {
        title: "Languages",
        skills:[
          {
            name: "HTML",
            rank: 4,
            avatar: "https://icon-library.net/images/icon-for-html/icon-for-html-3.jpg",
            text: "L’HyperText Markup Language, généralement abrégé HTML, est le langage de balisage conçu pour représenter les pages web. C’est un langage permettant d’écrire de l’hypertexte, d’où son nom. HTML permet également de structurer sémantiquement et logiquement et de mettre en forme le contenu des pages, d’inclure des ressources multimédias dont des images, des formulaires de saisie et des programmes informatiques. Il permet de créer des documents interopérables avec des équipements très variés de manière conforme aux exigences de l’accessibilité du web. Il est souvent utilisé conjointement avec le langage de programmation JavaScript et des feuilles de style en cascade (CSS). HTML est inspiré du Standard Generalized Markup Language (SGML). Il s'agit d'un format ouvert.",
            source: "https://fr.wikipedia.org/wiki/Hypertext_Markup_Language"
          },
          {
            name: "CSS",
            rank: 4,
            avatar: "https://cdn3.iconfinder.com/data/icons/social-media-logos-flat-colorful-1/2048/5351_-_CSS3-512.png",
            text:"Les feuilles de style en cascade, généralement appelées CSS de l'anglais Cascading Style Sheets, forment un langage informatique qui décrit la présentation des documents HTML et XML. Les standards définissant CSS sont publiés par le World Wide Web Consortium (W3C). Introduit au milieu des années 1990, CSS devient couramment utilisé dans la conception de sites web et bien pris en charge par les navigateurs web dans les années 2000.",
            source:"https://fr.wikipedia.org/wiki/Feuilles_de_style_en_cascade"
          },
          {
            name: "JavaScript",
            rank: 4,
            avatar: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/600px-JavaScript-logo.png",
            text:"JavaScript est un langage de programmation de scripts principalement employé dans les pages web interactives mais aussi pour les serveurs avec l'utilisation (par exemple) de Node.js. C'est un langage orienté objet à prototype, c'est-à-dire que les bases du langage et ses principales interfaces sont fournies par des objets qui ne sont pas des instances de classes, mais qui sont chacun équipés de constructeurs permettant de créer leurs propriétés, et notamment une propriété de prototypage qui permet d'en créer des objets héritiers personnalisés. En outre, les fonctions sont des objets de première classe. Le langage supporte le paradigme objet, impératif et fonctionnel. JavaScript est le langage possédant le plus large écosystème grâce à son gestionnaire de dépendances npm, avec environ 500 000 paquets en août 2017.",
            source:"https://fr.wikipedia.org/wiki/JavaScript"
          },
          {
            name: "PHP",
            rank: 4,
            avatar: "https://images.vexels.com/media/users/3/166470/isolated/preview/73835fa38fba6d35aff9de603dc5044a-php-programming-language-icon-by-vexels.png",
            text: "PHP: Hypertext Preprocessor, plus connu sous son sigle PHP (sigle auto-référentiel), est un langage de programmation libre, principalement utilisé pour produire des pages Web dynamiques via un serveur HTTP, mais pouvant également fonctionner comme n'importe quel langage interprété de façon locale. PHP est un langage impératif orienté objet. PHP a permis de créer un grand nombre de sites web célèbres, comme Facebook, Wikipédia, etc. Il est considéré comme une des bases de la création de sites web dits dynamiques mais également des applications web.",
            source:"https://fr.wikipedia.org/wiki/PHP"
          },
          {
            name: "SQL",
            rank: 3,
            avatar: "https://jeydubrulle.files.wordpress.com/2015/04/sql-logo.png?w=290",
            text: "SQL (sigle de Structured Query Language, en français langage de requête structurée) est un langage informatique normalisé servant à exploiter des bases de données relationnelles. La partie langage de manipulation des données de SQL permet de rechercher, d'ajouter, de modifier ou de supprimer des données dans les bases de données relationnelles. Outre le langage de manipulation des données, la partie langage de définition des données permet de créer et de modifier l'organisation des données dans la base de données, la partie langage de contrôle de transaction permet de commencer et de terminer des transactions, et la partie langage de contrôle des données permet d'autoriser ou d'interdire l'accès à certaines données à certaines personnes.",
            source:"https://fr.wikipedia.org/wiki/Structured_Query_Language"
          },
        ]
      },
      {
        title: "Bases de données",
        skills:[
          {
            name: "MySQL",
            rank: 3,
            avatar: "https://seeklogo.net/wp-content/uploads/2017/05/mysql-logo.png",
            text:"MySQL est un système de gestion de bases de données relationnelles (SGBDR). Il est distribué sous une double licence GPL et propriétaire. Il fait partie des logiciels de gestion de base de données les plus utilisés au monde, autant par le grand public (applications web principalement) que par des professionnels, en concurrence avec Oracle, PostgreSQL et Microsoft SQL Server.Son nom vient du prénom de la fille du cocréateur Michael Widenius, My. SQL fait référence au Structured Query Language, le langage de requête utilisé.",
            source:"https://fr.wikipedia.org/wiki/MySQL",
          },
          {
            name: "MongoDB",
            rank: 3,
            avatar: "https://humancoders-formations.s3.amazonaws.com/uploads/course/logo/22/thumb_bigger_formation-mongodb.png",
            text:"MongoDB est un système de gestion de base de données orienté documents, répartissable sur un nombre quelconque d'ordinateurs et ne nécessitant pas de schéma prédéfini des données. Il est écrit en C++. Le serveur et les outils sont distribués sous licence SSPL, les pilotes sous licence Apache et la documentation sous licence Creative Commons2. Il fait partie de la mouvance NoSQL.",
            source:"https://fr.wikipedia.org/wiki/MongoDB",
          },
        ]
      },
      {
        title:"Frameworks",
        skills:[
          {
            name: "Symfony 4",
            rank: 4,
            avatar: "https://cdn.worldvectorlogo.com/logos/symfony.svg",
            text:"Symfony est un ensemble de composants PHP ainsi qu'un framework MVC libre écrit en PHP. Il fournit des fonctionnalités modulables et adaptables qui permettent de faciliter et d’accélérer le développement d'un site web.",
            source:"https://fr.wikipedia.org/wiki/Symfony",
          },
          {
            name: "Vue JS",
            rank: 4,
            avatar: "http://assets.stickpng.com/thumbs/58482acecef1014c0b5e4a1e.png",
            text:"Vue.js est un framework JavaScript open-source utilisé pour construire des interfaces utilisateur. La bibliothèque est notamment utilisée par Adobe, Alibaba et Gitlab. Vue a été créé par Evan You après avoir travaillé pour Google en utilisant AngularJS dans plusieurs projets",
            source:"https://fr.wikipedia.org/wiki/Vue.js"
          },
        ]
      },
      {
        title:"CMS",
        skills:[
          {
            name: "Wordpress",
            rank: 2,
            avatar: "https://image.flaticon.com/icons/png/512/15/15986.png",
            text:"WordPress est un système de gestion de contenu (SGC ou content management system (CMS) en anglais) gratuit, libre et open-source. Ce logiciel écrit en PHP repose sur une base de données MySQL et est distribué par l'entreprise américaine Automattic. Les fonctionnalités de WordPress lui permettent de créer et gérer différents types de sites Web : blogue, site de vente en ligne, site vitrine ou encore portfolio. Il est distribué selon les termes de la licence GNU GPL version 2. Le logiciel est aussi à l'origine du service WordPress.com",
            source:"https://fr.wikipedia.org/wiki/WordPress"
          },
        ]
      },
      {
        title:"Gestion de projet",
        skills:[
          {
            name: "Git",
            rank: 4,
            avatar: "https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png",
            text:"Git est un logiciel de gestion de versions décentralisé. C'est un logiciel libre créé par Linus Torvalds, auteur du noyau Linux, et distribué selon les termes de la licence publique générale GNU version 2. En 2016, il s’agit du logiciel de gestion de versions le plus populaire qui est utilisé par plus de douze millions de personnes",
            source:"https://fr.wikipedia.org/wiki/Git"
          },
          {
            name: "Agile/SCRUM",
            rank: 4,
            avatar: "https://blog.myagilepartner.fr/wp-content/uploads/2017/07/scrum-agilite%CC%81-e1467743405662-1.png",
            text:"Scrum est un schéma d’organisation de développement de produits complexes. Il est défini par ses créateurs comme un « cadre de travail holistique itératif qui se concentre sur les buts communs en livrant de manière productive et créative des produits de la plus grande valeur possible ». Scrum est considéré comme un groupe de pratiques répondant pour la plupart aux préconisations du Manifeste Agile. L'infrastructure de développement s'appuie sur le découpage d'un projet en boîtes de temps, nommées « sprints ». Les sprints peuvent durer entre quelques heures et un mois (avec un sprint médian à deux semaines). Chaque sprint commence par une estimation suivie d'une planification opérationnelle. Le sprint se termine par une démonstration de ce qui a été achevé. Avant de démarrer un nouveau sprint, l'équipe réalise une rétrospective. Cette technique analyse le déroulement du sprint achevé, afin d'améliorer ses pratiques. Le flux de travail de l'équipe de développement est facilité par son auto-organisation, il n'y aura donc pas de gestionnaire de projet.",
            source:"https://fr.wikipedia.org/wiki/Scrum_(d%C3%A9veloppement)"
          },
        ]
      },
      {
        title:"Environnement",
        skills:[
          {
            name: "Linux",
            rank: 3,
            avatar: "https://cdn3.iconfinder.com/data/icons/logos-brands-3/24/logo_brand_brands_logos_linux-512.png",
            text:"Linux est, au sens restreint, le noyau de système d'exploitation Linux, et au sens large, tout système d'exploitation fondé sur le noyau Linux. Cet article couvre le sens large. À l'origine, le noyau Linux a été développé pour les ordinateurs personnels compatibles PC, et devait être accompagné des logiciels GNU pour constituer un système d'exploitation. Les partisans du projet GNU promeuvent depuis le nom combiné GNU/Linux. Depuis les années 2000, le noyau Linux est utilisé sur du matériel informatique allant des téléphones portables aux super-ordinateurs, et n'est pas toujours accompagné de logiciels GNU. C'est notamment le cas d'Android, qui équipe plus de 80 % des smartphones.",
            source:"https://fr.wikipedia.org/wiki/Linux"
          },
          {
            name: "Docker",
            rank: 3,
            avatar: "https://cdn1.iconfinder.com/data/icons/social-media-2106/24/social_media_social_media_logo_docker-512.png",
            text:"Docker est un logiciel libre permettant facilement de lancer des applications dans des conteneurs logiciels. Selon la firme de recherche sur l'industrie 451 Research, « Docker est un outil qui peut empaqueter une application et ses dépendances dans un conteneur isolé, qui pourra être exécuté sur n'importe quel serveur ». Il ne s'agit pas de virtualisation, mais de conteneurisation, une forme plus légère qui s'appuie sur certaines parties de la machine hôte pour son fonctionnement. Cette approche permet d'accroître la flexibilité et la portabilité d’exécution d'une application, laquelle va pouvoir tourner de façon fiable et prédictible sur une grande variété de machines hôtes, que ce soit sur la machine locale, un cloud privé ou public, une machine nue, etc",
            source:"https://fr.wikipedia.org/wiki/Docker_(logiciel)",
          },
          {
            name: "Node",
            rank: 3,
            avatar: "https://i0.wp.com/blog.js-republic.com/wp-content/uploads/2016/07/nodejs.png?fit=500%2C500",
            text:"Node.js est une plateforme logicielle libre et événementielle en JavaScript orientée vers les applications réseau qui doivent pouvoir monter en charge. Elle utilise la machine virtuelle V8 et implémente sous licence MIT les spécifications CommonJS. Parmi les modules natifs de Node.js, on retrouve http qui permet le développement de serveur HTTP. Il est donc possible de se passer de serveurs web tels que Nginx ou Apache lors du déploiement de sites et d'applications web développés avec Node.js. Concrètement, Node.js est un environnement bas niveau permettant l’exécution de JavaScript côté serveur.",
            source:"https://fr.wikipedia.org/wiki/Node.js",
          },
        ]
      }
    ]
  }),

  methods:{
    openSkill(skill){
      this.description.title = skill.name;
      this.description.text = skill.text;
      this.description.img = skill.avatar;
      this.description.source = skill.source;
      this.dialog = true;
    }
  }
};
</script>

<style scoped>

h2{
  color: white;
}
.card-skill {
  border-radius: 10px !important;
  color: rgb(0, 0, 0) !important;
  max-width: 344px;
  margin: 20px;
  padding: 0px 10px 0px 10px;
}
.skill{
  display: flex;
  flex-direction: row;
  flex-flow: row wrap; 
  margin: 20px;
  background-color: rgba(207, 43, 43, 0)
}
.name{
  margin: 15px 10px 10px 10px;
}
.avatar{
  margin-right:20px;
}
.block-content{
  max-width: 900px;
}
.block-card{
  display: flex;
  flex-flow: row wrap;
}
.div-text{
  height: 30px;
}
.card-text{
  color: rgb(180, 180, 180);
  white-space : nowrap;
  overflow : hidden;
  text-overflow :    ellipsis;
  max-width: inherit;
}
.block-img{
  margin-left: 50px;
  margin-right: 50px;
}
.title-card{
    color: rgb(79, 79, 172);
    font-weight: bold;
}
</style>