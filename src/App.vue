<template>
  <div>
    <choix_difficult_pendu/>
    <pendu :mot = "info_pendu"/>

  </div>
</template>

<script>
import pendu from "./components/pendu";
import choix_difficult_pendu from "@/components/choix_difficulté_pendu";

export default {
  name: 'App',
  components: {
    choix_difficult_pendu,
    pendu,
  },
  data: function () {
    return{
      info_pendu:{
        mot : "lemot",
        diff : 7, //7 facile 6 moyen 5 dificile
      }
    }
  },
  methods: {
  },
}
</script>

<style>
</style>
