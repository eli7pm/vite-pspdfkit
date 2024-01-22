<script setup lang="ts">
import PSPDFKit from "pspdfkit";
import { onBeforeUnmount, onMounted, ref, watch } from "vue";

const active = ref()
const documentList = ref([
  { id: 1, name: 'Brochure.docx', path: '/files/Brochure.docx' },
  { id: 2, name: 'Brochure.pdf', path: '/files/Brochure.pdf' },
  { id: 3, name: 'Your big idea.jpg', path: '/files/Your big idea.jpg' },
  { id: 4, name: 'Your big idea.png', path: '/files/Your big idea.png' },
  { id: 5, name: 'Your big idea.pptx', path: '/files/Your big idea.pptx' },
])


onBeforeUnmount(() => {
  PSPDFKit.unload(".file-viewer");
})

onMounted(() => {
  active.value = documentList.value[1]
})

watch(active, (_) => {
  PSPDFKit.unload(".file-viewer");
  PSPDFKit.load({
    licenseKey: 'zKZRa0kuj7TMbCa7IMdXTCoQMstQMnojfNW7eytsQTzJCBtt0VXVOpoIkrvX2rUWTRj4MuGd-K5VL39_Qj5sJZ_ipYTl5SW-PA2qL8CI2vZPugBe0l4p1Lw3T1838-JaldX3mbsV5nZLmWLsbbu_9MjggULPjh0ojFU3rvbtxXGrLUQSG_e527booQa2pyX0tNqmW6U311FM1DJYwba1eBeadsPIcm_SJqyQiGjK4pNqYVM6VnqmbbCMbf29bc2jxqmEXOD3qw3VDE7JDMgsmHyM3Z660wxV_0nnxLKKgItPYyq8cSlPWAz_pEk0O2lVAVRnpr6V3I-BVOjKpmocp8IYFtjJaUGaLXQ-tYueQ8khYfSphnYNoZFHYihBiUqUFypPgmGf9RqQsQQNWUIqjWeobKnCadxtpKCZs8EIY-XpAf5XsRDXMSm8l1J4iaEgJUxvs5tJAx78PM8UGwd4YNefRG0t_ez-u_N1K_QqIl9ZEySQKBVp1pFYfOk-XHs9cci84pNUTqybB_AXznJIm8S0PRbHhm5PCb19qOoQxjsjK8thxkvec_N8k1PRxwFBZv8UVjjcIk7Txbft-6a-5mC6JH-iw81BwynWo2Ra41sHS13_ZnE8dcpoX30IBlzDYCD9WnQwYGDO8qQUbgKsaJD4qaLVL9iaqWX0IhJjFsgYtutGaJqXNArFHjgo98yzU-KfcOf8vIjsc-HbQpy7I6vqH3TlLbsPUnPA2qg6s3BNA0ezGPci1RQxnrrXYodxdrjpS_P4hJursGVJhlkJyOfCgiQ_eTiMJOQZR6xGjEYozXdnsSBTgtBjA86i_a-O7i7YMxvQ4sXMN-W9WoLCAIubh_BY26XahBLvCsjuvYo=',
    // access the pdfFile from props
    document: _.path,
    baseUrl: location.protocol + "//" + location.host + "/",
    container: ".file-viewer",
  })
})
</script>
<template>
  <div class="p-5 w-full">
    <div class="grid grid-cols-3 bg-white w-full h-full">
      <div class="p-3">
        <ul>
          <li class="px-3 py-1 cursor-pointer" :class="active?.id === _document.id ? 'bg-violet-500 text-white rounded' : ''" @click="active = _document" v-for="(_document, index) in documentList" :key="index">
            {{ _document.name }}
          </li>
        </ul>
      </div>
      <div class="col-span-2">
        <h3>PSPDFKit Viewer</h3>
        <div class="p-3 bg-slate-200 rounded-md">
          <div class="file-viewer h-screen">

          </div>
        </div>
      </div>
    </div>
  </div>
</template>
