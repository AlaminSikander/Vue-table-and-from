<template>
    <h2 v-if="num === 0">Number is zero</h2>
    <h2 v-else-if="num<0">Numer is Nagative</h2>
    <h2 v-else-if="num>0">Numer is positive</h2>
    <h2 v-else>It is not a Number</h2>
    <h2 v-for="(name, index) in names" :key="name">{{index}} {{name}}</h2>
    <h2 v-for="(name, index) in fulNames" :key="name.fast">{{ index }} {{ name.fast }} {{ name.last }}</h2>
    <div v-for="actor in actors" :key="actor.name">
        <h2>{{actor.name}}</h2>
        <h3 v-for="movie in actor.movies" :key="movie">{{ movie }}</h3>
    </div>
    <h2 v-for="value in myInfo" :key="value">{{ value }}</h2>
    <h2 v-for="(value ,key) in myInfo" :key="value">{{ key }}: {{ value }}</h2>
    <template v-for="name in names" :key="name">
        <h2>{{ name }}</h2>
    <hr />
    </template>
</template>

<script>
export default {
    name: 'App',
    data(){
        return{
            num: "al",
            names: ['alamin', 'sajjat', 'nabil'],
            fulNames: [
                {
                    fast: 'alamin',
                    last: 'lol'
                },
                {
                    fast:'sajjat',
                    last: 'lol'
                },
                {
                    fast: 'nabil',
                    last: 'lol'
                }
            ],

            actors: [
                {
                    name: 'alamin',
                    movies: ['a', 'b']
                },
                {
                    name:'sajjat',
                    movies: ['c', 'd']
                },
                {
                    name: 'nabil',
                    movies: ['e', 'f']
                }
            ],
            myInfo:{
                name: 'alamin',
                age: 20,
                address: 'dhaka'
            }
        }
    }

}
</script>




<style>
#app {
font-family: Avenir, Helvetica, Arial, sans-serif; -webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
text-align: center;
color: #2c3e50;
margin-top: 60px;
}

</style>