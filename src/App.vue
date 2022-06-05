<template>
  <div>
    <main-screen 
      v-if="statusMatch==='default'" 
      @onStart='onHandleBeforeStart($event)'/>

    <interact-screen-vue  
        v-if="statusMatch==='match'"
        :cardsContext="settings.cardsContext"
        @onFinish="onGetResult"
    />
    <result-screen 
      v-if="statusMatch==='result'"
      :timer="timer"
      @onStartAgain="statusMatch='default'"
      />
      <coppy-right/>
  </div>
</template>

<script>

import {shuffled} from "./utils/array.js"
import  MainScreen from './components/MainScreen.vue'
import InteractScreenVue  from './components/InteractScreen.vue'
import ResultScreen from './components/ResultScreen.vue'
import CoppyRight from './components/CoppyRight.vue'

export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreenVue,
    ResultScreen,
    CoppyRight

  },
  data() {
    return {
      settings:{
        totalOfBlock:0,
        cardsContext:[],
        startedAt:null,
      },
      statusMatch:"default", 
      timer:0,
    }
  },
  
  methods: {
    onHandleBeforeStart(config){
      console.log("running",config)
      this.settings.totalOfBlock=config.totalOfBlock;
      const firstCard= Array.from({length: this.settings.totalOfBlock/2},(_, i) => i+1);
      const secondCard=[...firstCard];
      console.log(firstCard)
      console.log(secondCard)
      const cards=[...firstCard,...secondCard]
      console.log(cards)
      this.settings.cardsContext=shuffled(shuffled(shuffled(shuffled(cards))));
      this.settings.startedAt=new Date().getTime();
      this.statusMatch='match'
    },
    onGetResult(){
      // lay gia tri thoi gian hooan thanh
      this.timer= new Date().getTime() - this.settings.startedAt;
      this.statusMatch="result";
    }
  },
}
</script>


