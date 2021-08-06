<template>
  <div v-if="isModalOpened" class="modal-background">
    <div class="modal-inside">
      <h4>상세페이지</h4>
      <p>{{ modaldescription.title }}</p>
      <p>{{ modaldescription.content }}</p>
      <p>{{ modaldescription.price }}</p>
    </div>
    <div @click="onClickModalOutside" class="modal-outside"></div>
  </div>

  <div class="menu">
    <a v-for="pageName in menu" :key="pageName">{{ pageName }}</a>
  </div>

  <div v-for="(room, index) in rooms" :key="room" @click="onClickName(index)">
    <img :src="room.image" alt="" class="room-img" />
    <h4>{{ room.title }}</h4>
    <p>{{ room.price }}</p>
    <button @click="onClickReport(index)">
      신고
    </button>
    <span>신고수: {{ room.reportCount }}</span>
  </div>
</template>

<script>
import roomsRes from './assets/data/rooms'

export default {
  name: 'App',
  data() {
    return {
      isModalOpened: false,
      modalDescription: {},
      menu: ['Home', 'Shop', 'About'],
      rooms: roomsRes.map((room) => {
        return {
          ...room,
          reportCount: 0,
        }
      }),
    }
  },
  methods: {
    onClickReport(index) {
      this.rooms[index].reportCount++
    },
    onClickName(index) {
      this.modaldescription = this.rooms[index]
      this.isModalOpened = true
    },
    onClickModalOutside() {
      this.isModalOpened = false
    },
  },
  components: {},
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

.modal-background {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.modal-inside {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.modal-outside {
  width: 100%;
  height: 100%;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
