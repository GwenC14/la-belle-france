<template>
    <form id="app" class="CreateRegion">
        <h2>Ajouter un élément</h2>
        <div>
            <label for="new-region">
                <span>Ajouter une région</span>
                <input id="new-region" v-model="newRegion" type="text" name="newRegion" />
            </label>
        </div>
        <div>
            <label for="new-cheese">
                <span>Ajouter un fromage</span>
                <input id="new-cheese" v-model="valueCheese" type="text" name="newCheese" />
            </label>
            <button @click="moreCheese" :disabled="!isNotBlank(valueCheese)">+</button>

            <ul>
                <li v-for="(cheese, index) in newCheese" :key="cheese">
                    <p>{{cheese}}</p>
                    <button @click="deleteCheese($event, index)">Delete</button>
                </li>
            </ul>
        </div>
        <div>
            <label for="new-wine">
                <span>Ajouter un vin</span>
                <input id="new-wine" v-model="valueWine" type="text" name="newWine" />
            </label>
            <button @click="moreWine" :disabled="!isNotBlank(valueWine)">+</button>

            <ul>
                <li v-for="(wine, index) in newWine" :key="wine">
                    <p>{{wine}}</p>
                    <button @click="deleteWine($event, index)">Delete</button>
                </li>
            </ul>
        </div>
        <button @click="addRegion" :disabled="!isRegionValid()">Ajouter</button>
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

</style>