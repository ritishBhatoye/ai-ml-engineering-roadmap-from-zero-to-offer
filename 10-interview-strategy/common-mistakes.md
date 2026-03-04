<![CDATA[# Common Mistakes Students Make — And How to Avoid Them

> **These are the patterns I've seen in 500+ interviews.** Every one of these kills candidacies.

---

## Mistake 1: Tutorial Hell

**What happens:** You watch 50 hours of YouTube tutorials but can't implement anything without following along.

**Fix:** After watching any tutorial, close the video and rebuild it from memory. If you can't, you didn't learn it.

## Mistake 2: Skipping Math Fundamentals

**What happens:** You use XGBoost but can't explain gradient descent. Interviewers notice immediately.

**Fix:** Spend 2 weeks on math foundations. You don't need a PhD — but you need to explain gradient descent, Bayes' theorem, and eigenvalues.

## Mistake 3: Using Accuracy on Imbalanced Data

**What happens:** "My model gets 97% accuracy!" — on a dataset where 97% is one class.

**Fix:** Always check class distribution first. Use F1, AUC, or precision-recall for imbalanced problems.

## Mistake 4: Data Leakage Without Realizing It

**What happens:** "My model gets 99.5% AUC!" — because you fit the scaler on the full dataset before splitting.

**Fix:** Split first. Fit only on training data. Use `sklearn.Pipeline`.

## Mistake 5: No Projects, Only Coursework

**What happens:** Resume lists courses taken but no projects built.

**Fix:** Build 2-4 portfolio projects. Push them to GitHub with clean READMEs. Link from your resume.

## Mistake 6: Unreadable Code

**What happens:** Jupyter notebook with 50 unnamed cells, variables like `df2`, `X_new_final_v2`.

**Fix:** Write modular scripts. Use descriptive names. Add docstrings. Follow `clean-ml-code.md`.

## Mistake 7: Can't Explain Their Own Projects

**What happens:** "I followed a Kaggle tutorial" → can't answer "Why did you choose Random Forest?"

**Fix:** For every project decision, document WHY — metric choice, model choice, preprocessing steps. Practice explaining out loud.

## Mistake 8: Over-Relying on Deep Learning

**What happens:** Uses a transformer for binary classification on 1,000 rows of tabular data.

**Fix:** Start simple. XGBoost beats deep learning on tabular data 90% of the time. Complexity must be justified.

## Mistake 9: Ignoring Deployment

**What happens:** All projects end at `model.predict(X_test)`. No API, no Docker, no production awareness.

**Fix:** Deploy at least one project. Wrap in FastAPI, containerize with Docker. Even a local deployment counts.

## Mistake 10: No System Design Awareness

**What happens:** Can train a model but can't answer "How would you serve this to 1M users?"

**Fix:** Study the ML pipeline design framework. Practice whiteboard design for 3-4 common systems.

## Mistake 11: Generic Resume

**What happens:** "Performed data analysis using Python and Machine Learning" — says nothing.

**Fix:** Quantify impact: "Reduced churn prediction error by 12% using XGBoost with engineered features on a 100K-record dataset, deployed via FastAPI."

## Mistake 12: Not Practicing Mock Interviews

**What happens:** Knows the material but freezes under time pressure.

**Fix:** Do at least 5 mock interviews (friend, Pramp, or record yourself). Practice thinking aloud.

## Mistake 13: Applying Only to FAANG

**What happens:** Waits 6 months for a Google response. Ignores 100 mid-tier companies hiring ML interns.

**Fix:** Apply broadly: startups, mid-tier companies, FAANG. Each type tests different skills. More interviews = more practice.

## Mistake 14: Not Reading the Job Description

**What happens:** Applies with a generic resume that doesn't match the role's requirements.

**Fix:** Customize your resume for each application. Highlight projects that match the JD's requirements.

## Mistake 15: Giving Up Too Early

**What happens:** Gets rejected from 3 companies and stops applying.

**Fix:** Rejection is normal. The average student applies to 20-50 positions before getting an offer. Each interview is practice.

---

> **The good news:** Every mistake on this list is fixable. The students who succeed aren't geniuses — they're the ones who prepare systematically and don't repeat the same mistakes.
]]>
