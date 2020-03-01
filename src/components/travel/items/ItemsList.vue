<template>
    <div class="container is-fluid">
        <h2 class="subtitle">Szükséges eszközök, iratok</h2>
        <div class="level">
            <div class="level-left">
                <div class="level-item">
                    <button v-on:click="toggleDoneItems" v-bind:class="{ 'is-danger': !hideIfItemIsDone, 'is-success': hideIfItemIsDone }"  class="button is-small">{{ btnHideDoneItemsText }}</button>
                </div>
            </div>
            <div class="level-right">
                <div class="level-item">
                    <button v-on:click="toggleDescriptions" v-bind:class="{ 'is-info': !showDescriptions, 'is-dark': showDescriptions }" class="button is-small">{{ btnShowDescriptionsText }}</button>
                </div>
            </div>
        </div>
        <div class="columns is-multiline">
            <Item v-for="item in items" :key="item" v-bind="item" v-bind:hideIfDone="hideIfItemIsDone" ref="childComponent"></Item>
        </div>
    </div>
</template>

<script>
import Item from './Item.vue'

export default {
    name: 'ItemsList',
    components: {
        Item,
    },
    props: [
        "items",
    ],
    data() {
        return {
            hideIfItemIsDone: false,
            showDescriptions: false
        }
    },
    computed: {
        btnHideDoneItemsText() {
            if (this.hideIfItemIsDone) {
                return "Kész elemek mutatása";
            }

            return "Kész elemek elrejtése";
        },
        btnShowDescriptionsText() {
            if (this.showDescriptions) {
                return "Mind összecsuk";
            }
            
            return "Mind kinyit";
        }
    },
    methods: {
        toggleDoneItems() {
            this.hideIfItemIsDone = !this.hideIfItemIsDone;
        },
        toggleDescriptions() {
            this.showDescriptions = !this.showDescriptions;
        }
    },
    watch: {
        showDescriptions(newValue) {
            this.$refs.childComponent.forEach(function (el) {el.setDescriptionVisibility(newValue)});
        }
    }
}
</script>

<style scoped>
    .container {
        margin-top: 40px;
    }
</style>