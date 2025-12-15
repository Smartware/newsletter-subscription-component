<template>
  <div class="newsletter-subscription" :class="layoutClass">
    <!-- Image Left Layout -->
    <div v-if="layout === 'image-left'" class="flex flex-col md:flex-row gap-8 items-center">
      <div class="md:w-1/2">
        <img v-if="imageSrc" :src="imageSrc" :alt="imageAlt" class="w-full h-auto rounded-lg shadow-lg" />
      </div>
      <div class="md:w-1/2" :style="{ backgroundColor: backgroundColor }">
        <div class="p-6 rounded-lg">
          <NewsletterForm
            :headerText="headerText"
            :subText="subText"
            :buttonText="buttonText"
            :placeholderText="placeholderText"
            :primaryColor="primaryColor"
            :textColor="textColor"
            :borderColor="borderColor"
            :buttonTextColor="buttonTextColor"
            :formDisplay="formDisplay"
            @submit="handleSubmit"
          />
        </div>
      </div>
    </div>

    <!-- Image Right Layout -->
    <div v-else-if="layout === 'image-right'" class="flex flex-col md:flex-row gap-8 items-center">
      <div class="md:w-1/2 order-2 md:order-1" :style="{ backgroundColor: backgroundColor }">
        <div class="p-8 rounded-lg">
          <NewsletterForm
            :headerText="headerText"
            :subText="subText"
            :buttonText="buttonText"
            :placeholderText="placeholderText"
            :primaryColor="primaryColor"
            :textColor="textColor"
            :borderColor="borderColor"
            :buttonTextColor="buttonTextColor"
            :formDisplay="formDisplay"
            @submit="handleSubmit"
          />
        </div>
      </div>
      <div class="md:w-1/2 order-1 md:order-2">
        <img v-if="imageSrc" :src="imageSrc" :alt="imageAlt" class="w-full h-auto rounded-lg shadow-lg" />
      </div>
    </div>

    <!-- Image Background Layout -->
    <div v-else-if="layout === 'image-background'" class="relative min-h-screen flex items-center justify-center">
      <div class="absolute inset-0 bg-black bg-opacity-50" :style="{ backgroundImage: `url(${imageSrc})`, backgroundSize: 'cover', backgroundPosition: 'center', backgroundRepeat: 'no-repeat' }"></div>
      <div class="relative z-10 max-w-md mx-auto p-8 rounded-lg shadow-xl" :style="{ backgroundColor: backgroundColor }">
        <NewsletterForm
          :headerText="headerText"
          :subText="subText"
          :buttonText="buttonText"
          :placeholderText="placeholderText"
          :primaryColor="primaryColor"
          :textColor="textColor"
          :borderColor="borderColor"
          :buttonTextColor="buttonTextColor"
          :formDisplay="formDisplay"
          @submit="handleSubmit"
        />
      </div>
    </div>

    <!-- Form Only Layout -->
    <div v-else class="max-w-md mx-auto" :style="{ backgroundColor: backgroundColor }">
      <div class="p-8 rounded-lg shadow-lg">
        <NewsletterForm
          :headerText="headerText"
          :subText="subText"
          :buttonText="buttonText"
          :placeholderText="placeholderText"
          :primaryColor="primaryColor"
          :textColor="textColor"
          :borderColor="borderColor"
          :buttonTextColor="buttonTextColor"
          :formDisplay="formDisplay"
          @submit="handleSubmit"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NewsletterForm from './NewsletterForm.vue'

export default {
  name: 'NewsletterSubscription',
  components: {
    NewsletterForm
  },
  props: {
    // Layout Configuration
    layout: {
      type: String,
      default: 'form-only',
      validator: (value) => ['image-left', 'image-right', 'image-background', 'form-only'].includes(value)
    },
    formDisplay: {
      type: String,
      default: 'flex',
      validator: (value) => ['flex', 'grid'].includes(value)
    },

    // Content
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
    imageSrc: {
      type: String,
      default: ''
    },
    imageAlt: {
      type: String,
      default: 'Newsletter image'
    },

    // Theming
    primaryColor: {
      type: String,
      default: '#3B82F6'
    },
    textColor: {
      type: String,
      default: '#1F2937'
    },
    backgroundColor: {
      type: String,
      default: '#FFFFFF'
    },
    borderColor: {
      type: String,
      default: '#D1D5DB'
    },
    buttonTextColor: {
      type: String,
      default: '#FFFFFF'
    }
  },
  emits: ['submit'],
  computed: {
    layoutClass() {
      return `layout-${this.layout}`
    }
  },
  methods: {
    handleSubmit(email) {
      this.$emit('submit', email)
    }
  },
}
</script>


