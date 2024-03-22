<template>
  <div class="item-list">
    <div v-for="(item, index) in filteredItems" :key="index" class="item">
      <div class="item-details">
        <div class="item-info">
          <img :src="getImagePath(item.image)" alt="Item Image" class="item-image">
          <div>
            <p class="item-name">{{ item.name }}</p>
            <p class="item-price">Php {{ item.price }}</p>
          </div>
        </div>
      </div>
      <div class="button-group">
        <button @click="addToCart(item)" class="add-to-cart-btn">Add to Cart</button>
        <button @click="updateItem(index)" class="update-btn">Update</button>
        <button @click="removeItem(index)" class="remove-btn">Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      items: [
        { name: 'Blouse', price: 10, image: 'blouse.jpg' },
        { name: 'Hoodie', price: 20, image: 'hoodie.jpg' },
        { name: 'Jeans', price: 15, image: 'jeans.jpg' },
        { name: 'Leggings', price: 11, image: 'leggings.jpg' },
        { name: 'Long Sleeve', price: 32, image: 'longsleeve.jpg' },
        { name: 'Maxi dress', price: 23, image: 'maxidress.jpg' },
        { name: 'Puff Dress', price: 23, image: 'puffdress.jpg' },
        { name: 'Sleeveless', price: 23, image: 'sleeveless.jpg' },
        { name: 'Skirt', price: 23, image: 'skirt.jpg' },
        { name: 'T-Shirt', price: 23, image: 'tshirt.jpg' }
      ]
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter(item =>
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  },
  methods: {
    addToCart(item) {
      this.$emit('add-to-cart', item);
    },
    updateItem(index) {
      const item = this.items[index];
      const newName = prompt('Enter the new name:', item.name);
      const newPrice = parseFloat(prompt('Enter the new price:', item.price));
      
      if (newName && !isNaN(newPrice)) {
        item.name = newName;
        item.price = newPrice;
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    getImagePath(image) {
      return `/img/${image}`;
    }
  }
};
</script>

<style scoped>
.item-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  width: 80%;
}

.item-details {
  flex: 1;
}

.item-info {
  display: flex;
  align-items: center;
}

.item-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.item-name {
  margin: 0;
  font-weight: bold;
}

.item-price {
  margin: 0;
}

.button-group {
  display: flex;
  gap: 10px;
}

.add-to-cart-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-to-cart-btn:hover {
  background-color: #45a049;
}

.update-btn {
  background-color: #fdd835; /* Yellow color */
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.update-btn:hover {
  background-color: #fbc02d; /* Darker yellow color on hover */
}

.remove-btn {
  background-color: #f44336; /* Red color */
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.remove-btn:hover {
  background-color: #d32f2f; /* Darker red color on hover */
}

</style>
