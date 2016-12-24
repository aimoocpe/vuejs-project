<template>
    <div class="ui modal">
        <div class="header">Upload</div>
        <div class="content">
            <div v-show="uploading" ref="progress" class="ui progress">
                <div class="bar">
                    <div class="progress"></div>
                </div>
                <div class="label">Uploading...</div>
            </div>
            <br>
            <input @change="selectedFile" type="file" ref="file" style="display: none;">
            <div class="ui blue button" @click="$refs.file.click()">Select File</div>
            <div class="ui red button" @click="close">Close</div>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'

export default {
  data: () => ({
    uploading: false
  }),
  methods: {
    open () {
      $(this.$el)
        .modal({
          closable: false
        })
        .modal('show')
    },
    close () {
      $(this.$el).modal('hide')
    },
    selectedFile () {
      const file = this.$refs.file.files[0]
      if (!file) return
      this.uploading = true
      const task = firebase.storage().ref(`files/${Date.now()}`).put(file)
      task.on(firebase.storage.TaskEvent.STATE_CHANGED, (o) => {
        const percent = o.bytesTransferred / o.totalBytes * 100
        $(this.$refs.progress).progress({ percent: percent })
      })
      task.then((snapshot) => {
        this.uploading = false
        this.$emit('success', snapshot.downloadURL)
        this.close()
      })
    }
  }
}
</script>