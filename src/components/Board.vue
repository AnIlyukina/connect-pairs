<template>
  <div>Уровень: {{level}}</div>
  <div class= 'board'>
    <BoardItem 
      v-for="(cell, index) in cells" 
      :key="cell + '-' + index" 
      :icon="cell"
      :selected='cheakRoad(index)'
      :closed ='isRoadClosed(index)'
      @mousedown="mouseDown(index)"
      @mouseup="mouseUp(index)"
      @mousemove="go(index)"
      />
  </div>
  <button @click='reload()' class="reload">Сбросить уровень</button>
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

    let cells = ref([3,0,0,2,3,0,1,0,2,0,1,0,0,0,0,0])
    const path = ref([])
    const size = ref(4)
    const closedPath = ref([])
    const level = 1

    const mouseDown = (index) =>{
      path.value = []
      if(cells.value[index] && !isRoadClosed(index)){
        path.value.push(index)
      }
    }
    const mouseUp = (index) =>{

      if(index !== path.value[0] && cells.value[index] === cells.value[path.value[0]]){
        closedPath.value = closedPath.value.concat(path.value)
      } 

      path.value =[]

      cheakLevel()

    }
    const go = (index) =>{
      if(path.value.length){
        const lastIndex = path.value[path.value.length - 1];
        console.log(lastIndex)

        if (Math.abs(lastIndex - index) === 1 
          || Math.abs(lastIndex - index) === size.value 
          && !isRoadClosed(index)){
          path.value.push(index)
        }

        if(isRoadClosed(index) 
          || (cells.value[index] && cells.value[index] !== cells.value[path.value[0]])){
            path.value =[]
          }
      }

    }

    const cheakLevel = () =>{
      let completed = true;

      cells.value.forEach((cell, index) => {
        if(cell && !isRoadClosed(index)){
          completed = false 
        }
      })

      if(completed){
        alert('Вы выиграли')
      }
    }

    const cheakRoad = (index) =>{
      return path.value.findIndex(p => p === index) > -1
    }

    const isRoadClosed = (index) =>{
      return closedPath.value.findIndex(p => p === index) > -1
    }

    const start = (level) =>{
      if (level === 1){
        cells.value = [3,0,0,2,3,0,1,0,2,0,1,0,0,0,0,0]

      }

      if(level === 2){
        cells.value = [1,0,0,2,3,0,1,0,2,0,3,0,0,0,0,0]
  
      }

       size.value = 4
       path.value =[]
       closedPath.value =[]
    }

    start()

    const reload = () =>{
      start(level)
    }

    return{
      cells,
      mouseUp,
      mouseDown,
      go,
      cheakRoad,
      isRoadClosed,
      level, 
      reload
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
  margin: 20px auto;
}

.reload{
  cursor: pointer;
}

</style>