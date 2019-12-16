<template>
    <div id="board">
        <header>
            <div style="width: 200px">
                <b-input class="mx-4 sm title" 
                v-model="title"
                :value='title'></b-input>
            </div>
        </header>
        <b-container fluid class="mx-4 text-left">
            <b-row>
                <div v-for="(list, index) in lists" :key="index" class="list-wrapper"> 
                    <div class="header text-left d-flex flex-row">
                        <!-- <h3> {{ list.title }} </h3> -->
                        <b-input
                            class="list-header"
                            v-model="list.title"
                            :value="list.title"> </b-input>
                        <b-dropdown variant="light" no-caret>
                            <template v-slot:button-content>
                                <font-awesome-icon 
                                class="fa-icon fa-ellipsis-h" icon="ellipsis-h"></font-awesome-icon>
                            </template>
                            <b-dropdown-item href="#">Action</b-dropdown-item>
                            <b-dropdown-item href="#">Another action</b-dropdown-item>
                            <b-dropdown-item href="#">Something else here</b-dropdown-item>
                        </b-dropdown>
                    </div>
                    <div class="list-content">
                            <draggable v-model="list.card" group="list" @start="drag=true" @end="drag=false">
                                <p class="card-list my-2" v-for="(cardList, index2) in list.cards" :key="index2">
                                    {{ cardList.title }}
                                </p>
                            </draggable>
                    </div>
                    <AddNewList 
                        inputText="Enter a title for this card"
                        :index = "index"
                        btnType='card'
                        :buttonText="list.cards.length > 0 ? 'Add another card' : 'Add card'"
                        v-on:addNewCard="addNewCard" 
                        class="list-wrapper mt-3">
                    </AddNewList>
                </div>
                <b-col cols="3">
                    <AddNewList 
                        inputText="Enter List title"
                        btnType='list'
                        :buttonText="lists.length > 0 ? 'Add another list' : 'Add list'"
                        v-on:addNewList="addNewList" class="list-wrapper"></AddNewList>
                </b-col>
            </b-row>
        </b-container>
    </div>

    <!-- <div class="container-fluid position-relative mt-5">
        <div id="board">
            <div class="list-wrapper" v-for="(list, index) in lists" :key="index">
                <div class="list list-content" >
                    <b-card :title="list.title" sub-title="Card subtitle">
                        <b-card-text>
                        Some quick example text to build on the <em>card title</em> and make up the bulk of the card's
                        content.
                        </b-card-text>
                    </b-card>
                </div>
            </div>
            <AddNewList v-on:addNewList="addNewList" class="list-wrapper"> </AddNewList>

        </div>
    </div> -->
</template>

<script>

import AddNewList from './sub-components/AddNewList';
import draggable from 'vuedraggable';

export default {
    components: {
        AddNewList,
        draggable
    },
    data() {
        return {
            title: 'My Todo List',
            lists: [
                { title: "Test", cards: []}
            ],
            people: [
                'Dee',
                'Dee3',
                'Dee4',
                'Dee5'
            ]
        }
    },
    watch: {
    },
    methods: {
        /* eslint-disable no-console */
        addNewList(input) {
            this.lists.push({
                title: input,
                cards: []
            })
        },
        addNewCard(input, index) {
            this.lists[index]
                .cards.push(
                    {
                        title: input
                    }
                )
        }
    }
}


</script>

<style scoped>

header .title{
    font-size: 1.2em;
    border-color: #fff; 
    font-weight:bold;
    cursor: pointer;
    margin: 10px;
}

header .title:hover:not(:focus) {
    background-color: rgb(235, 235, 235)
}

.list-wrapper:not(:last-child) {
    width: 272px !important;
    margin: 0 4px;
    height: 100%;
    background-color: #eeeeee;
    padding: 10px;
}

.header h3 {
    font-size: 16px;
    font-weight: bold;
}

.list-header {
    background-color: #eee;
    border-color: #eee;
}

.list-header:focus {
    background-color: rgb(255, 255, 255);
    border-color: rgb(255, 255, 255);
}

.list-content .card-list{
    text-align: left;
    background-color: #fff;
    padding: 8px;
    box-shadow: 0px 0px 1px #eee;
    font-size: 14px;
    cursor: pointer;
}

.list-content .card-list:hover {
    background-color: rgb(248, 248, 248);
}

/* 
#board {
    user-select: none;
    white-space: nowrap;
    margin-bottom: 8px;
    overflow-x: auto;
    overflow-y: hidden;
    padding-bottom: 8px;
    position: absolute;
    width: 100%;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}

.list-wrapper {
    width: 272px;
    margin: 0 4px;
    height: 100%;
    box-sizing: border-box;
    display: inline-block;
    vertical-align: top;
    white-space: nowrap;
}

.list-wrapper:first-child {
    margin-left: 8px;
}

.list {
    background-color: #ebecf0;
    border-radius: 3px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    max-height: 100%;
    position: relative;
    white-space: normal;
}
.list-content {
    
} */
</style>