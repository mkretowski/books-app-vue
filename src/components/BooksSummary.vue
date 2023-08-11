<template>
  <div>
    <p>Books amount: {{ books.length }}</p>
    <p>Books price: {{ booksPrice.toFixed(2) }}</p>
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
      return this.books.reduce(
        (total, book) => total + parseFloat(book.price),
        0
      )
    }
  }
}
</script>
