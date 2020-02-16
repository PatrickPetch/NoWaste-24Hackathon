<template>
  <v-app id="background">

    <v-container class="dbf8e5">
    
    <!-- Shows the navigation column on the left of the screen -->
    <v-row>
      <v-col cols='4'>
        <v-card
          height="400"
          width="256"
          class="mx-auto-left"
          >

    <!-- Shows the main title and sub title of the navigation column -->
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
        <v-list-item
          v-for="item in menuitems"
          :key="item.title"
          link
        >

        <a :href="item.link" class="menu-item">
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </a>

        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
      </v-col>     
      <v-col> 

      <!-- Box for user to input the food name -->
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodName"
            label="Food name"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!-- Box for user to select the food location -->

      <v-row align="center">
        <v-col cols="15">
          <v-select
            v-model="foodLocation"
            :items="items"
            :menu-props="{ top: true, offsetY: true }"
            label="Food Location"
          ></v-select>
        </v-col>
      </v-row>
          
      <!-- Box for user to input the food clearing time -->
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodClearingTime"
            label="Clearing Time"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!-- Box for user to input allergens-->
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodIngredient"
            label="Allergen(s)"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      
      <!-- Box for user to input the food detail-->
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodDetail"
            label="Notes"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!-- Box for user to input the picture link -->
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodFile"
            label="Picture Link"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!-- Add Data Button -->
      <v-btn color=#3adf9a text @click="addData">
      Add Data!
      </v-btn>

      <!-- Clear Data Button-->
      <v-btn color=#ff7b7b text @click="clearData">
      Clear Data!
      </v-btn>
      
      </v-col>
    </v-row>

    

    </v-container>
  
  </v-app>
</template>

<script>
export default {
  /*information of variable for using in the input page*/
  data() {
    return {
      /*information of menu list on navigation column*/
      menuitems: [{title:"Home", link:"/"},{title:"List my food", link:"/input"}],

      /*lists for locations user can select*/
      items: ["North Spine","South Spine", "The ARC", "The Hive", "HSS", "ADM", "Others (Please specify)"],
      /*information of all other variables*/
      foodName: "",
      foodIngredient: "",
      foodClearingTime: "",
      foodDetail: "",
      foodLocation: "",
      foodFile: "",
    };
  },

  methods: {
    /*clearData method is used to clear all previous inputs when click on Clear Data button*/
    clearData(){
      localStorage.removeItem('foodArray');
    },
    /* add the data to foodObject to dictionary and then to array when click on Add Data button*/
    addData() {    
      let foodObject = {
        foodName: this.foodName,
        foodClearingTime: this.foodClearingTime,
        foodIngredient: this.foodIngredient,
        foodDetail: this.foodDetail,
        foodLocation: this.foodLocation,
        foodFile: this.foodFile,
      };

      let foodArray = localStorage.getItem('foodArray');
      /* If there is no foodArray, foodArray will be created*/
      if (!foodArray) foodArray = '[]';

      foodArray = JSON.parse(foodArray);
      /* add the new user input to foodArray*/
      foodArray.push(foodObject);

      let stringifiedFoodArray = JSON.stringify(foodArray);
      localStorage.setItem('foodArray', stringifiedFoodArray);

      /*Notification to user when all user input is added */
      alert('Your listing has been successfully added!');
    }
  },
  
};
</script>

<style>
/*Decorating the menu bar on the left*/
.menu-item, .menu-item .v-list-item__title{
  text-decoration: none;
  color: rgb(5, 2, 27);
}

/*Set the background color of the input page*/
#background{
  background-color: #dbf8e5;
}
</style>
