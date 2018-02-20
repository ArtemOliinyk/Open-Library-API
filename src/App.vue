<template>
  <div id="app">
    <div class="well">
      <form>
        <div class="form-group">
          <label for="firstname"> First name 1</label>
          <input type="text" id="firstname" class="form-control" placeholder="first name" v-model="formData.firstName">
        </div>
        <div class="form-group">
          <label for="lastname">Second name </label>
          <input type="text" id="lastname" class="form-control" placeholder="last name" v-model="formData.lastName">
        </div>
        <div class="form-group">
          <label for="url"> Your site </label>
          <input type="text" id="url" class="form-control" placeholder="url" v-model="formData.url">
        </div>
        <div class="form-group">
          <label for="badge"> Personal badge (only HTML like img src="*.jpg" ) </label>
          <textarea class="form-control" id="badge" cols="10" rows="3" v-model="formData.badge"></textarea>
        </div>
        <div class="form-group">
          <label for="book"> Your book ISBN </label>
          <input type="text" id="book" class="form-control" placeholder="book" v-model="formData.bookIsbn">
        </div>
        <div class="form-group">
          <label for="techno"> Your technologies </label>
          <input type="text" id="techno" class="form-control" placeholder="techno" v-model="formData.techno">
        </div>

        <button type="submit" class="btn btn-default"> Submit</button>
      </form>
    </div>
    <div class="well">
      <h4>Dear {{fullName}} !</h4>
      <p></p>
      <p>My site is <a href=""> here </a></p>
      <h5>My book is  </h5>
      <img src="">
      <p> My technologies</p>
      <ul>
        <li></li>
      </ul>
    </div>
    <div class="well"> Please submit the form</div>

  </div>
</template>


<script>
  export default {
    name: 'app',
    data() {
      return {
        formData: {
          firstName: "",
          lastName: "",
          url: "http://www.",
          badge: "",
          bookIsbn: "",
          techno: ""
        }
      }
    },
    computed: {
      fullName: function(){
        return this.formData.firstName + " " + this.formData.lastName;
      }
    },

  }
</script>

<style lang="scss">
  @import '../node_modules/bootstrap/scss/bootstrap.scss';

  .well{
    margin: 2%;
  }
</style>
