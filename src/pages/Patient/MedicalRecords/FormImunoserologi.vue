<script setup>
const props = defineProps({
    formInput: Object,
});
</script>

<template>
    <h3>Imunoserologi</h3>

    <div class="form-section-input">
<!--        <table class="uk-table uk-table-small uk-table-divider uk-table-responsive uk-table-middle table-input-lab">-->
<!--            <thead>-->
<!--                <tr>-->
<!--                    <th class="uk-width-small">Pemeriksaan</th>-->
<!--                    <th class="uk-width-medium">Nilai</th>-->
<!--                    <th class="uk-width-small">Satuan</th>-->
<!--                    <th class="uk-width-small">Nilai Normal</th>-->
<!--                </tr>-->
<!--            </thead>-->

<!--            <tbody v-for="(rowsItem, rowsIndex) in props.formInput.sub" :key="`sub-${rowsItem.value}-${rowsIndex}`">-->
<!--                <tr>-->
<!--                    <th>{{ rowsItem.name }}</th>-->
<!--                </tr>-->

<!--                <tr v-if="rowsItem.multiple === true && Array.isArray(rowsItem.option)" v-for="(columnInput, columIndex) in rowsItem.option" :key="`sub-${columnInput.label}-${columIndex}`">-->
<!--                    <td>{{ columnInput.label }}</td>-->
<!--                    <td>-->
<!--                        <select v-if="Array.isArray(columnInput.option)" class="uk-select form-select form-select-small" v-model="columnInput.hasil">-->
<!--                            <option value="">Pilih Nilai</option>-->
<!--                            <option v-for="item in columnInput.option" :key="item" :value="item">{{ item }}</option>-->
<!--                        </select>-->

<!--                        <input v-else type="text" class="uk-input form-input form-input-small" v-model="columnInput.hasil" placeholder="Masukkan nilai" />-->

<!--                        <div v-if="columnInput.label === 'VDRL' && columnInput.hasil === 'Reaktif'" class="uk-margin-small-top">-->
<!--                            <input type="text" class="uk-input form-input form-input-small" v-model="columnInput.titer" placeholder="Masukkan titer" />-->
<!--                        </div>-->

<!--                        <div v-if="rowsItem.value === 'widal' && columnInput.hasil === 'Positif'" class="uk-margin-small-top">-->
<!--                            <input type="text" class="uk-input form-input form-input-small" v-model="columnInput.titer" placeholder="Masukkan titer" />-->
<!--                        </div>-->
<!--                    </td>-->
<!--                    <td>{{ columnInput.satuan }}</td>-->
<!--                    <td>{{ columnInput.nilai_normal }}</td>-->
<!--                </tr>-->

<!--                <tr v-else>-->
<!--                    <td>{{ rowsItem.name }}</td>-->
<!--                    <td>-->
<!--                        <select class="uk-select form-select form-select-small" v-model="rowsItem.hasil">-->
<!--                            <option value="">Pilih Nilai</option>-->
<!--                            <option v-for="item in rowsItem.option" :key="item" :value="item">{{ item }}</option>-->
<!--                        </select>-->
<!--                    </td>-->
<!--                    <td>{{ rowsItem.satuan }}</td>-->
<!--                    <td>{{ rowsItem.nilai_normal }}</td>-->
<!--                </tr>-->
<!--            </tbody>-->
<!--        </table>-->

        <!-- input imunoserologi -->
        <div class="uk-card uk-card-default uk-card-body card-form-input">
            <table class="uk-table uk-table-small uk-table-middle uk-table-responsive uk-table-justify table-input-lab">
                <thead>
                    <tr>
                        <th class="uk-width-medium">Imunoserologi</th>
                        <th class="uk-width-small">Nilai</th>
                        <th class="uk-width-small">Satuan</th>
                        <th class="uk-width-small">Nilai Normal</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Golongan Darah</td>
                        <td>
                            <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="props.formInput.golongan_darah.hasil">
                                <option value="">Pilih Nilai</option>
                                <option v-for="item in props.formInput.golongan_darah.option" :key="item" :value="item">{{ item }}</option>
                            </select>
                        </td>
                        <td></td>
                        <td>{{ props.formInput.golongan_darah.nilai_normal }}</td>
                    </tr>

                    <tr>
                        <td>Rhesus</td>
                        <td>
                            <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="props.formInput.rhesus.hasil">
                                <option value="">Pilih Nilai</option>
                                <option v-for="item in props.formInput.rhesus.option" :key="item" :value="item">{{ item }}</option>
                            </select>

                            <div v-if="props.formInput.rhesus.hasOwnProperty('note') && (props.formInput.rhesus.hasil !== 'Negatif' && props.formInput.rhesus.hasil !== '')" class="uk-margin-small-top">
                                <input type="text" class="uk-input form-input form-input-small" v-model="props.formInput.rhesus.note" placeholder="Masukkan catatan" />
                            </div>
                        </td>
                        <td></td>
                        <td>{{ props.formInput.rhesus.nilai_normal }}</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- input hiv -->
        <div class="uk-card uk-card-default uk-card-body card-form-input">
            <table class="uk-table uk-table-small uk-table-middle uk-table-responsive uk-table-justify table-input-lab">
                <thead>
                    <tr>
                        <th class="uk-width-medium">HIV</th>
                        <th class="uk-width-small">Nilai</th>
                        <th class="uk-width-small">Satuan</th>
                        <th class="uk-width-small">Nilai Normal</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(column, index) in props.formInput.hiv" :key="`hiv_${index}`">
                        <td>{{ column.label }}</td>
                        <td>
                            <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="column.hasil">
                                <option value="">Pilih Nilai</option>
                                <option v-for="item in column.option" :key="item" :value="item">{{ item }}</option>
                            </select>

                            <div v-if="column.hasOwnProperty('note') && column.hasil === 'Reaktif'" class="uk-margin-small-top">
                                <input  type="text" class="uk-input form-input form-input-small" v-model="column.note" placeholder="Masukkan keterangan" />
                            </div>
                        </td>
                        <td></td>
                        <td>{{ column.nilai_normal }}</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- input sifilis -->
        <div class="uk-card uk-card-default uk-card-body card-form-input">
            <table class="uk-table uk-table-small uk-table-middle uk-table-responsive uk-table-justify table-input-lab">
                <thead>
                <tr>
                    <th class="uk-width-medium">Sifilis</th>
                    <th class="uk-width-small">Nilai</th>
                    <th class="uk-width-small">Satuan</th>
                    <th class="uk-width-small">Nilai Normal</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(column, index) in props.formInput.sifilis" :key="`hiv_${index}`">
                    <td>{{ column.label }}</td>
                    <td>
                        <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="column.hasil">
                            <option value="">Pilih Nilai</option>
                            <option v-for="item in column.option" :key="item" :value="item">{{ item }}</option>
                        </select>

                        <div v-if="column.hasOwnProperty('titer') && column.hasil === 'Reaktif'" class="uk-margin-small-top">
                            <input type="text" class="uk-width-1-1 uk-input form-input form-input-small" v-model="column.titer" placeholder="Masukkan nilai titer" />
                        </div>

                        <div v-if="column.hasOwnProperty('note') && column.hasil === 'Positif'" class="uk-margin-small-top">
                            <input type="text" class="uk-width-1-1 uk-input form-input form-input-small" v-model="column.note" placeholder="Masukkan keterangan" />
                        </div>
                    </td>
                    <td></td>
                    <td>{{ column.nilai_normal }}</td>
                </tr>
                </tbody>
            </table>
        </div>

        <!-- input hepatitis -->
        <div class="uk-card uk-card-default uk-card-body card-form-input">
            <table class="uk-table uk-table-small uk-table-middle uk-table-responsive uk-table-justify table-input-lab">
                <thead>
                    <tr>
                        <th class="uk-width-medium">Hepatitis</th>
                        <th class="uk-width-small">Nilai</th>
                        <th class="uk-width-small">Satuan</th>
                        <th class="uk-width-small">Nilai Normal</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(column, index) in props.formInput.hepatitis" :key="`hiv_${index}`">
                        <td>{{ column.label }}</td>
                        <td>
                            <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="column.hasil">
                                <option value="">Pilih Nilai</option>
                                <option v-for="item in column.option" :key="item" :value="item">{{ item }}</option>
                            </select>

                            <div v-if="column.hasOwnProperty('note') && column.hasil === 'Positif'" class="uk-margin-small-top">
                                <input type="text" class="uk-width-1-1 uk-input form-input form-input-small" v-model="column.note" placeholder="Masukkan keterangan" />
                            </div>
                        </td>
                        <td></td>
                        <td>{{ column.nilai_normal }}</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- input widal -->
        <div class="uk-card uk-card-default uk-card-body card-form-input">
            <table class="uk-table uk-table-small uk-table-middle uk-table-responsive uk-table-justify table-input-lab">
                <thead>
                    <tr>
                        <th class="uk-width-medium">Widal</th>
                        <th class="uk-width-small">Nilai</th>
                        <th class="uk-width-small">Satuan</th>
                        <th class="uk-width-small">Nilai Normal</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(column, index) in props.formInput.widal" :key="`widal_${index}`">
                        <td v-html="column.label"></td>
                        <td>
                            <select class="uk-width-1-1 uk-select form-select form-select-small" v-model="column.hasil">
                                <option value="">Pilih Nilai</option>
                                <option v-for="item in column.option" :key="item" :value="item">{{ item }}</option>
                            </select>

                            <!-- jika nilai positif, tampilkan input titer -->
                            <input v-if="column.hasil === 'Positif'" type="text" class="uk-width-1-1 uk-margin-small-top uk-input form-input form-input-small" v-model="column.titer" placeholder="Masukkan nilai titer" />
                        </td>
                        <td></td>
                        <td>{{ column.nilai_normal }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<style scoped>

</style>