# Personal Expense Tracker
Project that tracks your personal finance

- Authentication : to know who the user is 
- Dashboard : Total Balance, Total Income (month), Total expense (month)
- Recent Transations: list any 5 recent transations
- Add a quick action button to add expense
- Category: food, electricity, entertainment, salary : category type either expense or income according to the category, mentions while creating category
- Create Expense
- Creates Income
- All Transactions
- Settings: Manage user preferred currency
- Analytics: Pie Chart: Visual breakdown of expenses by category (e.g., Food: 40%, Rent: 60%).
Bar Chart: Income vs. Expense for the last 6 months. 


A. User Model
{
  name: String,
  email: { type: String, unique: true },
  password: String (hashed),
  currency: { type: String, default: "USD" },
  createdAt: Date
}

B. Transactions Model
{
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }, // IMPORTANT: Never mix users' data!
  amount: { type: Number, required: true }, // Always store as positive number.
  type: { type: String, enum: ['income', 'expense'], required: true },
  category: { type: String, required: true }, // e.g., "Food", "Rent"
  description: { type: String, trim: true, default: "" },
  date: { type: Date, default: Date.now },
  createdAt: Date
}

C. Category Model
{
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }, 
  name: { type: String, required: true },
  type: { type: String, enum: ['income', 'expense'] }, // Is this category for earning or spending?
  isDefault: { type: Boolean, default: false } // To prevent deleting built-in ones like "Salary"
}