<template>
  <div class="container">
    <!-- Form -->
    <form @submit.prevent="addData">
      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="formData.name" required>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="formData.email" required>
      </div>
      <div>
        <label for="dropdown">Dropdown:</label>
        <select id="dropdown" v-model="formData.dropdown">
          <option value="Option 1">Option 1</option>
          <option value="Option 2">Option 2</option>
          <option value="Option 3">Option 3</option>
        </select>
      </div>
      <div>
        <label>Checklist:</label>
        <div v-for="(item, index) in checklistOptions" :key="index">
          <input type="checkbox" v-model="formData.checklist" :value="item">{{ item }}
        </div>
      </div>
      <button type="submit">Submit</button>
      <button type="button" @click="resetForm">Reset</button>
    </form>

    <!-- Table -->
    <div>
      <input type="text" v-model="searchText" placeholder="Search">
      <table>
        <thead>
          <tr>
            <th @click="sortBy('name')">Name</th>
            <th @click="sortBy('email')">Email</th>
            <th @click="sortBy('dropdown')">Dropdown</th>
            <th>Checklist</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(data, index) in sortedData" :key="index">
            <td>{{ data.name }}</td>
            <td>{{ data.email }}</td>
            <td>{{ data.dropdown }}</td>
            <td>{{ data.checklist.join(', ') }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        dropdown: '',
        checklist: []
      },
      dataList: [],
      searchText: '',
      sortKey: '',
      sortDirection: 'asc'
    };
  },
  computed: {
    checklistOptions() {
      // Define your checklist options here
      return ['Option 1', 'Option 2', 'Option 3'];
    },
    sortedData() {
      const sorted = this.dataList.slice().sort((a, b) => {
        if (this.sortDirection === 'asc') {
          return a[this.sortKey] > b[this.sortKey] ? 1 : -1;
        } else {
          return a[this.sortKey] < b[this.sortKey] ? 1 : -1;
        }
      });

      if (this.searchText) {
        return sorted.filter(data =>
          data.name.toLowerCase().includes(this.searchText.toLowerCase()) ||
          data.email.toLowerCase().includes(this.searchText.toLowerCase()) ||
          data.dropdown.toLowerCase().includes(this.searchText.toLowerCase()) ||
          data.checklist.join(', ').toLowerCase().includes(this.searchText.toLowerCase())
        );
      } else {
        return sorted;
      }
    }
  },
  methods: {
    addData() {
      this.dataList.push({ ...this.formData });
      this.resetForm();
    },
    resetForm() {
      this.formData = {
        name: '',
        email: '',
        dropdown: '',
        checklist: []
      };
    },
    sortBy(key) {
      if (this.sortKey === key) {
        this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
      } else {
        this.sortKey = key;
        this.sortDirection = 'asc';
      }
    }
  }
};
</script>

<style scoped>
/* CSS styles */
.container {
  max-width: 800px;
  margin: 20px auto;
}
form {
  margin-bottom: 20px;
}
input[type="text"], input[type="email"], select {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}
button {
  padding: 10px 20px;
  cursor: pointer;
  background-color: #007bff;
  border: none;
  color: #fff;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  padding: 8px;
  border-bottom: 1px solid #ddd;
  text-align: left;
}
th {
  cursor: pointer;
}
</style>
