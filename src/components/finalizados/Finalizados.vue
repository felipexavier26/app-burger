<template>
    <div id="burger-table">
        <table class="burger-table" v-if="filteredBurgers.length">
            <thead>
                <tr id="burger-table-heading">
                    <th class="order-id">#</th>
                    <th>Cliente</th>
                    <th>Pão</th>
                    <th>Carne</th>
                    <th>Bebidas</th>
                    <th>Opcionais</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr class="burger-table-row" v-for="burger in filteredBurgers" :key="burger.id">
                    <td class="order-number">{{ burger.id }}</td>
                    <td>{{ burger.nome }}</td>
                    <td>{{ burger.pao }}</td>
                    <td>{{ burger.carne }}</td>
                    <td>{{ burger.bebida }}</td>
                    <td>
                        <ul class="opcionais-list">
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
                        </ul>
                    </td>
                    <td>
                        <select name="status" class="status" v-if="burger.status === 'Finalizado'"
                            @change="updateBurger($event, burger.id)" disabled>
                            <option v-for="s in status" :key="s.id" :value="s.tipo"
                                :selected="burger.status === s.tipo">
                                {{ s.tipo }}
                            </option>
                        </select>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

export default {
    name: "Finalizados",
    data() {
        return {
            burgers: [],
            status: [],
            msg: null,
        };
    },

    computed: {
        filteredBurgers() {
            return this.burgers.filter(burger =>
                ["Finalizado"].includes(burger.status)
            );
        }
    },

    methods: {
        async getPedido() {
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();
            this.burgers = data;
            console.log(this.burgers);
        },

        async getStatus() {
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();
            this.status = data;
        },
    },

    mounted() {
        this.getPedido();
        this.getStatus();
    },
}

</script>

<style scoped>
.burger-table {
    width: 100%;
    border-collapse: collapse;
    margin: 0 auto;
    max-width: 1200px;
}

#burger-table-heading {
    font-weight: bold;
    background-color: #f2f2f2;
}

.burger-table th,
.burger-table td {
    border: 1px solid #ddd;
    padding: 12px;
    text-align: left;
}

.burger-table td {
    vertical-align: top;
}

.opcionais-list {
    margin: 0;
    padding-left: 20px;
    list-style-type: disc;
}

.select,
.status {
    padding: 8px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
}

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>