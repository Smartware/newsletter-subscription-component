<template>
  <div class="newsletter-form">
    <h2 class="text-2xl font-bold mb-2" :style="{ color: textColor }">{{ headerText }}</h2>
    <p v-if="subText" class="mb-6" :style="{ color: textColor }">{{ subText }}</p>

    <form @submit.prevent="handleSubmit" :class="formDisplayClass">
      <div class="form-group">
        <input
          v-model="email"
          type="email"
          :placeholder="placeholderText"
          :class="inputClass"
          :style="{ borderColor: isValid ? borderColor : '#EF4444' }"
          @blur="validateEmail"
        />
        <span v-if="errorMessage" class="error-message text-red-500 text-sm mt-1">{{ errorMessage }}</span>
      </div>

      <button
        type="submit"
        :disabled="!isValid || isSubmitting"
        :class="buttonClass"
        :style="{ backgroundColor: primaryColor, color: buttonTextColor }"
      >
        {{ isSubmitting ? 'Subscribing...' : buttonText }}
      </button>
    </form>

    <div v-if="showSuccess" class="success-message mt-4 p-4 bg-green-100 text-green-800 rounded">
      Thanks for subscribing!
    </div>
  </div>
</template>

<script>
export default {
  name: 'NewsletterForm',
  props: {
    headerText: {
      type: String,
      required: true
    },
    subText: {
      type: String,
      default: ''
    },
    buttonText: {
      type: String,
      default: 'Subscribe'
    },
    placeholderText: {
      type: String,
      default: 'Enter your email'
    },
    primaryColor: {
      type: String,
      default: '#3B82F6'
    },
    textColor: {
      type: String,
      default: '#1F2937'
    },
    borderColor: {
      type: String,
      default: '#D1D5DB'
    },
    buttonTextColor: {
      type: String,
      default: '#FFFFFF'
    },
    formDisplay: {
      type: String,
      default: 'flex',
      validator: (value) => ['flex', 'grid'].includes(value)
    }
  },
  emits: ['submit'],
  data() {
    return {
      email: '',
      errorMessage: '',
      isValid: true,
      isSubmitting: false,
      showSuccess: false
    }
  },
  computed: {
    formDisplayClass() {
      return this.formDisplay === 'flex'
        ? 'flex flex-col sm:flex-row gap-4'
        : 'grid grid-cols-1 gap-4'
    },
    inputClass() {
      return `w-full px-4 py-2 border rounded focus:outline-none focus:ring-2 ${
        this.formDisplay === 'flex' ? 'sm:flex-1' : ''
      }`
    },
    buttonClass() {
      return `px-6 py-2 rounded font-medium transition-colors disabled:opacity-50 disabled:cursor-not-allowed ${
        this.formDisplay === 'flex' ? '' : 'w-full'
      }`
    }
  },
  methods: {
    validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

      if (!this.email.trim()) {
        this.errorMessage = 'Email address is required'
        this.isValid = false
        return false
      }

      if (!emailRegex.test(this.email)) {
        this.errorMessage = 'Please enter a valid email address'
        this.isValid = false
        return false
      }

      this.errorMessage = ''
      this.isValid = true
      return true
    },
    async handleSubmit() {
      if (!this.validateEmail()) {
        return
      }

      this.isSubmitting = true

      // Simulate API call
      try {
        // Mock submission delay
        await new Promise(resolve => setTimeout(resolve, 1000))

        console.log('Newsletter subscription:', this.email)
        this.$emit('submit', this.email)

        // Show success message
        this.showSuccess = true
        this.email = ''

        // Hide success message after 3 seconds
        setTimeout(() => {
          this.showSuccess = false
        }, 3000)

      } catch (error) {
        console.error('Subscription failed:', error)
      } finally {
        this.isSubmitting = false
      }
    }
  }
}
</script>

