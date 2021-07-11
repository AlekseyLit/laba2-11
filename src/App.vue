<template>
    <div class="container" :class="{ dark: darkTheme }">
        <Header @changeTheme="changeTheme" />
        <Main />
        <Footer />
    </div>
</template>

<script>
    import Header from './components/Header.vue'
    import Main from './components/Main.vue'
    import Footer from './components/Footer.vue'

    export default {
        name: 'App',
        components: {
            Header, Main, Footer
        },
        data() {
            return {
                darkTheme: false
            }
        },
        methods: {
            changeTheme() {
                this.darkTheme = !this.darkTheme;
            }
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    * {
        margin:0;
        padding:0;
        font-family: 'Roboto', sans-serif;
    }
    body {
        font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
        color: #333;
    }
    .container {
        padding: 0 50px;
    }
    .dark.container {
        background: black;
    }

</style>
