<template>
    <section>
        <h1>{{ pageTitle }}</h1>

        <ul>
            <li v-for="user of users" :key="user.id">
                <a href="#" @click.prevent="openUser(user)">
                    {{ user.name }}
                </a>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    name: "index",

    async fetch({store}) {
        if (store.getters['users/users'].length === 0) {
            await store.dispatch('users/fetchUsers')
        }
    },

    data: () => ({
        pageTitle: 'Users Page'
    }),

    computed: {
        users() {
            return this.$store.getters['users/users'].data
        }
    },

    methods: {
        openUser(user) {
            this.$router.push('/users/' + user.id)
        }
    }
}
</script>
