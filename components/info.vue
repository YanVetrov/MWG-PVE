<template>
    <div class="info">
        <div class="info_container">
        <div class="info_line" v-for="line in lines" :key='line.key'>
          <div class="info_key">{{line.key}}</div>
          <div class="info_value">{{currentTank[line.key]}}</div>
        </div>
        
        </div>
        <div class="repair" @click="$emit('repair')">
          <div class="repair_price">{{currentTank.repair}}</div>
          </div>
      </div>
</template>
<script>
export default {
    props:['lines','currentTank']
}
</script>