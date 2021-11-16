<template>
  <body>
  <header >
    <div id="header">
      <h1 id="rubrik" >Välkommen till BurgerOnline </h1>
      <img src="https://d3aux7tjp119y2.cloudfront.net/original_images/Tak2-CMSTemplate_IrMZHla.jpg" alt="Span" title="Hamburgaremeny" id="menybild">

    </div>
  </header>
  <main>

    <section id="burgerid" >

      <h4>Select a burger</h4>
      <p>the selection of the burger</p>
      <div class="burgerclass">
        <div style="float:left" id="burger1" >

          <h4>The fire burger</h4>
          <img src="https://assets.icanet.se/e_sharpen:80,q_auto,dpr_1.25,w_718,h_718,c_lfill/imagevaultfiles/id_217089/cf_259/smash_burger.jpg" alt="Span" title="Hamburgare" style="width:170px">
          <ul>

            <li>Vegansk</li>
            <li>God</li>
            <li class="special">Gluten</li>
          </ul>
        </div>
        <div style="float:left;" id="burger2"  >

          <h4>The smoky burger</h4>
          <img src="https://www.max.se/contentassets/23e325ee1e224f1e9ea8314c346e34c3/product_grilled-chicken-burger.png" alt="Span2" title="Hamburgare2" style="width:180px" >
          <ul>
            <li>Kyckling</li>
            <li class="special">Laktos</li>
            <li class="special">Glutenfri</li>
          </ul>
        </div>
        <div style="float:left;" id="burger3"  >

          <h4>The hot burger</h4>
          <img src="https://cdn3.vectorstock.com/i/1000x1000/03/67/spicy-hamburger-vector-10760367.jpg" alt="Span2" title="Hamburgare2" style="width:145px"  >
          <ul>
            <li class="special">Gluten</li>
            <li>Hot</li>
            <li>Meat</li>
          </ul>
        </div>
      </div>


    </section>
    <section style="clear:left" id="informatiodid" >

      <h4>Customer Information</h4>
      <p>information about adress mm..</p>
      <h4>Delivery information:</h4>
      <p>
        <label for="firstname">Full name</label><br>
        <input type="text" id="firstname" name="fn" required="required" placeholder="Full name">
      </p>
      <p>
        <label for="lastname">E-mail</label><br>
        <input type="email" id="lastname" name="ln" placeholder="E-mail adress">
      </p>
      <p>
        <label for="street">Street</label><br>
        <input type="text" id="street" name="ef" required="required" placeholder="Street adress">
      </p>
      <p>
        <label for="house">House</label><br>
        <input type="number" id="house" name="em" required="required" placeholder="House number">
      </p>
      <p>
        <label>Betalning</label>
        <select id="recipient" name="rcp" >
          <option>Kortbetalning</option>
          <option>Swish</option>
          <option selected="selected">Klarna</option>
          <option>Faktura</option>
        </select>
      </p>

      <p>Please select your Gender:</p>
      <input type="radio" id="html" name="genderbutton" value="Unidentified">
      <label for="html">man</label><br>
        <input type="radio" id="css" name="genderbutton" value="Women" checked="checked">
        <label for="css">female</label><br>
        <input type="radio" id="javascript" name="genderbutton" value="Man">
        <label for="javascript">do not wish to provide</label>

    </section>
    <button type="submit" id="buttonid">
      <img src="https://media.istockphoto.com/vectors/emoji-thumbs-up-icon-vector-id921715004" width="30px">
      Slutför beställning
    </button>
  </main>
  </body>
  <hr>
  <footer>&copy; Burgers inc.</footer>
  <div>
    Burgers
    <Burger v-for="burger in burgers"
            v-bind:burger="burger" 
            v-bind:key="burger.name"/>
  </div>
  <div id="map" v-on:click="addOrder">
    click here
  </div>
</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'

const socket = io();
function MenuItem (burgerName, calories, yourURL, glutenboolean, laktosboolean) {
  this.name=burgerName;
  this.kCal=calories;
  this.URL=yourURL;
  this.gluten=glutenboolean;
  this.laktos=laktosboolean;

}
const Burger1 = new MenuItem("FireBurger", 555, "http", "true", "false");
const Burger2 = new MenuItem("SmokeBurger", 555, "http", "true", "false");
const Burger3 = new MenuItem("ChickenBurger", 555, "http", "false", "true");
const hamburgers= [ Burger1, Burger2, Burger3 ]


console.log(hamburgers)

export default {
  name: 'Home',
  components: {
    Burger
  },

  data: function () {
    return {
      burgers: hamburgers
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
    }
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';

body {

}

#burgerid {
  background-color:gray; margin: 10px 5px 15px 20px;
  border: 2px dotted #ff9900;
  padding-left: 10px;
}
.burgerclass{
  background-color:gray;
  display:grid;
  grid-template-columns: 200px 200px;
  font-family: arial;

}
.special {
  font-weight: bold;
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
#burger1{

  grid-column: 1;
}
#burger2{

  grid-column: 2;
}
#burger3{

  grid-column: 3;
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
