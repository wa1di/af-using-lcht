# Adaptive Factorization using Linear-Chained Hash Tables

This repository was created in the aims to improve my understanding of the following paper: https://www.vldb.org/cidrdb/papers/2025/p21-gro.pdf

Compared to the natural language found in papers, I find formal definitions easier to work with due to their concise language. For that reason I have created formal-definitions.md for the sakes of my own personal reference.

While the paper mentions "As a part of this work, DuckDB v1.1.0 adopted the Linear-Chained Hash Table, introduced in this paper," I could not find anything referring to factorization or linear chained hash tables in the newest main branch of the official duckdb repository. For that reason I have searched for the author's repository and found gropaul/duckdb which features a branch named "factorization/aggregation/prod" which appears to be relevant to this given paper. With the help of the following command:

`git diff --color $(git merge-base main refs/remotes/origin/factorization/aggregation/prod)..refs/remotes/origin/factorization/aggregation/prod`,

I've created a diff of the branch ever since the branch was created. I've saved the diff output including the color codes, as diff_facaccpro.txt. If you download the file and open it in a linux terminal like:

`less -R dif_facaccpro.txt`,

it will open as a readable and color coded diff file.
