<template>
    <div>
        <div class="student-profile" :class="{ show: !isExpanded, hide: isExpanded}">
            <button class="expand-btn expand-btn-plus" @click="toggleExpand"></button>
            <img class="student-profile__image" :src="pic" alt="student profile pic">
            <div class="student-profile__group">
                <h1 class="student-profile__group__header">{{ firstName }} {{ lastName }}</h1>
                <div class="student-profile__group__info">
                    <p class="student-profile__group__info__item">Email: {{ email }}</p>
                    <p class="student-profile__group__info__item">Company: {{ company }}</p>
                    <p class="student-profile__group__info__item">Skill: {{ skill }}</p>
                    <p class="student-profile__group__info__item">Average: {{ calculateAverage() }}</p>
                </div>
            </div>
        </div>

        <div class="student-profile" :class="{ show: isExpanded, hide: !isExpanded}">
            <button class="expand-btn expand-btn-minus" @click="toggleExpand"></button>
            <img class="student-profile__image" :src="pic" alt="student profile pic">
            <div class="student-profile__group">
                <h1 class="student-profile__group__header">{{ firstName }} {{ lastName }}</h1>
                <div class="student-profile__group__info">
                    <p class="student-profile__group__info__item">Email: {{ email }}</p>
                    <p class="student-profile__group__info__item">Company: {{ company }}</p>
                    <p class="student-profile__group__info__item">Skill: {{ skill }}</p>
                    <p class="student-profile__group__info__item">Average: {{ calculateAverage() }}</p>
                    <ul class="student-profile__group__info__item__grades" 
                    v-for="(grade, index) in grades"
                    :key="index + grade">
                        <li >
                            Test {{ index + 1}}:    {{ Math.floor(Number(grade))}}%
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        props: [
            'student', 'isShowing'
        ],
        data() {
            return {
                firstName: this.student.firstName,
                lastName: this.student.lastName,
                email: this.student.email,
                company: this.student.company,
                skill: this.student.skill,
                pic: this.student.pic,
                grades: this.student.grades,
                isExpanded: false
            }
        },
        methods: {
            calculateAverage() {
                let sumOfGrades = 0
                for(let i = 0; i < this.grades.length; i++) {
                    sumOfGrades += Number(this.grades[i])
                }
                return (sumOfGrades / this.grades.length).toFixed(2)
            },
            showInfo() {
                
            },
            toggleExpand() {
                this.isExpanded = !this.isExpanded
            }
        }
    }
</script>

<style scoped>
    .student-profile {
        display: flex;
        justify-content: left;
        padding: 0;
        margin: 4px 0;
    }

    .student-profile__group {
        margin: 0 2rem;
        text-align: left;
        width: 60%;
    }

    .student-profile__image {
        margin-left: 1.5rem;
        margin-right: .5rem;
        border: 1px solid lightgrey;
        border-radius: 100%;
        height: 120px;
        width: 120px;
        image-rendering: auto;
        image-resolution: initial;
    }

    .student-profile__group__header {
        letter-spacing: 2px;
        text-transform: uppercase;
    }

    .student-profile__group__info {
        color: grey;
        margin-left: 1rem;
    }

    .student-profile__group__info__item {
        color: grey;
        margin: .5rem;
    }   

    .student-profile__group__info__item__grades {
        list-style: none;
        padding: 0;
        margin: 0;
        margin-left: 1rem;
    }

    .student-profile__group__info__item__grades li {
        padding: 0;
        margin: 5px 0;
    }

    .show {
        display: flex;
    }

    .hide {
        display: none;
    }

    .expand-btn {
        background-position: center;
        background-repeat: no-repeat;
        background-size: auto;
        height: 50px;
        width: 50px;
        order: 2;
        border: none;
        transition: all 0.3s;
    }

    .expand-btn:focus, .expand-btn:active {
        outline: 0;
        border: none;
    }

    .expand-btn-plus {
        background-image: url('../assets/plus-icon.svg');
    }

    .expand-btn-minus {
        background-image: url('../assets/minus-icon.svg');
    }
    
</style>
