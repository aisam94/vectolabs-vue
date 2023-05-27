<script >
export default {
  data() {
    return {
      data: [
        { id: 1, asset_name: 'Printer', department: 'HR' },
        { id: 2, asset_name: 'Monitor', department: 'IT' },
        { id: 3, asset_name: 'Barcode Scanner', department: 'ACCOUNT' },
      ]
    }
  },
  methods: {
    downloadCSV() {
      const csvContent = this.convertArrayOfObjectsToCSV(this.data);// convert data to csv
      const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' }); // creates blob obj
      // create 'link' to download csv
      const link = document.createElement('a');
      if (link.download !== undefined) {
        const url = URL.createObjectURL(blob);
        link.setAttribute('href', url);
        link.setAttribute('download', 'data.csv');
        link.style.visibility = 'hidden';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
      }
    },
    convertArrayOfObjectsToCSV(data) {
      const separator = ',';
      const keys = Object.keys(data[0]);
      const csvContent =
        keys.join(separator) +
        '\n' +
        data
          .map(item => {
            return keys.map(key => {
              return item[key];
            }).join(separator);
          })
          .join('\n');
      return csvContent;
    },
  }
}
</script>

<template>
  <header>
  </header>
  <main>
    <div>
      <table>
        <thead class="table-header">
          <tr>
            <th>Asset name</th>
            <th>Department</th>
          </tr>
        </thead>
        <tbody class="table-body">
          <tr v-for="item in data" :key="item.id">
            <td>{{ item.asset_name }}</td>
            <td>{{ item.department }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="download-csv">
      <button class="btn" @click="downloadCSV">Download CSV file</button>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

table {
  border-collapse: collapse;
  margin: 1rem;
  font-size: 20px;
}

table th,
table td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}

.table-header {
  background: #2980b9;
  font-weight: 900;
  color: white;
  text-align: center;
}

.table-body {
  background: white;
  color: black;
}

.btn {
  align-items: center;
  appearance: none;
  background-image: radial-gradient(100% 100% at 100% 0, #5adaff 0, #5468ff 100%);
  border: 0;
  border-radius: 6px;
  box-shadow: rgba(45, 35, 66, .4) 0 2px 4px, rgba(45, 35, 66, .3) 0 7px 13px -3px, rgba(58, 65, 111, .5) 0 -3px 0 inset;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-flex;
  font-family: "JetBrains Mono", monospace;
  height: 48px;
  justify-content: center;
  line-height: 1;
  list-style: none;
  overflow: hidden;
  padding-left: 16px;
  padding-right: 16px;
  position: relative;
  text-align: left;
  text-decoration: none;
  transition: box-shadow .15s, transform .15s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  white-space: nowrap;
  will-change: box-shadow, transform;
  font-size: 18px;
}

.btn:focus {
  box-shadow: #3c4fe0 0 0 0 1.5px inset, rgba(45, 35, 66, .4) 0 2px 4px, rgba(45, 35, 66, .3) 0 7px 13px -3px, #3c4fe0 0 -3px 0 inset;
}

.btn:hover {
  box-shadow: rgba(45, 35, 66, .4) 0 4px 8px, rgba(45, 35, 66, .3) 0 7px 13px -3px, #3c4fe0 0 -3px 0 inset;
  transform: translateY(-2px);
}

.btn:active {
  box-shadow: #3c4fe0 0 3px 7px inset;
  transform: translateY(2px);
}

.download-csv {
  display: flex;
  justify-content: center;
}
</style>
