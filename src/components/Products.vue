<template>
	<div class="products">
		<div class="header">
			<h1>Gestión de Productos</h1>
			<b-button variant="primary" class="add-product-button" @click="openAddProductModal()">Añadir Nuevo
				Producto</b-button>
			<AddProductModal :categories="categories" :product="selectedProduct" :isVisible="showModal"
				:isEditMode="isEditMode" @close="showModal = false" @add-product="addProduct" @edit-product="updateProduct" />
		</div>
		<div class="search-filter">
			<b-form-input v-model="searchQuery" placeholder="Buscar producto"></b-form-input>
			<b-form-select v-model="selectedCategory" :options="categories" class="filter-select"></b-form-select>
		</div>
		<div class="table-container">
			<b-table :items="filteredProducts" :fields="fields" class="product-table">
				<template #cell(actions)="data">
					<b-button class="mr-1" size="sm" variant="warning" @click="editProduct(data.item)">Editar</b-button>
					<b-button size="sm" variant="danger" @click="deleteProduct(data.item)">Eliminar</b-button>
				</template>
			</b-table>
		</div>
	</div>
</template>

<script>

import AddProductModal from './AddProductModal.vue';
import { products } from '../products';

export default {
	components: {
		AddProductModal
	},
	data() {
		return {
			products: products,
			showModal: false,
			selectedProduct: {},
			isEditMode: false,
			searchQuery: '',
			selectedCategory: null,
			categories: [
				{ value: null, text: 'Todas' },
				{ value: 'Fruta', text: 'Fruta' },
				{ value: 'Verdura', text: 'Verdura' },
			],
			fields: [
				{ key: 'name', label: 'Nombre' },
				{ key: 'category', label: 'Categoria' },
				{ key: 'price', label: 'Precio' },
				{ key: 'stock', label: 'Stock' },
				{ key: 'actions', label: 'Acciones' }
			]
		};
	},
	computed: {
		filteredProducts() {
			return this.products.filter(product => {
				return (!this.selectedCategory || product.category === this.selectedCategory) &&
					(!this.searchQuery || product.name.toLowerCase().includes(this.searchQuery.toLowerCase()));
			});
		}
	},
	methods: {
		openAddProductModal() {
			this.showModal = true;
			this.isEditMode = false;
			this.selectedProduct = {}
		},
		addProduct(product) {
			if (product.stock == null) {
        product.stock = 0;
      }
			this.products.unshift(product);
			this.showModal = false;
		},
		editProduct(product) {
			this.selectedProduct = product;
			this.isEditMode = true;
			this.showModal = true;
		},
		updateProduct(updatedProduct) {
			const index = this.products.findIndex(product => product.name === this.selectedProduct.name);
			if (index !== -1) {
				this.$set(this.products, index, updatedProduct);
			}
			this.showModal = false;
		},
		deleteProduct(product) {
			const index = this.products.findIndex(p => p.name === product.name);
			if (index !== -1) {
				this.products.splice(index, 1);
			}
		}
	}
};
</script>

<style scoped>
.products {
	padding: 20px;
}

.header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20px;
}

.add-product-button {
	margin-left: auto;
}

.search-filter {
	display: flex;
	justify-content: space-between;
	margin-bottom: 20px;
}

.filter-select {
	margin-left: 10px;
}

.product-table {
	border: 2px solid #dee2e6;
	width: 100%;
}

.table-container {
	max-height: 70vh;
	overflow-y: auto;
}
</style>