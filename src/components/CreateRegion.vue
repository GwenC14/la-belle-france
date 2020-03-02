<template>
    <form id="app" class="CreateRegion">
        <h2>Ajouter un élément</h2>

        <label for="new-region">
            <span>Ajouter une région</span>
            <input id="new-region" v-model="newRegion" type="text" name="newRegion" />
        </label>

        <label for="new-cheese">
            <span>Ajouter un fromage</span>
            <input id="new-cheese" v-model="valueCheese" type="text" name="newCheese" />
            <button class="button more" @click="moreCheese" :disabled="!isNotBlank(valueCheese)">+</button>
        </label>

        <ul class="added-item-content">
            <li class="added-item" v-for="(cheese, index) in newCheese" :key="cheese">
                <p>{{cheese}}</p>
                <button class="button slim" @click="deleteCheese($event, index)">Delete</button>
            </li>
        </ul>

        <label for="new-wine">
            <span>Ajouter un vin</span>
            <input id="new-wine" v-model="valueWine" type="text" name="newWine" />
            <button class="button more" @click="moreWine" :disabled="!isNotBlank(valueWine)">+</button>
        </label>

        <ul class="added-item-content">
            <li class="added-item" v-for="(wine, index) in newWine" :key="wine">
                <p>{{wine}}</p>
                <button class="button slim" @click="deleteWine($event, index)">Delete</button>
            </li>
        </ul>

        <button class="button important" @click="addRegion" :disabled="!isRegionValid()">Ajouter</button>
    </form>
</template>

<script>
    export default {
        name: "CreateRegion",

        data() {
            return {
                newRegion: '',
                newCheese: [],
                newWine: [],
                valueCheese: '',
                valueWine: ''
            }
        },

        methods: {
            addRegion(e) {
                e.preventDefault();
                let updateRegion = {};
                updateRegion.name = this.newRegion;
                updateRegion.wineList = this.newWine;
                updateRegion.cheeseList = this.newCheese;
                this.newRegion = '';
                this.newCheese = [];
                this.newWine = [];
                this.$emit('add-new-region', updateRegion);
            },

            moreCheese(e) {
                e.preventDefault();
                this.newCheese.push(this.valueCheese);
                this.valueCheese = '';
            },

            deleteCheese(e, index) {
                e.preventDefault();
                this.newCheese.splice(index, 1);
            },

            moreWine(e) {
                e.preventDefault();
                this.newWine.push(this.valueWine);
                this.valueWine = '';
            },

            deleteWine(e, index) {
                e.preventDefault();
                this.newWine.splice(index, 1);
            },

            isRegionValid() {
                return this.newRegion.trim().length > 0 && ( this.newCheese.length > 0 || this.newWine.length > 0 );
            },

            isNotBlank(inputValue) {
                return inputValue.trim().length > 0;
            }
        },
    }
</script>

<style scoped>

    label {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 50%;
        height: 40px;
        border: 1px solid darkslategray;
        margin-bottom: 10px;
        padding-left: 15px;
        border-radius: 30px;
    }

    label span {
        width: 25%;
    }

    input[type=text] {
        border: none;
        flex: 2;
        height: 100%;
        padding: 5px 0;
        background:  none;
    }

    input[type=text]:focus {
        outline: none;
    }

    h2 {
        margin-bottom: 25px;
    }

    .button.more {
        border: none;
        color: darkslategray;
        background-color: #ecf0f3;
        height: 100%;
        font-size: 21px;
        padding: 0;
        min-width: 60px;
        border-radius: 0 30px 30px 0 ;
    }

    .CreateRegion {
        margin-top: 50px !important;
    }

    .added-item {
        display: flex;
        align-items: center;
        margin-bottom: 5px;
    }

    .added-item:last-child {
        margin-bottom: 20px;
    }

    .added-item p {
        margin-right: 10px;
    }

    .added-item-content {
        padding-left: 20px;
    }

</style>