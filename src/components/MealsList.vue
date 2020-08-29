<template>
  <div class="meal-list">
      <h2><span style="float:left">Gerichte</span><span style="float:right">{{ selectionCount }}/{{ data.length }}</span></h2>
      <div id="line"></div>
        <ul><li v-for="item in data" v-bind:key="item.id" v-bind:class="[{ 'active': item.check }]" >
            <input type="checkbox" v-bind:name="item.name" v-bind:id="item.name" v-bind:value="item.name" v-model="item.check" v-on:click="selectionCounter(item); updateList(item.ingredients,item.id)">
            <label v-bind:for="item.name">{{item.icon}} {{item.name}}</label> 
            </li>
        </ul>
  </div>
</template>

<script>

export default {
  name: 'MealsList',
  props: {
    data:  {
      type: Array
    }
  },
data: function() {
    return {
      selectionCount: 0
    }
  },
  methods: {
    selectionCounter: function(item) {
      // let data = '>' + item.name + ',' + item.check+'/';
      // console.log({ data});
      if (!item.check) {
        return this.selectionCount += 1;
      } else {
        return this.selectionCount -= 1;
      }
    },
    updateList: function(content, id){
      //console.log({content})
      this.$emit('updateList', content, id);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.meal-list {
    /* border: 1px solid red; */
    width: 40%;
    margin-left: 6%;
    height:  100%;
    text-align: left;
}

h2 {
    font-size: 16px;
    font-weight: 500;
    font-style: normal;
    width: auto;
    height: 20px;
    color: #383838;
    padding: 8px 8px 8px 0;
    margin: 0;
}

h2 span:last-child {
  font-weight: 400;
}

div#line {
    display: block;
    height: 2px;
    width: 4%;
    background-color: #FF5858;
    margin-bottom: 24px;
}

ul {
    margin:0;
    padding:0;
    height: auto;
}

li {
    height: auto;
    width: auto;
    padding: 0;
    list-style: none;
    background-color: lightgray;
    margin: 8px 0;
    background: #FFFFFF;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.24);
    border-radius: 8px;
}

li input {
  display: none
}

li.active {
  background-color:#FF5858;
  color: #ffffff;
}

li label {
  font-size: 16px;
  line-height: 24px;
  height: 24px;
  padding: 8px 8px 8px 12px;
  display: inline-block;
  width: 100%;
}

li label:hover {
    cursor: pointer;
}

</style>
