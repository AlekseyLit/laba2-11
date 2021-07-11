<template>
	<header>
		<a href="/" class="logo">
            <i class="fas fa-laptop-code"></i>
		</a>
        <h1>Канбан-доска на Vue.js</h1>
        <div class="toggle" @click="$emit('changeTheme')">
        <i v-if="!this.$parent.darkTheme" class="fas fa-toggle-off"></i>
        <i v-else class="fas fa-toggle-on"></i>
    </div>
	</header>
</template>

<style>
    header {
        display: flex;
        justify-content:space-between;
        line-height: 50px;
        padding: 20px 0;
        border-bottom: 1px solid #000;
        margin-bottom:40px;
    }
    .logo {
        font-size: 50px;
        color: #333;
    }
    h1 {
        font-weight: normal;
        text-align: center;
    }
    .toggle {
        font-size: 30px;
        cursor:pointer;
    }
    .dark header  {
        color:#aaa;
        border-bottom-color:#aaa;
    }
    .dark .logo  {
        color:#aaa;
    }
</style>