<template>
  <div class="bg-gray-200 dark:bg-gray-800 min-h-screen">
    <Form v-slot="{ errors }" class="p-5" @submit="createProduct">
      <div class="mb-6">
        <label
          for="product_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Product Name</label
        >
        <Field
          name="product_name"
          :rules="isRequired"
          v-model="product.name"
          type="text"
          id="product_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Enter product name"
          required
        />
        <span class="text-red-700">{{ errors.product_name }}</span>
      </div>
      <div class="mb-6">
        <label
          for="product_barcode"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Product barcode</label
        >
        <Field
          name="product_barcode"
          :rules="isRequired"
          v-model="product.barcode"
          type="number"
          id="product_barcode"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Enter product barcode"
          required
        />
        <span class="text-red-700">{{ errors.product_barcode }}</span>
      </div>
      <div class="mb-6">
        <label
          for="product_stock"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Product stock</label
        >
        <Field
          name="product_stock"
          :rules="isRequired"
          v-model="product.stock"
          type="number"
          id="product_stock"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Enter product stock"
          required
        />
        <span class="text-red-700">{{ errors.product_stock }}</span>
      </div>
      <div class="mb-6 flex gap-4">
        <div class="basis-1/2">
          <label
            for="product_purchasedprice"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Product purchased price</label
          >
          <Field
            name="product_purchasedprice"
            :rules="isRequired"
            v-model="product.purchasedPrice"
            type="number"
            step="0.01"
            id="product_purchasedprice"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Enter product price"
            required
          />
          <span class="text-red-700">{{ errors.product_purchasedprice }}</span>
        </div>
        <div class="basis-1/2">
          <label
            for="product_sellingprice"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
            >Product selling price</label
          >
          <Field
            name="product_sellingprice"
            :rules="isRequired"
            v-model="product.sellingPrice"
            type="number"
            step="0.01"
            id="product_sellingprice"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Enter product price"
            required
          />
          <span class="text-red-700">{{ errors.product_sellingprice }}</span>
        </div>
      </div>

      <button
        type="submit"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-32 px-5 py-1.5 flex justify-center items-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      >
        <div role="status" v-if="isLoading">
          <IconC
            iconType="custom"
            iconName="SpinnerIcon"
            iconClass="mr-2 w-4 h-4 text-gray-200 animate-spin fill-blue-600"
          />
          <span class="sr-only">Loading...</span>
        </div>
        <div v-else>Submit</div>
      </button>
    </Form>
  </div>
</template>

<script>
import { useToast } from "vue-toastification";
import { Field, Form } from "vee-validate";

export default {
  name: "CreateProductView",
  components: {
    Field,
    Form,
  },
  setup() {
    const toast = useToast();
    return { toast };
  },
  data() {
    return {
      product: {
        name: "",
        barcode: "",
        stock: "",
        purchasedPrice: "",
        sellingPrice: "",
      },
      isLoading: false,
    };
  },
  methods: {
    isRequired(value) {
      return value ? true : "This field is required";
    },
    createProduct() {
      this.isLoading = true;
      this.$store
        .dispatch("productModule/createProduct", this.product)
        .then(() => {
          this.isLoading = false;
          this.$router.push({
            name: "products",
          });
          this.$toast.success("Product created successfully!");
        })
        .catch(() => {
          this.isLoading = false;
          this.$toast.error("Something went wrong!");
        });
    },
  },
};
</script>
