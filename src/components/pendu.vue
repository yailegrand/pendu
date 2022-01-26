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
    <img :src =  comp_image />
    {{pendu}}
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
      <br/>
      <br/>
      <!--saisie mot -->
      proposer une solution
      <input type="text" v-model="mot_tentative" v-on:keyup.enter="proposition" maxlength=this.mot.mot.length/>
      <input type="button" @click="proposition"  value="ok"/>
     </div>


  </div>
</template>

<script>
export default {
  name: "pendu",
  props: {
    dif: {
      type: Number,
    }
  },

  data: function () {
    return {
      mot : "lemot",
      //[ [ français anglais espagnol ],[ français anglais espagnol ] ]
      tab_langue: [ ["pendu","hangman","ahorcado"],
                    ["lettres déjà utilisées :","letters already used","letras ya usadas"],
                    ["saisie lettre","",""]
                  ],
      langue_maternelle : 0,
      langue_travail : 1,
      lettres : [] ,
      lettre_courante : '' ,
      nb_essai : 7,
      essai : 0,
      pendu : 0,
      mot_en_construction:[],
      nb_lettres_valides : 0,
      mot_tentative : ""
    }
  },

  computed:{
    comp_image : function(){
      return "https://www.checkyoursmile.fr/images/jeux/hangman/pic_" + this.pendu + ".png";
    }
  },

  methods: {
    nouvelle_lettre: function(){
      if(this.lettre_courante != "") {
        let i_lettre = this.mot.indexOf(this.lettre_courante)
        console.log(i_lettre);
        if (i_lettre != -1) {
          this.mot_en_construction[i_lettre] = this.lettre_courante;
          this.nb_lettres_valides++;
          console.log(this.mot.charAt(i_lettre));
        } else {
          this.pendu++;
        }
        this.lettres.push(this.lettre_courante)
        this.essai++;
        this.lettre_courante = '';

        this.fin();
      }
    },

    fin: function(){
      //fin de partie
      if(this.pendu >= this.dif){
        console.log("fin perdu");
      }
      if( this.nb_lettres_valides == this.mot.length){
        console.log("fin gagné");
      }
    },




    proposition: function(){
      if (this.mot_tentative === this.mot){
        console.log("fin gagné");
      }
      else{
        this.pendu ++;
        console.log("nop");
      }
      this.mot_tentative = "";
    }
  },

  mounted() {
    this.mot_en_construction = this.mot.length*["_"];
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