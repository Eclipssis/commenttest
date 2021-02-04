<template>
  <div class="product">
    <div class="product__header">
      <h2 class="product__title">{{ product.title }}</h2>
      <button class="btn">Сменить этап подбора</button>
    </div>

    <div class="product__body">
      <form>
        <input 
          v-model="commentText" 
          class="product__input" 
          placeholder="Написать комментарий"
          @focus="isOpenControls = true"
          @blur="onBlurInput"
        >

        <div class="comment-controls" :class="{open: isOpenControls}">
          <button 
            type="submit" 
            class="btn btn-blue"
            :class="{disabled: commentText.length === 0}"
            @click.prevent="onSaveComment"
          >
            Сохранить
          </button>
          <button class="btn btn-white" @click="onCancelComment">Отмена</button>
        </div>
      </form>
    </div>
    

    <div v-for="comment in product.commentsList" :key="comment.id">
      <Comment 
        :data="comment" 
        @onDeleteComment="onDeleteComment" 
        @onEditComment="onEditComment" 
      />
    </div>
    
  </div>
</template>

<script>

import Comment from "@/components/Comment.vue";

export default {
  name: "Product",

  components: {
    Comment
  },

  data() {
    return {
      currentUser: {
        name: 'Ольга Солошенко'
      },

      commentText: '',
      isOpenControls: false,

      product: {
        id: 576,
        title: 'Продукт А',
        commentsList: [
          {
            id: 1,
            text: 'тест коммент',
            author: {
              name: 'Ольга Солошенко',
              date: '11 Июля'
            }
          },
          {
            id: 2,
            text: 'тест коммент 2',
            author: {
              name: 'Ольга Солошенко',
              date: '13 Июля'
            }
          }
        ] 
      }
    }
  },

  methods: {
    onSaveComment() {
      const comment = {
        id: Math.floor(Math.random() * 10000) + 1,
        text: this.commentText,
        author: {
          name: this.currentUser.name,
          date: `${new Date().getDay()} Июля` // Should be formatted by moment
        }
      }

      this.product.commentsList.unshift(comment)
      this.commentText = ''
    },

    onEditComment (comment) {
      const index = this.product.commentsList.findIndex(item => item.id === comment.id)
      this.product.commentsList.splice(index, 1, comment)
    },

    onCancelComment () {
      this.commentText = ''
      this.isOpenControls = false
    },

    onDeleteComment (id) {
      const index = this.product.commentsList.findIndex(item => item.id === id)
      this.product.commentsList.splice(index, 1)
    },

    onBlurInput () {
      setTimeout(() => {
        this.isOpenControls = false
      }, 150);
    }
  },
};
</script>

<style lang="scss" scoped>
.product {
  display: inline-block;
  min-width: 550px;
  text-align: left;
  background: #fffbe8;
  padding: 20px 30px;
  border-left: 5px solid #63c969;
  border-radius: 5px;

  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
  }

  &__title {
    margin: 0;
    color: #63c969;
    font-weight: 400;
    padding-right: 15px;
  }

  &__body {
    padding: 10px 0;
    border-top: 1px solid #bbb;
    border-bottom: 1px solid #bbb;
  }

  &__input {
    height: 25px;
    border: none;
    background: none;
    font-size: 16px;
    &:focus {
      outline: none;
    }
  }
}

.comment-controls {
  display: none;
  margin-top: 15px;
  
  &.open {
    display: block;
  }
}
</style>