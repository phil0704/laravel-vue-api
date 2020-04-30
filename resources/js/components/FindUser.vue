<template>
    <section>
        <h2>Find a User by ID</h2>
        <form action="#" method="GET">
            <label for="id">
                User ID
                <input type="number" name="id" id="id">
            </label>
            <input type="submit" value="Find User">
        </form>
        <dl v-if="user">
            <dt>Name</dt>
            <dt>{{ user.name }}</dt>
            <dt>E-mail Address</dt>
            <dt>{{ user.email }}</dt>
        </dl>
        <p v-else>
           User not found.
        </p>
    </section>
</template>
<script>
export default {
    name: 'find-user',
    data () {
        return {
            user: false
        }
    }
}
</script>
<style>

</style>