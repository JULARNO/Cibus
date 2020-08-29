<template>
  <div class="ingredients-list">
      <h2><span style="float:left;">Einkaufsliste</span>
      <input type="button" value="Kopieren" id="copy-button" @click.stop.prevent="copyList()" disabled>
      <span style="float:right;">{{ this.ingredientCount }}</span></h2>
      <div id="line"></div>
        <ul id="list">
          <li v-for="item in ingredients" v-bind:key="item.id" v-html="item">
        </li>
        </ul>
  </div>
</template>

<script>

export default {
  name: 'IngredientsList',
  props: {
    data:  {
      type: Array
    }
  },
  data() {
    return {
      ingredients: null,
      ingredientCount: 0
    }
  },
  watch: {
    data: function(){
      const copyButton = document.getElementById('copy-button');
      //console.log('watch triggered');
      this.ingredientCount = this.data.length;

      if (this.data.length === 0) {
      copyButton.disabled = true;
      } else {
        
      copyButton.disabled = false;
      }
      return this.ingredients = this.data;
    }
  },
  methods: {
    copyList: function() {
      const copyButton = document.getElementById('copy-button');
      const list = document.getElementById('list');
        var range = document.createRange();
        range.selectNode(list);
        window.getSelection().removeAllRanges(); // clear current selection
        window.getSelection().addRange(range); // to select text
        document.execCommand('copy');
        window.getSelection().removeAllRanges();// to deselect
        copyButton.value = 'Done!';

        setTimeout(function() {
          copyButton.value = 'Kopieren';
        }, 3000);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ingredients-list {
    width: 40%;
    margin-left: 8%;
    height:  100%;
    text-align: left;
    background-color: #ffffff;
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

#copy-button {
  font-size: 16px;
  padding: 0 8px 0 16px;
  border: none;
  background-color: #ffffff;
  outline: none;
  color: #FF5858;
}

#copy-button:hover {
  cursor: pointer;
}

#copy-button:disabled{
  color: lightgray;
}

#copy-button:hover:disabled {
  cursor: not-allowed;
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
    padding-left:32px;
    height: auto;
}

li {
    height: auto;
    line-height: 24px;
    width: auto;
    padding: 0;
    list-style: disc;
    margin: 4px 0;
}
</style>
