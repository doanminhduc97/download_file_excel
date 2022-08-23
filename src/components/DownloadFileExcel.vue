<template>
  <div class="backdrop">
    <div class="modal">
      <button @click="downloadFile">download</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DownloadFileExcel',
  methods: {
    downloadFile() {
      let axios = {}
      let url = {}
      axios.post(url, {
        // body api
      },
      {responseType: 'blob'}
      ).then(res => {
        if (window.navigator.msSaveOrOpenBlob) {
          // IE 11
          window.navigator.msSaveOrOpenBlob(res.data, "NameFile.xlsx");
        } else {
          // google chome, Firefox, ...
          const url = window.URL.createObjectURL(new Blob([res.data]));
          const link = document.createElement('a');
          link.href = url;
          link.setAttribute('download', 'NameFile.xlsx');
          document.body.appendChild(link);
          link.click();
        }
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