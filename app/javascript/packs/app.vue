<template>
  <div id="app">

    <tickets-nav></tickets-nav>

    <div class="container">
      <div class="alert alert-success alert-dismissible" role="alert" v-if="successAlertMessage">
        <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <strong>Success!</strong> {{ successAlertMessage }}
      </div>
      <router-view></router-view>
      <hr>
      <tickets-footer></tickets-footer>
    </div> <!-- /container -->

  </div>
</template>

<script>
import Nav from './components/nav.vue';
import Footer from './components/footer.vue';
import { bus } from './tickets.js';

export default {
  data() {
    return {
      successAlertMessage: ''
    }
  },
  components: {
    ticketsNav: Nav,
    ticketsFooter: Footer
  },
  watch: {
    $route() {
      this.successAlertMessage = '';
    }
  },
  created: function() {
    bus.$on('successAlertMessage', (successAlertMessage) => {
      this.successAlertMessage = successAlertMessage;
    });
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}

</style>
