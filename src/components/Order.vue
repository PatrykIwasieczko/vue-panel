<template>
    <div class="card">
        <div class="patient">
            <h3>Dane pacjenta:</h3>
            <p>Imię: {{ order.patient.name }}</p>
            <p>Nazwisko: {{ order.patient.lastName }}</p>
            <p>PESEL: {{ order.patient.pesel }}</p>
        </div>
        <div class="medicine">
            <h3>Lek:</h3>
            <p>Nazwa leku: {{ order.medicine }}</p>
            <p>Czas podania: {{ order.applicationTime }}</p>
            <p>Ilość: {{ order.quantity }}</p>
            <p>Data: {{ order.date }}</p>
            <p>Oddział: {{ order.department }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "Order",
    props: ["order"],
};
</script>

<style scoped>
.card {
    margin: 2rem auto 0 auto;
    padding: 1rem;
    border: 1px solid #666;
    border-radius: 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 2rem;
}

.patient,
.medicine {
    display: flex;
    flex-direction: column;
    justify-content: start;
}

@media screen and (max-width: 600px) {
    .card {
        grid-template-columns: 1fr;
    }

    .patient,
    .medicine {
        margin: 0 auto;
    }
}
</style>
