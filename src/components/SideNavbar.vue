<script setup>
import {useRouter} from "vue-router";
import authAPI from "../utils/api/AuthAPI.js";
import {useLocalStorage} from "@vueuse/core";
import {onMounted, ref} from "vue";
import {CheckModuleVisibility} from "../utils/CheckModuleVisibility.js";

const router = useRouter();
const getRoleCode = ref(null);

async function handleLogout() {
    await authAPI.logout();
    const userProfile = useLocalStorage('user_profile', '');
    const userToken = useLocalStorage('user_token', '');

    userProfile.value = '';
    userToken.value = '';
    await router.push('/');
}

function handleGetRoleCode() {
    const userProfile = useLocalStorage('user_profile', null);
    getRoleCode.value = JSON.parse(userProfile.value).role.code ?? null;
}

onMounted(() => {
    handleGetRoleCode();
})
</script>

<template>
    <nav class="uk-card uk-card-body uk-height-viewport sidebar-nav">
        <div class="nav-logo">
            <img src="../assets/images/logo_pkm_botim.png" />
        </div>

        <ul class="uk-nav uk-nav-default nav-list" uk-nav>
            <li v-if="CheckModuleVisibility.dashboard.roles.includes(getRoleCode)">
                <router-link to="/admin">
                    <span class="las la-home"></span> Dashboard
                </router-link>
            </li>

            <li v-if="CheckModuleVisibility.patientVisitor.roles.includes(getRoleCode)">
                <router-link :to="{name: 'list-visitor-patient'}">
                    <span class="las la-clipboard"></span> Kunjungan Pasien
                </router-link>
            </li>

            <li v-if="CheckModuleVisibility.patient.roles.includes(getRoleCode)">
                <router-link :to="{name: 'list-patients'}">
                    <span class="las la-user"></span> Daftar Pasien
                </router-link>
            </li>

            <li v-if="CheckModuleVisibility.reports.roles.includes(getRoleCode)">
                <router-link :to="{name: 'reports'}">
                    <span class="las la-poll"></span> Laporan
                </router-link>
            </li>

            <li class="uk-parent"
            v-if="
            CheckModuleVisibility.masterData.user.roles.includes(getRoleCode) ||
            CheckModuleVisibility.masterData.klaster.roles.includes(getRoleCode) ||
            CheckModuleVisibility.masterData.spesimen.roles.includes(getRoleCode) ||
            CheckModuleVisibility.masterData.metodePembayaran.roles.includes(getRoleCode)">
                <a href="#">
                    <span class="las la-database"></span> Master Data <span uk-nav-parent-icon></span>
                </a>
                <ul class="uk-nav-sub">
                    <li>
                        <router-link :to="{name: 'list-user'}">
                            User
                        </router-link>
                    </li>
                    <li>
                        <router-link :to="{name: 'list-klaster'}">
                            Klaster
                        </router-link>
                    </li>
                    <li>
                        <router-link :to="{name: 'list-spesimen'}">
                            Spesimen
                        </router-link>
                    </li>
                    <li>
                        <router-link :to="{name: 'list-metode-pembayaran'}">
                            Metode Pembayaran
                        </router-link>
                    </li>
                </ul>
            </li>

            <li>
                <a href="#" @click="handleLogout()">
                    <span class="las la-sign-out-alt"></span> Logout
                </a>
            </li>
        </ul>
    </nav>
</template>

<style scoped>

</style>