<template>
	<main>
		<Modal v-if="showModal" @closeModal="closeModal" @submitModal="createTask($event)" />

		<button class="button" @click="openModal">Создать задачу</button>

		<div class="kanbanBoard">
			<KanbanColumn column="0" title="План" />
			<KanbanColumn column="1" title="В работе" />
			<KanbanColumn column="2" title="Готово" />
		</div>
	</main>
</template>

<script>
    import KanbanColumn from './KanbanColumn';
    import Modal from './Modal';

    export default {
        name: 'Main',
        components: { Modal, KanbanColumn },
        data() {
            return {
                showModal: false,
				taskCounter: 0,
                tasks: []
            }
        },
        methods: {
            openModal() {
                this.showModal = true;
            },
            closeModal() {
                this.showModal = false;
            },
            createTask(task) {
                let time = new Date;
                time = `${time.getDate()}.${String((time.getMonth() + 1)).padStart(2, '0')}.${time.getFullYear()} ${String(time.getHours()).padStart(2, '0')}:${String(time.getMinutes()).padStart(2, '0')}:${String(time.getSeconds()).padStart(2, '0')}`;
                const newTask = {
                    id: this.taskCounter,
                    date: time,
                    description: task.description,
                    priority: task.priority,
                    column: 0
                };
                this.taskCounter++;
                this.tasks.push(newTask);
                this.showModal = false;
            }
        }
    };
</script>

<style>
    .button {
        box-shadow:inset 0px 1px 3px 0px #91b8b3;
        background:linear-gradient(to bottom, #768d87 5%, #6c7c7c 100%);
        background-color:#768d87;
        border-radius:5px;
        border:1px solid #566963;
        color:#ffffff;
        font-size:15px;
        font-weight:bold;
        padding:11px 23px;
        text-decoration:none;
        text-shadow:0px -1px 0px #2b665e;
    }
    .button:not(:disabled):hover {
        background:linear-gradient(to bottom, #6c7c7c 5%, #768d87 100%);
        background-color:#6c7c7c;
        cursor:pointer;
    }
    .button:disabled {
        opacity: 0.5;
    }
    .kanbanBoard {
        padding:40px 0;
        margin-top:40px;
        display:flex;
        justify-content:space-between;
		min-height:400px;
    }

    .dark .button {
        box-shadow:inset 0px 1px 0px 0px #ffffff;
        background:linear-gradient(to bottom, #f9f9f9 5%, #e9e9e9 100%);
        background-color:#f9f9f9;
        border-radius:6px;
        border:1px solid #dcdcdc;
        display:inline-block;
        color:#666666;
        font-size:15px;
        font-weight:bold;
        padding:11px 23px;
        text-decoration:none;
        text-shadow:none;
    }
    .dark .button:not(:disabled):hover {
        background:linear-gradient(to bottom, #e9e9e9 5%, #f9f9f9 100%);
        background-color:#e9e9e9;
    }
</style>
