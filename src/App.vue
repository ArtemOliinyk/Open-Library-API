<template>
  <div id="app">
    <div class="well">
      <form>
        <div class="form-group">
          <label for="firstname"> First name </label>
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
          <label for="book"> My book ISBN ( like 0201558025, 0789312239)</label>
          <input type="text" id="book" class="form-control" placeholder="book" v-model="formData.bookIsbn">
        </div>
        <div class="form-group">
          <label for="techno"> My technologies (through "," )</label>
          <input type="text" id="techno" class="form-control" placeholder="techno" v-model="formData.techno">
        </div>

        <button type="submit" class="btn btn-default" v-on:click.prevent="submit"> Submit</button>
      </form>
    </div>

    <div class="well" v-if="isShowInfo">
      <h4>Dear {{fullName}} !</h4>
      <p v-html="formData.badge"> </p>
      <p>My site is <a :href="formData.url"> here </a></p>
      <h5>My book is '{{book.title}}' </h5>
      <img :src="book.url">
      <p> My technologies</p>
      <ul>
        <li class="font-normal" v-for="tech in techno"> {{tech}}</li>
      </ul>
    </div>
    <div v-else class="well"> Please submit the form</div>

  </div>
</template>


<script>

  import $ from 'jquery';

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
        },
        isShowInfo: false,
        book:{
          title: "",
          url: ""
        }
      }
    },
    methods:{
      submit: function () {
        this.isShowInfo = true;
      },
    },
    computed: {
      fullName: function(){
        return this.formData.firstName + " " + this.formData.lastName;
      },
      techno: function () {
        return this.formData.techno.split(",")
      }
    },
    watch:{
      "formData.bookIsbn" : function () {
        let url = "http://crossorigin.me/http://openlibrary.org/api/books?bibkeys=ISBN:" + this.formData.bookIsbn + "&format=json&jscmd=data";
        let inst = this;
        $.getJSON(url, function(data) {
          inst.book.title = data["ISBN:" + inst.formData.bookIsbn].title;
          inst.book.url = data["ISBN:" + inst.formData.bookIsbn].cover.large;
        });
      }
    }
  }
</script>

<style lang="scss">
  @import '../node_modules/bootstrap/scss/bootstrap.scss';

  .well{
    margin-bottom: 1%;
    padding: 2%;
    background-color: #ededef;
    font-weight: bold;
  }
  .well-info{

  }
  .font-normal{
    font-weight: normal;
  }
</style>
