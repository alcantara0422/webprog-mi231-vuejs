<template>
  <div class="comment-form">
    <h3>Leave a Comment</h3>
    <form @submit.prevent="submitComment">
      <div class="form-group">
        <label for="name">Name:</label>
        <input 
          type="text" 
          id="name" 
          v-model="comment.name" 
          required
          class="form-control"
        >
      </div>
      <div class="form-group">
        <label for="message">Message:</label>
        <textarea 
          id="message" 
          v-model="comment.message" 
          required
          class="form-control"
          rows="3"
        ></textarea>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'CommentForm',
  data() {
    return {
      comment: {
        name: '',
        message: '',
        date: null
      }
    }
  },
  methods: {
    submitComment() {
      const newComment = {
        ...this.comment,
        date: new Date().toISOString()
      }
      this.$emit('comment-submitted', newComment)
      this.comment.name = ''
      this.comment.message = ''
    }
  }
}
</script>

<style scoped>
.comment-form {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
.form-group {
  margin-bottom: 15px;
}
.form-control {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>
