<template>
  <h1>Hi</h1>
  <h2>Hello</h2>
  <hr />
  <p>The count is: {{ count }}</p>
  <hr />
  <input type="number" v-model="incrementValue" placeholder="Increment value" />
  <!-- <input type="number" :value="incrementValue" @input="incrementValue()"  placeholder="Increment value" /> -->
  <hr />
  <label>Curremt Increment Value: {{ incrementValue }}</label>
  <hr />
  <button @click="incrementCounter">Increment</button>
  <div>
    <p :ref="'abcdp'">Next value will be: {{ nextValue }}, {{ nextNextValue }}</p>
  </div>

  <label>Current Status:
    <span v-if="(count < 50)">Green</span>
    <span v-else-if="(count === 50)">Black</span>
    <span v-else>Red</span>
    <!-- <span v-show="(count < 50)">Green</span>
    <span v-show="(count === 50)">Black</span>
    <span v-show="(count>50)">Red</span> -->
  </label>
  <br />
  <br />
  <br />
  <ul>
    <!-- <li v-for="(c, idx) of colors" :key="idx" :id="idx" :name="('li_'+c+'-'+idx)" -->
    <li v-for="(c, idx) of colors" :key="idx" :name="getName(c, idx)"
      style="margin: 10px;"
      :style="{color: c, backgroundColor: backColor}"
      :title="c"
      :ref="getName(c, idx)"
      @mouseover="onLiHover(c,idx)">
       {{(++idx)}} - {{c}}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      incrementValue: 10,
      //nextValue: 5
      colors: ["Black", "Blue", "Green", "Red", "Yellow"],
      backColor: 'gray'
    }
  },
  computed: {
    nextValue() {
      return this.count + this.incrementValue;
    },
    nextNextValue() {
      return this.nextValue + this.incrementValue;
    }
  },
  methods: {
    incrementCounter() {
      this.count += this.incrementValue;
      //this.nextValue+= this.incrementValue;
    },
    inputChanged(e) {
      console.log(e);
    },
    getName(colorName, index){
      //return 'li_'+colorName + '-' +index;
      return `li_${colorName}-${index}`; // interpolation
    },
    onLiHover(colorName, index){

      this.$refs['abcdp'].style.backgroundColor = 'yellow';

      const elementName = this.getName(colorName, index);
      console.log(elementName);
      console.log(this.$refs);
      const element = this.$refs[elementName][0];
      console.log({element});
      if(element){
        element.style.backgroundColor = colorName;
      }
    }
  },
  watch: {
    count(newValue, oldValue) {
      // if(newValue > 50){
      //  this.count = 5;
      // }
      console.log({ newValue, oldValue });
    },
  }
}
</script>

<style>

</style>
