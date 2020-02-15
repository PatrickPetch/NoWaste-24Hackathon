<template>
  <v-app>
  <v-container class="white">
  <v-row>
    <v-col col='4'>
      <v-card
    height="400"
    width="256"
    class="mx-auto-left"
  >
    <v-navigation-drawer permanent>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title>
            NoWaste
          </v-list-item-title>
          <v-list-item-subtitle>
            Connecting Eaters to Feeders
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in menuitems"
          :key="item.title"
          link
        >

        <a :href="item.link" class="menu-item"> 
          <v-list-item-content>
            <v-list-item-title class="mx-auto-left">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </a>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
    </v-col>

    <v-col>
    

    <v-card  v-for="foodObject in foodArray" class="mx-auto" max-width="400">
      <v-img class="white--text align-end" height="200px" src="https://www.delonghi.com/Global/recipes/multifry/pizza_fresca.jpg">
        <v-card-title>{{ foodObject["foodName"] }}</v-card-title>
      </v-img>
      <v-card-subtitle class="pb-0">{{ getLocationName(foodObject.foodLocation) }}</v-card-subtitle>

      <v-card-text class="text--primary">
        <div>Clearing Time: {{foodObject.foodClearingTime}}</div>
        <div>Allergens: {{ foodObject.foodIngredient }}</div>
        <div>Notes: {{ foodObject.foodDetail }}</div>
      </v-card-text>

      <v-card-actions>
        <v-btn color=#3adf9a text>
          Like
        </v-btn>

        <v-btn color=#ff7b7b text>
          Dislike
        </v-btn>
        <br/>
        <br/>
      </v-card-actions>
    </v-card>
    </v-col>
    </v-row>
    </v-container>

  </v-app>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    // HelloWorld
  },
  data() {
    return {
      menuitems: [{title:"Home", link:"/"},{title:"List my food", link:"/input"}],
      foodObject: {},
      foodArray: []
      
    };
  },
  methods: {
    getLocationName(foodLocation) {
      if (foodLocation === "north-spine") return "North Spine";
      if (foodLocation === "south-spine") return "South Spine";
      if (foodLocation === "arc") return "The ARC";
      if (foodLocation === "hive") return "The Hive";
    },
    loadData() {
      this.foodArray = localStorage.getItem('foodArray');
      this.foodArray = JSON.parse(this.foodArray);
    }
  },
  mounted() {
    this.loadData();
  }
};
</script>

<style lang="scss" scoped>
h2 {
  font-size: 30px;
}

.titleMenu {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 18px;
  align-content: left;
}
.food-item {
  font-family: helvetica, sans-serif;
  font-size: 18px;
  color: white;
  background-color: coral;
  padding: 16px;
}
.menu-item, .menu-item .v-list-item__title{
  text-decoration: none;
  color: rgb(5, 2, 27);
  
}

.food-pic {
  width: 250px;
}
</style>
