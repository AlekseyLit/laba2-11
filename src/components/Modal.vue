<template>
	<div class="overlay">
        <div class="modal">
            <div class="modalClose" @click="$emit('closeModal')">
                <i class="fas fa-times"></i>
            </div>
            <form @submit.prevent class="modalForm">
                <div class="modalForm__element">
                    <label for="description">Описание</label>
                    <input type="text" id="description"
                           v-model="newTask.description" />
                </div>
                <div class="modalForm__element">
                    <label for="priority">Приоритет</label>
                    <select name="priority" id="priority" v-model="newTask.priority">
                        <option v-for="index in 3"
                                :key="index"
                                :selected="index === priority"
                                :value="index">
                                {{ index }}
                        </option>
                    </select>
                </div>
                <button class="button" :disabled="!(newTask.description && newTask.priority)"
                        @click="$emit('submitModal', {
                                    priority: newTask.priority,
                                    description: newTask.description,
                                })">
                    Сохранить
                </button>
            </form>
        </div>
	</div>
</template>

<script>
    export default {
        name: "Modal",
        data() {
            return {
                index: 0,
                newTask: {
                    description: "",
                    priority: 0
                }
            };
        },
        /*mounted(): вызывается после того как окно создалось*/
        mounted() {
            this.newTask.priority = this.priority || 0;
            this.newTask.description = this.description || "";
        },
        /*Параметр props хранит массив свойств, которым извне можно передать значения*/
        props: {
            priority: Number,
            description: String
        }
    };
</script>

<style>
	.overlay {
		position: fixed;
		left: 0;
		top: 0;
		width: 100vw;
		height: 100vh;
		background: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
        z-index: 100;
	}
	.modal {
        background: #fff;
        width:240px;height:240px;
        display: flex;
        flex-direction: column;
        align-items: center;
        position:relative;
        padding:30px;
	}
    .modalClose {
        position:absolute;
        top:0;right:5px;
        font-size:25px;
        cursor:pointer;
    }
    .modalForm {
        width:100%;
        font-size:18px;
    }
    .modalForm label {
        display:block;
        margin-bottom:10px;
    }
    .modalForm input, .modalForm input:active, .modalForm input:focus {
        padding:4px 0;
        width:100%;
        border: none;
        border-bottom: 1px solid #000;
        outline:none;
        font-size:18px;
    }

    .modalForm select, .modalForm select:active, .modalForm select:focus {
        width:100%;
        padding:4px 0;
        border: none;
        border-bottom: 1px solid #000;
        outline:none;
        font-size:18px;
    }
    .modalForm__element {
        margin-bottom:20px;
    }
</style>