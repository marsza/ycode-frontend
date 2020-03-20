<template>
  <div class="container">
      <div class="row">
        <h1>Create a Website</h1>
      </div>
      <div class="col-md-12">
          <form @submit.prevent="addWebsite">
                <div class="form-group">
                    <label>Website Name</label>
                    <input type="text" class="form-control" v-model="website.name" required>
                </div>
                <div class="form-group">
                    <label>Website Url</label>
                    <input type="text" class="form-control" v-model="website.url" required>
                </div>
                <br>
                <div class="form-group">
                    <button class="btn btn-primary">Create</button>
                </div>
          </form>

      </div>
  </div>
</template>

<script>
    export default {
        data(){
            return{
                website:{}
            }
        },
        methods: {
            addWebsite(){
                let apiUrl = 'https://ycodebackend.herokuapp.com/api/websites';
                this.axios.post(apiUrl, this.website).then((response) => {
                    console.log(response.data.status);
                    if (response.data.status !== false) {
                       this.$router.push({name: 'websites'}); 
                    } else {
                        alert('The URL used is not unique');
                    }
                    
                });
            }
        }
    }
</script>