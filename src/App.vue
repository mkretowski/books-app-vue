<template>
  <div id="app" class="app">
    <!-- heading -->
    <header class="app__heading">
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <books-list :removeBook="removeBook" :books="books" />

    <!-- no books message -->
    <books-length-msg :books="books" />

    <!-- add book form -->
    <book-form @add="addBook" />

    <!-- books summary -->
    <books-summary :books="books" />
  </div>
</template>

<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg'
import BookForm from './components/BookForm'
import BooksSummary from './components/BooksSummary'
export default {
  name: 'App',
  data: () => ({
    books: []
  }),
  mounted() {
    this.fetchBookData('9781491954249')
    this.fetchBookData('9781491985571')
    this.fetchBookData('9781617294136')
  },
  methods: {
    removeBook(index) {
      this.books.splice(index, 1)
    },
    addBook(book) {
      this.books.push({ ...book })
    },
    async fetchBookData(isbn) {
      try {
        const response = await fetch(
          `https://api.itbook.store/1.0/books/${isbn}`
        )
        const data = await response.json()
        if (!data.title || !data.price) {
          throw new Error('Invalid book data')
        }
        this.books.push({
          title: data.title,
          price: parseFloat(data.price.replace('$', ''))
        })
      } catch (error) {
        console.error(error)
      }
    }
  },
  components: {
    BooksList,
    BooksLengthMsg,
    BookForm,
    BooksSummary
  }
}
</script>

<style lang="scss" scoped>
.app {
  width: 100%;
  max-width: 1000px;
  padding: 2rem;
  margin: 0 auto;

  &__heading {
    font-size: 3rem;
    text-align: center;
    span {
      color: #5a58da;
    }
  }
}
</style>
