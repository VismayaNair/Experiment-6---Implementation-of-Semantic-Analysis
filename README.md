# Experiment-6---Implementation-of-Semantic-Analysis

## Aim : Construct a python program to read a text from a file.Identify the verbs from the text file and provide synonyms for all verbs using Natutal Language Processing 

## Algorithm:
 1.Import the necessary libraries: nltk and wordnet.
2.Define a function get_verbs(sentence) to identify verbs in a given sentence using part-of-speech tagging.
3.Define a function get_synonyms(word) to get synonyms for a given word using the WordNet corpus.
4.Define a function read_text_file(file_path) to read text from a file and return the content as a string.
In the main program:
5.Set the file_path variable to the path of the input text file.
6.Read the text from the file using the read_text_file() function.
7.Tokenize the text into sentences using the sent_tokenize() function from the nltk library.
8.Initialize an empty list all_verbs to store all identified verbs.
8.Initialize an empty dictionary synonyms_dict to store the synonyms for each verb.
9.Iterate over each sentence:
10.Call the get_verbs() function to identify verbs in the sentence.
11.Append the identified verbs to the all_verbs list.
12.For each verb, call the get_synonyms() function to get its synonyms and store them in the synonyms_dict dictionary.
13.Print the verbs and their synonyms.
14.Execute the main program.


## Program:
```
import nltk
from nltk.corpus import wordnet

nltk.download('averaged_perceptron_tagger')
nltk.download('wordnet')
nltk.download('punkt')

# Function to identify verbs in a sentence
def get_verbs(sentence):
    verbs = []
    pos_tags = nltk.pos_tag(nltk.word_tokenize(sentence))
    for word, tag in pos_tags:
        if tag.startswith('V'):  # Verbs start with 'V' in the POS tag
            verbs.append(word)
    return verbs


def get_synonyms(word):
    synonyms = []
    for syn in wordnet.synsets(word):
        for lemma in syn.lemmas():
            synonyms.append(lemma.name())
    return synonyms


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text


def main():
    file_path = 'sample.txt'

    text = read_text_file(file_path)
    sentences = nltk.sent_tokenize(text)

    all_verbs = []
    synonyms_dict = {}

    for sentence in sentences:
        verbs = get_verbs(sentence)
        all_verbs.extend(verbs)
        for verb in verbs:
            synonyms = get_synonyms(verb)
            synonyms_dict[verb] = synonyms

    with open('output.csv', 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['Verb', 'Synonyms'])
        for verb, synonyms in synonyms_dict.items():
            writer.writerow([verb, ', '.join(synonyms)])


if __name__ == '__main__':
    main()
```



## Output:


## Result
Thus, we have successfully implemented a program for Natural Language Processing.
