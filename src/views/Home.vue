<template>

  <body >
  <header id="header">
    <div >
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
      <p>Please fill in the boxes below</p>
      <p>
        <input v-model="wholename" placeholder="Full name" required="required" />
        {{ wholename}}
      </p>
      <p>
        <input v-model="email" placeholder="E-mail adress" required="required" />
        {{ email }}
      </p>
<!--      <p>-->
<!--        <input v-model="adress" placeholder="Street Adress" required="required" />-->
<!--        {{adress}}-->
<!--      </p>-->
<!--      <p>-->
<!--        <input v-model="nummer" placeholder="House Number" required="required" />-->
<!--        {{ nummer }}-->
<!--      </p>-->
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
      <input type="radio" id="one" value="Man" v-model="picked" />
      <label for="one">Man</label>
      <br />
      <input type="radio" id="two" value="Women" v-model="picked" />
      <label for="two">Women</label>
      <br />
      <input type="radio" id="three" value="Do not wish to provide" v-model="picked" />
      <label for="three">Do not wish to provide</label>
      <br />
      </div>

    </section>
    <h4>Delivery information:</h4>
    <p>Click on you current delivery location</p>
    <div class="wrapper1">
      <div id="map" v-on:click="setLocation" >
        <div v-bind:style="{ left: this.location.x + 'px',
                      top: this.location.y + 'px' }">
          T
        </div>

      </div>
    </div>
    <button v-on:click="addOrder" type="submit" id="buttonid">
            Slutför beställning
    </button>
  </main>


  </body>
  <hr>
  <footer>&copy; Burgers inc.</footer>



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
      burgers: newhamburgers,
      orderedBurger: {},
      location: {
        x: 0,
        y: 0
      },
      wholename: '',
      email: '',
      picked: 'Women',
      betalsätt: 'Swish',

    }
  },


  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    addOrder: function() {
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
            details: { x: this.location.x,
              y: this.location.y,

            },
        personalInfo: {wm:this.wholename,
                  em:this.email,

        gend: this.picked,
        pay: this.betalsätt},

            orderItems: this.orderedBurger
          }
      );
      console.log(this.wholename, this.email, this.betalsätt, this.picked, this.orderedBurger);
    },

    setLocation: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };

      this.location.x = event.clientX + 20 - offset.x ,
          this.location.y = event.clientY - 5 - offset.y


    },
    addToOrder: function (event) {
      this.orderedBurger[event.name]=event.amount
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
  padding-bottom: 10px;
  grid-template-columns: auto auto auto;
  background-color: gray;
  margin: 5px 5px 5px 20px;
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

  overflow:hidden;
}
#header div {
  height: 200px
}
#menybild {
  opacity: 0.5;
  width: 100%;
  height: auto;
  overflow: hidden;
}

#rubrik {
  position: absolute;
  padding-left:400px;
  padding-top: 35px;

}
  #map {
    width:1920px;
    height: 1078px;

    background: url(/img/polacks.jpg);


  }
  .wrapper1 {
    height: 300px;
    width: 300px;
    padding-left:30px;
    overflow: scroll;
    position: relative;
  }
#map div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}
</style>
