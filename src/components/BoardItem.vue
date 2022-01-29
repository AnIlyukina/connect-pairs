<template>
  <div class="board__item">
    {{icon ? icon : ''}}
  </div>
</template>

<script>
export default {  
  name:'BoardItem',
  props:{
    icon:{
      type: Number,
      required: false,
      default: 0
    }
  }
}
</script>

<style>

.board__item{
 
  width: 48px;
  height: 48px;
  border: 1px solid #16b5ff;
}

</style>