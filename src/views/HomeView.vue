<template>
  <main>
    <GameInfoComponent v-if="levelSelected && rivalSelected" :level="levelSelected" :rival="rivalSelected"/>
    <RivalsComponent @selectedRival="selectedRival" :rivals="rivals"/>
    <LevelsComponent @selectedLevel="selectedLevel" :rival="rivalSelected"/>
    
  </main>
</template>




<script>
import RivalsComponent from '../components/RivalsComponent.vue'
import LevelsComponent from '../components/LevelsComponent.vue'
import GameInfoComponent from '../components/GameInfoComponent.vue'

export default {
  components: { RivalsComponent, LevelsComponent, GameInfoComponent},
  data(){
    return{
      rivals: [
        {
          img: "avatar-one.png",
          name: "William Brown"
        },
        {
          img: "avatar-two.png",
          name: "John Anderson"
        },
        {
          img: "avatar-three.png",
          name: "Matthew Taylor"
        }
      ],
      levelSelected: null,
      rivalSelected: null
    }
  },
  methods: {
    selectedRival(rival){
      this.rivalSelected = rival;
    },
    selectedLevel(level){
      this.levelSelected = level;
    }
  }
}
</script>


<style lang="scss" scoped>
.test{
  max-height: 150px;
  color: white;
}
</style>