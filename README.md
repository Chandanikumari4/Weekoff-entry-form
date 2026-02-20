# Weekoff-entry-form
Create a responsive weekoff entry layout
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add Work Calendar</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="bg-gray-200 flex items-center justify-center min-h-screen p-4">

    <div class="bg-white w-full max-w-6xl rounded shadow-lg">

        <!-- Header -->
        <div class="flex justify-between items-center px-6 py-4 border-b">
            <h2 class="text-lg font-semibold text-gray-700">Add Work Calendar</h2>
            <button class="text-gray-400 hover:text-gray-600 text-xl">&times;</button>
        </div>

        <div class="p-6">

            <!-- Define Weekend -->
            <div class="mb-4">
                <p class="text-sm font-medium text-gray-600 mb-2">Define weekend</p>
                <label class="flex items-center gap-2 text-sm text-gray-700 cursor-pointer">
                    <input type="checkbox" id="halfToggle" class="w-4 h-4 text-blue-600 border-gray-300 rounded">
                    Half working day & half weekend
                </label>
            </div>

            <!-- Single Table (Fixed Layout) -->
            <div class="border rounded overflow-x-auto">

                <table class="w-full table-fixed text-sm border-collapse">
                    <thead class="bg-gray-50">
                        <tr>
                            <th class="w-40 min-w-[160px] p-3 text-left border"></th>
                            <th class="p-3 text-center border">All</th>
                            <th class="p-3 text-center border">1st</th>
                            <th class="p-3 text-center border">2nd</th>
                            <th class="p-3 text-center border">3rd</th>
                            <th class="p-3 text-center border">4th</th>
                            <th class="p-3 text-center border">5th</th>
                        </tr>
                    </thead>
                    <tbody id="calendarBody"></tbody>
                </table>

            </div><br>
 
            <div>Calendar year definition</div>
            <!-- Footer -->
            <div class="flex gap-3 mt-6">
                <button class="bg-blue-600 text-white px-4 py-2 rounded text-sm hover:bg-blue-700">
                    Save
                </button>
                <button class="bg-gray-200 px-4 py-2 rounded text-sm hover:bg-gray-300">
                    Cancel
                </button>
            </div>

        </div>
    </div>

    <script>
        const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        const calendarBody = document.getElementById("calendarBody");
        const halfToggle = document.getElementById("halfToggle");

        // Create table rows
        days.forEach(day => {
            const tr = document.createElement("tr");

            // Day name column
            const dayCell = document.createElement("td");
            dayCell.className = "p-3 border font-medium text-gray-700";
            dayCell.textContent = day;
            tr.appendChild(dayCell);

            // Columns: All + 1st to 5th
            const columns = ["all", "1", "2", "3", "4", "5"];

            columns.forEach(col => {
                const td = document.createElement("td");
                td.className = "p-3 border text-center";

                const checkbox = document.createElement("input");
                checkbox.type = "checkbox";
                checkbox.className = "day-checkbox";
                checkbox.dataset.day = day;
                checkbox.dataset.col = col;

                td.appendChild(checkbox);
                tr.appendChild(td);
            });

            calendarBody.appendChild(tr);
        });


        // All checkbox controls row
        document.querySelectorAll('.day-checkbox[data-col="all"]').forEach(allBox => {
            allBox.addEventListener("change", function () {
                const day = this.dataset.day;
                const isChecked = this.checked;

                document.querySelectorAll(`.day-checkbox[data-day="${day}"]`).forEach(box => {
                    if (box.dataset.col !== "all") {
                        box.checked = isChecked;
                    }
                });
            });
        });


        // Half working day toggle (visual example behavior)
        halfToggle.addEventListener("change", function () {
            if (this.checked) {
                alert("Half working day mode enabled");
            } else {
                alert("Half working day mode disabled");
            }
        });
    </script>

</body>

</html>
