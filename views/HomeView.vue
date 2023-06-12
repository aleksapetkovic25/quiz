<template>
  <main>
    <RivalsComponent @selectedRival="selectedRival" :rivals="rivals"/>
    <LevelsComponent @selectedLevel="selectedLevel" :rival="rivalSelected"/>
    <QuizGameComponent v-if="levelSelected && rivalSelected" :level="levelSelected" :rival="rivalSelected"/>
  </main>
</template>




<script>
import RivalsComponent from '../components/RivalsComponent.vue'
import LevelsComponent from '../components/LevelsComponent.vue'
import QuizGameComponent from '../components/QuizGameComponent.vue'

export default {
  components: { RivalsComponent, LevelsComponent, QuizGameComponent},
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
main{
  display: flex;
  align-items: center; /* vertically center */
  height: 100vh;
}
</style>