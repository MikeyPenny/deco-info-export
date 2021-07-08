<template>

    <b-form inline>
        <div class="row-form">
            <div class="input-label"><div class="numbers">1</div> First select your importsheet: </div>
            <b-form-select
                class="input-select"
                id="select-sheet"
                v-model="sheet"
                :options="sheets"
                required
            ></b-form-select>
        </div>
        <div class="row-form">
            <div class="input-label"><div class="numbers">2</div> Then which brands you would like?: </div>
            <b-form-select
                class="input-select"
                id="select-brand"
                v-model="selected"
                :options="brands"
                @change="onChangeSelector()"
                required
            ></b-form-select>
        </div>

        <div class="row-form">
            <div class="input-label"><div class="numbers">3</div> Name your download: </div>
                <b-form-input
                class="input-select"
                id="download-name"
                v-model="name"
                type="text"
                placeholder="Name your download"
                required
                ></b-form-input>
        </div>
        
        <div class="row-form button-row">
            <Button class="btn-reset" text="Reset" btnType="outline-primary" @click:option="onReset" />
            <Button class="btn-fill" text="Fill my sheet" btnType="primary" @click:option="onSubmit" />
        </div>
        
        
    </b-form>

</template>

<script>

import Button from './UI/Button.vue'


export default {
    name: 'DataSelector',
    data() {
        return {
            sheet: '',
            selected: '',
            name: '',
            
        }
    },
    props: [
        'sheets',
        'brands',
        'products'
    ],
    components: {
        Button,
    },
    methods: {
        onSubmit() {
            const data = {
                id: this.sheet,
                export_name: this.name,
                selected_brands: this.products
            }
            console.log(data)
        },
        onReset() {
            console.log('Reset')
            this.sheet = ''
            this.selected = ''
            this.name = ''
        },
        onChangeSelector() {
            this.$emit('change:select', this.selected)
        },
        // onChangeNameHandler(ev) {
        //     this.name = ev.target.value
        // }
    }
}    
</script>

<style scoped>
    .row-form {
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        width: 100%;
        margin-bottom: 20px;
    }
    .input-label {
        display: flex;
        align-items: center;
        width: 40%;
        padding: 2px;
        box-sizing: border-box;
        font-size: 15px;
    }
    .input-select {
        width: 60%;
    }
    .numbers {
        width: 10%;
        
        background-color: #070b60;
        border-radius: 50%;
        color: #fff;
        margin-right: 10px;
    }
    .button-row {
        justify-content: flex-end;
    }
    .btn-fill {
        margin-left: 30px;
        background-color: #070b60;
    }
    .btn-reset {
        border-color: #070b60;
        color: #070b60;
    }
</style>