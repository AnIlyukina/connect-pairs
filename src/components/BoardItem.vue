<template>
  <div :class="'board__item' 
    + (selected ? ' active' : '' ) 
    + (closed ? ' closed' : '') 
    ">
    <li v-if="icon" :class="'icon icon-' + icon "> </li>
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
  position: relative;
  width: 48px;
  height: 48px;
  border: 1px solid #da89ffbe;
}

.active{
  background-color: #b516ffc0;
}

.closed{
 background-color: #f18dec59;
}

.icon{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  list-style-type: none;
}

.icon-1{
  background-image: url('../assets/icon__angry.png');
  background-size: 50px 50px;
  background-position: 0 0;
}

.icon-2{
  background-image: url('../assets/icon__birthday.png');
  background-size: 50px 50px;
  background-position: 50px 0;
}

.icon-3{
  background-image: url('../assets/icon__eat.png');
  background-size: 50px 50px;
  background-position: 100px 0;
}

</style>