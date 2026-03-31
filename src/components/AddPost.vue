<template>
    <form @submit.prevent="createPost" :class="{error: maxCharacters > 20}"> 
        <label for="title">Назва Статті:</label>
        <input 
        v-model="state.userTitleInput" 
        type="text" 
        placeholder="Введіть текст" 
        id="title"/>
        <label for="text">Основний текст: <span>{{ maxCharacters }} /20</span></label>
        <textarea
         v-model="state.userTextInput"
          id="text" 
          placeholder="Введіть текст" 
          ></textarea>
        <button>Додати</button>
    </form>
</template>

<script>
import {reactive, computed} from 'vue';

export default {
    name: "AddPost",

    setup(props, ctx) {
        const state = reactive({
            userTitleInput: "",
            userTextInput: "",
        });

        const maxCharacters = computed(() => state.userTextInput.length);

        const createPost = () => {
               if (state.userTitleInput !== "" && state.userTextInput !== "") {
                 ctx.emit('add-post', state.userTitleInput, state.userTextInput);
                    
                    state.userTitleInput = "";
                    state.userTextInput = "";
        }
        };

        return {
            state,
            maxCharacters,
            createPost,
        }
    },


};
</script>

<style scoped>
   form {
        margin-top: 20px;
    }

form label {
        color: #505050;
    }
 form.error label {
        color: rgb(230, 31, 31);
    }

   form input,
   form textarea {
        width: 100%;
        background: #c6c391;
        border-radius: 5px;
        border: 2px solid #5e5b21;
        padding: 8px 10px;
        font-size: 14px;
        color: #5e5b21;
        outline: none;
        margin-bottom: 10px;
        margin-bottom: 10px;
        resize: none;
    }

aside form button {
    float: right;
    background: #aaa771;
    border: 2px solid #5e5b21;
    border-bottom-width: 4px;
    padding: 10px 12px;
    font-size: 13px;
    font-weight: bold;
    color: #5e5b21;
    border-radius: 5px;
    cursor: pointer;
}
aside form button:hover {
    margin-top: 2px;
    border-width: 2px;
    transition: all 400ms ease;
}

</style>
