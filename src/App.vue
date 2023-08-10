<template>
  <div id="app">
    <!-- heading -->
    <header>
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <books-list :removeBook="removeBook" :books="books" />

    <!-- no books message -->
    <p v-show="!books.length">No books...</p>

    <!-- no books message -->
    <books-length-msg :books="books" />

    <!-- add book form -->
    <form @submit.prevent="handleSubmit">
      <label>
        Title:
        <input v-model="form.title" type="text" name="title" />
      </label>
      <label>
        price:
        <input v-model="form.price" type="number" name="price" />
      </label>
      <button>Add book</button>
    </form>
  </div>
</template>

<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg'
export default {
  name: 'App',
  data: () => ({
    books: [
      {
        title: 'The Catcher in the Rye',
        price: 20
      },
      {
        title: 'Of Mice and Men',
        price: 18
      }
    ],
    form: {
      title: '',
      price: 0
    }
  }),
  methods: {
    removeBook(index) {
      this.books.splice(index, 1)
    },
    handleSubmit() {
      this.books.push({ ...this.form })
      this.form.title = ''
      this.form.price = 0
    }
  },
  components: {
    BooksList,
    BooksLengthMsg
  }
}
</script>
