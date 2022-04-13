<template>
  <div>
    <line-chart
      :key="updated"
      :chart-data="lineData"
      :chart-options="options"
    />
  </div>
</template>

<script>
import FakeData from '@/fake.json'

export default {
  data() {
    return {
      updated: 0,
      lineData: {
        labels: [],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '',
            data: [],
          },
          {
            label: 'Data Two',
            backgroundColor: '',
            data: [],
          },
        ],
      },
      options: {
        responsive: true,
        scales: {
          x: {
            display: true,
            title: {
              display: true,
            },
          },
          y: {
            display: true,
            title: {
              display: true,
              text: 'Value',
            },
          },
        },
      },
    }
  },
  async fetch() {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1')
    const data = await response.json()
    console.log('fake API title fetched:', data.title)

    const actualData = FakeData.data
    for (let i = 0; i < actualData.length; i++) {
      this.lineData.labels.push(actualData[i].date)
      this.lineData.datasets[0].backgroundColor = actualData[i].color1
      this.lineData.datasets[0].data.push(actualData[i].close)
      this.lineData.datasets[1].backgroundColor = actualData[i].color2
      this.lineData.datasets[1].data.push(actualData[i].high)
    }
    this.updated++
  },
}
</script>
