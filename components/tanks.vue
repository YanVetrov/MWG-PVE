<template>
    <div class="tanks_container">
        <img class="tank micro" @click="$emit('tap',-2)" v-if="currentIndex>=2" :src="require('~/assets/'+tanks[currentIndex-2].image)" :style="{opacity:tanks[currentIndex-2].locked?0.5:1}"/>
        <div style="height:109px" v-else />
        <img class="tank mini" @click="$emit('tap',-1)" v-if="currentIndex>=1" :src="require('~/assets/'+tanks[currentIndex-1].image)" :style="{opacity:tanks[currentIndex-1].locked?0.5:1}"/>
        <div style="height:70px" v-else />
        <img class="tank" :style="{opacity:currentTank.locked?0.5:1}" :src="require('~/assets/'+currentTank.image)" />
        <img class="tank mini" @click="$emit('tap',1)" v-if="currentIndex+1<tanks.length" :src="require('~/assets/'+tanks[currentIndex+1].image)" :style="{opacity:tanks[currentIndex+1].locked?0.5:1}"/>
        <div style="height:109px" v-else />
        <img class="tank micro" @click="$emit('tap',2)" v-if="currentIndex+2<tanks.length" :src="require('~/assets/'+tanks[currentIndex+2].image)" :style="{opacity:tanks[currentIndex+2].locked?0.5:1}"/>
        <div style="height:49px" v-else />
      </div>
</template>
<script>
export default {
    props:['currentTank','tanks','currentIndex']
}
</script>