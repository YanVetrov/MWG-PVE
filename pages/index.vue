<template>
<div class="wrapper">
  <div class="container">
    <div class="money">
      MTL {{balance}}
    </div>
    <div class="container_content">
      <info
      :currentTank="currentTank"
      :lines="lines"
      @repair="repair(currentTank.repair)">
      </info>
      <tanks 
       :currentTank="currentTank"
       :tanks="tanks" 
       :currentIndex="currentIndex" 
       @tap="currentTank=tanks[currentIndex+$event].id"/>
        
        <buttons 
        @raid="currentTank.type==='battle'&&!currentTank.locked?lock():0"
        @mine="currentTank.type==='miner'&&!currentTank.locked?lock():0"
        :currentTank="currentTank"
        :lockedTime="lockedTime"
        >
        </buttons>
    </div>
  </div>
  </div>
</template>

<script>
import {mapGetters,mapMutations,mapActions} from 'vuex'
import info from '~/components/info'
import buttons from '~/components/buttons'
import tanks from '~/components/tanks'
export default {
  components:{
    info,buttons,tanks
  },
  data(){
    return {
      tmp:'',
    }
  },
  methods:{
    ...mapMutations('global',['repair','unlock']),
    ...mapActions('global',['lock'])
  },
  computed:{
    ...mapGetters('global',['tanks','lines','balance']),
    currentTank:{
      get(){return this.$store.getters['global/currentTank']},
      set(id){this.$store.commit('global/currentTank',id)}
    },
    currentIndex(){
     return this.tanks.findIndex(el=>el.id===this.currentTank.id)
    },
    lockedTime(){
      if(this.currentTank.locked&&this.currentTank.unlockedTime>Date.now()){
      this.tmp;
      let minutes = Math.floor((this.currentTank.unlockedTime-Date.now()) / 60000);
      let seconds = (((this.currentTank.unlockedTime-Date.now()) % 60000) / 1000).toFixed(0);
      this.tmp=seconds;
      return minutes + ":" + (seconds < 10 ? '0' : '') + seconds;
      }
      else return null;
    }
  },
  mounted(){
    setInterval(()=>this.tmp=Date.now(),100)
  }
}
</script>

<style>
@import url('~/assets/style.css');
</style>
