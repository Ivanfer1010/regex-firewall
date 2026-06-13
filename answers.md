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

#Task 5
Command: grep -E "^[^#]" firewall.log | sed -E 's/^([0-9-]+) [0-9:]+ ([A-Z]+) ([A-Z]+).*/\1 \2 \3/' | head -n 5
Result: 
2018-05-25 FORWARD TCP
2018-02-22 FORWARD UDP
2018-03-20 REJECT UDP
2018-11-08 REJECT TCP
2018-07-24 REJECT TCP
Explanation: `grep` filters the headers. `sed` uses capture groups `()` to extract the date `([0-9-]+)`, ignore the time, and capture the action and protocol `([A-Z]+)`. The reverse references `\1 \2 \3` reconstruct the line by printing only those three elements.

#Task 6
Command: grep -E -c " ACCEPT TCP .* 80 [0-9]+$" firewall.log
Result: 93
Explanation: The literal `ACCEPT TCP` followed by `.*` is combined to quickly skip the source IP and port fields. Then, `80` identifies the correct destination port, ensured by `[0-9]+$` which pushes the match to the numeric size at the end of the line.

#Task 7
Command: grep -E -c "^[0-9-]+ 0[0-2]:[0-9]{2}:[0-9]{2} " firewall.log
Result: 13138
Explanation: The expression `^[0-9-]+` anchors the match by taking the date at the beginning of the line. Then, `0[0-2]` uses a range in a character class to restrict the time strictly to 00, 01, or 02, followed by the exact format of minutes and seconds.

#Bonus
Regex: ^[^ ]{1,15}$
Explanation: The anchors `^` and `$` evaluate the entire string from beginning to end. The negated character class `[^ ]` ensures that there are NO spaces (filtering out phrases), and the quantifier `{1,15}` limits the length to match the requirements of a valid hostname.