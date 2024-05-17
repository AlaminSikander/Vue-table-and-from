<template>
  <h2 v-bind:id="headingId">Heading</h2>
  <button v-bind:disabled="isDisabled">Bind</button>
  <h2 class="underline">Underlined text</h2>
  <h2 class="underline" v-bind:class="status">Status</h2>
  <h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2>
  <h2 v-bind:class="isSoldout ? 'sold-out': 'new'">Soldout? movie</h2>
  <h2 v-bind:class="['new', 'promoted']">Newly promoted movie</h2>
  <h2 v-bind:class="[isPromoted && 'promoted', isSoldout? 'sold-out' : 'new']"> Array conditional movie</h2>
  <h2 v-bind:class="{
  promoted: isPromoted,
  new: !isSoldout,
  'sold-out': isSoldout
  }">Object conditional movie</h2>

  <h2 v-bind:style="{
    color: highLightColor,
    fontSize: headerSize +'px'
  }">Inline Style</h2>

  <h2 v-bind:style="headerStyleObject">Style Object</h2>
</template>

<script>
export default {
  name : "App",
  data(){
    return {
      headingId: 'heading',
      isDisabled: false,
      isPromoted: true,
      isSoldout: true,
      status: 'success',
      highLightColor: 'orange',
      headerSize: 50,
      headerStyleObject: {
        color: 'orange',
        fontSize: '50px'
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

.underline {
text-decoration: underline;
}

.promoted {
font-style: italic;
}

.new {
color: green;
}

.sold-out {
color: rgb(255, 0, 0);
}

</style>