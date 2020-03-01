<template>
    <div class="container is-fluid">
        <h2 class="subtitle">Szükséges eszközök, iratok</h2>
        <div class="level">
            <div class="level-left">
                <div class="level-item">
                    <button v-on:click="toggleDoneItems" v-bind:class="{ 'is-danger': !hideIfItemIsDone, 'is-success': hideIfItemIsDone }"  class="button is-small">{{ btnHideDoneItemsText }}</button>
                </div>
            </div>
            <!--div class="level-right">
                <div class="level-item">
                    <button class="button is-dark is-small">Mind összecsuk</button>
                </div>
            </div-->
        </div>
        <Item v-for="item in items" :key="item" v-bind="item" v-bind:hideIfDone="hideIfItemIsDone"></Item>
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
            hideIfItemIsDone: false
        }
    },
    computed: {
        btnHideDoneItemsText() {
            if (this.hideIfItemIsDone) {
                return "Kész elemek mutatása";
            }

            return "Kész elemek elrejtése";
        }
    },
    methods: {
        toggleDoneItems() {
            this.hideIfItemIsDone = this.hideIfItemIsDone ? false : true;
        }
    }
}
</script>

<style scoped>
    .container {
        margin-top: 40px;
    }
</style>