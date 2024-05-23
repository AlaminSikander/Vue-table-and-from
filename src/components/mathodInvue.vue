<template>
  <h2>Add Mathod - {{ add(2,5,7) }} </h2>
  <h2>Add Mathod - {{ add(2,5,4) }} </h2>
  <h2>Multiply Method - {{ multiply(baseValue) }}</h2>
  <h2>{{ name }}</h2>
  <div>
    <button v-on:click="changName">Change Name</button>
  </div>

  <h2>{{ count }}</h2>
  <div>
    <button @click="increment(2, $event)">Increment</button>
    <button @click="decrement(2)">Decrement</button>
  </div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            baseMultiplier: 5,
            baseValue: 1,
            name: 'Al Amin',
            count: 0

        }
    },
    methods: {
        add(a, b, c) {
            return a + b + c
        },
        multiply(num){
            return num * this.baseMultiplier
        },
        increment(num, event) {
            this.count += num
            console.log('Event', event)
        },
        decrement(num) {
            this.count -= num
        },
        changName(){
            this.name = 'Sajjat'
        }

    },

}
</script>

<style>
    #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;}
</style>