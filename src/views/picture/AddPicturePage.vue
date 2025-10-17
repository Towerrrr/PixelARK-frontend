<template>
  <PictureUpload :picture="picture" :onSuccess="onSuccess" />
</template>

<script lang="ts">
import { ref } from 'vue';

const picture = ref<API.PictureVO>()
const onSuccess = (newPicture: API.PictureVO) => {
  picture.value = newPicture
}
</script>