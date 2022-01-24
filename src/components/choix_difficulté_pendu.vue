<template>
  <div id = "dif">
    difficulté :
    <select name="Difficulté" id="Difficulte" :disabled="val">
      <option value="">--Difficulté--</option>
      <option value="7">facile</option>
      <option value="6">moyen</option>
      <option value="5">difficile</option>
    </select>
    <input type="button" value="ok"/>
  </div>

</template>

<script>


export default {
  name: "choix_difficulté_pendu",

  data: function () {
    return {
      //[ [ français anglais espagnol ],[ français anglais espagnol ] ]
      tab_langue: [
        ["facile"],
        ["moyen"],
        ["difficile"]
      ],
      langue_maternelle: 0,
      langue_travail: 1,
    }
  },
}
</script>

<style scoped>
#dif{
  color: cornsilk;
  border-width: 2px ;
  border-style:solid;
  border-color: #e57373;
  border-radius: 5px ;
  padding:10px;
  margin:10px;
  background-color: #e57373 ;
}

</style>