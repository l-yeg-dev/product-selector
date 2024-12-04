<template>
  <div class="container">
    <div class="container_header">
      <div class="container_header_item-container">
        <div class="container_header_item-container_items">
          <div
              v-for="item in selectedUserItems"
              :key="item.id"
              class="container_header_item-container_items_item"
          >
            {{ item.name }}
          </div>
        </div>
        <div class="container_header_item-container_selected">Selected {{ selectedUserItems.length }} / 6</div>
      </div>
      <div class="container_header_item-container">
        <div
            class="container_header_item-container_item"
            :class="{ selected: selectedChoiceItem }"
        >
          {{ selectedChoiceItem?.name || 'No Item Selected' }}
        </div>
      </div>
    </div>
    <div class="container_body">
      <div class="container_body_items">
        <div
            v-for="item in userItems"
            :key="item.id"
            class="container_body_items_item"
        >
          <div
              class="container_body_items_item"
              :class="{ selected: selectedUserItems.includes(item) }"
              @click="toggleUserItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="container_body_items">
        <div
            v-for="item in choiceItems"
            :key="item.id"
            class="container_body_items_item"
            :class="{ selected: selectedChoiceItem && selectedChoiceItem.id === item.id }"
            @click="selectChoiceItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductSelector",
  data() {
    return {
      userItems: [
        { id: 1, name: 'Shoes 1' },
        { id: 2, name: 'Shoes 2' },
        { id: 3, name: 'Shoes 3' },
        { id: 4, name: 'Shoes 4' },
        { id: 5, name: 'T-shirt 1' },
        { id: 6, name: 'T-shirt 2' },
        { id: 7, name: 'T-shirt 3' },
        { id: 8, name: 'T-shirt 4' },
      ],
      choiceItems: [
        { id: 11, name: 'Jacket 1' },
        { id: 12, name: 'Jacket 2' },
        { id: 13, name: 'Jacket 3' },
        { id: 14, name: 'Jacket 4' },
        { id: 15, name: 'Hoodie 1' },
        { id: 16, name: 'Hoodie 2' },
        { id: 17, name: 'Hoodie 3' },
        { id: 18, name: 'Hoodie 4' }
      ],
      selectedUserItems: [],
      selectedChoiceItem: null
    };
  },
  methods: {
    toggleUserItem(item) {
      const index = this.selectedUserItems.indexOf(item);
      if (index === -1) {
        if (this.selectedUserItems.length < 6) {
          this.selectedUserItems.push(item);
        }
      } else {
        this.selectedUserItems.splice(index, 1);
      }
    },
    selectChoiceItem(item) {
      this.selectedChoiceItem = this.selectedChoiceItem?.id === item.id ? null : item;
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  width: 90vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 32px 16px;
  gap: 16px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.66);
  border-radius: 8px;
  &_header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 40px;
    width: 100%;
    height: 20vh;
    &_item-container {
      display: flex;
      justify-content: space-between;
      flex-direction: column;
      width: 100%;
      height: 100%;
      padding: 8px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.19);
      border-radius: 6px;
      &_items {
        display: flex;
        flex-wrap: wrap;
        gap: 6px;
        max-height: 120px;
        overflow: auto;
        &_item {
          display: flex;
          align-items: center;
          justify-content: center;
          max-width: 8vw;
          width: 100%;
          height: 5vh;
          border: 3px solid black;
          border-radius: 6px;
          font-size: 18px;
          font-weight: bold;
          cursor: pointer;
        }
        &_item:hover {
          opacity: 0.8;
          transition: 0.3s;
        }
      }
      &_selected {
        font-size: 20px;
        color: black;
        font-weight: bold;
      }
      &_item {
        width: 80%;
        height: 80%;
        margin: auto;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 32px;
        font-weight: bold;
        border: 5px solid #ce5e5e;
        color: #ce5e5e;
        transition: 0.6s;
        border-radius: 14px;
      }
      &_item.selected {
        transition: 0.6s;
        border: 5px solid #3881ED;
        color: #3881ED;
      }
    }
  }
  &_body {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
    width: 100%;
    &_items {
      display: flex;
      align-items: flex-start;
      justify-content: flex-start;
      gap: 4px;
      flex-wrap: wrap;
      width: 100%;
      height: 100%;
      max-height: 540px;
      overflow: auto;
      padding: 16px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.19);
      border-radius: 14px;
      &_item {
        display: flex;
        align-items: center;
        justify-content: center;
        max-width: 8vw;
        width: 100%;
        height: 5vh;
        border: 2px solid #FFF;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.06);
        border-radius: 6px;
        font-size: 18px;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
      }
      &_item:hover {
        opacity: 0.8;
        border: 2px solid #3881ED;
        transition: 0.3s;
      }
      &_item.selected {
        background: #3881ED;
        border: 3px solid #3881ED;
      }
    }
  }
}

::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px #8a8a8a;
  border-radius: 20%;
}
::-webkit-scrollbar-thumb {
  background: #505050;
  border-radius: 20%;
}

@media(max-width: 992px) {
  .container {
    &_header {
      &_item-container {
        &_item {
          font-size: 24px;
          width: 100%;
        }
        &_items {
          &_item {
            max-width: 100%;
          }
        }
      }
    }
    &_body {
      &_items {
        &_item {
          max-width: 100%;
        }
      }
    }
  }
}
</style>
