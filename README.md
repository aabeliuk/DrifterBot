# Introduction

This repo contains the source code and data for the paper *Neutral Bots Reveal Political Bias on Social Media* by Chen et al. ([preprint](https://arxiv.org/abs/2005.08141)).

Social media platforms attempting to curb abuse and misinformation have been accused of political bias. We deploy neutral social bots (we call them *drifters*) on Twitter to probe biases that may emerge from interactions between users, platform mechanisms, and manipulation by inauthentic actors. 

## Repo Structure

+ **`bot`** contains the source code of the drifters. Use `cd bot; python drifter_main.py <your drifter screen_name>` to activate the drifters.
+ **`data`** contains the code and intermediate data files for the analyses.
  + `data/hashtag_political_alignment` has the implementation of hashtag embedding.
  + [`data/GenerateDataFiles.ipynb`](/data/GenerateDataFiles.ipynb) generates data files for our analyses.
+ **`database`** contains the script to create a PostgreSQL database for the analyses.
+ **`exps`** contains scripts and a notebook to generate the plots and tables for the paper.
    + [`exps/FinalPaperPlots.ipynb`](/exps/FinalPaperPlots.ipynb) reads the output files generated by `data/GenerateDataFiles.ipynb` to produce the final figures.
    + [`exps/algorithm_bias_estimation.ipynb`](/exps/algorithm_bias_estimation.ipynb) reads the output files generated by `data/GenerateDataFiles.ipynb` and runs statistical tests to estimate the algorithmic bias.
+ **`exps/news_seed_popuparity`** contains the scripts and data for the news seed popularity analysis
+ **`metric`** contains the scripts to pre-processes the collected data for further analyses. Please run `metric_job.py` as an example. 
    + `analysis.py` and `metrics.py` compute the hashtag-based and url-based political valence score for each Tweet.
    + `time_series_scores.py` computes the political valence changes across time for all drifters. The notebook `data/GenerateDataFiles.ipynb` calls this script.
    + `generate_networks_for_each_bot.py` builds the ego networks for drifters and computes metrics for the echo chamber analyses. The notebook `data/GenerateDataFiles.ipynb` depends on files generated by this script.
+ **`others`** contains the code to initialize and clean up  the drifters.

## Dependencies

1. python 3
2. [twurl](https://github.com/twitter/twurl), modified as shown [here](https://github.com/twitter/twurl/issues/10), is used to manage the drifters. First you need to create a Twitter app. Each drifter account must authorize the app. The keys of the app can then be used with  `twurl` to control the drifters. 
3. [chatterbot](https://chatterbot.readthedocs.io/en/stable/) is used when drifters reply to tweets that mention them.
4. [tweepy](https://www.tweepy.org/) is used in analysis code.
5. [psycopg2](https://pypi.org/project/psycopg2/) is the database driver.
6. [botometer client library](https://github.com/IUNetSci/botometer-python) is used in conjunction with the [Botometer Pro API](https://botometer.iuni.iu.edu/#!/api) to get data from the Twitter API and then calculate bot scores for friends and followers of the drifters.

## Citation

Please cite our paper as:

```
@techreport{drifter2020,
  Author = {Wen Chen and Diogo Pacheco and Kai-Cheng Yang and Filippo Menczer},
  Institution = {arXiv},
  Number = {2005.08141},
  Title = {Neutral Bots Reveal Political Bias on Social Media},
  Type = {Preprint},
  Url = {https://arxiv.org/abs/2005.08141},
  Year = {2020}
}
```
