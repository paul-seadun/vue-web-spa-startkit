<template>
    <div class='page-wrapper'>
        <loading-indicator :showing='pageLoading'></loading-indicator>
        <header className="page-header">
            <div class="logo">
                WEMEDIA DASHBOARD
            </div>
            <ul class="nav">
                <li :class="{active: this.$route.path == '/tasks'}">
                    <router-link to="/tasks">TASK MANAGEMENT</router-link>
                </li>
                <li :class="{active: this.$route.path == '/translator/approval'}">
                    <router-link to="/translator/approval">TRANSLATION MANAGEMENT</router-link>
                </li>
                <li :class="{active: this.$route.path == '/community/approval'}">
                    <router-link to="/community/approval">ARTICLE MANAGEMENT</router-link>
                </li>
                <li :class="{active: this.$route.path == '/userManager'}">
                    <router-link to="/userManager">USER MANAGEMENT</router-link>
                </li>
                <li :class="{active: this.$route.path == '/settings'}">
                    <router-link to="/settings">SETTINGS</router-link>
                </li>
            </ul>

            <div class='user'>
                <span>{{currentUser}}</span>
            </div>

            <a :href="logoutURL" class="logout"><i class="anticon anticon-logout"></i></a>
        </header>

        <router-view class="page-content-wrapper"></router-view>
    </div>
</template>

<script>
    import Vue from 'vue'
    import Element from 'element-ui'
    import {mapState, mapActions} from 'vuex'
    import LoadingIndicator from './components/LoadingIndicator'

    Vue.use(Element);

    console.log(1)

    export default {

        name: 'App',

        data(){
            return {
                logoutURL: `${window.config.context}/logout`,
            }
        },

        beforeMount(){
            this.getCurrentUser();
        },

        components: {
            LoadingIndicator
        },


        methods: mapActions(['getCurrentUser']),

        computed: mapState({
            pageLoading: ({root}) => root.pageLoading,
            currentUser: ({root}) => root.currentUser
        })
    };


</script>


<style lang="less">
    @import "./layouts/css/index";
    @import "../node_modules/element-ui/lib/theme-default/index.css";

    header {
        min-width: @body-width;
        padding-left: 30px;
        height: @header-height;
        background-color: @header-color;
        position: relative;
        overflow: hidden;

        .logo {
            background: transparent url('./layouts/img/logo.png') 0 center no-repeat;
            padding-left: 40px;
            margin-right: 50px;
            font-size: 16px;
            float: left;
            line-height: @header-height;
            height: 100%;
            color: #fff;

        }

        ul {
            overflow: hidden;

            li {
                height: @header-height;
                line-height: @header-height;
                margin-right: 30px;
                display: inline-block;
                &.active {
                    a {
                        color: #fff;
                    }
                }

                a {
                    color: #BDDDFF;
                    text-decoration: none;
                    &:hover {
                        color: #fff;
                    }
                }
            }
        }

        .user {
            position: absolute;
            background: transparent url("./layouts/img/avatar.png") left center no-repeat;
            top: 0;
            right: 90px;
            padding-left: 35px;
            span {
                text-align: center;
                color: #fff;
                line-height: @header-height;
            }
        }

        .logout {
            position: absolute;
            right: 0;
            top: 0;
            font-size: 16px;
            color: #BDDDFF;
            width: 72px;
            height: @header-height;
            background-color: #0489ca;
            padding:24px 28px;

            &:hover {
                color: #fff;
                background-color: #028fd5;
            }
        }

    }

    .page-content-wrapper {
        margin: 0 auto;
        width: 1280px;
        padding: 20px;
    }
</style>


