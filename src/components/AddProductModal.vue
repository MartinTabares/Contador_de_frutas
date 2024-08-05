<template>
  <div v-if="isVisible" class="modal">
    <div class="modal-content">
      <h2>{{ isEditMode ? 'Editar Producto' : 'Agregar Producto' }}</h2>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name">Nombre:</label>
          <input type="text" id="name" v-model="product.name" required>
        </div>
        <div class="form-group">
          <label for="product-category">Categoría:</label>
          <select id="product-category" v-model="product.category" required>
            <option v-for="category in filteredCategories" :key="category.value" :value="category.value">
              {{ category.text }}
            </option>
          </select>
        </div>
        <div class="form-group">
          <label for="price">Precio:</label>
          <input type="number" id="price" v-model="product.price" required>
        </div>
        <div class="form-group">
          <label for="stock">Stock:</label>
          <input type="number" id="stock" v-model="product.stock" disabled>
        </div>
        <div class="button-group">
          <button v-if="!isEditMode" type="submit" class="btn btn-primary">Añadir</button>
          <button v-else type="submit" class="btn btn-success">Guardar</button>
          <button type="button" class="btn btn-secondary" @click="closeModal">Cancelar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
  props: {
    isVisible: Boolean,
    isEditMode: Boolean,
    product: {
      type: Object,
      default: () => ({})
    },
    categories: {
      type: Array,
      default: () => []
    }
  },

  computed: {
    filteredCategories() {
      return this.categories.filter(category => category.value !== null);
    }
  },

  methods: {
    closeModal() {
      this.$emit('close');
    },
    submitForm() {
      if (this.isEditMode) {
        this.$emit('edit-product', this.product);
      } else {
        console.log(this.product);
        this.$emit('add-product', this.product);
      }
    }

  }
};
</script>

<style scoped>
.modal {
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  left: 0;
  width: 110%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #8abb8a;
  padding: 20px;
  border-radius: 10px;
  width: 310px;
}

.form-group {
  margin-bottom: 20px;
}

input,
select {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.button-group {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.btn {
  padding: 10px 20px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
}

.btn-primary {
  background-color: #007bff;
  color: white;
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
}
</style>