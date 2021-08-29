<template>
  <div class="home">
    <Step1
      ref="step1"
      @down="download"
    />
  </div>
</template>

<script>
import Step1 from '@/components/step1.vue'
import { saveAs } from 'file-saver'
import { Packer } from 'docx'
import { CVCreator } from '@/components/cv-generator.js'
export default {
  name: 'Home',
  components: {
    Step1
  },
  methods: {
    download () {
      const doc = new CVCreator().create(this.$refs.step1.getData())
      Packer.toBlob(doc).then(blob => {
        saveAs(blob, 'example.docx')
      })
    }
  }
}
</script>
