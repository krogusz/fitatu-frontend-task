<template>
    <div class="page employees-list">
        <h1 class="employees-list__header">Employees</h1>
        <div v-if="loading" class="employees-list__loading">Loading...</div>
        <table v-else class="employees-list__list">
            <tr class="employees-list__list-header">
                <th>id</th>
                <th>Name</th>
                <th>Address</th>
                <th>Phone</th>
                <th>Email</th>
                <th>Editing</th>
            </tr>
            <tr v-for="employee in employees" class="employees-list__list-row">
                <td>{{employee.id}}</td>

                <td v-if="employee.id === edit"><input type = "text" name = "name" @input="updateEditElem" v-bind:value="employee.name"> </td> 
                <td v-else>{{employee.name}}</td>

                <td v-if="employee.id === edit">
                    <input type = "text" name = "street" @input="updateEditElem" :value="employee.address.street">
                    <input type = "text" name = "suite" @input="updateEditElem" :value="employee.address.suite">
                    <input type = "text" name = "city" @input="updateEditElem" :value="employee.address.city">
                </td> 
                <td v-else>{{employee.address.street}} {{employee.address.suite}} {{employee.address.city}}</td>

                <td v-if="employee.id === edit"><input type = "text" name = "phone" @input="updateEditElem" :value="employee.phone"></td> 
                <td v-else>{{employee.phone}}</td>

                <td v-if="employee.id === edit"><input type= "text" name = "email" @input="updateEditElem" :value="employee.email"></td> 
                <td v-else><a :href="`mailto:${ employee.email }`">{{employee.email}}</a></td>

                <td v-if="employee.id === edit"><input type="button" value="save" v-on:click= "save_row(employee.id)"> <input type="button" value="reject" v-on:click= "reject_row(employee.id)"></td>
                <td v-else><input type="button" value="edit"  v-on:click= "edit_row(employee.id)"></td>

            </tr>
        </table>
    </div>
</template>
<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                loading: false,
                employees: [],
                edit: -1,
                editedElem: {},
            }
        },
        created () {
            this.fetchData()
        },
        watch: {
            '$route': 'fetchData'
        },
        methods: {
            updateEditElem({type, target}){
                target.name === "street" || target.name === "suite" || target.name === "city" ? this.editedElem.address[target.name] = target.value : this.editedElem[target.name] = target.value ;
           },

            edit_row (a){
                this.edit = a;
                this.editedElem = JSON.parse(JSON.stringify(this.employees[a-1]));
            },

            save_row (a){
                this.employees[a-1] = this.editedElem;
               
                fetch(`https://jsonplaceholder.typicode.com/users/${a}`, {
                    method: 'PATCH',
                    body: JSON.stringify(this.employees[a-1]),
                    headers: {"Content-type": "application/json; charset=UTF-8"}
                })
                .then( response => {
                    this.editedElem = {};
                    this.edit =-1;
                    
                });

                
            },

            reject_row (a){
                this.edit=-1;
            },


            fetchData () {
                this.loading = true;

                axios.get('https://jsonplaceholder.typicode.com/users')
                    .then(({data}) => {
                        this.employees = data;
                    })
                    .finally(() => {
                        this.loading = false;
                    })
            }
        }
    };

</script>
<style lang="scss" scoped>
    .employees-list {
        &__header {
            font-size: 20px;
            padding: 0 0 10px;
        }

        &__loading {
            color: #999d9d;
            text-align: center;
        }

        &__list {
            font-size: 14px;
            width: 100%;
            border-collapse: collapse;
        }

        &__list-header {
            background: #f7f8f9;
            border-bottom: 1px solid #999d9d;

            th {
                padding: 8px;
            }
        }

        &__list-row {
            background: #fff;

            td {
                padding: 8px;
            }
        }
    }
</style>