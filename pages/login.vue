<template>
  <button @click="login('github')">Login with GitHub</button>
</template>

<script setup>
const user = useSupabaseUser()
const client = useSupabaseClient()
const router = useRouter()

// Login method using providers
const login = async(provider) => {
  const { error } = await client.auth.signIn({ provider })
  if (error) {
    return alert('Something went wrong !')
  }
  router.push('/')
}
</script>