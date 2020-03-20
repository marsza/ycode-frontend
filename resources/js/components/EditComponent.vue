<template>
  <div class="container">
      <div class="row">
          <h1>Edit Website</h1>
      </div>
      <div class="row">
          <div class="col-md-12">
            <form @submit.prevent="updateWebsite">
                <div class="form-group">
                    <label>Website Name</label>
                    <input type="text" class="form-control" v-model="website.name" required>
                </div>
                <div class="form-group">
                    <label>Website URL</label>
                    <input type="text" class="form-control" v-model="website.url" required>
                </div>
                <br>
                <div class="form-group">
                    <button class="btn btn-primary">Update</button>
                </div>
            </form>
          </div>
      </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                website: {}
            }
        },
        created() {
            let apiUrl = `https://ycodebackend.herokuapp.com/api/websites/search/${this.$route.params.id}`;
            this.axios.post(apiUrl).then((response) => {
                this.website = response.data;
            });
        },
        methods: {
            updateWebsite() {
                let apiUrl = `https://ycodebackend.herokuapp.com/api/websites/update/${this.$route.params.id}`;
                this.axios.post(apiUrl, this.website).then((response) => {
                    if (response.data.status != false) {
                        this.$router.push({name: 'websites'});
                    } else {
                        alert('The URL used is not unique');
                    }
                    
                });
            }
        }
    }
</script>