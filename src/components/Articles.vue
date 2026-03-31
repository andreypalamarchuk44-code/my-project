<template>
<main>
    <div v-if="articles.length > 0" id="articles">
    <div class="post" v-for="el in articles" :key="el.id">
    <button @click="deletePost(el.id)">Видалити</button>
    <h2>{{ el.title }}</h2>
    <p>{{ el.text }}</p>
</div>
</div>
    <h1 class="empty" v-else>Статей більше немає</h1>
</main>
<aside>
    <AddPost v-on:add-post="createPost" />

</aside>
</template>

<script>
import AddPost from './AddPost.vue';


export default {
    name: "Articles",
    components: {
        AddPost,
    },
    data() {
        return {
        
            articles: [
                {
                    id: 1,
                    title: "Google buy Apple",
                    text : "Ldsfsdfcsdfsdfdsfdsfdsf"
                },
                   {
                    id: 2,
                    title: "Microsoft kills Minecraft",
                    text : "Ldsfsdfcsdfsdfdsfdsfdsf"
                },
                   {
                    id: 3,
                    title: "Testing article",
                    text : "Ldsfsdfcsdfsdfdsfdsfdsf"
                },
                   {
                    id: 4,
                    title: "Tesla is now phone company",
                    text : "Ldsfsdfcsdfsdfdsfdsfdsf"
                },
            ],
        };
    },
methods: {
    deletePost(id) {
        this.articles = this.articles.filter((el) => el.id !== id)
    },
    createPost(userTitleInput, userTextInput) {
                this.articles.unshift({
                id: Math.random() * 1000,
                title: userTitleInput,
                text: userTextInput,
            });
    },
},
};

</script>

<style scoped>
main {
    float: left;
    width: 60%;
}
aside {
    float: left;
    width: 20%;
    margin-left: 10%;
}

#articles {
    margin: 20px;
}
#articles .post {
    background: #c6c391;
    padding: 20px;
    margin-bottom: 20px;
    border: 1px solid #aaa771;
    color: #5e5b21;
    float: left;
    width: 100%;
}
#articles .post button {
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
#articles .post button:hover {
    margin-top: 2px;
    border-width: 2px;
    transition: all 400ms ease;
}
.empty {
     margin: 20px;
     color: orange;
    }

 
</style>