<template>
    <div class="container is-fluid">
        <h1 class="title">Heó, heó, sziasztok!</h1>
        <div class="table-container">
            <table class="table is-fullwidth is-striped">
                <tr>
                    <th>Indulás:</th>
                    <td>{{ travel.startDate }}</td>
                </tr>
                <tr>
                    <th>Hazatérés:</th>
                    <td>{{ travel.endDate }}</td>
                </tr>
                <tr>
                    <th>Helszín:</th>
                    <td v-html="travel.location"></td>
                </tr>
                <tr>
                    <th>Távolság:</th>
                    <td>{{ travel.distance }} km</td>
                </tr>
                <tr>
                    <th>Menetidő:</th>
                    <td>{{ travel.travelTime }}</td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BaseData',
    props: [
        "travel",
    ]
}
</script>

<style scoped>
</style>