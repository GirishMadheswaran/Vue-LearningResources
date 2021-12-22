<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately atleast one input value is invalid</p>
            <p>Please check all inputs whether you entered atleast 1 characters</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="titleInput" v-model="title1"/>
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <input id="description" name="description" rows="3" ref="descInput" v-model="description1"/>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="linkInput" v-model="link1"/>
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';
import BaseDialog from './UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
    inject:['addResource'],
    data(){
        return{
            inputIsInvalid:false,
            title1:"",
            description1:"",
            link1:""
        }
    },
    methods:{
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;
            this.title1 = '';
            this.description1 = '';
            this.link1 = '';

            if(enteredTitle === '' || enteredDescription === '' || enteredLink === '' ){
                this.inputIsInvalid = true;
                return;
            }
            this.addResource(enteredTitle,enteredDescription,enteredLink)
        },
        confirmError(){
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
    .form-control{
        margin: 1rem 0;
    }
    input:focus,
    textarea:focus{
        outline: none;
        border-color: #3a0061;
        background-color: #f7ebff;
    }
    input,textarea{
        display: block;
        width: 100%;
        padding: 0.15rem;
        border: 1px solid black;
    }
    label{
        font-weight: bold;
        display: block;
        margin-bottom: 0.5rem;
    }
</style>