<script setup lang="ts">
</script>

<script lang="ts">

export default {
    data() {
        return {
            item: '',
            items: []
        }
    },
    methods: {
        async search(e: Event) { this.items = (await (await fetch(`https://api.nal.usda.gov/fdc/v1/foods/search?api_key=Lk3iBc7LT1vWeyRuRPrlof9n639DqmLkyd8ROLUv&query=${this.item}`)).json())['foods']; }
    }
}
</script>

<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <div class="navbar-brand fw-bold">Kitchen</div>
            <button class="btn btn-danger fw-bold">Log Out</button>
        </div>
    </nav>
    <div class="container-fluid p-3">
        <div class="card">
            <div class="card-body">
                <label class="form-label fw-bold">Select Food/Drink:</label>
                <input v-model="item" @input="search" list="food/drink" class="form-control">
                <datalist id="food/drink">
                    <option v-for="item in items">{{ item['description'] }}</option>
                </datalist>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
