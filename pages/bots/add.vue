<template>
  <div class="container">
    <form @submit.prevent="save">
      <div class="form-group">
        <label for="cookie">Cookie</label>
        <input id="cookie" v-model="sendData.cookie" type="text" class="form-control" placeholder="Nhập cookie">
      </div>
      <div class="form-group">
        <label for="proxy">Cookie</label>
        <input id="proxy" v-model="sendData.proxy" type="text" class="form-control" placeholder="Nhập proxy">
      </div>
      <div class="form-group">
        <label for="frequency">Giãn cách thời gian mỗi comment</label>
        <select id="frequency" v-model="sendData.frequency" class="form-control">
          <option value="1">
            1 phút
          </option>
          <option value="3">
            3 phút
          </option>
          <option value="5">
            5 phút
          </option>
          <option value="10">
            10 phút
          </option>
          <option value="30">
            30 phút
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
        proxy: '',
        frequency: 3
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
