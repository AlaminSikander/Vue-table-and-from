<template>
  <div class="form-container">
    <h1>Vue Form Example</h1>
    
    <form @submit.prevent="submitForm" class="form">
      <div class="form-group">
        <label for="name" class="form-label">Name:</label>
        <input type="text" id="name" v-model="formData.name" class="form-input" required>
      </div>
      
      <div class="form-group">
        <label for="email" class="form-label">Email:</label>
        <input type="email" id="email" v-model="formData.email" class="form-input" required>
      </div>
      
      <div class="form-group">
        <label for="gender" class="form-label">Gender:</label>
        <select id="gender" v-model="formData.gender" class="form-input" required>
          <option value="">Select Gender</option>
          <option value="male">Male</option>
          <option value="female">Female</option>
          <option value="other">Other</option>
        </select>
      </div>
      
      <div class="form-group">
        <label class="form-label">Interests:</label>
        <div class="checkbox-group">
          <label>
            <input type="checkbox" v-model="formData.interests" value="sports"> Sports
          </label>
          <label>
            <input type="checkbox" v-model="formData.interests" value="music"> Music
          </label>
          <label>
            <input type="checkbox" v-model="formData.interests" value="movies"> Movies
          </label>
        </div>
      </div>
      
      <button type="submit" class="submit-btn">Submit</button>
    </form>
    
    <p v-if="formSubmitted" class="success-message">Form submitted successfully!</p>
    

    
    <table class="data-table">
      <thead>
        <tr>
          <th >Name</th>
          <th>Email</th>
          <th>Gender</th>
          <th>Interests</th>
        </tr>
        <tr>
          <th><input type="text" id="name-search" v-model="nameSearch" class="search-input" @input="filterData"></th>
          <th><input type="text" id="email-search" v-model="emailSearch" class="search-input" @input="filterData"></th>
          <th><input type="text" id="gender-search" v-model="genderSearch" class="search-input" @input="filterData"></th>
          <th><input type="text" id="interests-search" v-model="interestsSearch" class="search-input" @input="filterData"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(data, index) in filteredData" :key="index">
          <td>{{ data.name }}</td>
          <td>{{ data.email }}</td>
          <td>{{ data.gender }}</td>
          <td>{{ data.interests.join(', ') }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        gender: '',
        interests: []
      },
      submittedData: [],
      nameSearch: '',
      emailSearch: '',
      genderSearch: '',
      interestsSearch: ''
    };
  },
  computed: {
    
    filteredData() {
      return this.submittedData.filter(data => {
        return data.name.toLowerCase().includes(this.nameSearch.toLowerCase()) &&
          data.email.toLowerCase().includes(this.emailSearch.toLowerCase()) &&
          data.gender.toLowerCase().includes(this.genderSearch.toLowerCase()) &&
          data.interests.join(', ').toLowerCase().includes(this.interestsSearch.toLowerCase());
      });
    }
  },
  methods: {
    submitForm() {
      this.submittedData.push({ ...this.formData });
      this.formSubmitted = true;
      this.resetForm();
    },
    resetForm() {
      this.formData = {
        name: '',
        email: '',
        gender: '',
        interests: []
      };
    },
    filterData() {
      // No need for manual filtering here, as it's handled by the computed property `filteredData`
    }
    
  }
};
</script>
<style scoped>
.form-container {
  max-width: 550px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

.form-label {
  font-weight: bold;
}

.form-input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.search-input{
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.checkbox-group {
  margin-top: 5px;
}

.submit-btn {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #0056b3;
}

.success-message {
  margin-top: 10px;
  color: green;
  font-weight: bold;
}
.data-table {
  margin-top: 20px;
  width: 100%;
  border-collapse: collapse;
}

.data-table th, .data-table td {
  border: 1px solid #ccc;
  padding: 8px;
}

.data-table th {
  background-color: #f2f2f2;
  text-align: left;
}
</style>
