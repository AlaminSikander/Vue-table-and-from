<template>
  <div id="app">
    <!-- Form for data input -->
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
        <label for="option">Select Option:</label>
        <select v-model="formData.option" required>
          <option disabled value="">Please select one</option>
          <option>Option 1</option>
          <option>Option 2</option>
          <option>Option 3</option>
        </select>
      </div>
      <div>
        <label>Checklist:</label>
        <div v-for="(item, index) in checklistOptions" :key="index">
          <input type="checkbox" :id="item" :value="item" v-model="formData.checklist">
          <label :for="item">{{ item }}</label>
        </div>
      </div>
      <button type="submit">Submit</button>
    </form>

    <!-- Search Filters -->
    <div>
      <input type="text" v-model="filters.name" placeholder="Search by Name">
      <input type="text" v-model="filters.email" placeholder="Search by Email">
      <input type="text" v-model="filters.option" placeholder="Search by Option">
    </div>

    <!-- Display Table -->
    <table>
      <thead>
        <tr>
          <th @click="sort('name')">Name</th>
          <th @click="sort('email')">Email</th>
          <th @click="sort('option')">Option</th>
          <th>Checklist</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in sortedFilteredData" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.option }}</td>
          <td>{{ item.checklist.join(', ') }}</td>
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
        option: '',
        checklist: []
      },
      checklistOptions: ['Option A', 'Option B', 'Option C'],
      dataList: [],
      filters: {
        name: '',
        email: '',
        option: ''
      },
      currentSort: '',
      currentSortDir: 'asc'
    };
  },
  methods: {
    addData() {
      this.dataList.push({
        id: this.dataList.length + 1,
        ...this.formData,
        checklist: [...this.formData.checklist]
      });
      this.resetForm();
    },
    resetForm() {
      this.formData = { name: '', email: '', option: '', checklist: [] };
    },
    sort(s) {
      if (s === this.currentSort) {
        this.currentSortDir = this.currentSortDir === 'asc' ? 'desc' : 'asc';
      } else {
        this.currentSort = s;
        this.currentSortDir = 'asc';
      }
    }
  },
  computed: {
    sortedFilteredData() {
      let result = this.dataList.filter(item => {
        return item.name.toLowerCase().includes(this.filters.name.toLowerCase()) &&
               item.email.toLowerCase().includes(this.filters.email.toLowerCase()) &&
               item.option.toLowerCase().includes(this.filters.option.toLowerCase());
      });
      if (this.currentSort) {
        result.sort((a, b) => {
          let modifier = this.currentSortDir === 'asc' ? 1 : -1;
          if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
          if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
          return 0;
        });
      }
      return result;
    }
  }
}
</script>

<style scoped>
input, select, button {
  margin: 10px;
  padding: 8px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ccc;
  padding: 8px;
  cursor: pointer;
}
</style>
