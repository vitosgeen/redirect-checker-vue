<template>
  <div class="container redirect-checker">
    <h1>{{ msg }}</h1>
    <p>
      301 vs 302, meta refresh & javascript redirects
    </p>
    <div>
      <div>
        <div>
          <div class="d-flex justify-content-center">
            <form @submit.prevent="handleSubmit" class="check-redirect-form">
              <div class=" input-group ">
                <div class="col-auto">
                  <div class="url-input-field form-floating">
                    <input type="url" class="form-control redirect-input" placeholder="Url" id="url-input" v-model="urlInput" required />
                    <label for="url-input" class="form-label">Url</label>
                    <span>{{ urlInput }}</span>
                  </div>
                </div>
                <div class="col-auto ">
                  <input type="submit" id="send-input" value="Check" class="btn btn-primary btn-lg redirect-button" />
                </div>
              </div>           
            </form>  
          </div>
            <div class="clearfix"></div>
            <div class="result-block d-flex justify-content-center mt-2">
              <div class="col-auto ">
                <p v-html="statusRedirect" class="p">
                  
                </p>
              </div>
            </div> 
            <div class="result-block d-flex justify-content-center mt-2">
              <div class="col-auto term-display">
                <p  v-html="headersRedirect" class="term">
                
                </p>
              </div>
            </div> 
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RedirectChecker',
  props: {
    msg: String
  },
  data() {
    return {
      urlInput: '',
      statusRedirect: '',
      headersRedirect: '',
    }
  },
  methods: {
    handleSubmit() {
      console.log(process.env);
      this.statusRedirect = "";
      this.headersRedirect = "";
      fetch(process.env.VUE_APP_REDIRECT_CHECK_API_URL + '/?url=' + this.urlInput)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
          this.redirectsHandler(data)
      });
    },
    redirectsHandler(data) {
      if (!Object.prototype.hasOwnProperty.call(data, "Redirects")) {
        return
      }
      for (var k in data.Redirects ) {
        var item = data.Redirects[k];
        if (this.headersRedirect.length !== 0) {
          this.headersRedirect += "<br/><br/>";
        }
        this.statusRedirect += item.status + "<br />";
        this.headersRedirect += "URL: " + item.url + "<br/>";
        this.headersRedirect += "Status: " + item.status + "<br/>";
        for (var h in item.headers ) {
          var itemh = item.headers[h]
          this.headersRedirect += h + ": " + itemh + "<br/>";
        }
        if (item.error.length > 0) {
          this.headersRedirect += "ERROR: " + item.error + "<br/>";
        }
      }
    },
  },
  setup() {
    const form = {
      urlInput: "",
    };

    return {
      form,
    };
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>