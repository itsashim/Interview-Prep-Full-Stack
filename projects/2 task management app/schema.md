USER model: 
{
  name: String,
  email: { type: String, unique: true },
  password: String,
  preferences: {
    dailyReminderTime: { type: String, default: "08:00" }, // e.g., "08:00"
    timezone: { type: String, default: "UTC" }
  }
}

TASK model: 
{
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true, index: true }, // Index for fast user queries
  title: { type: String, required: true, trim: true },
  description: { type: String, default: "" },
  status: { 
    type: String, 
    enum: ['todo', 'in-progress', 'done'], 
    default: 'todo',
    index: true // We will query this a lot for the Board view
  },
  priority: { type: String, enum: ['low', 'medium', 'high'], default: 'medium' },
  dueDate: { type: Date, default: null },
  // **** THE NEW STUFF ****
  parentTask: { type: mongoose.Schema.Types.ObjectId, ref: 'Task', default: null }, // For Sub-tasks!
  order: { type: Number, default: 0 }, // For drag-and-drop sorting inside the Kanban columns
  completedAt: { type: Date, default: null }, // Set to Date.now() when status becomes 'done'
  createdAt: { type: Date, default: Date.now }
}


4. The "Gotcha" Edge Cases (Day 2 Edition)

Since you asked for edge cases, here is your new checklist:

    Overdue Tasks: If today's date > dueDate and status !== 'done', it should automatically show a red "Overdue" badge on the frontend. (Do NOT change the database; just compute this logic in the frontend or via a virtual field in Mongoose).

    Sub-task Logic:

        If a parent task has 5 sub-tasks, and the user checks off all 5, the parent task should automatically change status to done. (This requires a post save hook in Mongoose or a frontend calculation).

        Deleting a parent task must cascade delete all its sub-tasks (or set their parentTask to null).

    Drag and Drop Optimism: When a user drags a task from "To-Do" to "Done", don't wait for the backend to respond. Update the UI instantly (Optimistic UI), then send the API request. If it fails, revert it.

    Natural Language Input: If a user types "Buy milk tomorrow at 5pm" into the "Quick Add" bar, can you parse "tomorrow" and "5pm" to set the dueDate automatically? (Use a library like chrono-node for this).

    Infinite Scroll vs Pagination: If a user has 10,000 tasks, loading them all will crash the browser. Implement cursor-based pagination (e.g., GET /tasks?limit=20&cursor=xyz).