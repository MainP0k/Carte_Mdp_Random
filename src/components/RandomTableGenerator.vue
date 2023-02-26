<template>
  <div>
    <table>
      <thead>
        <tr>
          <th></th>
          <th v-for="(header, index) in colHeaders" :key="index">
            {{ header }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
          <th>{{ rowHeaders[rowIndex] }}</th>
          <td v-for="(cell, cellIndex) in row" :key="cellIndex">
            {{ Array.isArray(cell) ? cell.join("") : cell }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
table {
  border-collapse: collapse;
  margin: 0 auto;
}

th,
td {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: center;
}

th {
  background-color: #f2f2f2;
  font-weight: bold;
}

th:first-child,
td:first-child {
  font-weight: bold;
}
</style>

<script>
export default {
  data() {
    return {
      tableData: [],
      rows: 9,
      cols: 9,
      characters:
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789",
      colHeaders: ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J"],
      rowHeaders: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10"],
    };
  },
  mounted() {
    this.generateTable();
  },
  methods: {
    generateTable() {
      const table = [];
      for (let i = -1; i < this.rows; i++) {
        const row = [];
        for (let j = -1; j < this.cols; j++) {
          if (i === -1 && j === -1) {
            row.push("TestN1");
          } else {
            const chars = [];
            for (let k = 0; k < 4; k++) {
              chars.push(
                this.characters.charAt(
                  Math.floor(Math.random() * this.characters.length)
                )
              );
            }
            row.push(chars);
          }
        }
        table.push(row);
      }
      this.tableData = table;
    },
  },
};
</script>