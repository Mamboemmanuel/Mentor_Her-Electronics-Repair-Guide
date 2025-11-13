# Intelligent Student Advisory System - Prolog Report

## 1. Logic Design

The advisory system models expertise through facts and rules.
- **Specializations and required skills** are coded using `specialization/2` and `skill_required/2` facts.
- **Minimum GPA per specialization** is set with `min_gpa/2`.
- **Student profiles** contain their unique ID, name, career goal, GPA, and interest (skills).
- **Suitability rules** combine GPA and skill matches: A specialization is recommended if the student’s GPA meets or exceeds the minimum, and they have at least two matching interests.

## 2. Backtracking and Cut (!)

Standard Prolog rules use backtracking to explore all applicable choices, as in `all_suitable_specializations/2`.
To **control backtracking**, we use the cut operator (!) in `recommend_specialization/2`. This means only the first matching specialization is returned and others are not explored. This is useful for quick, single recommendations.

Example:
```prolog
recommend_specialization(john, Spec). % Returns just one: 'Artificial Intelligence'
all_suitable_specializations(john, Specs). % Returns all: ['Artificial Intelligence', 'Data Science', 'Software Engineering']
```

## 3. Recursion

Skill matching is recursively counted with `count_matching_skills/3` and its helper, which traverses through required skills and sums matches. This allows reasoning about how well a student's interests align with the skills needed for each specialization.

## 4. Sample Run Results

**Student 1: John Mwangi**
- Interests: programming, algorithms, logic, data analysis
- GPA: 3.6
- Recommendations: AI, Data Science, Software Engineering
- Reason: GPA exceeds all, high skill match
- Career goal: AI Researcher

**Student 2: Linda Okello**
- Interests: security, programming, risk assessment, cryptography
- GPA: 3.1
- Recommendations: Software Engineering, Cybersecurity
- Reason: GPA meets Cybersecurity barely, multiple matching skills

**Student 3: Sam Ouma**
- Interests: hardware, protocols, troubleshooting, security
- GPA: 2.9
- Recommendations: Networking, Cybersecurity
- Reason: Skill match weighs more, GPA accepted for Networking

## 5. Challenges and Solutions

- **Skill match threshold:** Determining the minimum number required (chose 2 for realistic advisory).
- **Overlapping interests:** Used recursive matching with `findall/2` for precise skill counts.
- **Controlled backtracking:** Demonstrated both full options and cut-based single recommendations.
- **Logic clarity:** Each rule fully commented for reuse/understanding.

## 6. Optional Extensions

Career goals can be referenced for further tailoring, and advice logic can offer explanations when there are multiple choices.

## 7. Conclusion

This program demonstrates foundational AI expert system techniques: logical reasoning, recursion, and controlled inference. It is easily extensible, transparent, and demonstrates Prolog as a language for intelligent advisory systems.
