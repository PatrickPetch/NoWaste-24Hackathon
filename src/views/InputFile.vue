<template>
  <v-app>

    <!-- One v-container is enough -->
    <!-- Add more v-row for each line (equivalent to <div></div> / <br />) -->

    <!-- If you want two column, add v-col inside v-row -->
    <!-- 
      Eg:
        // This will give a 3 column row
        <v-row>
          <v-col>...</v-col>
          <v-col>...</v-col>
          <v-col>...</v-col>
        </v-row>
     -->

    <v-container class="white">

    <v-row>
      <v-col cols='4'>
        <v-card
          height="400"
          width="256"
          class="mx-auto-left"
        >
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

      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodName"
            label="Food name"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!--Drop down list -->

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
          
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodClearingTime"
            label="Clearing Time"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodIngredient"
            label="Allergen(s)"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      
      <v-row no-gutters>
        <v-col>
          <v-text-field
            v-model="foodDetail"
            label="Detail"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <!-- <v-file-input
        v-model="foodFile"
        label="File input"
        filled
        prepend-icon="mdi-camera"
      ></v-file-input> -->

      <v-btn color=#3adf9a text @click="addData">
      Add Data!
      </v-btn>

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
  data() {
    return {
      menuitems: [{title:"Home", link:"/"},{title:"List my food", link:"/input"}],
      items: ["North Spine","South Spine", "The ARC", "The Hive", "HSS", "ADM", "Others (Please specify)"],
      foodName: "",
      foodIngredient: "",
      foodClearingTime: "",
      foodDetail: "",
      foodLocation: "",
      foodFile: "",
    };
  },

  methods: {
    clearData(){
      localStorage.removeItem('foodArray');
    },
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
      if (!foodArray) foodArray = '[]';

      foodArray = JSON.parse(foodArray);
      foodArray.push(foodObject);

      let stringifiedFoodArray = JSON.stringify(foodArray);
      localStorage.setItem('foodArray', stringifiedFoodArray);
      
      // localStorage.getItem('keyName');
      // localStorage.setItem("foodObject", JSON.stringify(foodObject));

      alert(JSON.stringify(foodArray));
    }
  },
  
};
</script>

<style>
.menu-item, .menu-item .v-list-item__title{
  text-decoration: none;
  color: rgb(5, 2, 27);
  
}


</style>
