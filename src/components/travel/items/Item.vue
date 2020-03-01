<template>
    <div class="card" v-if="isVisible">
        <header class="card-header">
            <p class="card-header-title">
                {{ name }}
            </p>
            <a v-on:click="toggleDescription(this)" class="card-header-icon" aria-label="more options">
                <span class="icon">
                    <i v-bind:class="{ 'fa-angle-down': !isOpened, 'fa-angle-up': isOpened }" @click="toggleDescription" class="fas"  aria-hidden="true"></i>
                </span>
            </a>
        </header>
        <div class="card-content" v-if="isOpened">
            <div class="content">
                {{ description }}
            </div>
        </div>
        <footer class="card-footer has-text-centered" v-if="isOpened">
            <div class="card-footer-item">
                <span class="tag is-danger" v-if="required">Kötelező</span>
                <span class="tag is-dark" v-else>Opcionális</span>
            </div>
            <div class="card-footer-item">
                <span class="tag is-info" v-if="type" v-text="type"></span>
            </div>
            <div class="card-footer-item">
                <label class="checkbox">
                    <input type="checkbox" v-on:change="toggleDoneAttr" v-bind:checked="isDone">
                    Kész
                </label>
            </div>
        </footer>
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: [
        "uuid",
        "name",
        "description",
        "required",
        "type",
        "hideIfDone",
    ],
    data() {
        return {
            isDone: false,
            isOpened: false
        }
    },
    computed: {
        isVisible() {
            if (this.hideIfDone) {
                return !this.isDone;
            }
            return true;
        }
    },
    mounted() {
        if (localStorage.getItem(this.uuid) === "true") {
            this.isDone = true;
        }
    },
    watch: {
        isDone(newValue) {
            localStorage.setItem(this.uuid, newValue);
        }
    },
    methods: {
        toggleDescription() {
            this.isOpened = !this.isOpened;
        },
        toggleDoneAttr() {
            this.isDone = !this.isDone;
        }
    }
}
</script>

<style scoped>
.card {
    margin-bottom: 15px;
}
</style>