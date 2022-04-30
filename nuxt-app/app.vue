<script setup>
  // search from input
  const search = () => {
    // get value from input with id="input"
    const value = document.getElementById('input').value
    if(!value && value.length < 3) {
      alert('Please enter a login with at least 3 characters')
      return
    }
    // fetch data from github api
    fetch(`https://api.github.com/search/users?q=${value}`)
      .then(response => response.json())
      .then(data => {
        // get users from data
        const users = data.items
        // get container with id="users"
        const container = document.getElementById('users')
        // clear container
        container.innerHTML = ''
        // loop through users
        users.forEach(user => {
          // create div element
          const div = document.createElement('div')
          // add class to div
          div.classList.add('user')
          // create img element
          const img = document.createElement('img')
          // add src to img
          img.src = user.avatar_url
          // create h2 element
          const h2 = document.createElement('h2')
          // add text to h2
          h2.textContent = user.login
          // create p element
          const p = document.createElement('p')
          // add text to p
          p.textContent = user.html_url
          // append img and h2 to div
          div.appendChild(img)
          div.appendChild(h2)
          div.appendChild(p)
          // append div to container
          container.appendChild(div)
        })
      })
  }
</script>

<template>
  <div class="search">
    <input type="text" id="input" v-model="query" @keyup.enter="search" placeholder="Search for github avatar...">
    <button @click="search">Search</button>
  </div>
  <div id="users"></div>
</template>

<style scoped>
.hello {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 3rem;
  padding: 10rem;
}
</style>
