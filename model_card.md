# Model Card: Mood Machine

This model card is for the Mood Machine project, which includes **two** versions of a mood classifier:

1. A **rule based model** implemented in `mood_analyzer.py`
2. A **machine learning model** implemented in `ml_experiments.py` using scikit learn

You may complete this model card for whichever version you used, or compare both if you explored them.

## 1. Model Overview

**Model type:**  
Describe whether you used the rule based model, the ML model, or both.  
Example: “I used the rule based model only” or “I compared both models.”

**Intended purpose:**  
What is this model trying to do?  
Example: classify short text messages as moods like positive, negative, neutral, or mixed.

**How it works (brief):**  
For the rule based version, describe the scoring rules you created.  
The score is based on counting positive and negative words, handling negation, and weighting certain words or emojis.

For the ML version, describe how training works at a high level (no math needed).
The model learns patterns in the training data to predict labels for new posts.



## 2. Data

**Dataset description:**  
Summarize how many posts are in `SAMPLE_POSTS` and how you added new ones.
6 original posts + 4 new posts = 10 total posts.

**Labeling process:**  
Explain how you chose labels for your new examples.  
Mention any posts that were hard to label or could have multiple valid labels.
I labeled the new posts based on my interpretation of the mood expressed. Some posts were tricky, like "Lowkey stressed but kind of proud of myself," which I labeled as "mixed" because it expresses both stress and pride.

**Important characteristics of your dataset:**  
Examples you might include:  

- Contains slang or emojis  
- Includes sarcasm  
- Some posts express mixed feelings  
- Contains short or ambiguous messages
Some include slang ("lowkey"), emojis ("🥲"), and mixed feelings ("Can't decide if I'm sad or just really tired").

**Possible issues with the dataset:**  
Think about imbalance, ambiguity, or missing kinds of language.
The dataset is small and may not cover all the ways people express mood. Some posts are ambiguous and could be labeled differently by different people.

## 3. How the Rule Based Model Works (if used)

**Your scoring rules:**  
Describe the modeling choices you made.  
Examples:  

- How positive and negative words affect score  
- Negation rules you added  
- Weighted words  
- Emoji handling  
- Threshold decisions for labels

I assigned +1 for each positive word and -1 for each negative word. I also added a rule that if a negation word (like "not") appears before a positive word, it flips the score of that word. I weighted certain words like "love" more heavily. For emojis, I treated "🥲" as a positive signal. I set thresholds such that a score > 0 is "positive," < 0 is "negative," and = 0 is "neutral." If there are mixed signals, I label it as "mixed."

**Strengths of this approach:**  
Where does it behave predictably or reasonably well?
It can capture clear cases of positive or negative mood based on the presence of certain words. It also allows for some handling of negation and mixed feelings.

**Weaknesses of this approach:**  
Where does it fail?  
Examples: sarcasm, subtlety, mixed moods, unfamiliar slang.
It struggles with sarcasm, subtle expressions of mood, and posts that contain mixed feelings. It also may not handle slang or new expressions well if they are not in the positive or negative word lists.

## 4. How the ML Model Works (if used)

**Features used:**  
Describe the representation.  
Example: “Bag of words using CountVectorizer.”

**Training data:**  
State that the model trained on `SAMPLE_POSTS` and `TRUE_LABELS`.

**Training behavior:**  
Did you observe changes in accuracy when you added more examples or changed labels?

**Strengths and weaknesses:**  
Strengths might include learning patterns automatically.  
Weaknesses might include overfitting to the training data or picking up spurious cues.

## 5. Evaluation

**How you evaluated the model:**  
Both versions can be evaluated on the labeled posts in `dataset.py`.  
Describe what accuracy you observed.
The rule based model achieved an accuracy of 70% on the training data, while the ML model achieved 100% accuracy. 
However, but struggled with sarcasm and mixed feelings, while the ML model may have overfit to the small training set.

**Examples of correct predictions:**  
Provide 2 or 3 examples and explain why they were correct.

**Examples of incorrect predictions:**  
Provide 2 or 3 examples and explain why the model made a mistake.  
If you used both models, show how their failures differed.

## 6. Limitations

Describe the most important limitations.  
Examples:  

- The dataset is small  
- The model does not generalize to longer posts  
- It cannot detect sarcasm reliably  
- It depends heavily on the words you chose or labeled

The dataset is small and may not capture the full range of language people use to express mood. The model may not generalize well to longer posts or different contexts. It also struggles with sarcasm and mixed feelings, which are common in real language.

## 7. Ethical Considerations

Discuss any potential impacts of using mood detection in real applications.  
Examples: 

- Misclassifying a message expressing distress  
- Misinterpreting mood for certain language communities  
- Privacy considerations if analyzing personal messages

Mood detection could have significant impacts if used in real applications. Misclassifying a message expressing distress as "neutral" or "positive" could lead to missed opportunities for support. The model may also misinterpret mood for certain language communities that use slang or emojis differently. Additionally, analyzing personal messages raises privacy concerns, and users should be informed about how their data is being used.

## 8. Ideas for Improvement

List ways to improve either model.  
Possible directions:  

- Add more labeled data  
- Use TF IDF instead of CountVectorizer  
- Add better preprocessing for emojis or slang  
- Use a small neural network or transformer model  
- Improve the rule based scoring method  
- Add a real test set instead of training accuracy only

To improve the models, I could add more labeled data to better capture the variety of language people use to express mood. For the ML model, I could experiment with using TF IDF instead of CountVectorizer to give more weight to important words. I could also add better preprocessing for emojis and slang to capture their sentiment more accurately. For the rule based model, I could refine the scoring method by adding more nuanced rules for handling mixed feelings and sarcasm. Finally, I could create a separate test set to evaluate the models on unseen data rather than just reporting training accuracy.
