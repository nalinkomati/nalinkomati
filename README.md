import tkinter as tk
from tkinter import messagebox

# Define the quiz questions and answers
questions = [
    {
        "question": "What is the first step in starting a business?",
        "options": ["Market Research", "Choosing a business name", "Creating a logo", "Finding investors"],
        "answer": "Market Research"
    },
    {
        "question": "Which financial document shows your business's profits and losses?",
        "options": ["Balance Sheet", "Income Statement", "Cash Flow Statement", "Equity Statement"],
        "answer": "Income Statement"
    },
    {
        "question": "What is the purpose of a business plan?",
        "options": ["To raise funds", "To outline the goals and strategy", "To market the business", "All of the above"],
        "answer": "All of the above"
    },
    {
        "question": "What does 'ROI' stand for in business?",
        "options": ["Rate of Investment", "Return on Investment", "Return on Interest", "Resale of Investment"],
        "answer": "Return on Investment"
    }
]

# Global variables to keep track of the quiz state
current_question = 0
score = 0

# Function to check the user's answer
def check_answer(selected_option):
    global current_question, score

    # Get the correct answer for the current question
    correct_answer = questions[current_question]["answer"]

    # Check if the selected option is correct
    if selected_option == correct_answer:
        score += 1

    # Move to the next question
    current_question += 1

    # If there are more questions, update the UI; otherwise, show the result
    if current_question < len(questions):
        show_question()
    else:
        show_result()

# Function to display the current question
def show_question():
    global current_question

    question_data = questions[current_question]
    
    # Clear the existing options
    for widget in options_frame.winfo_children():
        widget.destroy()

    # Update the question label
    question_label.config(text=question_data["question"])

    # Add the answer options as buttons
    for option in question_data["options"]:
        option_button = tk.Button(options_frame, text=option, width=20, command=lambda option=option: check_answer(option))
        option_button.pack(pady=5)

# Function to show the final result
def show_result():
    result = f"Quiz Over! You scored {score} out of {len(questions)}"
    messagebox.showinfo("Quiz Result", result)

    # Reset the quiz
    global current_question, score
    current_question = 0
    score = 0

    # Start the quiz again
    show_question()

# Set up the main window
root = tk.Tk()
root.title("Entrepreneur Quiz App")
root.geometry("500x400")

# Question label
question_label = tk.Label(root, text="Welcome to the Entrepreneur Quiz!", font=("Arial", 16), wraplength=400)
question_label.pack(pady=20)

# Frame for the answer options
options_frame = tk.Frame(root)
options_frame.pack(pady=20)

# Start the quiz by showing the first question
show_question()

# Run the Tkinter event loop
root.mainloop()
