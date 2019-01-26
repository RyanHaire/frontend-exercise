<template>
    <div class="student-list-view">
        <StudentSearchBar :searchInput="findStudentByName" @searchInputChanged="searchInputChanged"/>
        <ul class="student-list" v-if="students && students.length">
            <li class="student-list-item" v-for="student in filteredStudents"
                :key="student.id">
                <Student 
                    :student="student" 
                    isShowing="isShowing"/>
            </li>
        </ul>
    </div>
</template>

<script>
    import Student from './Student.vue'
    import StudentSearchBar from './StudentSearchBar.vue'

    export default {
        components: {
            Student,
            StudentSearchBar
        },
        data() {    
            return  { 
                students: [],
                findStudentByName: ''
            }
        },
        computed: {
            filteredStudents() {
                let filter = new RegExp(this.findStudentByName, 'i')
                return this.students.filter(student => (student.firstName.match(filter) || student.lastName.match(filter)))
            }
        },
        methods: {
            findStudent(input) {
                this.findStudentByName = input
                console.log('studentListView (searchInput): ', this.findStudentByName)
            },
            searchInputChanged(input) {
                this.findStudentByName = input
            }
        },
        created () {
            fetch('https://www.hatchways.io/api/assessment/students')
            .then(result => {
                return result.json()
            }).then(result => {
                this.students = result.students;
            }).catch((error) => {
                console.log('error', error)
            })
        }
    }
</script>

<style scoped>
    .student-list-view {
        list-style: none;
        border-radius: 6px;
        width: 78%;
        height: 75vh;
        margin: 12.5vh auto;
        padding: 0;
        background: #fff;
        overflow: scroll;
        scroll-behavior: smooth;
        -webkit-overflow-scrolling: touch;
    }

    .student-list {
        list-style: none;
        padding: 0;
        height: auto;
        margin-top: 10px;
        width: 100%;
    }

    .student-list li:not(:last-child) {
        border-bottom: 1px solid lightgrey;
    }

 
</style>
