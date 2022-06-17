<template>
  <div id="app">
    <aside>
      <h1>Test App</h1>
      <nav>
        <ul>
          <li>
            <router-link to="/" :class="{ active: $route.path === '/' }">
              Home
            </router-link>
          </li>
          <li>
            <router-link
              to="/admin"
              :class="{ active: $route.path === '/admin' }"
            >
              Admin
            </router-link>
          </li>
        </ul>
      </nav>
    </aside>

    <main>
      <router-view />
    </main>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
  display: flex;
}

#app aside {
  width: 300px;
  height: 100vh;
  background: #fff;
}
#app aside h1 {
  text-align: center;
}

#app main {
  flex-grow: 1;
  height: 100vh;
}

ul {
  list-style: none;
  padding: 0;
  width: 100%;
  margin-top: 100px;
}
ul > li {
  display: block;
}
ul > li > a {
  display: block;
  padding: 15px 25px;
  width: 100%;
}

ul > li > a:hover {
  background: rgba(66, 185, 131, 0.2);
}

nav a.active {
  color: var(--main-color);
  border-right: 4px solid var(--main-color);
  background: rgba(66, 185, 131, 0.2);
}

main {
  overflow-y: auto;
  padding: 50px 100px;
}
</style>
