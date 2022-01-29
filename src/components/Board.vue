<template>
  <div v-if="gameStatus === 1">Вы выиграли , хорош играть !!! Игра начинается с начала</div>
  <div>Уровень: {{level}}</div>
  <div 
    class= 'board'
    :style="{width: 50 * size + 'px', height: 50 * size + 'px'}">
    <BoardItem 
      v-for="(cell, index) in cells" 
      :key="cell + '-' + index" 
      :icon-id="cell"
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
    let level = ref(1)
    let maxVelel = 3
    let gameStatus = ref(0) // 0 -play 1 - win

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
        goToNextLevel()
      }
    }

    const goToNextLevel = () =>{
      level.value +=1
      gameStatus.value = 0

      if(level.value > maxVelel ){
        level.value = 1
        gameStatus.value = 1
      }

      start(level.value)
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
        size.value = 4

      }

      if(level === 2){
        cells.value = [1,0,0,2,3,0,1,0,2,0,3,0,0,0,0,0]
        size.value = 4
      }

      if(level === 3){
        cells.value = [0,0,0,0,0,3,4,0,1,0,4,0,3,0,2,0,0,1,0,0,0,0,2,0,0]
        size.value = 5
      }

       path.value =[]
       closedPath.value =[]
    }

    start(level.value)

    const reload = () =>{
      start(level.value)
    }

    return{
      cells,
      mouseUp,
      mouseDown,
      go,
      cheakRoad,
      isRoadClosed,
      level, 
      reload,
      size,
      gameStatus
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