<template>
    <form @submit.prevent="handleSubmit" class="space-y-2">
        <input type="text" placeholder="No Induk Siswa" v-model="dataForm.nis"
            class="input input-bordered w-full max-w-full" />
        <input type="text" placeholder="Nama Siswa" v-model="dataForm.nama"
            class="input input-bordered w-full max-w-full" />
        <input type="number" placeholder="Nilai Siswa" v-model="dataForm.nilai"
            class="input input-bordered w-full max-w-full" />
        <button class="btn btn-success me-2" type="submit">SAVE</button>
        <button class="btn btn-outline btn-error" @click="handleReset" type="reset">CANCEL</button>
    </form>
</template>

<script>
export default {
    props: ['dataForm'],
    emits: ['submit'],
    methods: {
        handleSubmit(e) {
            this.$emit('submit', e)
        },
        handleReset(e) {
            // mengosongka semua data form
            for (const key in this.dataForm) {
                this.dataForm[key] = null
            }
        }
    }
}
</script>