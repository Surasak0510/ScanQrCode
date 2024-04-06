<template>
  <div class="container">
    <div class="row d-flex mt-5 mb-3">
      <a href="/" type="button" class="btn btn-primary mx-auto">Home</a>
    </div>
    <div class="row d-flex">
      <div class="col-12">
        <div id="reader" class="mx-auto"></div>
        <div id="result" v-if="scannedData">
          <h2>Success!</h2>
          <p>
            <a :href="scannedData" target="_blank">{{ scannedData }}</a>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Html5QrcodeScanner } from 'html5-qrcode';

export default {
  data() {
    return {
      scannedData: null,
    };
  },
  mounted() {
    const scanner = new Html5QrcodeScanner(
      'reader',
      {
        qrbox: { width: 250, height: 250 },
        fps: 20,
      }
    );

    scanner.render(this.onScanSuccess, this.onScanError);
  },
  methods: {
    onScanSuccess(result) {
      this.scannedData = result;
      // Optionally stop scanning after a successful scan
      scanner.clear();
    },
    onScanError(err) {
      // console.error(err);
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
}

#reader {
  width: 600px;
}

#result {
  text-align: center;
  font-size: 1.5rem;
}
</style>