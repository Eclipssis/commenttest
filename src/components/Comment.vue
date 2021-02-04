<template>
  <div class="comment">
    
    <div v-if="isEditComment">
      <input 
        :value="changedCommentText" 
        @input="onChangeCommentText"
        class="comment__input"
      >

      <div class="comment-controls">
        <button 
          type="submit" 
          class="btn btn-blue"
          :class="{disabled: changedCommentText.length === 0}"
          @click.prevent="onSaveComment"
        >
          Сохранить
        </button>
        <button class="btn btn-white" @click="isEditComment = false">Отмена</button>
      </div>
    </div>
    
    <p v-else class="comment__text">{{ data.text }}</p>

    <div class="comment__author">
      <i class="user-icon"></i>
      <span class="comment__authorname">{{ data.author.name }},</span>
      <span class="comment__timestamp">{{ data.author.date }}</span>

      <Dropdown v-model="isDropDownOpen">
        <template v-slot:list>
          <button class="dropdown-item" @click="onEditComment">Редактировать</button>
          <button class="dropdown-item" @click="onOpenConfirmModal">Удалить</button>
        </template>
      </Dropdown>

      <!-- Modal should be a component! -->
      <div class="modal" :class="{open: isConfirmModalOpen}">
        <div class="modal__header">
          <h2 class="modal__title">Удаление комментария</h2>
        </div>
        
        <div class="modal__footer">
          <button class="btn btn-red dropdown-item--inline" @click="$emit('onDeleteComment', data.id)">Удалить</button>
          <button class="btn btn-white dropdown-item--inline" @click="isConfirmModalOpen = false">Отмена</button>
        </div>
      </div>
      <!-- Modal should be a component! -->

    </div>
  </div>
</template>

<script>
import Dropdown from '@/components/Dropdown.vue';

export default {
  name: "Comment",

  components: {
    Dropdown,
  },

  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },

  data() {
    return {
      changedCommentText: this.data.text,
      isDropDownOpen: false,
      isEditComment: false,
      isConfirmModalOpen: false,
    }
  },

  methods: {
    onOpenConfirmModal () {
      this.isConfirmModalOpen = true
      this.isDropDownOpen = false
    },

    onChangeCommentText(event) {
      this.changedCommentText = event.target.value
    },

    onEditComment() {
      this.isEditComment = true
      this.isDropDownOpen = false
    },

    onSaveComment() {
      this.isEditComment = false
      this.isDropDownOpen = false
      let comment = { ...this.data, text: this.changedCommentText }

      this.$emit('onEditComment', comment)
    }
  },
};
</script>

<style scoped lang="scss">

.comment {
  margin: 20px 0 10px;

  &__text {
    font-weight: 700;
    margin: 0 0 5px;
  }

  &__author {
    position: relative;
    display: flex;
    align-items: center;
    color: #a0a0a0;
  }

  &__authorname {
    display: inline-block;
    margin-left: 5px;
  }

  &__timestamp {
    display: inline-block;
    margin-left: 5px;
  }

  &__input {
    font-weight: 700;
    height: 15px;
    border: none;
    border-bottom: 1px solid #000;
    background: none;
    font-size: 16px;
    margin-bottom: 10px;
    &:hover {
      outline: none;
    }
  }
}

.comment-controls {
  margin-bottom: 10px;
}
</style>
