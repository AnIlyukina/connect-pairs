<template>
  <div class= 'board'>
    <BoardItem v-for="(cell, index) in cells" :key="cell + '-' + index" :icon="cell"/>
  </div>
</template>

<script>

import BoardItem from './BoardItem.vue'
export default {
  name:'Board',
  components:{
    BoardItem
  },
  data(){
    return{
      cells: [1,0,0,2,3,0,1,0,2,0,3,0,0,0,0,0]
    }
  }
}
</script>

<style>

.board{
  width: 200px;
  height: 200px;
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;
}

</style>