# Work Timeline Tracker

A single-file, zero-dependency web application for visualizing project timelines and managing tasks. This tool is a standalone `index.html` file that runs in any modern browser, making it perfect for quick, portable project management without any setup.

## Features

* **Interactive Timeline:** A drag-and-scroll timeline that displays tasks within colored "Phase" lanes.

* **Task Management:** Add, edit, and move tasks. Tasks can be assigned a status:

  * 🔵 **Ongoing** (Blue)

  * 🟡 **Halted / Issues** (Yellow)

  * 🔴 **Failed** (Red)

  * 🟢 **Completed** (Dimmed Green)

* **Task Details:** Click any task to manage its sub-tasks, add a description, assign it to a person, and add an external link (which appears as a 🔗 icon).

* **Sub-Task Management:** Each task has its own list of sub-tasks, which also have their own status and description.

* **Customizable Phases:** Create "Phase" lanes (e.g., "Design", "Development") and assign them a custom pastel color.

* **Data Persistence:** Save your entire project to a `.json` file and load it back in later.

* **Markdown Reports:** Export a `.md` report that lists all **Ongoing** and **Halted** tasks, grouped by assignee and phase, perfect for daily status updates.

* **"Today" Marker:** A red line on the timeline automatically shows the current date (hardcoded to GMT+8).

## Usage

1. **Open:** Download the `index.html` file and open it in any modern web browser (Chrome, Firefox, Safari, Edge).

2. **Add Phases:** Click "Add Phase" to create your project's main lanes (e.g., "Planning", "Testing").

3. **Add Tasks:** Click "Add Task" to create a task. You can assign its name, phase, assignee, link, description, and dates in the modal.

4. **Edit:** Click any task on the timeline to open the "Task Details" panel. Here you can add sub-tasks or click "Edit Task" (in the top-right controls) to change its details, including moving it to a new phase.

5. **Save/Load:** Use the "Save JSON" button to download your project data. Use "Load JSON" to upload and restore a previously saved project.

6. **Export Report:** Click "Export Report" to download a `Task Status - DD - MM - YYYY.md` file with a summary of all active tasks.

## Customization

Since this is a single-file application, all customization happens within `index.html`.

### 1. Default Data

The application loads with dummy data. To start with a blank project, find the `timelineData` variable in the `<script>` tag and change it to a blank array or a default "To Do" phase:

```javascript
// Before
let timelineData = [
    { id: 1, phaseName: "Design", color: "#8c9e83", tasks: [...] },
    // ... more data
];

// After (for a blank project)
let timelineData = [];

// Or, for a default setup
let timelineData = [
    { id: Date.now(), phaseName: "To Do", color: "#757575", tasks: [] }
];
```

### 2. Colors

* **Phase Colors:** The available pastel colors for phases are defined in the `phaseColorPalette` object. You can add, remove, or change these hex codes.

    ```javascript
    const phaseColorPalette = {
        '#757575': 'Default Grey',
        '#8c9e83': 'Sage',
        '#a1c6e1': 'Sky',
        // ... add your own hex codes and names
    };
    ```

* **Task Status Colors:** The colors for task statuses (Ongoing, Halted, etc.) are defined in the CSS `<style>` tag at the top of the file. You can change the hex codes in the `:root` section.

    ```css
    :root {
        --primary-color: #4fc3f7; /* Ongoing */
        --accent-green: #81c784; /* Completed */
        --accent-orange: #ffb74d; /* Halted */
        --accent-red: #e57373; /* Failed / Today */
    }
    ```

### 3. Timezone

The "Today" marker is hardcoded to `Asia/Singapore` (GMT+8). To change this, find the `getTodayGmt8` function and change the `timeZone` property to your desired IANA timezone.

```javascript

function getTodayGmt8() {
    // ...
    const options = {
        timeZone: 'Asia/Singapore', // <-- Change this
        // ...
    };
    // ...
}
```

## Extending the Functionality

All application logic is contained within the `<script>` tag. The app follows a simple data-driven pattern.

**To add a new property (e.g., "Priority" for Tasks):**

1. **Update Data Model:** Go to `handleAddTaskSubmit` and add the new field to the `newTask` object.

    ```javascript
    const newTask = {
        id: Date.now(),
        name: document.getElementById('modal-task-name').value,
        priority: document.getElementById('modal-task-priority').value, // <-- New
        // ... other properties
    };
    ```
2. **Update Modals:**

    * Add the new input field (e.g., a `<select>` for priority) to the HTML string in `showAddTaskModal`.

    * Add the same field to `showEditTaskModal`, making sure to set its value from the `task` object (e.g., `value="${task.priority || 'low'}"`).

3. **Save Changes:** In `handleSaveTaskChanges`, find the task and update the new property from the modal's input.
    ```javascript
    task.priority = document.getElementById('modal-edit-priority').value; // <-- New
    ```

4. **Display Data:** If you want to show the priority, you can modify `createTaskClipElement` to add an icon, or `renderTaskDetails` to show it in the details panel.

5. **Render:** The `handleSaveTaskChanges` and `handleAddTaskSubmit` functions already call `renderAll()`, which will re-draw the timeline with your new data.