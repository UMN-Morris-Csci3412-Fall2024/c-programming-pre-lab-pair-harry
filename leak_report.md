# Leak report

_Use this document to describe whatever memory leaks
you find in `clean_whitespace.c` and how you might fix
them. You should also probably remove this explanatory
text._



1. Leak in strip function:
The strip function uses calloc to allocate memory for the cleaned string.
However, the calling code (including test cases) doesn’t free this memory after using it, which causes a memory leak.


2. Incomplete memory handling in is_clean function:
The is_clean function does free memory in some cases, but only when the cleaned string is different from the original.
If the strings are the same or if strip returns an empty string, the allocated memory isn’t freed, leading to a leak.

Here are how to fix it:
1. Free memory in the strip function:
After calling strip, the calling code should always free the memory for the cleaned string when it’s no longer needed.


2. Add memory freeing to test cases:
Test cases that call strip should free the memory returned by the function. This will prevent memory leaks during testing.


3. Fix the logic in is_clean:
The is_clean function should free memory for all dynamically allocated strings, even if the cleaned string is the same as the original. If strip returns an empty string, we should still free the memory to avoid a leak.