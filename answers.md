#Task 1
Command: grep -E -c "^[^#]" firewall.log
Result: 100000
Explanation: The anchor `^` indicates the beginning of the line. The negated character class `[^#]` matches any character that is not a hashtag, thus ignoring the 4 headers and counting the 100,000 lines of actual events.

#Task 2
Command: grep -E -c " (DROP|REJECT) " firewall.log
Result: 60156
Explanation: The `(DROP|REJECT)` grouping uses the `|` toggle operator to search for either action. The spaces before and after the grouping ensure that it only matches the exact 'action' field and not random letters elsewhere.