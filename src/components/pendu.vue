<template>
  <div id="pendu">
    <br/>
    <!--pendu-->
    {{tab_langue[0][langue_maternelle]}}
    <hr/>
    <div id = "let">
      <!--lettres deja utilisées-->
      {{tab_langue[1][langue_maternelle]}}
      <template v-for="item in lettres" >
        {{item}}
      </template>
    </div>

    <!-- image pendu -->
    <br/>
    <img :src =  'tab_img_pendu[pendu]'/>
    <br/>

    <div id = "saisie">
      <!--mot en cours de pendaison-->
      <template v-for="item in mot_en_construction" >
        {{item+" "}}
      </template>
      <br/>
      <br/>

      <!--saisie lettre-->
      {{tab_langue[2][langue_maternelle]}}
      <input type="text" v-model="lettre_courante" v-on:keyup.enter="nouvelle_lettre" maxlength="1"/>
      <input type="button" @click="nouvelle_lettre"  value="ok"/>
     </div>

  </div>
</template>

<script>
export default {
  name: "pendu",
  props: {
    mot: {
      type: Object,
    }
  },

  data: function () {
    return {
      //[ [ français anglais espagnol ],[ français anglais espagnol ] ]
      tab_langue: [ ["pendu","hangman","ahorcado"],
                    ["lettres déjà utilisées :","letters already used","letras ya usadas"],
                    ["saisie lettre","",""]
                  ],
      langue_maternelle : 0,
      langue_travail : 1,
      tab_img_pendu : [
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_0.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_1.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_2.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_3.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_4.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_5.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_6.png",
        "https://www.checkyoursmile.fr/images/jeux/hangman/pic_7.png"
      ],
      lettres : [] ,
      lettre_courante : '' ,
      nb_essai : 7,
      essai : 0,
      pendu : 0,
      mot_en_construction: new Array(this.mot.mot.length).fill("_"),
      nb_lettres_valides : 0,
    }
  },

  methods: {
    nouvelle_lettre: function(){
      let i_lettre = this.mot.mot.indexOf(this.lettre_courante)
      console.log(i_lettre);
      if ( i_lettre != -1) {
        this.mot_en_construction[i_lettre] = this.lettre_courante;
        this.nb_lettres_valides++;
        console.log(this.mot.mot.charAt(i_lettre));
      }else{
        this.pendu ++;
      }
      this.lettres.push(this.lettre_courante)
      this.essai ++;
      this.lettre_courante = '';

      //fin de partie
      if(this.pendu >= this.mot.diff){
        console.log("fin perdu");
      }
      if( this.nb_lettres_valides == this.mot.mot.length){
        console.log("fin gagné");
      }
    }
  },
}
</script>

<style scoped>
#saisie,#let{
  color: cornsilk;
  border-width: 2px ;
  border-style:solid;
  border-color: #e57373;
  border-radius: 5px ;
  padding:10px;
  margin:10px;
  background-color: #e57373 ;
}


#pendu{
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