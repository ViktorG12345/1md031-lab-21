<template>

  <div  id="burger3"  >

    <h4>{{ burger.name }} {{ burger.kCal }}</h4>
    <img v-bind:src="burger.img" alt="Span2" title="Hamburgare" style="width: 200px;">
    {{ amountOrdered }}

    <ul>
      <li class="special">Gluten</li>
      <li>Hot</li>
      <li>Meat</li>
    </ul>
    <button v-on:click="IncreaseNumber" type="submit" id="Increase">
      Increase
    </button>
    <button v-on:click="DecreaseNumber" type="submit" id="Decrease">
      Decrease
    </button>
  </div>

</template>
<script>

export default {
  name: 'Burger',
  props: {
    burger: Object
  },

  data: function () {
    return {
      amountOrdered: 0,
    }
  },
  addBurger: function () {
    this.amountOrdered += 1;
    this.$emit('orderedBurger', { name:   this.burger.name,
          amount: this.amountOrdered
        }
    );
  },
  methods: {
    IncreaseNumber: function () {
    this.amountOrdered += 1;
    this.$emit('orderedBurger', { name:   this.burger.name,
        amount: this.amountOrdered
      }
  );
},
    DecreaseNumber:function () {
    this.amountOrdered -= 1;
    this.$emit('orderedBurger', { name:   this.burger.name,
        amount: this.amountOrdered
      }
  );
},

  }
}

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
