<template>
  <div class="backdrop">
    <div class="modal">
      <button @click="downloadFile">download</button>
    </div>
  </div>
</template>
<script>
// ver: 0.16.2
import XLSX from 'xlsx';
export default {
  name: 'DownloadFileExcel2',
  data() {
    return {
      downloadFileHeader: {
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
      axios.post(url, {
        // body api
      }).then(res => {
        var wb = XLSX.book_new();
        var jobHarr = [this.downloadJobHeader.headerName];
        var jobWorksheet = XLSX.utils.json_to_sheet(res.data, {header: this.downloadJobHeader.headerMapping, skipHeader: true, origin: 'A2'});
        // set width for column
        jobWorksheet["!cols"] = [{width: 20}, {width: 20}, {width: 20}];
        XLSX.utils.sheet_add_json(jobWorksheet, jobHarr, {skipHeader: true, origin: 'A1'});
        XLSX.utils.book_append_sheet(wb, jobWorksheet, 'Job');
        XLSX.writeFile(wb, 'NameFile.xlsx', {cellStyles: true });
      })
    },
    setExcelDownloadHeader() {
      var downloadFileHeader = {};
      // set header column excel
      downloadFileHeader['column1'] = 'column1';
      downloadFileHeader['column2'] = 'column2';
      downloadFileHeader['column3'] = 'column2';

      this.downloadFileHeader.headerName = Object.keys(downloadFileHeader);
      this.downloadFileHeader.headerMapping = this.downloadFileHeader.headerName.map(function(item, idx, arr) {
        return downloadJobHeader[item];
      })


    }
  },
}
</script>
<style scoped>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
  }
  .backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
  }
  h1 {
    color: #03cfb4;
    border: none;
    padding: 0;
  }

  .modal p {
    font-style: normal;
  }
</style>