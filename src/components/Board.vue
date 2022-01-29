<template>
  <div class= 'board'>
    <BoardItem 
      v-for="(cell, index) in cells" 
      :key="cell + '-' + index" 
      :icon="cell"
      :selected='cheakRoad(index)'
      :closed ='cheakClosedRoad(index)'
      @mousedown="mouseDown(index)"
      @mouseup="mouseUp(index)"
      @mousemove="go(index)"
      />
  </div>
</template>

<script>
import { ref } from 'vue'

import BoardItem from './BoardItem.vue'
export default {
  name:'Board',
  components:{
    BoardItem
  },

  setup(){

    const cells = ref([1,0,0,2,3,0,1,0,2,0,3,0,0,0,0,0])
    const path = ref([])
    const size = ref(4)
    const closedPath = ref([])

    const mouseDown = (index) =>{
      path.value = []
      if(cells.value[index]){
        path.value.push(index)
      }
    }
    const mouseUp = (index) =>{

      if(index !== path.value[0] && cells.value[index] === cells.value[path.value[0]]){
        closedPath.value = closedPath.value.concat(path.value)
      } 

      path.value =[]
    }
    const go = (index) =>{
      if(path.value.length){
        const lastIndex = path.value[path.value.length - 1];
        console.log(lastIndex)
        if (Math.abs(lastIndex - index) === 1 || Math.abs(lastIndex - index) === size.value ){
          path.value.push(index)
        }
      }

    }


    const cheakRoad = (index) =>{
      return path.value.findIndex(p => p === index) > -1
    }

    const cheakClosedRoad = (index) =>{
      return closedPath.value.findIndex(p => p === index) > -1
    }

    return{
      cells,
      mouseUp,
      mouseDown,
      go,
      cheakRoad,
      cheakClosedRoad
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