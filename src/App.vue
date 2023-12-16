<template>
  <div class="app">
    <h2>База студентів</h2>

    <ul>
      <li v-for="student in students" :key="student.id">
        {{ student.name }} - {{ student.score }} балів
      </li>
    </ul>

    <p>
      Середній бал стдентів:
      <span :class="{ 'green': averageScoreIncreases, 'red': averageScoreDecreases }">
        {{ averageScore }}
        <span v-if="averageScoreIncreases" class="up">&uArr;</span>
        <span v-if="averageScoreDecreases" class="down">&dArr;</span>
      </span>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [],
      prevAverageScore: 0,
      averageScoreIncreases: false,
      averageScoreDecreases: false,
    }
  },
  computed: {
    averageScore() {
      if (this.students.length === 0) return 0;
      const totalScore = this.students.reduce((sum, student) => sum + student.score, 0)
      return (totalScore / this.students.length).toFixed(2)
    },
  },
  watch: {
    averageScore(newScore, oldScore) {
      console.log(`Зміна середнього балу: ${oldScore} → ${newScore}`)
      this.averageScoreIncreases = newScore > this.prevAverageScore
      this.averageScoreDecreases = newScore < this.prevAverageScore
      this.prevAverageScore = newScore
    },
  },
  methods: {
    generateStudent() {
      let nameList = [
        'Time', 'Past', 'Future', 'Dev', 'Fly', 'Flying', 'Soar', 'Soaring', 'Power', 'Falling', 'Fall', 'Jump', 'Cliff',
        'Mountain', 'Rend', 'Red', 'Blue', 'Green', 'Yellow', 'Gold', 'Demon', 'Demonic', 'Panda', 'Cat', 'Kitty', 'Kitten',
        'Zero', 'Memory', 'Trooper', 'Bandit', 'Fear', 'Light', 'Glow', 'Tread', 'Deep', 'Deeper', 'Deepest', 'Mine', 'Your',
      ]

      return {
        id: (new Date()).getTime(),
        name: nameList[Math.floor(Math.random() * nameList.length)],
        score: Math.floor(Math.random() * 100)
      }
    },
  },
  created() {
    setInterval(() => {
      this.students.push(this.generateStudent())
    }, 5000);
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  padding: 8px;
  font-size: 16px;
}

.green {
  color: green;
}

.red {
  color: red;
}

.up,
.down {
  font-size: 16px;
  margin-left: 5px;
}
</style>



