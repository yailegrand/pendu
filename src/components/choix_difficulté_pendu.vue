<template>
  <div id = "dif">
    <div>
      {{ jeu }}
    </div>

    <div id = "choix">
      difficulté :
      <select name="Difficulté" id="Difficulte" >
        <option value="">--{{tab_langue[0][langue_maternelle]}}--</option>
        <option value="1">{{tab_langue[1][langue_maternelle]}}</option>
        <option value="2">{{tab_langue[2][langue_maternelle]}}</option>
        <option value="3">{{tab_langue[3][langue_maternelle]}}</option>
      </select>
      <input type="button" value="ok"/>
    </div>

    <br/>
    <img :src =  'image'/>
    <br/>

    <div id = "texte">
      {{ regles_du_jeu }}
    </div>
  </div>

</template>

<script>


export default {
  name: "choix_difficulté_pendu",

  data: function () {
    return {
      id_jeu:"",
      jeu:"Pendu",
      regles_du_jeu:"les règles ",
      image : "https://www.checkyoursmile.fr/images/jeux/hangman/pic_0.png",
      //[ [ français anglais espagnol ],[ français anglais espagnol ] ]
      tab_langue: [
          ["Difficulté","Difficulty"],
        ["facile","easy"],
        ["moyen","medium"],
        ["difficile","hard",]
      ],
      langue_maternelle: 0,
      langue_travail: 1,
    }
  },
  methods: {
    init_component: function(){
      //"select name, description from game where id = " + this.id

    }
  },
  mounted() {
    //jeu, regles = "select name, description from game where id = " + this.id
    //this.jeu =jeu
    //this.regles_du_jeu =regles
  },

}
</script>

<style scoped>
#choix{
  color: cornsilk;
  border-width: 2px ;
  border-style:solid;
  border-color: #e57373;
  border-radius: 5px ;
  padding:10px;
  margin:10px;
  background-color: #e57373 ;
}

#dif{
  color: #000000;
  border-width: 2px ;
  border-style:solid;
  border-color: #f5f6fa;
  border-radius: 5px ;
  padding:10px;
  margin:10px;
  background-color: #d7ccc8;
}

</style>