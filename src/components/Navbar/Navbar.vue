<template>
    <div class="navbar flex">
        <el-menu :default-active="$route.name" class="el-menu-nav" mode="horizontal" @select="handleSelect" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
            <div class="flex">
                <el-menu-item class="logo" @click="toRouter('/home')">发声网</el-menu-item>
            </div>
            <div class="navMain flex">
                <el-menu-item index="home" @click="toRouter('/home')">首页</el-menu-item>
                <el-menu-item index="2" @click="toRouter()">我要揭发</el-menu-item>
                <el-menu-item index="hc" @click="toRouter('/hc/list')">求助中心</el-menu-item>
                <el-menu-item index="4" @click="toRouter()">社区论坛</el-menu-item>
                <el-menu-item index="5" @click="toRouter('/info')">相关资讯</el-menu-item>
                <el-menu-item index="6" @click="toRouter()">万人墙</el-menu-item>
            </div>
            <div class="profile flex">
                <el-menu-item index="scHome" @click="toRouter('/sc/home')" v-if="isLogin">
                    <!-- <el-avatar class="myAvator" src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"></el-avatar> -->
                    {{ currentUser }}
                </el-menu-item>
                <el-menu-item index="8" @click="logout()">登出</el-menu-item>
            </div>

        </el-menu>
    </div>
</template>

<script>
export default {
    name: "Navbar",
    data() {
        return {
            activeIndex: "1"
        };
    },
    computed: {
        isLogin() {
            if (localStorage.getItem("userName") && localStorage.getItem("userToken")) {
                this.$store.commit("userStatus", localStorage.getItem("userName"));
            } else {
                this.$store.commit("userStatus", null);
            }
            return this.$store.getters.isLogin;
        },
        currentUser() {
            return this.$store.getters.currentUser;
        }
    },
    methods: {
        handleSelect(key, keyPath) {
            console.log(key, keyPath);
        },
        toRouter(path) {
            !path ? alert("敬请期待") : this.$router.push({ path });
        },
        logout() {
            localStorage.clear();
            this.$message({
                message: "登出成功",
                type: "success",
                center: true
            });
            this.toRouter("/login");
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flex {
    display: flex;
}
.navbar {
    height: 60px;
    align-items: center;
    justify-content: space-around;
}
.logo {
    display: flex;
    font-size: 32px;
    font-weight: 600;
    color: #fff;
}
.navMain .el-menu-item.is-active {
    border-bottom: 3px solid;
}
.el-menu-nav {
    height: 60px;
    display: flex;
    justify-content: space-around;
    flex: 1;
}
.profile {
}
</style>
