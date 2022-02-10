<template>
    <div>
        <nav-menu></nav-menu>
        <router-view/>
        <!-- 子页面显示地方 -->
    </div>
</template>

<script>
    import NavMenu from './common/NavMenu'
    export default {
        name: 'Home',
        components: { NavMenu }        
    }
</script>

<style scoped>
</style>