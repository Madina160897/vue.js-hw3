<script>
export default {
    data() {
        return {
            posts: [],
            title: '',
            postBlock: '',
            isElementText: true,
            editId: "",
            editTitle: "",
            editPost: "",
            isElementStyle: true,
            editStyle: "",

            styleObject: {
                color: "black",
                background: "#f4f7f7",
                fontFamily: "Times New Roman",
                fontSize: "25px",
                fontStyle: "normal"
            }
        }
    },
    methods: {
        add() {
            if (this.title === '' || this.postBlock === '') {
                return
            }
            const newPost = {
                id: this.posts.length + 1,
                title: this.title,
                postBlock: this.postBlock,
            }
            this.posts.push(newPost)
            this.title = '',
                this.postBlock = ''
        },
        hideText(id) {
            this.editId = id
            this.isElementText = !this.isElementText
        },
        savePost() {
            if (this.editTitle === '' || this.editPost === '') {
                return
            }
            let editNewPost = {
                id: this.editId,
                title: this.editTitle,
                postBlock: this.editPost,
            }
            this.posts = this.posts.map(post => {
                if (post.id == editNewPost.id) {
                    return editNewPost
                }
                return post
            })
            this.editTitle = '',
                this.editPost = ''
            this.isElementText = true
        },
        hideStyle(id) {
            this.editId = id
            this.isElementStyle = !this.isElementStyle
        },
        saveStyle() {
            if (this.activeColor == "" || this.activeBackgr == "" || this.fontFamily == "" || this.fontSize == "" || this.fontWeight == "") {
                return
            }
            let newStyle = {
                color: this.activeColor,
                background: this.activeBackgr,
                fontFamily: this.fontFamily,
                fontSize: this.fontSize + "px",
                fontStyle: this.fontStyle,
            }
            
            this.styleObject = newStyle

            this.isElementStyle = true
        }
    }
}
</script>

<template>
    <div>
        <form class="Post" @submit.prevent>
            <input :value="title" @input="title = $event.target.value" type="text" placeholder="Название поста">
            <textarea :value="postBlock" @input="postBlock = $event.target.value" cols="30" rows="10"
                placeholder="Пост"></textarea>
            <button class="btn" @click="add">Создать</button>
        </form>

        <div class="post-block" v-for="post in posts" :style="styleObject">
            <b>{{ post.title }}</b>
            <div class="text-block">{{ post.postBlock }}</div>
            <div class="btn-block">
                <button class="btn" @click="hideStyle(post.id)">Редактировать стиль</button>
                <button class="btn" @click="hideText(post.id)">Редактировать текст</button>
            </div>
        </div>

        <div class="post-block" v-if="!isElementText">
            <b>Редактировать текст</b>
            <input :value="editTitle" @input="editTitle = $event.target.value" type="text" placeholder="Название поста">
            <textarea :value="editPost" @input="editPost = $event.target.value" cols="30" rows="10"
                placeholder="Пост"></textarea>
            <button class="btn" @click="savePost">Сохранить</button>
        </div>

        <div class="post-block" v-if="!isElementStyle">
            <h1>Редактировать стиль</h1>
            <b>Цвет текста</b>
            <input class="color-bock" type="color" v-model="activeColor">
            <b>Цвет фона</b>
            <input class="color-bock" type="color" placeholder="цвет фона" v-model="activeBackgr">
            <b>Стиль шрифта</b>
            <input type="text" placeholder="шрифт" v-model="fontFamily">
            <b>Размер шрифта</b>
            <input type="text" placeholder="размер шрифта" v-model="fontSize">
            <b>Начертание шрифта (курсив, жирный)</b>
            <input type="text" placeholder="начертание шрифта" v-model="fontStyle">
            <button class="btn" @click="saveStyle">Изменить</button>
        </div>
    </div>
</template>

<style scoped>
.Post {
    display: flex;
    flex-direction: column;
    width: 400px;
    margin: 5% auto;
    border: 2px solid #2dcdd3;
    background-color: #f4f7f7;
    border-radius: 20px;
    padding: 5%;
    font-size: 16px;
}

input,
textarea {
    margin-bottom: 20px;
    padding: 10px;
    font-size: 16px;
    border: 2px solid #5c9ea1;
    background-color: #ffffff9c;
    border-radius: 15px;
}

.btn {
    align-self: flex-end;
    font-size: 16px;
    padding: 10px;
    border-radius: 10px;
    background-color: rgb(216, 216, 216);
    border: 1px solid transparent;
}

.post-block {
    display: flex;
    flex-direction: column;
    width: 400px;
    margin: 5% auto;
    border: 2px solid #2dcdd3;
    border-radius: 20px;
    padding: 5%;
}

b {
    text-align: center;
    margin-bottom: 10px;
    font-size: 20px;
}

.text-block {
    font-size: 20px;
    text-align: justify;
    border: 2px solid #2dcdd3;
    border-radius: 5px;
    background-color: white;
    padding: 20px;
}

.btn-block {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 15px;
}

.color-bock{
    width: 100px;
    height: 50px;
}
</style>