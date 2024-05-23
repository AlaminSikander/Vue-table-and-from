<template>
  <div>
    <pre>
      {{ JSON.stringify(fromValue, null, 2) }}
    </pre>
  </div>
  <form action="" @submit="SubmitForm">
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
    <div>
      <label for="job-locaqtion">Job Locaqtion</label>
      <select id="job-locaqtion" multiple v-model="fromValue.jobLocaqtion">
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="bangladesh">Bangladesh</option>
      </select>   
    </div>

    <div>
      <input type="checkbox" id="remortlocation" v-model="fromValue.remortlocation" true-value="yes" false-value="no">
      <label for="remoteLocation">Remote Location</label>
    </div>

    <div>
      <label for="">Skill Set</label>
      <input type="checkbox" id="html" value="html" v-model="fromValue.skillSet"/>
      <label for="html">HTML</label>
      <input type="checkbox" id="css" value="css" v-model="fromValue.skillSet"/>
      <label for="css">CSS</label>
      <input type="checkbox" id="js" value="js" v-model="fromValue.skillSet"/>
      <label for="js">JS</label>
    </div>

    <div> 
      <label>Years of Experience</label> 
      <input type="radio" id="0-2" value="0-2" v-model="fromValue.yearsOfExperience"/> 
      <label for="0-2">0-2</label> 

      <input type="radio" id="3-5" value="3-5" v-model="fromValue.yearsOfExperience"/>
      <label for="3-5">3-5</label>

      <input type="radio" id="6-10" value="6-10" v-model="fromValue.yearsOfExperience"/>
      <label for="6-10">6-10</label> 
    </div>

    <div>
      <button>Submit</button>
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
        country: '',
        jobLocaqtion: [],
        remoteLocation: "no",
        skillSet: [],
        yearsOfExperience: ''
      }
      
    }
  },
  methods: {
    SubmitForm(event){
      event.preventDefault();
      console.log('From Values', this.fromValue);
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