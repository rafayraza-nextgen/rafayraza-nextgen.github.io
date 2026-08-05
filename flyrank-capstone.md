# Finding SEO Quick Wins Using Machine Learning

## 1. Title + Abstract
* **Question:** How can content teams automatically identify which web pages need immediate updates to improve search visibility?
* **Method:** We engineered search performance features and built a simple human-rule baseline to identify high-visibility, low-click pages. We then trained an interpretable Decision Tree Classifier on 90 days of web traffic data to mirror and scale this logic.
* **Validation:** To ensure honesty, we validated the model using a strict client-grouped data split to prevent the algorithm from simply memorizing specific website traffic patterns.
* **Key Result:** The model successfully matched the human baseline with 100% precision on the test set, relying heavily on proportional Click-Through Rate (CTR) rather than raw volume.
* **Impact:** This results in a ranked action playbook that automatically routes the best "Quick Win" pages to human editors.

---

## 2. Introduction
Content teams and SEO managers often oversee thousands, or even millions, of web pages. It is impossible to manually review the analytics for every single page to decide what needs an update. Grouping pages automatically helps teams manage large websites by immediately surfacing the highest-value opportunities. By using data to prioritize work, teams can focus their limited human editing time on the pages that will actually drive traffic growth, rather than guessing where to start.

---

## 3. Data
This project utilizes a large-scale search intelligence dataset covering a 90-day time window of web traffic. To maintain strict data privacy and safety, all personally identifiable information and proprietary data were removed prior to modeling. Specifically, fields such as `client_hash_id`, exact domain names, page URLs, and raw search queries were completely excluded from the feature set. The model only looks at aggregated numerical performance metrics.

---

## 4. Methodology
To build the feature vector, we selected safe metrics that describe page performance: `impressions_90d`, `clicks_90d`, and an engineered `ctr` (Click-Through Rate) feature. Missing values were filled with zero. We chose a Decision Tree Classifier because it is highly interpretable, allowing us to easily audit the exact thresholds it learned and ensuring the model does not act as a "black box." For validation, we used a Client-Grouped Split (GroupKFold). This honest split ensures that pages from the same website do not bleed across the training and testing sets, forcing the model to learn universal SEO rules rather than memorizing a specific client's data.

---

## 5. Results
The model successfully grouped pages into distinct action categories. When compared against the rigid human baseline, the Decision Tree model achieved 100% accuracy, precision, and recall on the isolated test set. Feature importance analysis revealed that the model learned to lean heavily on the `ctr` (Click-Through Rate) ratio rather than just raw impression volume, making it highly effective at spotting underperforming titles. The final output is a ranked queue sorting pages from highest to lowest potential impact.

---

## 6. Limitations
This tool is not fully autonomous and cannot replace human editorial judgment. Our model provides directional, decision-support insights based on observed and measured historical patterns, helping prioritize content reviews. It cannot score brand new pages (under 90 days old) due to a lack of traffic history, and its recommendations may become stale if Google releases a major core algorithm update.

---

## 7. Ranked Recommendations
Based on the model's outputs, we recommend the following content action playbook:

* **Quick Win - Update Title (High Priority):** Pages with high impressions but low CTR. These are highly visible on Google, but users are not clicking. The immediate action is for a human to rewrite the title tag and meta description.
* **Protect - Monitor Traffic (Secondary Priority):** Pages with high impressions and healthy clicks. No immediate edits are needed, but they should be monitored for sudden drops.
* **The No-Go List:** We established a strict rule that legal pages (Privacy Policies, Terms and Conditions), checkout pages, and contact pages must never be automated or altered based on these traffic signals.

---

## 8. Reproducibility
The full Python code, data pipelines, and Jupyter Notebooks used to generate this research are publicly available. You can view the code and reproduce the results by visiting my GitHub repository here: 
[https://github.com/rafayraza-nextgen/flyrank-ml-internship](https://github.com/rafayraza-nextgen/flyrank-ml-internship)

---

## 9. Data Credit
Built on the FlyRank ML Internship dataset. For more information, visit [https://flyrank.ai](https://flyrank.ai).
