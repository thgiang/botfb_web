<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Lịch sử tương tác</h1>
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Hành động</th>
              <th>ID bài viết</th>
              <th>Thời gian</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(log, l_index) in logs" :key="l_index">
              <td>
                <span v-if="log.action === 'COMMENT'">Comment</span>
                <span v-else>Reaction loại {{ log.action }}</span>
              </td>
              <td>
                <span v-if="log.comment_id !== null && log.comment_id !== ''"><a target="_blank" :href="'https://facebook.com/'+log.comment_id">{{ log.comment_id }}</a></span>
                <span v-else-if="log.post_id !== ''"><a target="_blank" :href="'https://facebook.com/'+log.post_id">{{ log.post_id }}</a></span>
              </td>
              <td>{{ log.created_at }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      logs: []
    }
  },
  mounted () {
    this.$axios.get('/api/logs').then((response) => {
      this.logs = response.data.data.data
    }).catch((e) => {
      // eslint-disable-next-line no-console
      console.log('Lỗi khi đọc logs')
      // eslint-disable-next-line no-console
      console.log(e)
    })
  }
}
</script>
