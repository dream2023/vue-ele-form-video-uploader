<template>
  <ele-upload-video
    :class="desc.class"
    :style="desc.style"
    style="line-height: 1"
    v-bind="attrs"
    v-model="newValue"
    v-on="onEvents"
  />
</template>

<script>
import EleUploadVideo from 'vue-ele-upload-video'
import formMixin from 'vue-ele-form/lib/mixins/formMixin'

export default {
  name: 'EleFormVideo',
  mixins: [formMixin],
  components: {
    EleUploadVideo
  },
  data () {
    return {
      isUploadMixin: true
    }
  }
}
</script>
