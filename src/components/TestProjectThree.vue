<template>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th @click="sort('name')">Name <span v-if="sortKey === 'name'">{{ sortOrders['name'] > 0 ? '↓' : '↑' }}</span></th>
          <th @click="sort('registered')">Registered <span v-if="sortKey === 'registered'">{{ sortOrders['registered'] > 0 ? '↓' : '↑' }}</span></th>
          <th @click="sort('role')">Role <span v-if="sortKey === 'role'">{{ sortOrders['role'] > 0 ? '↓' : '↑' }}</span></th>
          <th @click="sort('status')">Status <span v-if="sortKey === 'status'">{{ sortOrders['status'] > 0 ? '↓' : '↑' }}</span></th>
          <th>Action</th>
        </tr>

        <tr>
          <th><input v-model="filters.name" placeholder="Filter by name" @input="applyFilters" class="search-input"/></th>
          <th><input v-model="filters.registered" placeholder="Filter by date" @input="applyFilters" type="date" class="search-input"/></th>
          <th>
            <select v-model="filters.role" @change="applyFilters" class="search-input">
              <option value="">All</option>
              <option>Guest</option>
              <option>Member</option>
              <option>Staff</option>
              <option>Admin</option>
            </select>
          </th>
          <th>
            <select v-model="filters.status" @change="applyFilters" class="search-input">
              <option value="">All</option>
              <option>Pending</option>
              <option>Active</option>
              <option>Banned</option>
            </select></th>
          <th></th>
        </tr>

      </thead>
      <tbody>
        <tr v-for="user in paginatedUsers" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.registered }}</td>
          <td>{{ user.role }}</td>
          <td><span :class="statusClass(user.status)">{{ user.status }}</span></td>
          <td><button>Show</button></td>
        </tr>
      </tbody>
    </table>
    <div class="pagination">
  <span v-if="currentPage > 1" @click="currentPage--">«</span>
  <span v-for="n in totalPages" :key="n" @click="currentPage = n" :class="{ active: n === currentPage }">{{ n }}</span>
  <span v-if="currentPage < totalPages" @click="currentPage++">»</span>
</div>
    <div class="items-per-page">
      <label>Items per page:</label>
      <select v-model="itemsPerPage" @change="currentPage = 1">
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="15">15</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        { id: 1, name: 'John Doe', registered: '2018/01/01', role: 'Guest', status: 'Pending' },
        { id: 2, name: 'Samppa Nori', registered: '2018/01/01', role: 'Member', status: 'Active' },
        { id: 3, name: 'Estavan Lykos', registered: '2018/02/01', role: 'Staff', status: 'Banned' },
        { id: 4, name: 'John Doe', registered: '2018/01/01', role: 'Guest', status: 'Pending' },
        { id: 5, name: 'Samppa Nori', registered: '2018/01/01', role: 'Member', status: 'Active' },
        { id: 6, name: 'Estavan Lykos', registered: '2018/02/01', role: 'Staff', status: 'Banned' },
        { id: 7, name: 'John Doe', registered: '2018/01/01', role: 'Guest', status: 'Pending' },
        { id: 8, name: 'Samppa Nori', registered: '2018/01/01', role: 'Member', status: 'Active' },
        { id: 9, name: 'Estavan Lykos', registered: '2018/02/01', role: 'Staff', status: 'Banned' },
        { id: 10, name: 'John Doe', registered: '2018/01/01', role: 'Guest', status: 'Pending' },
        { id: 11, name: 'Samppa Nori', registered: '2018/01/01', role: 'Member', status: 'Active' },
        { id: 12, name: 'Estavan Lykos', registered: '2018/02/01', role: 'Staff', status: 'Banned' },
        // Additional users
      ],
      filters: {
        name: '',
        registered: '',
        role: '', 
        status: ''
      },
      sortKey: '',
      sortOrders: { name: 1, registered: 1, role: 1, status: 1 },
      currentPage: 1,
      itemsPerPage: 10
    };
  },
  computed: {
    filteredUsers() {
      return this.users.filter(user => {
        return (!this.filters.name || user.name.toLowerCase().includes(this.filters.name.toLowerCase()))
            && (!this.filters.registered || user.registered === this.filters.registered)
            && (!this.filters.role || user.role === this.filters.role)
            && (!this.filters.status || user.status === this.filters.status);
      });
    },
    sortedUsers() {
      return [...this.filteredUsers].sort((a, b) => {
        if (!this.sortKey) return 0;
        let modifier = this.sortOrders[this.sortKey];
        if (a[this.sortKey] < b[this.sortKey]) return -1 * modifier;
        if (a[this.sortKey] > b[this.sortKey]) return 1 * modifier;
        return 0;
      });
    },
    paginatedUsers() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      return this.sortedUsers.slice(start, start + this.itemsPerPage);
    },
    totalPages() {
      return Math.ceil(this.filteredUsers.length / this.itemsPerPage);
    }
  },
  methods: {
    sort(key) {
      this.sortOrders[key] = this.sortKey === key ? this.sortOrders[key] * -1 : 1;
      this.sortKey = key;
    },
    statusClass(status) {
      return {
        'status-pending': status === 'Pending',
        'status-active': status === 'Active',
        'status-banned': status === 'Banned',
        'status-inactive': status === 'Inactive'
      };
    },
    applyFilters() {
      this.currentPage = 1; // Reset to first page when filters change
    }
  }
};
</script>

<style scoped>
.table-container {
  font-family: Arial, sans-serif;
  margin: 40px;
}

.filter-section {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  position: relative;
}

.search-input{
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.filter-section input {
  width: 100%;
  padding: 8px;
  border: 2px solid #ccc;
  border-radius: 4px;
}

.filter-icon {
  position: absolute;
  right: 10px;
  top: 12px;
  color: #888;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f4f4f4;
}

.status-pending {
  color: #E67E22; /* Orange */
}

.status-active {
  color: #2ECC71; /* Green */
}

.status-banned {
  color: #E74C3C; /* Red */
}

.status-inactive {
  color: #95A5A6; /* Grey */
}

button {
  background-color: #3498DB; /* Blue */
  color: white;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  cursor: pointer;
}

.pagination {
  display: flex;
  justify-content: center;
}

.pagination span {
  cursor: pointer;
  padding: 5px;
  user-select: none;
}

.pagination .active {
  text-decoration: underline;
}

.items-per-page {
  display: flex;
  align-items: center;
}

.items-per-page select {
  margin-left: 10px;
  padding: 5px;
}
</style>
