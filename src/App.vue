<template>
  <div>
    <h1>Vue app</h1>
    <!-- <modal /> -->
    <button @click="downloadFile">Download File</button>
  </div>
</template>

<script>
import XLSX from 'xlsx';
import HelloWorld from './components/HelloWorld.vue'
import Modal from './components/Modal.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    Modal
  },
  data() {
    return {
      downloadJobHeaders: {
        headerName: {},
        headerMapping: {},
      }
    }
  },
  created() {
    this.setExcelDownloadHeader();
  },
  methods: {
    downloadFile() {
      // let axios = {}
      // let url = {}
      // axios.post(url, {
        // body api
      // }).then(res => {
        const res = {
          data: [
            {
              myName: "Đức",
              age: 18,
              address: "HN"
            },
            {
              myName: "Đức",
              age: 18,
              address: "HN"
            },
            {
              myName: "Đức",
              age: 18,
              address: "HN"
            },
            {
              myName: "Đức",
              age: 18,
              address: "HN"
            }

          ]
        }
        var wb = XLSX.utils.book_new();
        var jobHarr = [this.downloadJobHeaders.headerName];
        var jobWorksheet = XLSX.utils.json_to_sheet(res.data, {header: this.downloadJobHeaders.headerMapping, skipHeader: true, origin: 'A2'});
        // set width for column
        jobWorksheet["!cols"] = [{width: 20}, {width: 20}, {width: 20}];
        XLSX.utils.sheet_add_json(jobWorksheet, jobHarr, {skipHeader: true, origin: 'A1'});
        XLSX.utils.book_append_sheet(wb, jobWorksheet, 'Job');
        XLSX.writeFile(wb, 'NameFile.xlsx', {cellStyles: true });
      // })
    },
    setExcelDownloadHeader() {
      var downloadJobHeaders = {};
      // set header column excel
      downloadJobHeaders['my Name'] = 'myName';
      downloadJobHeaders['age'] = 'age';
      downloadJobHeaders['address'] = 'address';

      this.downloadJobHeaders.headerName = Object.keys(downloadJobHeaders);
      this.downloadJobHeaders.headerMapping = this.downloadJobHeaders.headerName.map(function(item, idx, arr) {
        return downloadJobHeaders[item];
      })
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
