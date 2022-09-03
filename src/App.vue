<template>
  <RedirectChecker msg="Check Your Redirects and Statuscode"/>
</template>

<script>
import RedirectChecker from './components/RedirectChecker.vue'
import "bootstrap/dist/css/bootstrap.min.css"
import "bootstrap/dist/css/bootstrap-grid.min.css"
import "bootstrap/dist/css/bootstrap-utilities.min.css"
import "bootstrap/dist/css/bootstrap-reboot.min.css"
import "bootstrap/dist/css/bootstrap.rtl.min.css"
import "bootstrap"

export default {
  name: 'App',
  components: {
    RedirectChecker
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.redirect-button {
  border-radius: 0 5px 5px 0;
  height: 60px;
}
form div.url-input-field input.redirect-input {
  border-radius: 5px 0 0 5px;
  height: 60px;
  min-width: 400px;
}
.term:empty {
  display: none;
}
.term {
  font-family: monospace;
  color: #fff;
  opacity: 0.8;
  font-size: 1em;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 10px;
  text-align: left;
}

.term:after {
  content: "_";
  opacity: 1;
  animation: cursor 1s infinite;
}
.term-display {
  background-color: #000000;
  max-width: 600px;
}
@keyframes cursor {
  0% {
    opacity: 0;
  }
  40% {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
