<template>
  <q-page class="q-pa-md">
    <q-file
      color="teal"
      filled
      v-model="fileModel"
      label="選擇圖片"
      @update:model-value="breedModel = null"
    >
      <template v-slot:prepend>
        <q-icon name="cloud_upload" />
      </template>
    </q-file>

    <q-img v-if="fileModel" :src="imgURL(fileModel)" class="fit q-mt-md" />

    <q-btn class="fit q-mt-md" outline rounded label="辨識" @click="fetchBreed" />

    <div class="q-mt-md">辨識結果：{{ breedModel }}</div>
  </q-page>
</template>

<script setup lang="ts">
import { api } from 'src/boot/axios'
import { ref } from 'vue'

const fileModel = ref<File | null>(null)
const breedModel = ref<string | null>(null)

const imgURL = (file: File) => URL.createObjectURL(file)

const fetchBreed = async () => {
  const formData = new FormData()
  formData.append('file', fileModel.value as File)

  const response = await api.post('/upload-image/', formData, {
    headers: {
      'Content-Type': 'multipart/form-data',
    },
  })

  breedModel.value = response.data.class
}
</script>
