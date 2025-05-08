<template>
  <div class="p-6 mx-auto ">
    <h1 class="text-2xl font-bold mb-6">Product Table with Add/Edit Modal</h1>
    <div class="flex justify-end mb-4">
      <button
        @click="openAddModal"
        class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded transition-colors btn"
      >
        Add Product
      </button>
    </div>
    <div class="overflow-x-auto">
      <table class="min-w-full border">
        <thead>
          <tr class="bg-gray-200">
            <th class="p-3 border">ID</th>
            <th class="p-3 border">Name</th>
            <th class="p-3 border">Quantity</th>
            <th class="p-3 border">Price</th>
            <th class="p-3 border">Total Price</th>
            <th class="p-3 border">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="item.id || index" class="hover:bg-gray-50">
            <td class="p-3 border">{{  index + 1 }}</td>
            <td class="p-3 border">{{ item.name }}</td>
            <td class="p-3 border">{{ item.quantity }}</td>
            <td class="p-3 border">₹{{ item.price.toFixed(2) }} </td>
            <td class="p-3 border">₹{{ (item.quantity * item.price).toFixed(2) }}</td>
            <td class="p-3 border">
              <button @click="openEditModal(item)" class="bg-yellow-400 hover:bg-yellow-500 text-white px-3 py-1 rounded mr-2 btn">✎ Edit </button>
              <button @click="deleteItem(item)" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded btn">🗑️ Delete</button>
            </td>
          </tr>
        </tbody>
        <tfoot>
          <tr v-if="items.length === 0" class="bg-gray-100">
            <td class="p-3 border text-center" colspan="6">No products available</td>
          </tr>
          <tr v-else class="bg-gray-100 font-semibold">
            <td class="p-3 border" colspan="2">Total</td>
            <td class="p-3 border">{{ totalQuantity }}</td>
            <td class="p-3 border"></td>

            <td class="p-3 border">₹{{ totalPrice.toFixed(2) }}</td>
            <td class="p-3 border">
              <button 
                @click="clearAll"
                class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded btn"
              >
                Clear All
              </button>
            </td>
          </tr>
        </tfoot>
      </table>
    </div>
    <ProductModal
      :show="showModal"
      :is-edit="isEditMode"
      :product="modalItem"
      @close="closeModal"
      @save="handleSave"
    />
  </div>
</template>

<script setup>
const items = ref([]);
const showModal = ref(false);
const isEditMode = ref(false);

const modalItem = ref({
  id: null,
  name: '',
  quantity: 0,
  price: 0
});

const totalQuantity = computed(() => 
  items.value.reduce((sum, item) => sum + item.quantity, 0)
);

const totalPrice = computed(() => 
  items.value.reduce((sum, item) => sum + (item.quantity * item.price), 0)
);

const openAddModal = () => {
  isEditMode.value = false;
  modalItem.value = { id: null, name: '', quantity: 0, price: 0 };
  showModal.value = true;
}

function openEditModal(item) {
  isEditMode.value = true;
  modalItem.value = { ...item };
  showModal.value = true;
}

function closeModal() {
  showModal.value = false;
}

function handleSave(productData) {
  if (isEditMode.value) {
    const index = items.value.findIndex(item => item.id === productData.id);
    if (index !== -1) {
      items.value[index] = { ...productData };
    }
  } else {
    items.value.push({
      ...productData
    });
  }
  closeModal();
}


function deleteItem(id) {
  const index = items.value.findIndex((item) => item.name === id.name);
  if (index !== -1) {
    items.value.splice(index, 1);
  }
}
function clearAll() {
  items.value = [];
}
</script>
