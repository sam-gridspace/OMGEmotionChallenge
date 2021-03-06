# OMGEmotionChallenge

Website: https://www2.informatik.uni-hamburg.de/wtm/OMG-EmotionChallenge/

**Organization**

Pablo Barros, University of Hamburg, Germany </br>
Egor Lakomkin, University of Hamburg, Germany </br>
Henrique Siqueira, Hamburg University, Germany </br>
Alexander Sutherland, Hamburg University, Germany </br>
Stefan Wermter, Hamburg University, Germany </br>

**OMG Emotion Dataset** 

Our One-Minute-Gradual Emotion Dataset (OMG-Emotion Dataset) is composed of 420 relatively long emotion videos with an average length of 1 minute, collected from a variety of Youtube channels. The videos were selected automatically based on specific search terms related to the term monologue. Using monologue videos allowed for different emotional behaviors  to be presented in one context that changed gradually over time.. Videos were separated into clips based on utterances, and each utterance was annotated by at least five independent subjects using the Amazon Mechanical Turk tool. To maintain the contextual information for each video, each annotator watched the clips of a video in sequence and had to annotate each video using an arousal/valence scale.

Each annotator was also given the full contextual information of the video up to that point when annotating the dataset. That means that each annotator could take into consideration not only the vision and audio information but also the context of each video, i.e. what was spoken in the current and previous utterances through the context clips provided by the annotation tool. In this manner, each annotation is based on multimodal information, different from most recent datasets on emotion recognition. This gives our corpus an advantage when used in cross-modal research, especially when analyzing the audio, vision, and language modalities.

[![Watch the video](https://www2.informatik.uni-hamburg.de/wtm/OMG-EmotionChallenge/images/challenge_details/video1_cover.png)](https://www2.informatik.uni-hamburg.de/wtm/OMG-EmotionChallenge/images/challenge_details/video_01.mp4)

**Annotations and Labels** 

We used the Amazon Mechanical Turk platform to create utterance-level annotation for each video, exemplified in the Figure below. We assure that for each video have a total of 5 different annotations. To make sure that the contextual information was taken into consideration, the annotator watched the whole video in a sequence and was asked, after each utterance, to annotate the arousal and valence of what was displayed. We provide a gold standard for the annotations. This results in trustworthy labels that are truly representative of the subjective annotations from each of the annotators, providing an objective metric for evaluation. That means that for each utterance we have one value of arousal and valence. We then calculate the Concordance Correlation Coefficient (CCC) for each video, which represents the correlation between the annotations and varies from -1 (total disagreement) to 1 (total agreement).

We release the dataset with the gold standar for arousal and valence as well the invidivual annotations for each reviewer, which can help the development of different models. We will calculate the final CCC against the goldstandard for each video. We also distribute the transcripts of what was spoken in each of the videos, as the contextual information is important to determine gradual emotional change through the utterances. The participants are encouraged to use crossmodal information in their models, as the videos were labeled by humans without distinction of any modality. 
We also will let available to the participant teams a set of scripts which will help them to pre-process the dataset and evaluate their model during in the training phase.

![Screenshot](https://www2.informatik.uni-hamburg.de/wtm/OMG-EmotionChallenge/images/challenge_details/Arousal_and_Valence_Annotation-KT_Long-Term_Emotional_Behavior_Dataset.png)


**Dataset Structure** 

The dataset is separated into the following files:

- omg_TrainVideos.csv
- omg_ValidationVideos.csv
- DetailedAnnotations 
- omg_TrainTranscripts.csv 
- omg_TestTranscripts.csv

Each of the data CSV files contain the following information:


link: The link to access the youtube video
start:  the timestamp where the video starts
end: the timestamp where the video ends
video: the video-id, used to associate the video with the annotations
utterance: the utterance name, used to associate the video with the annotations
arousal: the calculated goldstandard of the arousal
valence: the calculated goldstandard of the valence
emotionMaxVote: the resulting categorical emotion from voting over all annotations

the transcripts csvs contain the following information:

link: The link to access the youtube video
video: the video-id, used to associate the video with the annotations
utterance: the utterance name, used to associate the video with the annotations
transcript: The transcript of the audio from each video

We compute the arousal/valence value of a model with the goldstandard of the test set. The categorical emotion will not be used for evaluating the model, but could be usefull when designing or training your model. The categorical emotion is encoded as follows: 
- 0 -  Anger
- 1 - Disgust 
- 2 - Fear 
- 3 - Happy 
- 4 - Neutral 
- 5 - Sad 
- 6 - Surprise

The DetailedAnnotations folder contains all the annotations for each utterance. Each annotation was made when taking into consideration the video as part of a sequence, so it could be useful to use this additional information when designing your 
models.

The Transcripts folder contains all the transcripts for each of the utterance in the dataset.

**Baselines**

To serve a baseline for this challenge, we used three different modesl: one for each modality. 

The vision baseline was made with an updated version of the Face channel [1] pre-trained on the FER+ dataset and fine-tuned with 10 randomly selected faces of each training utterance.

We calculate the Congruence Correlation Coeficient (CCC) and Mean-Squared Error (MSE) for both arousal and valence of the validation set only.

| Modality  | CCC Arousal | CCC Valence | MSE Arousal | MSE Valence | 
| ------------- | ------------- |------------- |------------- |------------- |
| Vision [1]   | 0.13  | 0.27 | 0.054 | 0.132 |

[1] Barros, P., & Wermter, S. (2016). Developing crossmodal expression recognition based on a deep neural model. Adaptive behavior, 24(5), 373-396.


**Scripts** 

We provide the following scripts:

- prepare_data.py: a script used to read, download, cut and organize the dataset.
- calculateEvaluationCCC.py: a script used to calculate the Correlation Concordance Coeficient (CCC) of the output of a model and the validation set. The file with the model's output must be a CSV file containng the following information: 

```
video,utterance,arousal,valence
74de88564,utterance_1.mp4,0.05738688939330001,0.115515408794,
74de88564,utterance_2.mp4,0.05738688939330001,0.119515408794,
74de88564,utterance_3.mp4,0.05738688939330001,0.2122515408794,
74de88564,utterance_4.mp4,0.05738688939330001,0.314515408794,
74de88564,utterance_5.mp4,0.05738688939330001,0.10294515408794,
74de88564,utterance_6.mp4,0.05738688939330001,0.1224515408794,
74de88564,utterance_7.mp4,0.05738688939330001,0.654515408794,
...

```

It is important to note that the order of the videos and utterances present in this file **must** be the same as the order of the videos and utterances on the  omg_ValidationVideos.csv.

**How to participate**

Important dates: 
- Publishing of training and validation data with annotations: March 14, 2018. 
- Publishing of the test data, and opening of the online submission: April 27, 2018.
- Closing of the submission portal (Code and Results): April 30, 2018. 
- Closing of the submission portal (Paper): May 03, 2018. 
- Announcement of the winner through the submission portal: May 04, 2018.


To participate, please send us an email to barros@informatik.uni-hamburg.de with the title "OMG-Emotion Recognition Team Registration". This e-mail must contain the following information: 
- Team Name
- Team Members
- Affiliation

Each team can have a maximum of 5 participants. You will receive from us the access to the dataset and all the important information about how to train and evaluate your models. 
For the final submission, each team will have to send us a .csv file containing the final arousal/valence values for each of the utterances on the test dataset. We also request a link to a GitHub repository where your solution must be stored, and a link to an ArXiv paper with 2-4 pages describing your model and results. The best papers will be invited to submit their detailed research to a journal yet to be specified. Also, the best participating teams will hold an oral presentation about their solution during the WCCI/IJCNN 2018 conference.

**License**

This corpus is distributed under the Creative Commons CC BY-NC-SA 3.0 DE license. If you use this corpus, you have to agree with the following itens:

- To cite our reference in any of your papers that make any use of the database. 
- The references are provided at the end of this page.
- To use the corpus for research purpose only.
- To not provide the corpus to any second parties.


**More information** 

- You can access a detailed information about an early version of the dataset here: https://arxiv.org/abs/1803.05434
- You can also find usefull scripts for processing the dataset here: https://github.com/knowledgetechnologyuhh/OMGEmotionChallenge

For more informations: barros@informatik.uni-hamburg.de
