<template>
    <div class="sushi-block">
      <img
          :src="image"
          alt="Sushi"
          class="sushi-block__image"
      />
      <h4 class="sushi-block__title">{{ title }}</h4>
      <div class="sushi-block__ingredients">{{ ingredients }}</div>
      <div class="sushi-block__bottom" @click="addToCart()">
        <div class="sushi-block__price">от {{ price }} ₽</div>
        <div class="button button--outline button--add">
          <svg
              fill="none"
              height="12"
              viewBox="0 0 12 12"
              width="12"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M10.8 4.8H7.2V1.2C7.2 0.5373 6.6627 0 6 0C5.3373 0 4.8 0.5373 4.8 1.2V4.8H1.2C0.5373 4.8 0 5.3373 0 6C0 6.6627 0.5373 7.2 1.2 7.2H4.8V10.8C4.8 11.4627 5.3373 12 6 12C6.6627 12 7.2 11.4627 7.2 10.8V7.2H10.8C11.4627 7.2 12 6.6627 12 6C12 5.3373 11.4627 4.8 10.8 4.8Z"
                fill="white"
            />
          </svg>
          <span>Добавить</span>
          <i v-if="count">{{ count }}</i>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { computed, ref } from 'vue'
  import useCart from '../composables/useCart'
  
  export default {
    props: {
      id: Number,
      title: String,
      price: Number,
      image: String,
      ingredients: String,
    },
  
    setup (props) {
      const { addSushi, getCountForId } = useCart()
  
      const addToCart = () => {
        addSushi({
          id: props.id,
          price: props.price,
        })
      }
  
      const count = computed(() => getCountForId(props.id))
  
      return {
        addToCart,
        count
      }
    }
  }
  </script>