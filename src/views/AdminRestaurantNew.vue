<template>
  <div class="container py-5">
    <!-- 餐廳表單 AdminRestaurantForm -->
    <AdminRestaurantForm @after-submit="handleAfterSubmit" :is-processing="isProcessing" />
  </div>
</template>

<script>
import AdminRestaurantForm from '../components/AdminRestaurantForm.vue'
import adminAPI from '../apis/admin.js'
import { Toast } from '../utils/helper.js'

export default {
  components: {
    AdminRestaurantForm,    
  },
  data() {
    return {
      isProcessing: false
    }
  },
  methods: {
    async handleAfterSubmit(formData) {
      try {
        this.isProcessing = true
        const {data} = await adminAPI.restaurants.create ({formData})
        if (data.status !== 'success') {
          throw new Error(data.message)
        }
        this.$router.push({name:'admin-restaurants'})

      } catch (error) {
        this.isProcessing = false
        Toast.fire ({
          icon: 'error',
          title: '無法新增餐廳，請稍後再試'
        })
      }
    },
  },
};
</script>
