<template>
    <v-app id="inspire">
        <top-nav></top-nav>
        <v-main class="grey lighten-3 my-auto pt-10">
            <v-container>
                <v-row class="primary main-header-div">
                    <v-dialog v-model="logoutDialog" max-width="290">
                        <v-card>
                            <v-card-title class="">
                                Are you sure?
                            </v-card-title>
                            <v-card-text
                                >You will be logged out from your
                                account.</v-card-text
                            >
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn
                                    color="red darken-1"
                                    text
                                    @click="logout"
                                >
                                    Logout
                                </v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-dialog>
                    <v-col cols="12">
                        <div class="text-center">
                            <v-avatar size="100" class="avatar">
                                <img
                                    :src="require('../assets/logo.jpg')"
                                    alt=""
                                />
                            </v-avatar>
                            <div class="mt-10">
                                <template v-if="authenticated && user != null">
                                    <h3 class="profile-name">
                                        {{ user.name }}
                                    </h3>
                                    <p class="mb-0 profile-detail">
                                        {{ user.fav_team }} | {{ user.phone }}
                                    </p>
                                    <p class="mb-0 profile-detail">
                                        {{ user.region }}
                                    </p>
                                </template>
                                <v-btn
                                    v-if="authenticated"
                                    class="primary edit-profile-btn"
                                    >Edit Profile</v-btn
                                >
                                <v-btn
                                    v-else
                                    to="/login"
                                    class="primary edit-profile-btn"
                                    >Login Account</v-btn
                                >
                            </div>
                        </div>
                        <v-list color="mt-5 rounded" flat>
                            <v-list-item-group>
                                <v-list-item>
                                    <v-list-item-content>
                                        <v-list-item-title>
                                            <v-icon class="mr-3"
                                                >mdi-clipboard-text</v-icon
                                            >
                                            <span class="list-text"
                                                >Terms & Conditions</span
                                            >
                                        </v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                                <v-list-item>
                                    <v-list-item-content>
                                        <v-list-item-title>
                                            <v-icon class="mr-3"
                                                >mdi-help</v-icon
                                            >
                                            <span class="list-text"
                                                >Frequently Asked Question</span
                                            >
                                        </v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                                <v-list-item>
                                    <v-list-item-content>
                                        <v-list-item-title>
                                            <v-icon class="mr-3"
                                                >mdi-star</v-icon
                                            >
                                            <span class="list-text"
                                                >Give Us Feedbacks</span
                                            >
                                        </v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                                <v-list-item>
                                    <v-list-item-content>
                                        <v-list-item-title>
                                            <v-icon class="mr-3"
                                                >mdi-phone-in-talk</v-icon
                                            >
                                            <span class="list-text"
                                                >Contact Us</span
                                            >
                                        </v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                                <v-list-item
                                    @click="logoutDialog = true"
                                    v-if="authenticated"
                                >
                                    <v-list-item-content>
                                        <v-list-item-title>
                                            <v-icon class="mr-3"
                                                >mdi-exit-to-app</v-icon
                                            >
                                            <span class="list-text"
                                                >Logout</span
                                            >
                                        </v-list-item-title>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-list-item-group>
                        </v-list>
                    </v-col>
                </v-row>
            </v-container>
            <bottom-navigation></bottom-navigation>
        </v-main>
    </v-app>
</template>
<script>
import BottomNavigation from "../components/BottomNavigation.vue";
import TopNav from "../components/TopNav.vue";
import { mapGetters, mapActions } from "vuex";
export default {
    components: { TopNav, BottomNavigation },
    data: () => ({
        logoutDialog: false,
    }),
    computed: {
        ...mapGetters({
            authenticated: "auth/authenticated",
            user: "auth/user",
        }),
    },
    methods: {
        ...mapActions({
            logoutAction: "auth/Logout",
        }),
        logout() {
            this.logoutAction().then(() => {
                (this.logoutDialog = false),
                    this.$router
                        .replace({
                            name: "Setting",
                        })
                        .catch(() => {});
            });
        },
    },
};
</script>

<style scoped>
.main-header-div {
    max-height: 100px;
    border-radius: 0 0 20px 20px;
}

.avatar {
    display: absolute;
    border-radius: 100% !important;
    outline: 2px solid #fff;
    border: 3px solid #4c2fe3;
    top: 30px;
}

.profile-detail {
    font-size: 13px;
}

.edit-profile-btn {
    margin-top: 10px;
    font-size: 13px;
    letter-spacing: 1px;
    text-transform: capitalize;
}

.list-text {
    font-size: 15px;
    letter-spacing: 0.2px;
}
</style>