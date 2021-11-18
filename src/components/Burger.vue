<template>

  <div  id="burger3"  >

    <h4>{{ burger.name }} {{ burger.kCal }}</h4>
    <img v-bind:src="burger.img" alt="Span2" title="Hamburgare" >

    <ul>
      <li class="special">Gluten</li>
      <li>Hot</li>
      <li>Meat</li>
    </ul>
  </div>

  <div>


  </div>

</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#burger3  {
  width:20px
}
</style>
