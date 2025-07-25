<script setup>
import {onMounted, reactive} from 'vue';
import {toastFailed, toastSuccess} from "../../utils/alerts.js";
import {useRouter} from "vue-router";
import patientAPI from "../../utils/api/Patient/PatientAPI.js";
import {datePickerOnlyDate} from "../../utils/datePickerUtil.js";
import CheckPermissionAccess from "../../utils/CheckPermissionAccess.js";

const formsInput = reactive({
    medical_number: '',
    fullname: '',
    address: '',
    dob: '',
    gender: 'L',
    phone_number: '',
    active: "1"
});
const router = useRouter();
const errorDetail = reactive({});

function onValidationForm() {
    errorDetail.medical_number = '';
    errorDetail.fullname = '';
    errorDetail.address = '';
    errorDetail.dob = '';
    errorDetail.phone_number = '';
    errorDetail.isError = false;

    if( formsInput.fullname === '' ) {
        errorDetail.fullname = 'Nama wajib diisi';
        errorDetail.isError = true;
    }

    if( formsInput.medical_number === '' ) {
        errorDetail.medical_number = 'Nomor rekam medis wajib diisi';
        errorDetail.isError = true;
    }

    if( formsInput.address === '' ) {
        errorDetail.address = 'Alamat wajib diisi';
        errorDetail.isError = true;
    }

    if( formsInput.dob === '' ) {
        errorDetail.dob = 'Tanggal lahir wajib diisi';
        errorDetail.isError = true;
    }
}

async function onHandleSubmit() {
    onValidationForm();

    if( errorDetail.isError === false) {
        const fetchApi = await patientAPI.create(formsInput);

        if( fetchApi.statusCode === 201 ) {
            toastSuccess(`Pasien dengan nomor rekam medis ${formsInput.medical_number} berhasil ditambahkan`);
            await router.push({ name: 'list-patients'});
        } else {
            toastFailed(fetchApi.data.message);
        }
    }
}

async function handleGetPermission() {
    if( CheckPermissionAccess('write') === false ) {
        await router.push({ name: 'list-patients'});
    }
}

onMounted(async() => {
    datePickerOnlyDate('#input-dob');
    handleGetPermission();
});
</script>

<template>
    <section class="form-section">
        <div class="form-header-title">Tambah Pasien</div>

        <div class="uk-form-stacked form-section-input">
            <form @submit.prevent="onHandleSubmit()">
                <div class="uk-margin">
                    <label for="input-medical-number" class="uk-form-label form-label form-label-required">Nomor Rekam Medis</label>
                    <div class="uk-form-controls">
                        <input type="text" class="uk-width-1-1 uk-input form-input" v-model="formsInput.medical_number"/>
                    </div>

                    <div v-if="errorDetail.medical_number !== ''" class="uk-text-danger">{{ errorDetail.medical_number }}</div>
                </div>

                <div class="uk-margin">
                    <label for="input-nama" class="uk-form-label form-label form-label-required">Nama</label>
                    <div class="uk-form-controls">
                        <input type="text" class="uk-width-1-1 uk-input form-input" v-model="formsInput.fullname"/>
                    </div>

                    <div v-if="errorDetail.fullname !== ''" class="uk-text-danger">{{ errorDetail.fullname }}</div>
                </div>

                <div class="uk-margin">
                    <label for="input-dob" class="uk-form-label form-label form-label-required">Tanggal Lahir</label>
                    <div class="uk-form-controls">
                        <input type="text" class="uk-width-1-1 uk-input form-input" id="input-dob" v-model="formsInput.dob"/>
                    </div>

                    <div v-if="errorDetail.dob !== ''" class="uk-text-danger">{{ errorDetail.dob }}</div>
                </div>

                <div class="uk-margin">
                    <label for="input-active" class="uk-form-label form-label form-label-required">Jenis Kelamin</label>
                    <div class="uk-form-controls">
                        <select class="uk-width-1-1 uk-select form-select" v-model="formsInput.gender" aria-label="Select">
                            <option value="L">Laki - Laki</option>
                            <option value="P">Perempuan</option>
                        </select>
                    </div>
                </div>

                <div class="uk-margin">
                    <label for="input-telepon" class="uk-form-label form-label">Nomor Telepon</label>
                    <div class="uk-form-controls">
                        <input type="text" class="uk-width-1-1 uk-input form-input" v-model="formsInput.phone_number" maxlength="15" />
                    </div>

                    <div v-if="errorDetail.phone_number !== ''" class="uk-text-danger">{{ errorDetail.phone_number }}</div>
                </div>

                <div class="uk-margin">
                    <label for="input-address" class="uk-form-label form-label form-label-required">Alamat</label>
                    <div class="uk-form-controls">
                        <textarea class="uk-width-1-1 uk-textarea form-input" v-model="formsInput.address"></textarea>
                    </div>

                    <div v-if="errorDetail.address !== ''" class="uk-text-danger">{{ errorDetail.address }}</div>
                </div>

                <div class="uk-margin">
                    <router-link :to="{ name: 'list-patients' }" class="uk-button uk-button-default uk-margin-small-right button button-default">
                        Kembali
                    </router-link>
                    <button class="uk-button uk-button-primary button button-primary">
                        Tambah
                    </button>
                </div>
            </form>
        </div>
    </section>
</template>

<style scoped>

</style>