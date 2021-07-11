<template>
	<div class="task" draggable="true" @dragstart="dragStart($event, task)">
        <Modal v-show="showModal" @closeModal="closeModal"
               :priority="task.priority" :description="task.description"
               @submitModal="editTask($event)" />
        <h4>{{ "Задача №" + (task.id + 1) }}</h4>
        <div class="taskPriority" :class="'taskPriority' + task.priority">{{ task.priority }}</div>
        <p>{{ task.description }}</p>
        <p>{{ task.date }}</p>
        <div class="taskButtons">
            <button v-show="+column > 0" class="buttonArrow" @click="changeColumn(-1)">
                <i class="fas fa-chevron-circle-left"></i>
            </button>
            <button class="button" @click="openModal">Edit</button>
            <button class="buttonArrow" @click="changeColumn(1)">
                <i v-if="+column == 2" class="fas fa-trash-alt"></i>
                <i v-else class="fas fa-chevron-circle-right"></i>
            </button>
        </div>
	</div>
</template>

<script>
    import Modal from './Modal';

    export default {
        name: "Task",
        components: { Modal },
        data() {
            return {
                showModal: false
            };
        },
        props: {
            task: Object,
            column: String
        },
        methods: {
            openModal() {
                this.showModal = true;
            },
            closeModal() {
                this.showModal = false;
            },
            editTask(newTask) {
                this.task.description = newTask.description;
                this.task.priority = newTask.priority;
                this.showModal = !this.showModal;
            },
            changeColumn(direction) {
                this.$emit("change-column", {
                    direction: direction,
                    task: this.task
                });
            },
            dragStart(e, task) {
                e.dataTransfer.dropEffect = "move";
                e.dataTransfer.effectAllowed = "move";
                e.dataTransfer.setData("itemId", task.id.toString());
            }
        }
    };
</script>

<style>
    .task {
        position:relative;
        padding:10px 20px;
        border-bottom:1px solid #333;
    }
    .taskPriority {
        position:absolute;
        top:10px;right:20px;
        border-radius: 50%;
        width:25px;height:25px;
        color:#333;
        text-align: center;
        font-size:16px;
        line-height: 25px;
    }
    .taskPriority1 {
        background: #ff253a;
    }
    .taskPriority2 {
        background: #fff709;
    }
    .taskPriority3 {
        background: #4ed04c;
    }
    .task h4 {
        margin-bottom:4px;
    }
    .task p {
        margin-bottom:8px;
    }
    .taskButtons {
        text-align: right;
    }
    .taskButtons button {
        border: none;
        font-size:16px;
        margin-left: 15px;
        cursor:pointer;
    }
    .buttonArrow {
        background: none;
    }
</style>
