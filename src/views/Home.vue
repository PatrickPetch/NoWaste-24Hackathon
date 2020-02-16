<template>
  <v-app id="background">
  
  <v-container class="dbf8e5">
  
  <!-- Showing the navigation column on the left of the screen -->
  <v-row>
    <v-col col='4'>
      <v-card
        height="400"
        width="256"
        class="mx-auto-left"
      >

      <!-- Show the main title and sub title of the navigation column -->
        <v-navigation-drawer permanent>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="title">
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

    <!-- Listing all the options for the navigation bar -->
        <v-list-item
          v-for="item in menuitems"
          :key="item.title"
          link
        >

    <!-- Linking all the items on the navigation bar to the link-->
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
    
    <!-- Shows the detail of each food by using the 'v-for' loop -->
    <v-card  v-for="foodObject in foodArray" v-bind:key="foodObject.id" class="mx-auto" max-width="400">
      
      <!-- Show the picture  of the food using the link from user input-->
      <v-img class="black--text align-end" height="200px" :src="foodObject.foodFile"></v-img>

      <!-- Show the food name and location from the user input-->
      <v-card-title class = "title" >{{ foodObject["foodName"] }}</v-card-title>
      <v-card-subtitle class="pb-0">{{foodObject.foodLocation }}</v-card-subtitle>

      <!-- Show the information of the food from the user input -->
      <v-card-text class="text--primary">
        <div>Clearing Time: {{foodObject.foodClearingTime}}</div>
        <div>Allergens: {{ foodObject.foodIngredient }}</div>
        <div>Notes: {{ foodObject.foodDetail }}</div>
      </v-card-text>

      <!-- Like and Dislike buttons -->
      <v-card-actions>
        <!-- Like button -->
        <v-btn color=#3adf9a text>
          Like
        </v-btn>
        <!-- Dislike button -->
        <v-btn color=#ff7b7b text>
          Dislike
        </v-btn>
      </v-card-actions>

    </v-card>


    </v-col>
    </v-row>
    </v-container>

  </v-app>
</template>

<script>

export default {
  name: "Home",
  components: {},
  /*information of variable for using in this home page*/
  data() {
    return {
      menuitems: [{title:"Home", link:"/"},{title:"List my food", link:"/input"}],
      foodObject: {},
      foodArray: []
      
    };
  },
  methods: {
    /* Obtain the user input data from the local storage to show the food listing*/
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
/*Decorating the menu bar on the left*/
.menu-item, .menu-item .v-list-item__title{
  text-decoration: none;
  color: rgb(5, 2, 27);
}

/*Set the background color of the home page*/
#background{
  background-color: #dbf8e5;
}
</style>
