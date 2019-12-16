<template>
    <div class="header">
        <b-nav>
            <b-container class="text-left p-3 m-0" >
                <b-row>
                    <b-col>
                         <b-button>
                            <font-awesome-icon icon="home"/>
                         </b-button>
                         <b-button>
                            <font-awesome-icon icon="bookmark"/>
                            Boards
                         </b-button>

                         <b-btn-group>
                            <b-input
                                v-on:focus.native="onFocus"
                                v-on:blur.native="onBlur"
                                v-model="search"
                                :class="{ extend: isClicked }" class="search-form mb-2 mb-sm-0" 
                                placeholder="Search">
                            </b-input>
                             <font-awesome-icon 
                                v-show="!isClicked"
                                class="search_icon" 
                                icon="search"></font-awesome-icon>
                             <font-awesome-icon 
                                color="#000" 
                                v-show="isClicked" 
                                @click="clearSearch"
                                class="search_icon" icon="times"></font-awesome-icon>
                         </b-btn-group>
                    </b-col>
                    <b-col>
                        <span class="title"> Todos </span>
                    </b-col>
                </b-row>
            </b-container>
        </b-nav>
    </div> 
</template>
<script>
import '../module/fontAwesomeModule'

export default {
    data() {
        return {
            isClicked : false,
            search: ""
        }
    },
    computed: {
        
    },
    methods: {
        onFocus() {
            /* eslint-disable no-console */
            this.isClicked = true;
        },
        onBlur() {
            this.isClicked = false;
            this.clearSearch();
        },
        clearSearch() {
            this.search ="";
        }
    }
}
</script>
<style scoped>
.header {
    height: 60px;
    background-color: #000;
    color: #fff;
}

.header button {
    margin: 0px 5px;
}

.header button.search {
    width: 140px;
}

.search-form {
    width: 200px;
    display: inline-block;
    color: #fff;
    background-color: #6c757d;
    border-color: #6c757d;
    transition: .3s;
}

.search-form.extend {
    width: 300px;
}

.title {
    font-size: 20px;
}

.search_icon {
    position: absolute;
    top: 10px;
    right: 7px;
}
</style>