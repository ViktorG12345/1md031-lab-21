<template>

  <body>
  <header >
    <div id="header">
      <h1 id="rubrik" >Välkommen till BurgerOnline </h1>
      <img src="https://d3aux7tjp119y2.cloudfront.net/original_images/Tak2-CMSTemplate_IrMZHla.jpg" alt="Span" title="Hamburgaremeny" id="menybild">

    </div>
  </header>
  <main>

      <div class="wrapper">
        <Burger v-for="burger in burgers"
                v-bind:burger="burger"
                v-bind:key="burger.name"
                v-on:orderedBurger="addToOrder($event)"
        />
      </div>


    <section style="clear:left" id="informatiodid" >

      <h4>Customer Information</h4>
      <p>information about adress mm..</p>
      <h4>Delivery information:</h4>
      <p>
        <input v-model="förnamn" placeholder="Firstname" required="required" />
        {{ förnamn }}
      </p>
      <p>
        <input v-model="lastname" placeholder="Lastname" required="required" />
        {{ lastname }}
      </p>
      <p>
        <input v-model="adress" placeholder="Street Adress" required="required" />
        {{adress}}
      </p>
      <p>
        <input v-model="nummer" placeholder="House Number" required="required" />
        {{ nummer }}
      </p>
      <p>
        <label>Betalning </label>
        <select v-model="betalsätt" >
          <option>Kortbetalning</option>
          <option>Swish</option>
          <option>Klarna</option>
          <option>Faktura</option>
        </select>
      </p>

      <p>Please select your Gender:</p>
      <div>
      <input type="radio" id="one" value="One" v-model="picked" />
      <label for="one">Man</label>
      <br />
      <input type="radio" id="two" value="Two" v-model="picked" />
      <label for="two">Women</label>
      <br />
      <input type="radio" id="three" value="three" v-model="picked" />
      <label for="three">do not wish to provide</label>
      <br />
      </div>

    </section>
    <button v-on:click="InformationOrder" type="submit" id="buttonid">
            Slutför beställning
    </button>
  </main>
  </body>
  <hr>
  <footer>&copy; Burgers inc.</footer>

  <div id="map" v-on:click="addOrder">
    click here
  </div>
</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'

const socket = io();
// function MenuItem (burgerName, calories, yourURL, gluteboolean, laktosboolean) {
//   this.name=burgerName;
//   this.kCal=calories;
//   this.img=yourURL;
//   this.gluten=gluteboolean;
//   this.lactose=laktosboolean;

//}
//const Burger1 = new MenuItem("FireBurger", 555, "https://assets.icanet.se/e_sharpen:80,q_auto,dpr_1.25,w_718,h_718,c_lfill/imagevaultfiles/id_217089/cf_259/smash_burger.jpg", "true", "false");
//const Burger2 = new MenuItem("SmokeBurger", 785, "https://patch.com/img/cdn20/users/61455/20210603/125539/styles/patch_image/public/smashburger-classic___03125520204.jpg", "false", "false");
//const Burger3 = new MenuItem("ChickenBurger", 455, "https://www.max.se/contentassets/23e325ee1e224f1e9ea8314c346e34c3/product_grilled-chicken-burger.png", "true", "true");
//const hamburgers= [ Burger1, Burger2, Burger3 ]

import menu from '../assets/menu.json'
const newhamburgers= [menu[0], menu[1], menu[2]]


export default {
  name: 'Home',
  components: {
    Burger
  },

  data: function () {
    return {
      burgers: newhamburgers
    }
  },



  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    },

    InformationOrder:function(){
      console.log(this.förnamn, this.lastnamn, this.adress, this.nummer, this.betalsätt, this.picked)
    },
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
    },
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';


#burgerid {
  background-color:gray; margin: 10px 5px 15px 20px;
  border: 2px dotted #ff9900;
  padding-left: 10px;
}
.wrapper{
  display: grid;
  grid-template-row: 1;
  grid-gap: 10px;
  padding-left: 10px;
  grid-template-columns: auto auto auto;
  background-color: gray;
  margin: 10px 5px 15px 20px;
  border: 2px dotted #ff9900;


}


#informatiodid {
  background-color:darkgray;
  margin: 10px 5px 20px 20px;

  border: 2px dotted #ff9900;
  padding-left: 10px;
  padding-bottom: 10px;
  font-family: "Times New Roman";

}
button:hover {

  background-color:gray;
}

#header {
  margin: 0px 5px 0px 20px;

  height: 150px;
  overflow:hidden;
}
#menybild {
  opacity: 0.5;
  width: 100%;
  height: auto;
}

#rubrik {
  position: absolute;
  padding-left:400px;
  padding-top: 35px;

}
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }
</style>
