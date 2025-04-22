### Python Comprehension Questions (15 minutes)

#### Example 1: Python Fundamentals

**Data Types and Mutability**:
- Explain the difference between mutable and immutable data types in Python.
- Give examples of each type and explain how their behavior differs when passed to functions.

**List Comprehensions**:
- Explain what list comprehensions are and how they work.
- Convert this for loop to a list comprehension:

```python
numbers = [1, 2, 3, 4, 5]
squared = []
for num in numbers:
    if num % 2 == 0:
        squared.append(num ** 2)
```

**Function Arguments**:
- Explain the difference between `*args` and `**kwargs` in Python functions.
- What potential issues might arise when using mutable default arguments in Python functions?

#### Example 2: Python Concepts

**Error Handling**:
- Explain the purpose of try/except blocks in Python.
- What's the difference between an Exception and an Error in Python?
- When would you use a `finally` clause?

**File Handling**:
- Compare and contrast the different file modes in Python (`'r'`, `'w'`, `'a'`, etc.).
- Why is it recommended to use the `with` statement when working with files?

**Modules and Packages**:
- What's the difference between a module and a package in Python?
- Explain the purpose of the `__init__.py` file in a package.
- How would you import a specific function from a module in a different package?


### Python Code Challenge (40 minutes)

#### Example 1: Text Analyzer

**Problem Description:**
Create a text analyzer that processes a text file and provides various statistics about its contents. The analyzer should count words, find the most common words, calculate average word length, and identify sentences.

**Requirements:**

1. Count the total number of words in the text
2. Find the 5 most common words and their frequencies
3. Calculate the average word length
4. Count the number of sentences
5. Find the longest sentence
6. Handle basic text cleaning (remove punctuation, convert to lowercase)


**Starter Code:**

```python
"""
Text Analyzer

This program analyzes text files and provides statistics about their contents.

Functions to implement:
1. count_words - Count the total number of words
2. find_common_words - Find the most common words and their frequencies
3. calculate_avg_word_length - Calculate the average word length
4. count_sentences - Count the number of sentences
5. find_longest_sentence - Find the longest sentence
"""

import re
from collections import Counter
from typing import List, Dict, Tuple


def read_file(file_path: str) -> str:
    """Read the contents of a file."""
    with open(file_path, 'r', encoding='utf-8') as file:
        return file.read()


def clean_text(text: str) -> str:
    """
    Clean the text by converting to lowercase and handling punctuation.
    
    Args:
        text: The input text to clean
        
    Returns:
        Cleaned text
    """
    # TODO: Implement this function
    # 1. Convert text to lowercase
    # 2. Handle punctuation appropriately
    pass


def count_words(text: str) -> int:
    """
    Count the total number of words in the text.
    
    Args:
        text: The input text
        
    Returns:
        Total number of words
    """
    # TODO: Implement this function
    pass


def find_common_words(text: str, n: int = 5) -> List[Tuple[str, int]]:
    """
    Find the n most common words and their frequencies.
    
    Args:
        text: The input text
        n: Number of common words to find
        
    Returns:
        List of tuples containing words and their frequencies
    """
    # TODO: Implement this function
    # 1. Split text into words
    # 2. Count word frequencies
    # 3. Return the n most common words with their frequencies
    pass


def calculate_avg_word_length(text: str) -> float:
    """
    Calculate the average word length.
    
    Args:
        text: The input text
        
    Returns:
        Average word length
    """
    # TODO: Implement this function
    # 1. Split text into words
    # 2. Calculate the average length
    pass


def count_sentences(text: str) -> int:
    """
    Count the number of sentences in the text.
    
    Args:
        text: The input text
        
    Returns:
        Number of sentences
    """
    # TODO: Implement this function
    # 1. Split text into sentences (consider ., !, ? as sentence endings)
    # 2. Count the sentences
    pass


def find_longest_sentence(text: str) -> str:
    """
    Find the longest sentence in the text.
    
    Args:
        text: The input text
        
    Returns:
        The longest sentence
    """
    # TODO: Implement this function
    # 1. Split text into sentences
    # 2. Find the longest one
    pass


def analyze_text(file_path: str) -> Dict:
    """
    Analyze the text and return various statistics.
    
    Args:
        file_path: Path to the text file
        
    Returns:
        Dictionary containing text statistics
    """
    # Read and clean the text
    text = read_file(file_path)
    cleaned_text = clean_text(text)
    
    # Analyze the text
    word_count = count_words(cleaned_text)
    common_words = find_common_words(cleaned_text)
    avg_word_length = calculate_avg_word_length(cleaned_text)
    sentence_count = count_sentences(text)  # Use original text for sentences
    longest_sentence = find_longest_sentence(text)  # Use original text for sentences
    
    # Return the statistics
    return {
        "word_count": word_count,
        "common_words": common_words,
        "avg_word_length": avg_word_length,
        "sentence_count": sentence_count,
        "longest_sentence": longest_sentence
    }


def main():
    # For testing, create a sample text file
    sample_text = """
    The quick brown fox jumps over the lazy dog. This sentence is often used because it contains every letter of the English alphabet. The five boxing wizards jump quickly! How vexingly quick daft zebras jump.
    
    Python is a high-level, general-purpose programming language. Its design philosophy emphasizes code readability with the use of significant indentation. Python is dynamically-typed and garbage-collected. It supports multiple programming paradigms, including structured, object-oriented, and functional programming.
    
    The fox and the dog were friends in the end. The fox, the dog, and the zebras all lived happily ever after.
    """
    
    with open("sample_text.txt", "w", encoding="utf-8") as f:
        f.write(sample_text)
    
    # Analyze the text
    stats = analyze_text("sample_text.txt")
    
    # Print the results
    print("Text Analysis Results:")
    print(f"Total words: {stats['word_count']}")
    print("\nMost common words:")
    for word, freq in stats['common_words']:
        print(f"- {word}: {freq}")
    print(f"\nAverage word length: {stats['avg_word_length']:.2f} characters")
    print(f"Number of sentences: {stats['sentence_count']}")
    print(f"\nLongest sentence:\n{stats['longest_sentence']}")


if __name__ == "__main__":
    main()
```

#### Example 2: Task Manager

**Problem Description:**
Create a simple command-line task manager that allows users to add, view, update, and delete tasks. Each task should have a title, description, due date, and priority level.

**Requirements:**

1. Add new tasks with title, description, due date, and priority
2. View all tasks or filter by priority
3. Mark tasks as complete
4. Delete tasks
5. Save tasks to a file and load them when the program starts
6. Handle basic error cases


**Starter Code:**
```python
"""
Task Manager

This program implements a simple command-line task manager with the following features:
- Add new tasks
- View all tasks or filter by priority
- Mark tasks as complete
- Delete tasks
- Save tasks to a file and load them when the program starts

Classes to implement:
1. Task - Represents a single task
2. TaskManager - Manages the collection of tasks
"""

import json
import os
from datetime import datetime, date
from typing import List, Dict, Any, Optional


class Task:
    """Represents a single task."""
    
    def __init__(self, title: str, description: str, due_date: date, priority: str, completed: bool = False):
        """
        Initialize a new task.
        
        Args:
            title: Task title
            description: Task description
            due_date: Due date (datetime.date object)
            priority: Priority level (high, medium, low)
            completed: Whether the task is completed
        """
        # TODO: Implement this method
        # 1. Initialize task attributes
        # 2. Validate inputs (e.g., priority should be high, medium, or low)
        pass
    
    def to_dict(self) -> Dict[str, Any]:
        """
        Convert the task to a dictionary for serialization.
        
        Returns:
            Dictionary representation of the task
        """
        # TODO: Implement this method
        # 1. Convert task attributes to a dictionary
        # 2. Convert date objects to strings for JSON serialization
        pass
    
    @classmethod
    def from_dict(cls, data: Dict[str, Any]) -> 'Task':
        """
        Create a task from a dictionary.
        
        Args:
            data: Dictionary containing task data
            
        Returns:
            Task object
        """
        # TODO: Implement this method
        # 1. Extract task attributes from the dictionary
        # 2. Convert string dates back to date objects
        # 3. Create and return a new Task object
        pass
    
    def __str__(self) -> str:
        """Return a string representation of the task."""
        # TODO: Implement this method
        # 1. Format the task as a string for display
        pass


class TaskManager:
    """Manages a collection of tasks."""
    
    def __init__(self, file_path: str = "tasks.json"):
        """
        Initialize the task manager.
        
        Args:
            file_path: Path to the JSON file for storing tasks
        """
        self.file_path = file_path
        self.tasks: List[Task] = []
        self.load_tasks()
    
    def add_task(self, title: str, description: str, due_date_str: str, priority: str) -> Task:
        """
        Add a new task.
        
        Args:
            title: Task title
            description: Task description
            due_date_str: Due date string (YYYY-MM-DD)
            priority: Priority level
            
        Returns:
            The added task
        """
        # TODO: Implement this method
        # 1. Parse the due date string
        # 2. Create a new Task object
        # 3. Add it to the tasks list
        # 4. Save tasks to file
        # 5. Return the new task
        pass
    
    def get_all_tasks(self) -> List[Task]:
        """
        Get all tasks.
        
        Returns:
            List of all tasks
        """
        # TODO: Implement this method
        pass
    
    def get_tasks_by_priority(self, priority: str) -> List[Task]:
        """
        Get tasks filtered by priority.
        
        Args:
            priority: Priority level to filter by
            
        Returns:
            List of tasks with the specified priority
        """
        # TODO: Implement this method
        # 1. Filter tasks by priority
        # 2. Return the filtered list
        pass
    
    def mark_task_completed(self, index: int) -> Optional[Task]:
        """
        Mark a task as completed.
        
        Args:
            index: Index of the task in the tasks list
            
        Returns:
            The updated task or None if index is invalid
        """
        # TODO: Implement this method
        # 1. Check if the index is valid
        # 2. Mark the task as completed
        # 3. Save tasks to file
        # 4. Return the updated task
        pass
    
    def delete_task(self, index: int) -> bool:
        """
        Delete a task.
        
        Args:
            index: Index of the task in the tasks list
            
        Returns:
            True if successful, False otherwise
        """
        # TODO: Implement this method
        # 1. Check if the index is valid
        # 2. Remove the task from the list
        # 3. Save tasks to file
        # 4. Return success status
        pass
    
    def save_tasks(self) -> bool:
        """
        Save tasks to a JSON file.
        
        Returns:
            True if successful, False otherwise
        """
        # TODO: Implement this method
        # 1. Convert tasks to dictionaries
        # 2. Write to JSON file
        # 3. Handle potential errors
        # 4. Return success status
        pass
    
    def load_tasks(self) -> bool:
        """
        Load tasks from a JSON file.
        
        Returns:
            True if successful, False otherwise
        """
        # TODO: Implement this method
        # 1. Check if the file exists
        # 2. Read from JSON file
        # 3. Convert dictionaries to Task objects
        # 4. Handle potential errors
        # 5. Return success status
        pass


def display_menu():
    """Display the main menu."""
    print("\nTask Manager")
    print("1. Add a new task")
    print("2. View all tasks")
    print("3. View tasks by priority")
    print("4. Mark a task as completed")
    print("5. Delete a task")
    print("6. Exit")


def main():
    task_manager = TaskManager()
    
    while True:
        display_menu()
        choice = input("\nEnter your choice (1-6): ")
        
        if choice == "1":
            # Add a new task
            title = input("Enter task title: ")
            description = input("Enter task description: ")
            due_date = input("Enter due date (YYYY-MM-DD): ")
            priority = input("Enter priority (high/medium/low): ")
            
            try:
                task = task_manager.add_task(title, description, due_date, priority)
                print(f"\nTask added: {task}")
            except ValueError as e:
                print(f"\nError: {e}")
        
        elif choice == "2":
            # View all tasks
            tasks = task_manager.get_all_tasks()
            
            if tasks:
                print("\nAll Tasks:")
                for i, task in enumerate(tasks):
                    print(f"{i+1}. {task}")
            else:
                print("\nNo tasks found.")
        
        elif choice == "3":
            # View tasks by priority
            priority = input("\nEnter priority (high/medium/low): ")
            tasks = task_manager.get_tasks_by_priority(priority)
            
            if tasks:
                print(f"\nTasks with {priority} priority:")
                for i, task in enumerate(tasks):
                    print(f"{i+1}. {task}")
            else:
                print(f"\nNo tasks found with {priority} priority.")
        
        elif choice == "4":
            # Mark a task as completed
            tasks = task_manager.get_all_tasks()
            
            if tasks:
                print("\nAll Tasks:")
                for i, task in enumerate(tasks):
                    print(f"{i+1}. {task}")
                
                try:
                    index = int(input("\nEnter the number of the task to mark as completed: ")) - 1
                    task = task_manager.mark_task_completed(index)
                    
                    if task:
                        print(f"\nTask marked as completed: {task}")
                    else:
                        print("\nInvalid task number.")
                except ValueError:
                    print("\nPlease enter a valid number.")
            else:
                print("\nNo tasks found.")
        
        elif choice == "5":
            # Delete a task
            tasks = task_manager.get_all_tasks()
            
            if tasks:
                print("\nAll Tasks:")
                for i, task in enumerate(tasks):
                    print(f"{i+1}. {task}")
                
                try:
                    index = int(input("\nEnter the number of the task to delete: ")) - 1
                    
                    if task_manager.delete_task(index):
                        print("\nTask deleted successfully.")
                    else:
                        print("\nInvalid task number.")
                except ValueError:
                    print("\nPlease enter a valid number.")
            else:
                print("\nNo tasks found.")
        
        elif choice == "6":
            # Exit
            print("\nExiting Task Manager. Goodbye!")
            break
        
        else:
            print("\nInvalid choice. Please enter a number between 1 and 6.")


if __name__ == "__main__":
    main()
```