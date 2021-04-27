<template>
    <div class="buttons">
        <div 
        @click="$emit('raid')"
        :style="{opacity:currentTank.type==='battle'&&!currentTank.locked?1:0.5}" 
        class="button raid">
          <img src="~/assets/raid.png" />
        </div>
        <span v-if="lockedTime">{{lockedTime}}</span>
        <div 
        @click="$emit('mine')"
        :style="{opacity:currentTank.type==='miner'&&!currentTank.locked?1:0.5}" 
        class="button mine">
          <img src="~/assets/mine.png" />
        </div>
      </div>
</template>
<script>
export default {
    props:['currentTank','lockedTime']
}
</script>