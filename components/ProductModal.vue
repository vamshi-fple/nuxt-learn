<template>
    <div v-if="show" class="fixed inset-0  bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div class="bg-white rounded-lg shadow-xl w-full max-w-md">
        <div class="p-6">
          <h2 class="text-xl font-bold mb-4">
            {{ isEdit ? 'Edit Product' : 'Add New Product' }}
          </h2>
          
          <form @submit.prevent="handleSubmit">
            <div class="mb-4">
              <label class="block text-gray-700 mb-2" for="name">Product Name</label>
              <input
                id="name"
                v-model="formData.name"
                type="text"
                class="w-full px-3 py-2 border rounded"
                required
              >
            </div>
            
            <div class="grid grid-cols-2 gap-4 mb-4">
              <div>
                <label class="block text-gray-700 mb-2" for="quantity">Quantity</label>
                <input
                  id="quantity"
                  v-model.number="formData.quantity"
                  type="number"
                  min="1"
                  class="w-full px-3 py-2 border rounded"
                  required
                >
              </div>
              <div>
                <label class="block text-gray-700 mb-2" for="price">Price</label>
                <input
                  id="price"
                  v-model.number="formData.price"
                  type="number"
                  min="0.01"
                  step="0.01"
                  class="w-full px-3 py-2 border rounded"
                  required
                >
              </div>
              <div>
                <label class="block text-gray-700 mb-2" for="price"> Total Price</label>
                <input
                  id="price"
                  type="number"
                 :value="formData.price * formData.quantity"
                  min="0.01"
                  step="0.01"
                  class="w-full px-3 py-2 border rounded"
                readonly
                >
              </div>
            </div>
            
            <div class="flex justify-end space-x-3">
              <button
                type="button"
                @click="close"
                class="px-4 py-2 border rounded hover:bg-gray-100 btn"
              >
                Cancel
              </button>
              <button
                type="submit"
                class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 btn"
              >
                {{ isEdit ? 'Update' : 'Save' }}
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>  
  const props = defineProps({
    show: {
      type: Boolean,
      required: true
    },
    isEdit: {
      type: Boolean,
      default: false
    },
    product: {
      type: Object,
      default: () => ({
        id: null,
        name: '',
        quantity: 0,
        price: 0
      })
    }
  });
  
  const emit = defineEmits(['close', 'save']);
  
  const formData = ref({ ...props.product });
  
  watch(() => props.product, (newProduct) => {
    formData.value = { ...newProduct };
  }, { deep: true });
  
  function close() {
    emit('close');
  }
  
  function handleSubmit() {
    emit('save', { ...formData.value });
  }
  
  </script>
  
  <style scoped>
 .btn {
  border: none;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
}
  </style>