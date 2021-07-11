<template>
    <div class="kanbanColumn"
         @dragover.prevent="dragOver"
         @dragenter.prevent="dragEnter"
         @dragleave="dragLeave"
         @drop="drop($event, column)">
        <h3>{{title}} ({{countTask(column)}})</h3>

        <Task v-for="task in this.$parent.tasks.filter((task) => task.column === +column)"
              :task="task" :key=task.id
              :column="column"
              @change-column="changeColumn($event, task)"/>
    </div>
</template>

<script>
import Task from './Task';

export default {
    props: {
        title: String,
        column: String
    },

	components: {Task},

	methods: {
        countTask(column) {
            return this.$parent.tasks.filter((task) => {
                return task.column === +column;
            }).length;
        },

        changeColumn(e, task) {
            if ((task.column + e.direction) > 2) {
                this.$parent.tasks.splice(this.$parent.tasks.findIndex(el => el.id === task.id), 1);
            } else {
                task.column += e.direction;
            }
        },
        drop(e, column) {
            const itemId = parseInt(e.dataTransfer.getData("itemId"));
            for (let task in this.$parent.tasks) {
                if (this.$parent.tasks[task].id == +itemId) {
                    this.$parent.tasks[task].column = +column;
                }
            }
        },
        dragOver() {},
        dragEnter() {},
        dragLeave() {},
        dragEnd() {}
	}
};
</script>

<style>
    .kanbanColumn {
        background: #F9F9F9;
        margin: 0;
        padding: 20px 0;
        flex: 1 1 0px;
    }
    .kanbanColumn:nth-child(2) {
        margin: 0 20px;
    }
    .kanbanColumn h3 {
        text-align: center;
        margin-bottom: 20px;
    }
    .dark .kanbanColumn {
        background: #9594AA;
    }
</style>
