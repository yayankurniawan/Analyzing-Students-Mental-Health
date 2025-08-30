# Analyzing Students Mental Health
<img width="945" height="522" alt="image" src="https://github.com/user-attachments/assets/2d2cea83-f339-4554-8d89-9874f8901587" />

Does going to university in a different country affect your mental health? A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.

Explore the students data using PostgreSQL to find out if you would come to a similar conclusion for international students and see if the length of stay is a contributing factor.

Here is a data description of the columns you may find helpful.

| Field Name    | Description                                      |
| ------------- | ------------------------------------------------ |
| `inter_dom`     | Types of students (international or domestic)   |
| `japanese_cate` | Japanese language proficiency                    |
| `english_cate`  | English language proficiency                     |
| `academic`      | Current academic level (undergraduate or graduate) |
| `age`           | Current age of student                           |
| `stay`          | Current length of stay in years                  |
| `todep`         | Total score of depression (PHQ-9 test)           |
| `tosc`          | Total score of social connectedness (SCS test)   |
| `toas`          | Total score of acculturative stress (ASISS test) |

Explore and analyze the data to see how the length of stay () impacts the average mental health diagnostic scores of the international students present in the study.studentsstay

- Return a table with nine rows and five columns.
- The five columns should be aliased as: , , , , and , in that order.staycount_intaverage_phqaverage_scsaverage_as
- The average columns should contain the average of the (PHQ-9 test), (SCS test), and (ASISS test) columns for each length of stay, rounded to two decimal places.todeptosctoas
- The column should be the number of international students for each length of stay.count_int
- Sort the results by the length of stay in descending order.

```
SELECT 
    stay,                                 -- Length of stay of the student (in years)
    COUNT(stay) AS count_int,             -- Number of international students for each length of stay
    ROUND(AVG(todep), 2) AS average_phq,  -- Average depression score (PHQ-9), rounded to 2 decimals
    ROUND(AVG(tosc), 2) AS average_scs,   -- Average social connectedness score (SCS test), rounded to 2 decimals
    ROUND(AVG(toas), 2) AS average_as     -- Average acculturative stress score (ASISS test), rounded to 2 decimals
FROM students
WHERE inter_dom = 'Inter'                 -- Only include international students
GROUP BY stay                             -- Group results by length of stay
ORDER BY stay DESC;                       -- Sort from longest stay to shortest
```
| Stay (years) | Count | Avg PHQ-9 | Avg SCS | Avg ASISS |
|--------------|--------|-----------|---------|-----------|
| 10           | 1      | 13.00     | 32.00   | 50.00     |
| 8            | 1      | 10.00     | 44.00   | 65.00     |
| 7            | 1      | 4.00      | 48.00   | 67.00     |
| 6            | 4      | 4.50      | 36.00   | 65.42     |
| 4            | 14     | 8.57      | 33.93   | 87.71     |
| 3            | 46     | 9.09      | 37.13   | 78.63     |
| 2            | 39     | 8.28      | 37.08   | 77.67     |
| 1            | 95     | 7.48      | 38.11   | 72.80     |

Key Insights : 

1. Depression (PHQ-9):

- Students with a longer stay (7–10 years) show higher depression scores (10–13).

- Those in the first 1–4 years have lower averages (7.5–9).

2. Social Connectedness (SCS):

- Scores remain moderate (33–48) across all groups.

- Staying longer does not guarantee stronger social ties.

3. Acculturative Stress (ASISS):

- Highest in the first years (72–88), then decreases with longer stays (45–65).
