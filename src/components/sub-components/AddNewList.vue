<template>
    <div class="text-left">
        <b-button 
            v-show="!isToggled"
            @click="isToggled = !isToggled"
            class="addListBtn text-left">
            <font-awesome-icon 
                class="fa-icon" icon="plus"></font-awesome-icon>
                {{ buttonText }}
        </b-button>
        
        <div class="mt-2 list-div" :style="{ display: isToggled ? 'block' : 'none'}">
            <b-input 
                @keyup.enter="addList"
                v-model="input"
                size="sm" 
                :placeholder="inputText"></b-input>
            <div class="list-buttons">
                <b-button
                    :disabled="input == ''" 
                    @click="addList"
                    size="sm" class="mr-2 mt-2"> 
                    Add {{ btnType }} 
                </b-button>   
                <font-awesome-icon 
                    @click="isToggled = !isToggled, input = ''"
                    class="fa-icon fa-times" icon="times"></font-awesome-icon>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        index: Number,
        inputText: String,
        buttonText: String,
        btnType: String
    },
    data() {
        return {
            isToggled: false,
            input: ""
        }
    },
    methods: {
        addList() {
            if (this.btnType == 'card') {
                this.$emit('addNewCard', this.input, this.index);
                this.input = "";
                this.isToggled = false;

                return;
            }

            this.$emit('addNewList', this.input);
            this.input = "";
            this.isToggled = false;

            return;
        }
    }
}
</script>

<style scoped>
.addListBtn {
    width: 224px;
    font-size: 14px;
}

.list-buttons {
    position: relative;
}

.fa-times {
    position: relative;
    left: 15px;
    top: 5px;
}
</style>