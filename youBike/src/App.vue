<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const youbikeData = ref([])

const fetchData = async () => {
  try {
    const response = await axios.get(
      'https://tcgbusfs.blob.core.windows.net/dotapp/youbike/v2/youbike_immediate.json'
    )
    youbikeData.value = response.data
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  fetchData()
})
</script>

<template>
  <div id="app">
    <header>
      <nav>
        <div>
          <a href="/">
            <img
              alt="YouBike logo"
              class="logo"
              src="https://flowbite.com/docs/images/logo.svg"
              width="20"
              height="20"
            />
            <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">
              YouBike範本
            </span>
          </a>
          <div>
            <input
              type="text"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
              placeholder="輸入站點地址"
            />
            <button
              type="submit"
              class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center cursor-pointer"
            >
              查詢
            </button>
          </div>
        </div>
      </nav>
    </header>
    <main>
      <div class="overflow-x-auto shadow-md">
        <table class="w-full text-sm text-left rtl:text-right text-gray-500 table-fixed">
          <thead class="text-white uppercase bg-blue-600 dark:text-white">
            <tr>
              <th class="font-semibold text-center p-2">站點編號</th>
              <th class="font-semibold text-center p-2">站點名稱</th>
              <th class="font-semibold text-center p-2">站點所在區域</th>
              <th class="font-semibold text-center p-2">站點地址</th>
              <th class="font-semibold text-center p-2">總車位數量</th>
              <th class="font-semibold text-center p-2">可租借的腳踏車數量</th>
              <th class="font-semibold text-center p-2">站點緯度</th>
              <th class="font-semibold text-center p-2">站點經度</th>
              <th class="font-semibold text-center p-2">可歸還的腳踏車數量</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="station in youbikeData"
              :key="station.sno"
              class="odd:bg-white even:bg-gray-100 border-b hover:bg-blue-100"
            >
              <td class="p-2 text-center">{{ station.sno }}</td>
              <td class="p-2 text-center">{{ station.sna }}</td>
              <td class="p-2 text-center">{{ station.ar }}</td>
              <td class="p-2 text-center">{{ station.address }}</td>
              <td class="p-2 text-center">{{ station.total_bike }}</td>
              <td class="p-2 text-center">{{ station.available_rent_bikes }}</td>
              <td class="p-2 text-center">{{ station.lat }}</td>
              <td class="p-2 text-center">{{ station.lng }}</td>
              <td class="p-2 text-center">{{ station.available_return_bikes }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </main>
    <footer></footer>
  </div>
</template>

<style scoped>
/* 添加一些基本樣式 */
/* nav {
  display: flex;
  align-items: center;
  justify-content: center;
}
.logo {
  margin-right: 10px;
}

.station-item {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
} */
</style>
