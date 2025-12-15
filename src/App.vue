<script setup>
import NewsletterSubscription from './components/NewsletterSubscription.vue'

const handleSubscription = (email) => {
  console.log('New subscription:', email)
  // it will send the email to the backend
}
</script>

<template>
  <div id="app" class="min-h-screen bg-gray-100 py-12">
    <div class="container mx-auto px-4">
      <h1 class="text-3xl font-bold text-center mb-8">Newsletter Subscription Demo</h1>

      

      <!-- Image Left Layout -->
      <div class="mb-12">
        <NewsletterSubscription
          headerText="Join Our Community"
          subText="Subscribe to receive exclusive content and updates."
          buttonText="Join Now"
          placeholderText="Your email here"
          primaryColor="#10B981"
          textColor="#1F2937"
          backgroundColor="#FFFFFF"
          borderColor="#D1D5DB"
          buttonTextColor="#FFFFFF"
          layout="image-left"
          formDisplay="flex"
          imageSrc="./src/images/G3yF3ewbAAAMAgY.jpeg"
          imageAlt="Image"
          @submit="handleSubscription"
        />
      </div>

      <!-- Image Right Layout -->
      <div class="mb-12">
        <NewsletterSubscription
          headerText="Get the Latest Updates"
          subText="Subscribe for weekly newsletters and special offers."
          buttonText="Subscribe"
          placeholderText="Email address"
          primaryColor="#F59E0B"
          textColor="#1F2937"
          backgroundColor="#FFFFFF"
          borderColor="#D1D5DB"
          buttonTextColor="#FFFFFF"
          layout="image-right"
          formDisplay="grid"
          imageSrc="./src/images/G3yF3ewbAAAMAgY.jpeg"
          imageAlt="Image"
          @submit="handleSubscription"
        />
      </div>

      <!-- Image Background Layout -->
      <div class="mb-12">
        <NewsletterSubscription
          headerText="Welcome to Our Newsletter"
          subText="Stay connected with our latest news and insights."
          buttonText="Sign Up"
          placeholderText="Enter email"
          primaryColor="#EF4444"
          textColor="#FFFFFF"
          backgroundColor="rgba(855, 855, 275, 0.9)"
          borderColor="#FFFFFF"
          buttonTextColor="#FFFFFF"
          layout="image-background"
          formDisplay="flex"
          imageSrc="./src/images/G3yF3ewbAAAMAgY.jpeg"
          imageAlt="Image"
          @submit="handleSubscription"
        />
      </div>

      <!-- Form Only Layout -->
      <div class="mb-12">
        <NewsletterSubscription
          headerText="Stay Updated!"
          subText="Get the latest news and updates delivered to your inbox."
          buttonText="Subscribe"
          placeholderText="Enter your email address"
          primaryColor="#3B82F6"
          textColor="#1F2937"
          backgroundColor="#FFFFFF"
          borderColor="#D1D5DB"
          buttonTextColor="#FFFFFF"
          layout="form-only"
          formDisplay="flex"
          @submit="handleSubscription"
        />
      </div>
    </div>
  </div>
</template>
