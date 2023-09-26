# EmoJeneration-and-TwitterTwin

## Table of Contents
* [Introduction](#Introduction)
* [Demo and Link](#Demo-and-Link)
* [Creating the Dataset](#Creating-The-Dataset)
* [Model Development](#Model-Development)
* [Results](#Results)
* [Conclusion](#Conclusion)
* [TwitterTwin](#TwitterTwin)
* [Acknowledgements](#Acknowledgements)

## Introduction
### Communicating with Modern-Day Hieroglyphics 

In today's digital age, online communication is a fundamental part of our lives. The concept of an online voice, comprised by words and emojis, has become an integral aspect of one’s identity both online and in person. Because tone is easily lost over online communication, emojis in particular have become an extremely valuable tool to communicate clearly and effectively.

We aim to investigate if there are generational differences in the understanding and functionality of emojis. We designed and implemented a predictive classification model utilizing gradient-boosted decision trees. This model classifies an inputted piece of text into one of five distinct generational groups. To ensure the model's accuracy and relevance, we constructed a dataset composed exclusively of tweets containing emojis. This dataset formed the basis for training and testing for the multiple models we experimented with, allowing us to finely tune their predictive capabilities. During the development phase, we employed advanced data processing, downsampling, and data augmentation techniques to optimize the model's performance.

Our research delves into the intricate relationship between emoji usage and generational characteristics, shedding light on the nuanced ways in which emojis function as a means of expression across different age groups. Understanding these dynamics is pivotal not only for interpersonal communication, but also for businesses seeking to connect with specific audiences and decode the intricate language of emojis in the digital era.

## Demo and Link

https://github.com/EmoJeneration/EmoJeneration-and-TwitterTwin/assets/114437706/2e3ba260-810a-4267-85f0-7e498890c19e

Link to EmoJeneration on HuggingFace: https://huggingface.co/spaces/olivianuzum/EmoJeneration 

## Creating the Dataset

### Data Collection
We chose to extract data from Twitter because of the conversational and personal writing style it allows for, which provides excellent context for each user’s usage of emojis. To create our dataset, we recorded twitter handles and age groups (0-4, based on generational boundaries) from online lists of celebrities by age in order to verify the age of each user. 

To obtain our dataset, we scraped 2100 of each celebrity's most recent emoji-containing, original tweets using rtweet. To ensure that we preserved the authentic voices of celebrities, we excluded retweets from our dataset. We only included tweets with emojis so as to focus the model’s understanding on the meaning and functionality of emojis, rather than their prevalence. 

### Cleaning
We built a function to only remove some special characters, seeing as there are certain special characters, namely emojis, that are important to the model. We used langid to filter our dataset so that it was made up entirely of English tweets. Given that the list of Twitter users from which we scraped included many global celebrities, the language identification model flagged a considerable number of non-English tweets. The dataset went from 139,000 to 85,000 unique tweets.  We used NLTK to remove stop words and tokenize the tweets.

We found that groups 1 and 2 had both the highest number of users and the most active twitter usage. Conversely, celebrities from groups 0 and 4, the oldest and youngest groups, had the lowest volume of tweets. This disproportionate representation resulted in an uneven dataset weighted towards groups 1 and 2. To amend this issue, we cut the dataset so that each group had the same number of tweets, and would therefore be represented equally by the model.

<img width="570" alt="Screenshot 2023-09-18 at 2 25 22 PM" src="https://github.com/EmoJeneration/EmoJeneration-DecisionTrees/assets/114313385/58c992a7-3d1e-4913-acd6-b52e3bddf321">

## Model Development

### TF-IDF and BERTweet
To process our textual data and extract meaningful features, we adopted two distinct yet complementary approaches: TF-IDF (Term Frequency-Inverse Document Frequency) and BERTweet sentence transformers.

By employing two distinct data processing methodologies, we systematically compare the performance of these techniques in the context of understanding generational boundaries in emoji usage. The utilization of separate models facilitated an in-depth evaluation of their strengths and weaknesses, ultimately providing valuable insights into which methodology best suited our research objectives. This comparative analysis not only enhanced the robustness of our investigation but also ensured that we selected the most suitable approach for achieving reliable and meaningful results.

### Data Augmentation and Downsampling
After downsampling the original dataset to create equal sized groups, in an effort to improve model performance we considered various data augmentation techniques. One such method we explored was back translation. However, we encountered a unique challenge in our project—preserving the emojis that hold significant meaning in online communication. Emojis serve as important indicators of tone, sentiment, and intent in our dataset. Additionally, back translating our entire dataset would have required significant amounts of time and computational resources. 

Given these considerations, we opted for an alternative data augmentation technique, naw.ContextualWordEmbsAug, which allowed us to enrich our data with contextually relevant word substitutions while retaining emojis and dataset size. This method, powered by contextual embeddings, works by adding and substituting words with relevant alternatives, effectively expanding the vocabulary and expressions within our text data while preserving the contextual meaning. These contextual embeddings, generated by pre-trained models like BERT and GPT-2, capture word meanings based on the surrounding context, allowing the model to understand the nuances of language usage in online communication. It not only increased the quantity of our training examples but also introduced linguistic variations that mirror the dynamic nature of language used across different generations.

### XGBoost
XGBoost, a gradient-boosted decision tree framework, emerged as the optimal choice for our classification models due to its robustness and versatility in handling both structured and unstructured data. In our quest to fine-tune model performance, we meticulously experimented with various hyperparameters, including the learning rate and other critical parameters, to ensure the models' accuracy and efficiency.

### The Final Models
To comprehensively assess the models' efficacy, we pursued a structured approach by creating four distinct models. Two models were constructed for each data processing methodology, TF-IDF and BERTweet. The first set utilized the downsampled dataset, while the second set incorporated the augmented dataset. This allowed us to evaluate how the inclusion of more data impacts model performance. We conducted an extensive evaluation, measuring precision, recall, and F1 scores across all generational classes, in addition to overall model performance metrics. This rigorous analysis enabled us to gain valuable insights into the strengths and limitations of each model and data processing approach, ultimately guiding our selection of the most effective strategy for discerning generational boundaries in emoji usage.

### Results

<img width="570"
src="https://raw.githubusercontent.com/EmoJeneration/images/main/overall.png">

<details>
<summary>Downsampled Datset With TFIDF</summary>

![Precision](https://raw.githubusercontent.com/EmoJeneration/images/main/1111.png)
![Recall](https://raw.githubusercontent.com/EmoJeneration/images/main/1112.png)
![F1](https://raw.githubusercontent.com/EmoJeneration/images/main/1113.png)

</details>

<details>
<summary>Augmented Datset With TFIDF</summary>

![Precision](https://raw.githubusercontent.com/EmoJeneration/images/main/2111.png)
![Recall](https://raw.githubusercontent.com/EmoJeneration/images/main/2112.png)
![F1](https://raw.githubusercontent.com/EmoJeneration/images/main/2113.png)

</details>

<details>
<summary>Downsampled Datset With BERTweet</summary>

![Precision](https://raw.githubusercontent.com/EmoJeneration/images/main/3111.png)
![Recall](https://raw.githubusercontent.com/EmoJeneration/images/main/3112.png)
![F1](https://raw.githubusercontent.com/EmoJeneration/images/main/3113.png)

</details>

<details>
<summary>Augmented Datset With BERTweet</summary>

![Precision](https://raw.githubusercontent.com/EmoJeneration/images/main/4111.png)
![Recall](https://raw.githubusercontent.com/EmoJeneration/images/main/4112.png)
![F1](https://raw.githubusercontent.com/EmoJeneration/images/main/4113.png)

</details>

The model utilizing TF-IDF and gradient boosted decision trees with the downsampled dataset performed the best due to its consistency in precision, recall, and F1 scores among each group. This indicates the least amount of bias, as well as an overall prediction accuracy of about 53%. This model performed at a slightly higher accuracy using the augmented dataset (<1%), but had a higher standard deviation of recall scores.

To evaluate the weight of the emojis over the TF-IDF model’s performance we removed the emojis from both the reduced and augmented datasets. This produced a significant decrease in the precision, recall, and F1 scores. Hence, emojis prove to be a valuable distinction between each generation’s communication style.

From the precision, recall, and F1 scores per group, groups 1 and 2 consistently scored lower than the others in all 3 of these methods of evaluation. This could be attributed to similarities in the conversational styles and usage of emojis between groups 1 and 2, which makes it harder for the model to distinguish between them and accurately guess which group a tweet is coming from. 

For both the reduced and augmented datasets, the model using TF-IDF significantly outperformed the model using Bertweet. It’s possible that the dimensionality reduction through the TF-IDF model was beneficial for our dataset, and helped improve the accuracy of the model. 

The model using Bertweet and the model using TF-IDF without emojis both performed significantly better with the augmented dataset over the reduced dataset. However, the augmentation did not improve the performance of the model using TF-IDF to a significant extent. This indicates that a larger dataset was beneficial for these models to use and extract relevant features. In contrast, the TF-IDF model with emojis was able to bridge the gap between the difference in dataset sizes, indicating that emojis provide extremely relevant and important features to the data.

## Conclusion
Our exploration into the realm of online voices and generational boundaries through predictive classification models led us to several key insights into the relationship between language, emojis, and generational groups.

### Key Findings
Our analysis established that the TF-IDF methodology, when applied to the original dataset containing emojis, yielded the strongest predictive model with 53% precision. This finding underscores the effectiveness of traditional text-based feature extraction methods in discerning the nuances of generational online voices. It demonstrates that, despite the proliferation of advanced language models, classic techniques like TF-IDF still hold their ground when it comes to predicting age groups based on textual input.

Perhaps one of the most intriguing observations from our study was the crucial role played by emojis in enhancing the accuracy of our predictive model. When we examined the datasets without emojis, they significantly underperformed in comparison to those containing emojis. This outcome emphasizes that emojis are not mere embellishments but integral components of online communication. They contribute significantly to the distinct online voices of different generations, acting as markers of expression and emotion that transcend language barriers.

Our research highlights that different generations do indeed possess unique online voices that can be predicted with a degree of reliability. This implies that online communication evolves in distinctive ways across age groups, and these variations can be deciphered through machine learning techniques. The success of our model in making age group predictions based on online behavior suggests that generational traits leave discernible imprints in digital conversations. The role of emojis in our study goes beyond their mere presence; it delves into their evolution over time and the nuanced ways in which they are used by different generations. This finding underscores the need to consider the evolving nature of emojis when interpreting online discourse and devising communication strategies.

### Limitations
Online communication is a complex interplay of numerous factors, including personal preferences, cultural influences, and contextual nuances. Our model represents just one facet of an individual's online voice, thus it cannot comprehensively encapsulate the entirety of online identity.

One of the key limitations we encountered was the variability in model performance among different age groups. Specifically, Groups 1 and 2, roughly representing Millennials and Gen X,  displayed lower predictive accuracy. This could be because these two generations share a similar history of internet and social media use, thus resulting in similar communication patterns. Conversely, Group 0 (Gen Z), 4 (Baby Boomers), and 5 (The Silent Generation), who have more of a distinguishable history and relationship to the internet, albeit for entirely different reasons, exhibited more discernible online communication patterns. The challenges faced by our model in distinguishing between closely related age groups emphasize the intricate nature of generational boundaries and the blurred lines between certain age cohorts.

The use of Twitter data from celebrities in our study brought both advantages and limitations to our research. We opted for this approach out of necessity, as relying on celebrity Twitter accounts provided a reliable means of knowing the age of the users whose data we scraped. However, it's important to highlight a crucial limitation: celebrities do not typically tweet in the same manner as the general Twitter user population. Many of the celebrity Twitter accounts we analyzed were laden with advertisements, promotional tweets, and endorsements. This stark contrast to the way the majority of people tweet online is a significant constraint on the generalizability of our findings.

Our prior exploration through TwitterTwin, a project aimed at matching Twitter users to popular celebrities based on semantic similarity, revealed this limitation. While TwitterTwin excelled at matching celebrities in related industries, such as politicians to Barack Obama or basketball enthusiasts to LeBron James, it often returned only a handful of celebrities for most Twitter users. Notably, those celebrities frequently exhibited a more casual and authentic tweeting style with fewer promotions. This observation underscores the challenge posed by the presence of ads and promotions in celebrity Twitter accounts. Beyond the structural difference in the content of promotional tweets, questions regarding the authenticity of these tweets arise. It's not always guaranteed that the celebrity themselves authored these promotional posts, raising uncertainties about whether the content accurately reflects the celebrity's authentic online voice.

Our reliance on celebrity tweets, while necessary for age group prediction due to the availability of verified age data, comes with a trade-off. This limitation prompts us to acknowledge that while our findings offer insights into generational online voices, they are shaped by the context of celebrity Twitter accounts and may not fully represent the broader Twitter user population's online behaviors and language use.

### Future Directions
Looking ahead, there are several avenues for further optimizing and expanding upon our research project. One of the key areas of improvement could involve refining the definition of generational boundaries to make them as distinct as possible. Fine-tuning these boundaries could enhance the model's predictive accuracy and provide a more nuanced understanding of generational online voices.

Additionally, creating a new dataset based on tweets or text from non-celebrities represents an intriguing direction for future research. While this would undoubtedly pose practical challenges, it could provide a more representative sample of the broader Twitter user population. This expanded dataset would enable us to test and validate our model against a wider range of online voices and potentially uncover additional insights into the linguistic behaviors of different generations.

Exploring alternative data processing techniques and machine learning algorithms is another avenue for improvement. Instead of relying solely on a single data processing method and machine learning algorithm for each model, experimenting with various combinations could lead to enhanced predictive capabilities. This approach would involve a comprehensive evaluation of different feature extraction techniques, algorithm choices, and model architectures to determine the most effective combination for age group prediction.

While there are numerous directions for improving our model, it's worth noting that the current performance is already quite strong given the complexity of the task. The conclusions drawn regarding communication patterns, generational groups, and the role of emojis are likely to remain consistent even with model optimizations. Overall, future iterations of this research hold the potential to provide even deeper insights into the evolving dynamics of online communication and generational differences in the digital age.

### Final Summary and Practical Applications
In summary, our research has illuminated the significance of emojis in shaping online voices and has provided valuable insights into the predictability of age groups based on digital communication patterns. Understanding these dynamics is not only crucial for academic research but also has practical implications for businesses seeking to engage with specific audiences and harness the power of emojis as a tool for effective online communication. As online voices continue to evolve in response to cultural shifts and technological advancements, our study serves as a stepping stone toward a deeper understanding of the intricate language of emojis in the digital age.

## TwitterTwin
Twitter twin is an exploratory project that investigates the language patterns of a broader population. It is an interactive model that inputs any twitter user’s handle and returns the celebrity from our database whose tweets most closely resembles the tweets of the inputted user. Due to the limitations of creating a dataset with verified ages, the broad scope of TwitterTwin provides valuable insight into trends between language and emoji usage.

This model uses sentence transformers and an FAISS index to match inputted Twitter users to one of 19 Twitter celebrities based on semantic similarity. Inputted users typically match with someone in a similar field, for example Mitt Romney and Barack Obama. We found that average twitter users typically match with a select few out of our database, indicating that many verified celebrities on Twitter are not representative of the average user’s tweets. 

The celebrities that match most frequently on TwitterTwin exhibit a casual Twitter presence, whereas the celebrities that match less frequently often contain promotional material for the celebrity’s personal projects, or ads.The language used in these promotions/ads differs from the casual and conversational style that is most prevalently found on Twitter. Further, promotional material is likely heavily edited or entirely written by the celebrity’s management. 

Through TwitterTwin, we gained a better understanding of EmoJeneration’s dataset. Because EmoJeneration strictly uses verified users, the dataset contains a large amount of promotional material that is not representative of the average user’s language. This may affect the model’s training and accuracy scores, seeing as promotions tend to use particular language/emojis.

## Acknowledgements
Thank you to everyone at Data Science UCSB, especially our mentors Mehir Arora and Mateo Wang!
