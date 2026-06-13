#Task 1
Command: grep -E -c "^[^#]" firewall.log
Result: 100000
Explanation: The anchor `^` indicates the beginning of the line. The negated character class `[^#]` matches any character that is not a hashtag, thus ignoring the 4 headers and counting the 100,000 lines of actual events.

#Task 2
Command: grep -E -c " (DROP|REJECT) " firewall.log
Result: 60156
Explanation: The `(DROP|REJECT)` grouping uses the `|` toggle operator to search for either action. The spaces before and after the grouping ensure that it only matches the exact 'action' field and not random letters elsewhere.

#Task 3
Command: grep -E -c " 11\." firewall.log
Result: 33217
Explanation: The leading space ensures that we are delimiting the source IP address field. The period (`.`) is used to escape the dot, forcing the regular expression engine to treat it as a literal character instead of the standard wildcard.

#Task 4
Command: grep -E -c " [0-9]{7}$" firewall.log
Result: 2343
Explanation: The space delimits the beginning of the last field (the size). The class `[0-9]` along with the quantifier `{7}` searches for exactly seven numbers. The anchor `$` fixes this match strictly to the end of the line.