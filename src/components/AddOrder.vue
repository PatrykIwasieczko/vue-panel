<template>
    <div class="container">
        <div class="errors" v-if="errors.length">
            <b>Popraw błędy w formularzu:</b>

            <ul>
                <li v-for="(error, index) in errors" :key="index">
                    {{ error }}
                </li>
            </ul>
        </div>

        <form @submit.prevent="checkForm">
            <select v-model="medicine">
                <option disabled :value="null">Wybierz lek</option>
                <option v-for="(medicine, index) of medicines" :key="index">{{
                    medicine
                }}</option>
            </select>
            <select v-model="applicationTime">
                <option disabled :value="null"
                    >Wybierz godzinę podania leku</option
                >
                <option
                    v-for="(applicationTime, index) of applicationTimes"
                    :key="index"
                    >{{ applicationTime }}</option
                >
            </select>
            <date-pick
                :inputAttributes="{
                    readonly: true,
                    placeholder: 'Data podania leku...',
                }"
                v-model="date"
                :displayFormat="'DD.MM.YYYY'"
            ></date-pick>
            <input
                type="number"
                min="1"
                v-model="quantity"
                name="quantity"
                placeholder="Ilość tabletek..."
            />
            <select v-model="department">
                <option disabled :value="null">Wybierz oddział</option>
                <option
                    v-for="(department, index) of departments"
                    :key="index"
                    >{{ department }}</option
                >
            </select>
            <input
                type="text"
                v-model="patient.name"
                name="patientName"
                placeholder="Imię pacjenta..."
            />
            <input
                type="text"
                v-model="patient.lastName"
                name="patientLastName"
                placeholder="Nazwisko pacjenta..."
            />
            <input
                type="number"
                v-model="patient.pesel"
                name="patientPesel"
                placeholder="PESEL pacjenta..."
            />
            <input type="submit" value="Stwórz" class="btn" />
        </form>
    </div>
</template>

<script>
import DatePick from "vue-date-pick";
import "vue-date-pick/dist/vueDatePick.css";
export default {
    name: "AddOrder",
    components: { DatePick },
    data() {
        return {
            medicines: [
                "Acodin",
                "Amlozek",
                "Karwedilol",
                "Paracetamol",
                "Sildenafil",
                "Tiamazol",
                "Tramal",
            ],
            applicationTimes: ["8:00", "15:00", "22:00"],
            departments: [
                "Choroby wewnętrzne",
                "Ginekologia",
                "Kardiologia",
                "Neurologia",
                "Pulmunologia",
                "Urologia",
            ],
            medicine: null,
            applicationTime: null,
            date: null,
            quantity: null,
            department: null,
            patient: {
                name: null,
                lastName: null,
                pesel: null,
            },
            errors: [],
        };
    },
    methods: {
        addOrder() {
            const newOrder = {
                medicine: this.medicine,
                applicationTime: this.applicationTime,
                date: this.date,
                quantity: this.quantity,
                department: this.department,
                patient: {
                    name: this.patient.name,
                    lastName: this.patient.lastName,
                    pesel: this.patient.pesel,
                },
            };
            this.$emit("add-order", newOrder);
            this.medicine = null;
            this.applicationTime = null;
            this.date = null;
            this.quantity = null;
            this.department = null;
            this.patient.name = null;
            this.patient.lastName = null;
            this.patient.pesel = null;
        },
        checkForm: function() {
            this.errors = [];

            if (!this.medicine) {
                this.errors.push("Wprowadź nazwę leku");
            }
            if (!this.applicationTime) {
                this.errors.push("Wprowadź godzinę podania leku");
            }
            if (!this.date) {
                this.errors.push("Wprowadź datę podania leku");
            }
            if (!this.quantity) {
                this.errors.push("Wprowadź ilość podawanego leku");
            }
            if (!this.department) {
                this.errors.push("Wprowadź oddział");
            }
            if (!this.patient.name) {
                this.errors.push("Wprowadź imię pacjenta");
            }
            if (!this.patient.lastName) {
                this.errors.push("Wprowadź nazwisko pacjenta");
            }
            if (!this.patient.pesel) {
                this.errors.push("Wprowadź PESEL pacjenta");
            } else if (this.patient.pesel.length !== 11) {
                this.errors.push("Numer PESEL powinien mieć 11 cyfr");
            }

            if (!this.errors.length) {
                this.addOrder();
            }
        },
    },
};
</script>

<style scoped>
.errors {
    margin: 0 0 2rem 0;
}
form {
    display: flex;
    flex-direction: column;
}
input,
select {
    padding: 5px;
}
::v-deep .vdpComponent.vdpWithInput > input {
    width: 100%;
    padding: 5px;
}
</style>
