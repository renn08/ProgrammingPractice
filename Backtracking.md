# Backtracking

When doing backtracking, we typical need a stop criteria(since backtracking is usually recursive), the problem has a tree like down road, a idx indicate how deep we have go into tree and a stack-like data structure to pass through functions and finally a collections of answers when a criteria meet need to put stack like datastructure into answer.

Usually go a dfs fashion, put something in stack go into a branch and after that pop that try things out (backtrack is this step)