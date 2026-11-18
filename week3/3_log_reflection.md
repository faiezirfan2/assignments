Log, Audit Table, and Reflection


1. AI Interpretation Audit Table

Claim / Statement from AI: "Price increases are driven by steady retail adjustments."

Color Code:      Amber

How It Was Checked: Checked variance in Python. Intro of "steady retail adjustments" lacks direct proof in basic stats.

Acceptance Status: Modified / Caution


Claim / Statement from AI: "Sweetener D saw the highest increase at +23.83%."

Color Code: Green

How It Was Checked: Recomputed using percentage change formula in Jupyter Notebook.

Acceptance Status: Accepted



Claim / Statement from AI: "Mean and median alignment improves purchasing power by 15%."

Color Code: Red

How It Was Checked: Refers to external consumer income data absent from the teaching sheet.

Acceptance Status:  Rejected



2. Confused Classmate Transcript Excerpt

•	Classmate AI: "Why bother checking both the mean and median if the mean is just the regular average?"

•	User: "If prices spike in one city, the mean gets pulled up while the median stays in the true middle where most transactions happen."

•	Classmate AI: "Ah, so the median protects you from being skewed by extreme prices?"

•	User: "Exactly. For a newsroom audience, the median shows what typical shoppers actually pay."



3. Reflection
•	Where did the first draft exceed the data? I caught myself assuming external causes (like transport issues) when the ledger only contained raw prices and dates.

•	What did the audit reveal? The audit forced me to separate strict mathematical observations from unverified assumptions about consumer behavior.




 
