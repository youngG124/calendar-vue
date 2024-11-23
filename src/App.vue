<template>
  <div>
    <h1>Welcome to My Vue App</h1>
    <div class="my-section">
      <!-- Your custom HTML -->
      <p>This is my custom HTML content.</p>
      <div id="calendar">
        <h2 id="month-year"></h2>
        <table>
          <thead>
            <tr>
              <th>Sun</th>
              <th>Mon</th>
              <th>Tue</th>
              <th>Wed</th>
              <th>Thu</th>
              <th>Fri</th>
              <th>Sat</th>
            </tr>
          </thead>
          <tbody id="calendar-body"></tbody>
        </table>
        <div class="button-container">
          <button id="prev-month" class="prev-next">Previous Month</button>
          <button id="next-month" class="prev-next">Next Month</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
