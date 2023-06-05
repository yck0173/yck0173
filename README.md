- 👋 Hi, I’m @yck0173
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
yck0173/yck0173 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html>

<head>
    <title>Calendar Example</title>
    <style>
        body {
            text-align: center;
        }

        .calendar {
            width: 350px;
            font-family: Arial, sans-serif;
        }

        .header {
            font-weight: bold;
            padding: 10px;
            background-color: white;
        }

        .weekdays {
            display: flex;
            justify-content: center;
            padding: 5px;
            background-color: white;
        }

        .weekdays .day {
            width: 46px;
        }

        .days {
            justify-content: center;
            display: flex;
            flex-wrap: wrap;
            padding: 2px;
        }

        .days .day {
            width: 45px;
            height: 45px;
            line-height: 45px;
            border: 1px solid black;
        }

        /* 이전달과 다음달의 날짜 */
        .days .day.other-month {
            color: grey;
        }

        /* 오늘 날짜 표시 */
        .days .day.today {
            background-color: palegreen;
        }
    </style>

</head>

<body>

    <body>
        <div class="calendar">

            <div class="header"></div>
            <button class="prev" onclick="prevMonth()">&lt;</button>
            <button class="today" onclick="goToday()">Today</button>
            <button class="next" onclick="nextMonth()">&gt;</button>

            <div class="weekdays">
                <div class="day">일</div>
                <div class="day">월</div>
                <div class="day">화</div>
                <div class="day">수</div>
                <div class="day">목</div>
                <div class="day">금</div>
                <div class="day">토</div>
            </div>
            <div class="days"></div>
        </div>
    </body>

    <script>
        var currentDate = new Date();

        function renderCalendar() {
            // 달력 요소 가져오기
            var calendar = document.querySelector('.calendar');

            // 헤더 요소 가져오기
            var header = calendar.querySelector('.header');

            // 요일 요소 가져오기
            var daysContainer = calendar.querySelector('.days');

            // 수행했던 동작을 삭제하고 새로운 달을 화면에 보여준다.
            header.textContent = '';
            daysContainer.innerHTML = '';
            
            var year = currentDate.getFullYear();
            var month = currentDate.getMonth();
            var date = new Date(year, month);

            // 현재 월과 연도를 표시하도록 헤더 텍스트 설정
            header.textContent = date.toLocaleString('default', { month: 'long' }) + ' ' + year;

            // 현재 달의 일수 구하기
            var daysInMonth = new Date(year, month + 1, 0).getDate();

            // 해당 월의 첫 번째 날의 인덱스 가져오기
            var firstDayIndex = new Date(year, month, 1).getDay();

            // 월의 첫째 날이 일요일이 아닌 경우 이전 달의 날짜를 렌더링
            if (firstDayIndex > 0) {
                var prevMonth = new Date(year, month, 0);
                var prevMonthDays = prevMonth.getDate();
                for (var i = firstDayIndex -1; i >= 0; i--) {
                    var dayElement = createDayElement(prevMonthDays - i, 'other-month');
                    daysContainer.appendChild(dayElement);
                }
            }

            // 현재 달의 날짜를 구한다
            for (var day = 1; day <= daysInMonth; day++) {
                var dayElement = createDayElement(day);
                daysContainer.appendChild(dayElement);
            }

            // 다음 달의 날짜를 가져온다(31일 이후)
            var remainingSlots = 42 - (firstDayIndex + daysInMonth);
            for (var i = 1; i <= remainingSlots; i++) {
                var dayElement = createDayElement(i, 'other-month');
                daysContainer.appendChild(dayElement);
            }

            // 오늘 날짜 강조 
            var today = new Date();
            if (today.getFullYear() === year && today.getMonth() === month) {
                var todayElement = daysContainer.querySelector(`.day[data-day="${today.getDate()}"]`);
                if (todayElement) {
                    todayElement.classList.add('today');
                }
            }
        }

        function createDayElement(day, className) {
            var dayElement = document.createElement('div');
            dayElement.textContent = day;
            dayElement.classList.add('day');
            if (className) {
                dayElement.classList.add(className);
            }
            dayElement.setAttribute('data-day', day);
            return dayElement;
        }

        // 이전달로 이동하는 버튼의 기능
        function prevMonth() {
            currentDate.setMonth(currentDate.getMonth() - 1);
            renderCalendar();
        }

        // 다음달로 이동하는 버튼의 기능
        function nextMonth() {
            currentDate.setMonth(currentDate.getMonth() + 1);
            renderCalendar();
        }

        // 현재달로 이동하는 버튼의 기능
        function goToday() {
            currentDate = new Date();
            renderCalendar();
        }

        // 달력을 랜더링한다.
        renderCalendar();
    </script>

</html>
