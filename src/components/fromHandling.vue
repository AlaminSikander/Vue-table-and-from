<template>
  <div>
    <pre>
      {{ JSON.stringify(fromValue, null, 2) }}
    </pre>
  </div>
  <form action="">
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" v-model="fromValue.name">
    </div>
    <div>
      <label for="profileSummary">Profile Summary</label>
      <textarea id="profileSummary" v-model="fromValue.profileSummary"/>
    </div>

    <div>
      <label for="country">Country</label>
      <select id="country" v-model="fromValue.country">
        <option value="">Select a Country</option>
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="bangladesh">Bangladesh</option>
      </select>   
    </div>
    
  </form>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      fromValue: {
        name: '',
        profileSummary: '',
        country: ''
      }
      
    }
  }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /* text-align: center; */
    color: #2c3e50;
    margin: 60px;
}

label {
  display: flex;
  margin-bottom: 5px;
  font-weight: bold;
}

input + label { 
  font-weight: bold; 
  display: inline-flex; 
  margin-right: 20px;
}
input[type='text'],
textarea,
select{
display: block;
width: 400px;
padding: 6px 12px;
font-size: 14px;
line-height: 1.42857143;
color: #555;
background-color:#fff;
background-image: none;
border: 1px solid #ccc;
border-radius: 4px;
}
</style>