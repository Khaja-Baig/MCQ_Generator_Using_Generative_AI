MCQ Generator using Google's Generative AI
This Python script generates multiple-choice questions (MCQs) using Google's Generative AI model. It ensures that the generated questions are unique and saves them to a text file.

Features
Generates unique multiple-choice questions based on a given topic and difficulty level.
Saves the generated questions to a text file.
Handles API rate limiting with retries and exponential backoff.
Prerequisites
Python 3.6 or higher
Google Generative AI SDK (google-generativeai)
Installation
Clone the repository:

bash
Copy code
git clone <repository_url>
cd <repository_directory>
Install required packages:

bash
Copy code
pip install google-generativeai
Usage
Run the script:

bash
Copy code
python mcq_generator.py
Enter the required inputs:

Gemini API key: Your API key for accessing Google's Generative AI.
Topic: The subject or topic for which you want to generate MCQs.
Number of MCQs: The number of unique MCQs you want to generate.
Difficulty level: The difficulty level of the questions (e.g., easy, medium, hard).
Output:

The script will generate the specified number of unique MCQs and save them to a text file named <topic>_mcqs.txt.
Code Explanation
Main Functions
configure_genai(api_key): Configures the Generative AI model with the provided API key.
tokenize(text): Tokenizes the text into a set of words for similarity comparison.
jaccard_similarity(set1, set2): Calculates the Jaccard similarity between two sets of words.
generate_mcqs(subject, diff_level, num_mcqs, retries=5): Generates unique MCQs based on the given topic, difficulty level, and number of questions.
save_mcqs_to_txt(mcqs, filename): Saves the generated MCQs to a text file.
main(): The main function that runs the script, takes user inputs, and coordinates the MCQ generation and saving process.
Example Output
sql
Copy code
Enter your Gemini API key: YOUR_API_KEY
Enter the topic: Physics
Enter the number of MCQs: 5
Enter the difficulty level of questions: Medium

Generated 1/5 unique MCQs
Generated 2/5 unique MCQs
Generated 3/5 unique MCQs
Generated 4/5 unique MCQs
Generated 5/5 unique MCQs

5 MCQs on the topic 'Physics' have been generated and saved to Physics_mcqs.txt
Error Handling
The script handles API rate limits by retrying with exponential backoff.
If the API quota is exhausted, the script waits and retries up to 5 times before failing.
License
This project is licensed under the MIT License. See the LICENSE file for details.

Contributing
Contributions are welcome! Please create an issue or pull request if you have suggestions for improvements or bug fixes.

Contact
For any questions or support, please open an issue on the GitHub repository.

