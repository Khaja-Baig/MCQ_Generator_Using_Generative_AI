\## Copilot Great, I have the complete code now! Here\'s a README file
for your project: MCQ GeneratorThis project generates multiple choice
questions (MCQs) using the Gemini AI model. The generated MCQs are saved
to a text file. Features- Generates unique MCQs based on a given subject
and difficulty level. - Ensures the uniqueness of questions using
Jaccard similarity. - Handles API rate limits with exponential
backoff. - Saves the generated MCQs to a text file. Requirements- Python
3.x - google-generativeai library Installation- Clone the repository:

git clone https://github.com/yourusername/mcq-generator.git cd
mcq-generator

\- Install the required libraries:

pip install google-generativeai

Usage- Configure the Gemini AI API key:

configure_genai(api_key)

\- Run the script:

python mcq_generator.py

\- Follow the prompts to enter the subject, number of MCQs, and
difficulty level. Functions- configure_genai(api_key): Configures the
Gemini AI API key. - tokenize(text): Tokenizes the input text. -
jaccard_similarity(set1, set2): Calculates the Jaccard similarity
between two sets. - generate_mcqs(subject, diff_level, num_mcqs,
retries=5): Generates unique MCQs based on the given parameters. -
save_mcqs_to_txt(mcqs, filename): Saves the generated MCQs to a text
file. Example import google.generativeai as genai import json import re
import time

new_tem = \[\]

def configure_genai(api_key): genai.configure(api_key=api_key)

def tokenize(text): return set(re.findall(r\'\\w+\', text.lower()))

def jaccard_similarity(set1, set2): intersection =
len(set1.intersection(set2)) union = len(set1.union(set2)) if union ==
0: return 0 return intersection / union

def generate_mcqs(subject, diff_level, num_mcqs, retries=5): model =
genai.GenerativeModel(\'gemini-pro\') mcqs = set() prompt_template = (
f\"Generate {num_mcqs} unique multiple choice questions of difficulty
level \'{diff_level}\' on the topic \'{subject}\'. The format should
be:\\n\\n\" \"Question: \[question text\]\\n\" \"A) \[option 1\]\\n\"
\"B) \[option 2\]\\n\" \"C) \[option 3\]\\n\" \"D) \[option 4\]\\n\"
\"Correct Answer: \[correct option letter\]\" ) batch_size = num_mcqs
for attempt in range(retries): try: while len(new_tem) \< num_mcqs:
response = model.generate_content(prompt_template) mcq_texts =
response.text.strip().split(\"\\n\\n\") for mcq_text in mcq_texts: if
mcq_text.strip() == \"\": continue try: start_index =
mcq_text.index(\':\') + 1 end_index = mcq_text.index(\'?\') new_q =
mcq_text\[start_index:end_index\].strip() except ValueError: continue
new_q\_tokens = tokenize(new_q) is_similar = False for existing_q in
new_tem: existing_q\_tokens = tokenize(existing_q) similarity =
jaccard_similarity(new_q\_tokens, existing_q\_tokens) if similarity \>
0.8: is_similar = True break if not is_similar: new_tem.append(new_q) if
mcq_text not in mcqs: mcqs.add(mcq_text) print(f\"Generated
{len(new_tem)}/{num_mcqs} unique MCQs\") if len(new_tem) \>= num_mcqs:
break if len(new_tem) \>= num_mcqs: break except Exception as e: if
\"429 Resource has been exhausted\" in str(e): print(e) if attempt \<
retries - 1: wait_time = 60 \* (attempt + 1) print(f\"Quota exhausted.
Retrying after {wait_time} seconds\...\") time.sleep(wait_time) else:
raise else: raise e time.sleep(1) return list(mcqs)\[:num_mcqs\]

def save_mcqs_to_txt(mcqs, filename): with open(filename, \'w\') as
txt_file: for mcq in mcqs: txt_file.write(mcq + \'\\n\\n\')

def main(): api_key = input(\"Enter your Gemini API key: \")
configure_genai(api_key) subject = input(\"Enter the topic: \") num_mcqs
= int(input(\"Enter the number of MCQs: \")) diff_level = input(\"Enter
the difficulty level of questions: \")

try: generated_mcqs = generate_mcqs(subject, diff_level, num_mcqs)
txt_filename = f\"{subject}\_mcqs.txt\" save_mcqs_to_txt(generated_mcqs,
txt_filename) print(f\"\\n{num_mcqs} MCQs on the topic \'{subject}\'
have been generated and saved to {txt_filename}\") except Exception as
e: print(f\"An error occurred: {e}\")

if \_\_name\_\_ == \"\_\_main\_\_\": main()

LicenseThis project is licensed under the MIT License. Feel free to
customize this README file further to suit your needs! If you have any
other requests or need additional information, just let me know. 😊
