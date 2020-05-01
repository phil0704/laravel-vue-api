<template>
    <section>
        <h2>Update User Name</h2>
        <form  @submit="update" action="#" method="GET">
            <label for="id">
                User ID
                <input type="number" name="id" id="id" v-model="userId">
            </label>
            <label for="name">
                User name
                <input type="text" name="name" id="id" v-model="userName">
            </label>
            <input type="submit" value="Update User">
        </form>
        <dl v-if="user">
            <dt>Status</dt>
            <dd>User was successfully updated.</dd>
            <dt>Name</dt>
            <dd>{{ user.name }}</dd>
            <dt>E-mail Address</dt>
            <dd>{{ user.email }}</dd>
        </dl>
        <p v-else>
           User not found.
        </p>
    </section>
</template>
<script>
export default {
    name: 'update-user-name',
    data () {
        return {
            userId: '',
            userName: '',
            user: false
        }
    },
    methods: {
        update (event) 
        { // Make sure our form doesn't refresh the page.
         event.preventDefault();
         // Convert user Id from string/float to integer.
         const userId = parseInt( this.userId );
         // Grab the user name.
         const userName = this.userName;
         // search for the user. // Note: ${} syntax is a "template literal."
         axios.patch(`/laravel-vue-api/public/api/user/${userId}`, {
            name: userName // Submit
         })
         .then(response => {
            // console.log( response );
            // Get the user from the response.
            const user = response.data;
            // Store the user in our data.
            this.user = user;
            // Clear the name and ID fields.
            this.userId = '';
            this.userName = '';
         })
         .catch ( error => { // CATCH is used for a request FAILURE.
             // The user wasn't found; so false!
             this.user = false;
             // Output the error message to console for easy debugging.
             console.log( error );
         })
        }
    }
}
</script>
<style>

</style>