<template>
  <div class="container">
    <form @submit.prevent="save">
      <div class="form-group">
        <label for="cookie">Cookie</label>
        <input id="cookie" v-model="sendData.cookie" type="text" class="form-control" placeholder="Nhập cookie">
      </div>
      <div class="form-group">
        <label for="frequency">Bài viết/phút</label>
        <select id="frequency" class="form-control">
          <option value="">
            - Chọn số lượng bài viết -
          </option>
          <option value="1">
            1 bài / 10 phút
          </option>
          <option value="2">
            2 bài / 10 phút
          </option>
          <option value="3">
            3 bài / 10 phút
          </option>
        </select>
      </div>
      <button type="submit" class="btn btn-success">
        Lưu
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      sendData: {
        cookie: '',
        frequency: 2
      }
    }
  },
  methods: {
    save () {
      this.$axios.post('/api/bot/new', this.sendData).then((response) => {
        if (response.data.status === 'success') {
          alert('Lưu thành công')
        } else {
          alert(response.data.message)
        }
      }).catch((e) => {
        // eslint-disable-next-line no-console
        console.log(e)
        alert('Lỗi khi lưu')
      })
    }
  }
}
</script>

<style>

</style>
