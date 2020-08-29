<template>
  <div id="app" class="flex-container">
    <meals-list v-bind:data="content" @updateList="onSelection"/>
    <ingredients-list v-bind:data="ingredients"/>
  </div>
</template>

<script>
import masterData from '../src/masterData';
import MealsList from './components/MealsList';
import IngredientsList from './components/IngredientsList';

export default {
  name: 'App',
  components: {
    MealsList,
    IngredientsList
  },
  data() {
    return {
      content: masterData().meals,
      ingredients: [],
      history: []
    }
  },
  methods: {
    onSelection: function(newIngredients, id){
        //console.log({newIngredients});
        //console.log(newIngredients,id);
        //console.log('Current: '+this.history);
        if (this.history.includes(id)){
          //console.log(id + ' already added!');
          var index = this.history.indexOf(id);
          //console.log(index);
          this.history.splice(index,1);
          //console.log('Altered: '+ this.history);
        } else {
          //console.log(id +' added!');
          this.history.push(id);
        }
        
        this.generateIngredientList();
    },
    generateIngredientList: function(){
        let newIngredients = [];

        this.history.forEach(element => {
            newIngredients.push(this.content[element].ingredients);
        });
        //console.log(newIngredients);

        if (newIngredients.length > 0) {
        newIngredients = newIngredients.reduce((a, b) => {
          return a.concat(b);
        });
        }

        var count = [];
        newIngredients.forEach(e => {
          count[e] = (count[e]||0) + 1;
        });
        console.log(count);
        
        //let summedIngredients = [];
        // newIngredients.forEach(element => {
        //    //console.log(element);
        //   if (count[newIngredients.indexOf(element)] > 1){
        //     console.log(element);
        //   }
        //   //element.splice(newIngredients.indexOf(element),1);
        // });

        return this.ingredients = newIngredients.sort();
    }
  }
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Work+Sans:wght@300;400;500&display=swap');
#app {
  font-family: 'Work Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  margin-top: 4%;
  font-weight: 400;
}

.flex-container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}
</style>
