<template>

  <div  id="burger3"  >

    <h4>{{ burger.name }} </h4>
    <img v-bind:src="burger.img" alt="Span2" title="Hamburgare" id="burgervue">


    <ul>
      <li class="special">Kalorier: {{burger.kCal}}</li>
      <span v-if="burger.lactose==true"> <li> <span id = "allergies">Contains lactose </span> </li> </span>
      <span v-if="burger.gluten==true"> <li> <span id = "allergiesgluten">Contains gluten </span> </li> </span>
    </ul>
    <button v-on:click="IncreaseNumber" type="submit" id="Increase" style="background: aliceblue">
      Increase
    </button>
    {{amountOrdered}}
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
      if(this.amountOrdered>0)
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
#burgervue {
  width: auto;
  height: 170px;
}


</style>
