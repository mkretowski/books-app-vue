<template>
  <div>
    <p>Books amount: {{ books.length }}</p>
    <p>Books price: {{ booksPrice }}</p>
  </div>
</template>
<script>
export default {
  name: 'BooksSummary',
  props: {
    books: {
      type: Array,
      required: true
    }
  },
  computed: {
    booksPrice() {
      return this.books.reduce((total, book) => total + parseInt(book.price), 0)
    }
  }
}
</script>
