# claimlens

An insurance claim and fraud detection website. Enter a claim, and a machine-learning model scores its fraud risk, explains which factors drove the score, and recommends what to do next. Everything runs in the browser with a single HTML file, so there is nothing to install or build.

## Features

- **Fraud scoring**: a logistic-regression model returns a fraud probability from 0 to 100%.
- **Three decisions**: Approve (under 30%), Review (30-60%), Investigate (over 60%).
- **Explainable results**: bars show which factors raised or lowered the risk.
- **Claims log**: every scored claim is saved in the browser. Search, filter by decision, delete rows, or export to CSV.
- **Dashboard**: live counts of claims scored, flagged claims, average risk and payout on hold, plus a risk-score histogram.
- **Model panel**: shows hold-out accuracy and learned weights, with a Retrain button.
- **Motion design**: masked headline reveal, staggered steps, easing demo, morphing submit button, mouse parallax and a full-screen menu. Respects reduced-motion settings.

## Run it

1. Download or clone the repo.
2. Open `index.html` in a browser, or right-click it in VS Code and choose **Open with Live Server**.

Try it: click **Load risky example**, then **Score this claim**.

## How it works

1. On page load, the model trains on 800 synthetic claims and tests on 200 held-out claims.
2. Each claim is converted into 10 numeric signals: claim vs coverage, new policy, prior claims, late reporting, missing police report, missing documents, no witness, night or weekend incident, round amount, and claim-type risk.
3. Each signal is multiplied by its learned weight, summed, and passed through a sigmoid to give a probability.
4. The probability maps to a decision, and the per-feature contributions are shown as the explanation.

## Important note

The model is trained on **synthetic data**, so it is a working demo and not a production fraud detector. Its accuracy figure does not reflect real-world performance. A score is a signal for human review, never a final verdict.

## Using real data

1. Collect historical claims with a confirmed `is_fraud` label (1 or 0).
2. Train a model in Python (scikit-learn, XGBoost or LightGBM), checking precision, recall and ROC-AUC rather than accuracy alone, since fraud is rare.
3. Serve it through an API (for example FastAPI) with a `/score` endpoint.
4. Replace the in-browser `score()` function with a `fetch("/score")` call.
5. Review the model for bias and leakage, and retrain regularly as fraud patterns change.

## Deploy

It is a static site. Deploy to GitHub Pages, Netlify or Vercel by pointing at the repo root. No build command is needed.

## Tech stack

HTML, CSS and vanilla JavaScript. No frameworks or dependencies, apart from the Google Fonts stylesheet.

## Roadmap

- Python training script for real claims data
- FastAPI scoring backend
- Login and shared database
- Gradient-boosted model with SHAP explanations

## License

MIT
