<template>
    <div>
        <div class="card student-list m-2 p-2">
            <h4 class="card-title">Student List</h4>

            <div id="student-table">
                <table class="table">
                    <tr>
                        <th>Name</th>
                        <th>StarID</th>
                        <th>Present?</th>
                    </tr>

                    <tr v-for="student in students"
                        v-bind:key="student.starID"
                        v-bind:class="student.present ? 'present' : 'absent'">

                        <td>{{ student.name }}</td>
                        <td>{{ student.starID }}</td>
                        <td><input type="checkbox" v-on:change="arrivedOrLeft(student, $event.srcElement.checked)"></td>

                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "StudentTable",
        props: {
            students: Array
        },
        methods: {
            arrivedOrLeft(student, present) {
                // TODO emit message to parent App.vue
                this.$emit('student-arrived-or-left', student, present)
            }
        }
    }
</script>

<style scoped>
    .present { color: grey; font-style: italic; }
    .absent { color: black; font-weight: bold; }
</style>