#Task 1
Command: grep -E -c "^[^#]" firewall.log
Result: 100000
Explanation: The anchor `^` indicates the beginning of the line. The negated character class `[^#]` matches any character that is not a hashtag, thus ignoring the 4 headers and counting the 100,000 lines of actual events.

