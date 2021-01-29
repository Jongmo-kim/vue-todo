<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer">
            <i class="fas fa-plus addBtn" v-on:click="addTodo"  @click="showModal = true" id="showModal"></i>
        </span>
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고
                <i class="fas fa-times closeModalBtn" @click="showModal = false"></i>
            </h3>
            <h4 slot="body">값이 입력되지 않았습니다.</h4>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal'
import {mapMutations} from 'vuex'

export default {
    data(){
        return {
            newTodoItem: "",
            showModal : false
        }
    },
    methods: {
        addTodo(){
            if (this.newTodoItem !== '') {
                this.$store.commit('addOneItem',this.newTodoItem);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newTodoItem = '';

        },
    },
        components:{
            Modal
        }
}
</script>

<style scoped>

    input:focus{
        outline: none;
    }
    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;   
    }
    .inputBox input{
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer{
        float:right;
        background: linear-gradient(to right, #6478FB,#8763FB);
        display:block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn{
        color: white;
        vertical-align: middle;
    } 
    .closeModalBtn { 
        color: #42b983;
    }
</style>