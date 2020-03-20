<template>
    <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <h1>Websites</h1>
                </div>
                
            </div><br>
            <div class="row">
                <div class="col-md-12">
                    <table class="table table-hover">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>Url</th>
                                <th>Edit</th>
                                <th>Delete</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="website in orderedWebsites" :key="website.id">
                                <td>{{ website.id }}</td>
                                <td>{{ website.name }}</td>
                                <td>{{ website.url }}</td>
                                <td><router-link :to="{name: 'edit', params: { id: website.id}}" class="btn btn-primary">Edit</router-link></td>
                                <td><button class="btn btn-danger" @click.prevent="deleteWebsite(website.id)">Delete</button></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                websites: []
            }
        },
        computed: {
            orderedWebsites: function() {
                return _.orderBy(this.websites, 'id')
            }
        },
        created() {
            let apiUrl = 'https://ycodebackend.herokuapp.com/api/websites';
            this.axios.get(apiUrl).then(response => {
                this.websites = response.data;
            });
        },
        methods: {
            deleteWebsite(id) {
                let apiUrl = `https://ycodebackend.herokuapp.com/api/websites/${id}`;
                this.axios.delete(apiUrl).then((response) => {
                    this.websites.splice(this.websites.indexOf(id), 1);
                });
            }
        }
    }
</script>