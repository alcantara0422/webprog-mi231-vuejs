<template>
  <div class="comment-list">
    <h3>Comments</h3>
    <div v-if="comments.length === 0" class="no-comments">
      No comments yet. Be the first to comment!
    </div>
    <div v-for="comment in comments" :key="comment.date" class="comment">
      <div class="comment-header">
        <strong>{{ comment.name }}</strong>
        <span class="date">{{ formatDate(comment.date) }}</span>
      </div>
      <div class="comment-body">
        {{ comment.message }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CommentList',
  props: {
    comments: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    formatDate(dateString) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(dateString).toLocaleDateString(undefined, options)
    }
  }
}
</script>

<style scoped>
.comment-list {
  max-width: 600px;
  margin: 20px auto;
}
.comment {
  border: 1px solid #ddd;
  border-radius: 8px;
  margin-bottom: 15px;
  padding: 15px;
}
.comment-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}
.date {
  color: #666;
  font-size: 0.9em;
}
.no-comments {
  text-align: center;
  color: #666;
  padding: 20px;
}
</style>
