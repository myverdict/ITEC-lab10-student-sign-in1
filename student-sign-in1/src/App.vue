<template>
    <div id="app">
        <!-- add the 3 components here -->
        <new-student-form v-on:student-added="newStudentAdded"></new-student-form>

        <student-table v-bind:students="students"
                       v-on:student-arrived-or-left="studentArrivedOrLeft"></student-table>

        <student-message v-bind:student="mostRecentStudent"></student-message>
    </div>
</template>

<script>
    import NewStudentForm from "./components/NewStudentForm.vue";
    import StudentTable from "./components/StudentTable.vue";
    import StudentMessage from "./components/StudentMessage.vue";

    export default {
        name: 'App',
        components: {
            NewStudentForm,
            StudentTable,
            StudentMessage
        },
        data() {
            return {
                students: [],
                mostRecentStudent: {}
            }
        },
        methods: {
            newStudentAdded(student) {
                this.students.push(student);
                this.students.sort(function (s1, s2) {
                    return s1.name.toLowerCase() > s2.name.toLowerCase() ? 1 : -1;
                })
            },
            studentArrivedOrLeft(student, present) {
                // find student in this.students, set present value
                let updateStudent = this.students.find(function(s) {
                    if(s.name === student.name && s.starID === student.starID)
                    {
                        return true;
                    }
                })

                if(updateStudent)
                {
                    updateStudent.present = present;
                    this.mostRecentStudent = student;
                }
            }                       // end of studentArrivedOrLeft method in the methods section
        }                           // end of the methods section
    }
</script>

<style>

</style>
