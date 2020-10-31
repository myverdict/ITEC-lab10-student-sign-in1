<!--
    This is a child component. Its' job is to collect information about the new student,
    validate it and it will send an event to the parent App.vue.
    (Be a form, display a form, validate the form and send an event to the parent).
-->

<template>
    <div>
        <div class="alert alert-danger" v-show="errors.length > 0">
            <ul>
                <li v-for="error in errors" v-bind:key="error">
                    {{ error }}
                </li>
            </ul>
        </div>

        <div class="card add-student m-2 p-2">
            <h4 class="card-title">Add new student</h4>

            <div class="form-group">
                <label for="name">Name</label>
                <input id="name" class="form-control" v-model.trim="newStudentName">
            </div>

            <div class="form-group">
                <label for="starID">Star ID</label>
                <input id="starID" class="form-control" v-model.trim="newStarID">
            </div>

            <button class="btn btn-primary" v-on:click="addStudent">Add</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "NewStudentForm",
        data() {
            return {
                newStudentName: "",       // initial empty values for the student name
                newStarID: "",            // initial empty values for the student star id
                errors: []                // initial empty errors array
            }
        },
        methods: {
            addStudent() {
                this.errors = [];

                if(!this.newStudentName)
                {
                    this.errors.push("Student name is required.");
                }

                if(!this.newStarID)
                {
                    this.errors.push("Star ID is required.");
                }

                // Validate the student's name & starID are entered
                if(this.errors.length === 0)
                {
                    let student = { name: this.newStudentName, starID: this.newStarID, present: false };

                    // TODO emit message to parent App.vue with new student
                    this.$emit('student-added', student);

                    this.newStudentName = "";
                    this.newStarID = "";
                }
            },                // end of addStudent method in the methods section
        }                     // end of the methods section
    }
</script>

<style>

</style>