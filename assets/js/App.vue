<template>
    <v-app id="inspire">
        <v-navigation-drawer
                fixed
                v-model="drawer"
                app
        >
            <v-list dense>
                <v-list-tile
                        v-for="item in routes"
                        :key="item.title"
                        :to="item.path"
                >
                    <v-list-tile-action>
                        <v-icon>{{ item.icon }}</v-icon>
                    </v-list-tile-action>
                    <v-badge color="red" v-if="item.badge">
                        <span slot="badge">{{ item.badge }}</span>
                        <span>{{ item.name }}</span>
                    </v-badge>
                    <v-list-tile-content v-else>{{ item.name }}</v-list-tile-content>
                </v-list-tile>
            </v-list>
        </v-navigation-drawer>
        <v-toolbar color="indigo" dark fixed app>
            <v-toolbar-side-icon @click.stop="drawer = !drawer"/>
            <v-toolbar-title>PHP Test Go</v-toolbar-title>
        </v-toolbar>
        <v-content>
            <v-container fluid fill-height>
                <v-layout>
                    <router-view/>
                </v-layout>
            </v-container>
        </v-content>
        <v-footer color="indigo" dark app>
            <span class="white--text">&copy; <a href="https://github.com/TheRatG/phptestgo" target="_blank">TheRatG</a> {{ new Date().getFullYear() }}</span>
            <v-fab-transition>
                <v-btn
                        fab
                        dark
                        fixed
                        bottom
                        right
                        color="red"
                        v-scroll="onScroll"
                        v-show="fab"
                        @click="toTop"
                >
                    <v-icon>keyboard_arrow_up</v-icon>
                </v-btn>
            </v-fab-transition>
        </v-footer>
    </v-app>
</template>

<script>
    export default {
        data: () => ({
            fab: false,
            drawer: null,
            routes: []
        }),
        props: {
            source: String
        },
        created() {
            this.$router.options.routes.forEach(route => {
                this.routes.push(route)
            });
        },
        mounted() {
            this.onScroll()
        },
        methods: {
            onScroll() {
                if (typeof window === 'undefined') {
                    return;
                }
                const top = window.pageYOffset
                    || document.documentElement.offsetTop
                    || 0;
                this.fab = top > 300
            },
            toTop() {
                window.scrollTo(0, 0)
            }
        }
    }
</script>

<style scoped>

</style>