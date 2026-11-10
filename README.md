# Amazon Food Review Sentiment Analysis

CSE 3521 · Autumn 2026 · Group Theta

A team project that classifies food review text as **negative** (1–2 stars), **neutral** (3 stars), or **positive** (4–5 stars), and compares model predictions in a Streamlit application.

## Current status

The initial app is deployed on **Streamlit Community Cloud**: [Open the live prototype](https://hgbwwg2ig7z6vw2xbgxjz9.streamlit.app/).

**Demo** mode trains Bag-of-Words + Multinomial Naive Bayes and TF-IDF + Logistic Regression on 18 invented food reviews. These are interface demonstrations, not Amazon-trained project models, held-out evaluation, or evidence of predictive quality. **Team models** mode accepts complete, trusted fitted pipelines; no official artifacts are included yet.

The repository is **public**, as required by the project specification (pp. 1, 4, 8), and is owned and administered by **NBNBTM**. Anyone can view the code; direct write access remains limited to the owner and accepted collaborators. No teammates have been invited yet.

## Team

| Member | Primary role |
| --- | --- |
| Abdullah Felemban | Project Lead / Data Engineer |
| Ziwei Li | Data / ML Engineer |
| Lindsey Yang | App Engineer; repository owner |
| Jeffery Lin | Analyst / Writer |

## Run locally

Use Python **3.12**. From this folder:

```sh
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m streamlit run app.py --server.address 127.0.0.1
```

The current Mac already has `.venv` installed. Double-click `run_app.command`, or run:

```sh
.venv/bin/python -m streamlit run app.py --server.address 127.0.0.1
```

Open the local address printed by Streamlit. Choose an example or paste a review, select models, and click **Analyze review**. The app makes no external AI/API requests and has no review-upload or persistence feature. Probabilities are uncalibrated model outputs, not a guarantee that the prediction is correct.

## Model handoff

See [models/README.md](models/README.md). The feature/model owner should export the **entire fitted preprocessing + classifier pipeline**, using the pinned inference dependencies and string class names `negative`, `neutral`, `positive`:

- `models/naive_bayes.joblib`
- `models/logistic_regression.joblib`

The app forwards the entered string unchanged. Agree on `Summary + Text` composition before training, consistent with the charter. Never use `Score` as a feature. Team mode reports missing/incompatible files rather than substituting demo predictions. Only trusted team artifacts may be loaded; joblib can execute Python code.

The deep model will need a separate adapter after the team supplies it. This prototype does not complete the required deep/modern model, full model comparison, or M3 report.

## Data and reproducibility

Group Theta uses the instructor-assigned **seed 49** to draw 50,000 reviews from the full Amazon Fine Food Reviews dataset. Generate `data/group_sample_seed49.csv` using the steps in [data/README.md](data/README.md), then share that file within the team for all project stages. The charter reports 46,391 reviews after removing duplicate texts and a sample positive-class proportion of 78.1%. Recalculate held-out evaluation metrics from the agreed split.

The charter plans duplicate removal before a stratified 80/20 split, shared across models, with feature fitting on training data only. Cross-validation/tuning belongs within the training partition; reserve the test set for final evaluation. Training commands and real-data results will be added by the responsible teammates when implemented. Demo pipelines are fitted in memory by `get_demo_models()`; they require no download.

`requirements.txt` pins the direct runtime dependencies. `requirements-lock.txt` captures the complete tested Python environment. Use the lock file for an identical dependency set:

```sh
python -m pip install -r requirements-lock.txt
python -m unittest discover -s tests -v
```

## Course basis and remaining work

- `Week 6.2/lecture06.pdf`, PDF pp. 4–10: Bag-of-Words, fixed vocabulary, n-grams, TF-IDF.
- `Week 9/lecture09.pdf`, PDF pp. 12–16: Naive Bayes and text/sentiment classification.
- `group_project.pdf`, p. 2: at least two feature representations, two classical models, one deep/modern model, evaluation, and a Streamlit app with two trained models.
- M1 is due Nov 10 at 11:59 pm under the professor's [updated deadline and group-seed announcement](https://osu.instructure.com/courses/208628/discussion_topics/4312999). `group_project.pdf`, pp. 4–5, lists M2 on Nov 15 and M3 on Nov 22 at 11:59 pm.
- `group_project.pdf`, pp. 6–7: final report/slides due Nov 29 at 11:59 pm; live demo date is **See Carmen**, not verified here.
- `group_project.pdf`, p. 8: repository organization, reproducibility, and continuing genuine contribution history.

Remaining team work: obtain/clean the assigned data, train/evaluate official models on the shared split, deliver compatible artifacts, add the deep model, and complete the required report/screenshots. No Carmen submission has been performed.

## Deployment

Live prototype: https://hgbwwg2ig7z6vw2xbgxjz9.streamlit.app/

Streamlit Community Cloud uses repository `NBNBTM/cse3521-amazon-food-sentiment`, branch `main`, entrypoint `app.py`, and Python 3.12. The prominent **DEMO ONLY** warning remains visible. The cloud app has been checked for blank-input handling and side-by-side predictions; real Amazon-trained models are not included yet.

References: [Streamlit deployment](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app), [Streamlit AppTest](https://docs.streamlit.io/develop/api-reference/app-testing/st.testing.v1.apptest), [scikit-learn model persistence](https://scikit-learn.org/stable/model_persistence.html). Course materials above are read-only local references and are not republished in the repository.
