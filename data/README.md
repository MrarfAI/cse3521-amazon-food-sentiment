# Group Theta data

The professor assigned **seed 49** to Group Theta. Each team generates its own 50,000-review sample from Amazon Fine Food Reviews. Use the same generated sample throughout the project. The instructions and seed table appear in the [professor's updated announcement](https://osu.instructure.com/courses/208628/discussion_topics/4312999).

## Generate the team sample

1. Sign in to Kaggle and download the [Amazon Fine Food Reviews dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews).
2. Unzip the archive and place `Reviews.csv` in this local `data/` directory.
3. Run the following from the repository root with the project environment activated. It follows the professor's sampling procedure.

```python
import pandas as pd

reviews = pd.read_csv("data/Reviews.csv")
sample = reviews.sample(n=50000, random_state=49)
sample.to_csv("data/group_sample_seed49.csv", index=False)
```

4. Share `group_sample_seed49.csv` within the team and retain it for subsequent milestones. Record the shared file's checksum, duplicate-text rule, split seed, and train/test row identifiers when the data owner implements the training pipeline.

Raw CSV files are ignored by Git. Keep review data and credentials out of the public repository.

## Labels and analysis

The charter maps `Score` to three labels, with 1–2 negative, 3 neutral, and 4–5 positive. Use `Score` only to construct the target. The latest charter reports 3,609 duplicate texts removed, 46,391 remaining reviews, and 78.1% positive reviews in that deduplicated sample. These are the team's reported statistics. Determine the majority label from training data and calculate the baseline accuracy on the held-out test set.

The app's **DEMO ONLY** mode fits models on 18 invented reviews embedded in `sentiment.py`. Team model training uses the seed-49 sample and the agreed preprocessing and data split.
