# Quiz questions

This is only a "quiz" in the loosest sense that it's asking questions whose
answers will be part of your grade. Please use *any resources you want*, as
long as you list those resources (e.g. peers, websites, etc.)

## Navigating logs

1. What is the SHA for the last commit made by Prof. Xanda on the branch
xanda_0000_movie_processing?
(For this and future questions, the first 5 characters is plenty - neither
Git nor I need the whole SHA.)
9b257

2. What is the SHA for the last commit associated with line 9 of this file?
b2ed3

3. What did line 12 of this file say in commit d1d83?

2. I should really finish writing this.

4. What changed between commit e474c and 82045?
The int is added to the line below
-    gross_sort = lambda x : x["Gross"]
+    gross_sort = lambda x : int(x["Gross"])
The -5 is modified to a -6.
-    top_five = rows[:-5:-1]
+    top_five = rows[:-6:-1]

## Predicting merges

Assume at the start of each of these three questions that your
branch for switching to a top-10 list was called `top_ten`
and your branch generalizing to any number of movies was called `top_N`.
Predict the behavior of these three possible operations - you don't
have to provide a full `diff` but you should describe at a high level
what changes would happen.

These questions are supposed to be separate paths, not cumulative;
for example, you should *not* assume that the operations of 5 were run
before 6. When testing outcomes later in the lab, you should make sure to
revert back to the state of the branch before you started these questions.

5. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git merge top_N
```
We first check out the test branch and then perform the merge on this branch. This resulted in a fast-forward merge essentially making the test branch and the top_N branch identical. The test branch changed and the process_movie_data.py file got changed to reflect the changes made in the branch top_N. The top_N branch stayed the same.

6. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout top_ten
git merge test
```
We first check out the top_ten branch and then perform the merge of test on this branch. This resulted in a 3-way merge causing the creation of a new commit called a merge commit. The top_ten branch changed with the quiz.md file being renamed to answers.md in the top_ten branch. The process_movie_data.py file is unchanged. The top_10 branch changed and the test branch remained unchanged.

7. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git rebase top_ten
git rebase top_N
```
We first checkout the test branch. We then run the first rebase in which the test branch is rebased onto the top_ten branch. It rearranges the commit tree such that there is a new commit after the rebase command is run. Since the test branch was rebased onto top_ten it now includes all the commits from top_ten and the new rebase commit. The second rebase resulted in a merge conflict, which was resolved manually based on the instructions in the assignment. The test branch has been rebased onto top_N branch, which means it now contains the commits from top_N. After the conflict was resolved a new commit was created. Thus, after both the rebases the test branch process_movie_data.py has all the changes from top_N, with the default parameter modified to 10.
