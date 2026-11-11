Cleaning Log & Reflection

AI Code Trial (Verdicts)

clean = clean.dropna() (AI Suggestion)

Verdict: Reject (Wrong Suggestion).
Reason: 
The AI suggested dropping all rows with missing values or invalid formats to quickly get a "clean" dataset. I rejected this because deleting Row 5 (missing price) removes a real, valid observation. Retaining missing values as NaN is more honest than deleting data to make counts look neat.

clean.drop_duplicates()

Verdict: Keep.
Reason:
Row 96 was an exact duplicate of Row 8 (Staple A). Dropping it brought Staple A down to 23 rows. I kept this change because an honest sample with natural variation is better than keeping artificial duplicates just to look pretty.

str.strip().str.title()

Verdict: Keep & Flag.
Reason: 
Standardized lowercase "oil b" into "Oil B", which pushed Oil B's count to 25. The syntax clean works, but this entry is flagged for audit to verify if it was a formatting typo or a corrupted record.

pd.to_numeric( clean["price"].astype(str).str.replace(",", ""), errors="coerce")

Verdict: Modify.
Reason:
Instead of deleting problematic entries, I stripped the comma from "1,250" and converted extreme outliers (like 9999) to NaN without losing the row structure.


Reflection

•	AI vs. My Decisions:
The AI prioritized making the dataset look uniform by deleting missing records. I chose to preserve honest data, keeping missing values visible as NaN and flagging count imbalances like Oil B (25) and Staple A (23) rather than forcing artificial totals.

•	What I Learned:
Diagnostic checks like .value_counts() and errors="coerce" are essential. Without them, hidden issues like string commas and casing typos would quietly distort final statistical averages.

