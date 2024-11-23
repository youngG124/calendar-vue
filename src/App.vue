<template>
  <div>
    <h1>Web-Calendar-Magazine</h1>
    <div class="my-section">
      <!-- Your custom HTML -->
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
          <tbody ref="calendarBody"></tbody>
        </table>
        <div class="button-container">
          <button ref="prevMonthButton" class="prev-next">Previous Month</button>
          <button ref="nextMonthButton" class="prev-next">Next Month</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  mounted() {
    // Log to ensure mounted hook runs
    console.log('App mounted');

    const calendarBody = this.$refs.calendarBody; // Use ref to access calendar body
    const monthYearDisplay = document.getElementById("month-year"); // No issues with this, since it's not part of Vue's reactivity
    const prevMonthButton = this.$refs.prevMonthButton; // Access previous month button
    const nextMonthButton = this.$refs.nextMonthButton; // Access next month button

    let currentDate = new Date(); // Set the current date for the calendar

    const today = new Date();
    const todayDate = today.getDate();
    const todayMonth = today.getMonth();
    const todayYear = today.getFullYear();

    // Render the calendar on page load
    renderCalendar(currentDate);

    // Function to render the calendar
    function renderCalendar(date) {
      console.log('Rendering Calendar');

      calendarBody.innerHTML = ''; // Clear any existing calendar content

      const month = date.getMonth();
      const year = date.getFullYear();
      monthYearDisplay.textContent = date.toLocaleDateString('en-US', {
        month: 'long',
        year: 'numeric',
      });

      const firstDay = new Date(year, month, 1).getDay();
      const daysInMonth = new Date(year, month + 1, 0).getDate();

      let day = 1;
      for (let i = 0; i < 6; i++) {
        const row = document.createElement('tr');

        for (let j = 0; j < 7; j++) {
          const cell = document.createElement('td');

          if (i === 0 && j < firstDay) {
            cell.innerHTML = ''; // Empty cell before the first day of the month
          } else if (day > daysInMonth) {
            cell.innerHTML = ''; // Empty cell after the last day of the month
          } else {
            const dayNumber = document.createElement('span');
            dayNumber.textContent = day;
            dayNumber.classList.add('day-number');

            if (day === todayDate && month === todayMonth && year === todayYear) {
              cell.classList.add('today');
            }

            const img = document.createElement('img');
            img.src = `images/${month + 1}_${day}.jpg`; // Replace with actual image paths

            cell.appendChild(img);
            cell.appendChild(dayNumber);

            cell.addEventListener('click', () => onCellClick(dayNumber.textContent, month, year));
            day++;
          }

          row.appendChild(cell);
        }

        calendarBody.appendChild(row);
      }
    }

    // Event listeners for month navigation buttons
    prevMonthButton.addEventListener('click', goToPreviousMonth);
    nextMonthButton.addEventListener('click', goToNextMonth);

    // Handle clicks on calendar cells
    function onCellClick(day, month, year) {
      if (todayDate >= day) {
        console.log(`You clicked on: ${day}/${month + 1}/${year}`);
      }
    }

    // Navigate to the next month
    function goToNextMonth() {
      currentDate.setMonth(currentDate.getMonth() + 1);
      renderCalendar(currentDate);
    }

    // Navigate to the previous month
    function goToPreviousMonth() {
      currentDate.setMonth(currentDate.getMonth() - 1);
      renderCalendar(currentDate);
    }
  },
};
</script>

<style>
@import './assets/style.css';
</style>
