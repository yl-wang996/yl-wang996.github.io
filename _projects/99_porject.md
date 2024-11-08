---
layout: page
title: Curriculum Learning in Sentiment Analysis
description: Seminar course
img: assets/img/project5_Curriculum_Learning_in_Sentiment_Analysis.png
importance: 1
category: work
related_publications: true
---
This is a [proposal](https://drive.google.com/file/d/1UOC79kRCLMUrYx1E7UzaAC-prQyFCHK5/view?usp=sharing) of the course seminar, in which the "learning dynamics" has been explored along with the curriculum learning on the task sentiment analysis.

## 1. Introduction
Curriculum learning and anti-curriculum learning investigate the benefits of ordered training, which was inspired by human studying procedures. The examples for training in curriculum learning are ordered by their difficulty levels and are exposed to the model in different ways. In this paper, we will investigate whether curriculum learning could improve the performance of models, more specifically DistilBERT models, compared to standard learning which does not apply curricula. We first calculate the difficulty scores for all the examples in a given dataset based on their loss values. Then, we reorder the dataset with the help of the difficulty scores and quantify the benefits of ordered learning by conducting different experiments on four kinds of learning: curriculum, anti-curriculum, random-curriculum, and standard. Our experiments show that curricula only have marginal benefits when the training time is limited. However, with noisy data added, curricula do improve the performance of a model in general.

## 2. Conclusion
In this paper, we explored the benefits of three types of curricula over standard learning by running an extensive amount of experiments on DistilBERT using our custom IMDB dataset. The results of the experiments show that curricula are not helpful to find the best result when the standard dataset is used and the standard training time is applied. The results do show that curricula have a remarkable performance in terms of the average scores and standard deviation of the accuracy scores. We did obtain some similar results compared to the one which take image as input under the settings of standard learning configuration and added noisy data. And we could conclude that we successfully adopted the general setup in the paper to sentiment analysis.

<h3>The experiment result</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include figure.liquid loading="eager" path="assets/img/project5_Curriculum_Learning_in_Sentiment_Analysis.png" title="example image" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</div>





