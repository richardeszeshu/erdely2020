<template>
    <div class="card" v-if="isVisible">
        <header class="card-header">
            <p class="card-header-title">
                {{ name }}
            </p>
            <a v-on:click="toggleDescription(this)" class="card-header-icon" aria-label="more options">
                <span class="icon">
                    <i class="fas fa-angle-down" aria-hidden="true"></i>
                </span>
            </a>
        </header>
        <div class="card-content">
            <div class="content">
                {{ description }}
            </div>
        </div>
        <footer class="card-footer has-text-centered">
            <div class="card-footer-item">
                <span class="tag is-danger" v-if="required">Kötelező</span>
                <span class="tag is-dark" v-else>Opcionális</span>
            </div>
            <div class="card-footer-item">
                <span class="tag is-info" v-if="type" v-text="type"></span>
            </div>
            <div class="card-footer-item">
                <label class="checkbox">
                    <input type="checkbox" v-on:change="toggleDoneAttr">
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
        "name",
        "description",
        "required",
        "type",
        "hideIfDone"
    ],
    computed: {
        id() {
            var hash = 0, i, chr, len;
            if (this.name.length === 0) return hash;
            for (i = 0, len = this.name.length; i < len; i++) {
                chr   = this.name.charCodeAt(i);
                hash  = ((hash << 5) - hash) + chr;
                hash |= 0; // Convert to 32bit integer
            }
            return hash;
        },
        isDone: {
            get() {
                return localStorage.getItem(this.id) ? true : false
            },

            set(value) {
                localStorage.setItem(this.id, value);
            }
        },
        isVisible() {
            if (this.hideIfDone) {
                return this.isDone ? false : true;
            }
            return true;
        }
    },
    methods: {
        toggleDescription() {
            console.log('clicked:');
        },
        toggleDoneAttr() {
            this.isDone = this.isDone === true ? false : true;
        }
    }
}
</script>

<style scoped>
.card {
    margin-bottom: 15px;
}
</style>