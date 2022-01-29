<template>
  <div :class="'board__item' + (selected ? ' active' : '' ) + (closed ? ' closed' : '') ">
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
    },
    selected:{
      type: Boolean,
      required: false,
      default: false
    },
    closed:{
      type: Boolean,
      required: false,
      default: false
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

.active{
  background-color: #16b5ff;
}

.closed{
 background-color: #16ff3559;
}

</style>