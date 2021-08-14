# Be a Reg-Expert

Imagine that you're a coder that is creating an application that has to parse randomly sourced data and user input, and that your application needs to have the ability to recognize specific patterns. How would you accomplish such functionality? Furthermore, imagine that your application needs to be able to validate the incoming data to be sure that it's in the expected format and doesn't contain any malicious data. How do we validate data format? Lastly, imagine that your application also needs to be able to find and replace certain words, characters, or phrases in a stream of data. Is it possible that there is a single tool that could handle all three of these examples? You bet there is! Regular expressions (generally referred to as regex) are a very powerful tool that can make data parsing much easier and more efficient. Let's learn how regex works and see some examples of what it can do.

## Summary

In this tutorial we will be using a common regular expression (regex) that is used to identify whether a string is a URL or not. We will be learning regex by breaking down the example regex into it's different parts and explaining exactly how each section functions independently, and how it works in tandum with the other parts of the expression. Here is our example:

"/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/"

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors "^","$"
In regex, an anchor is a character that indicates the start or end of a particular line. They can be used independently or together to give you greater control over how strict your search parameters are. For example:

^Starting a line with the carrot character alone will search for all examples where the start of the line matches "Starting" exactly. This means it would not match with "starting", "start", "STARTING, or any combination other than the exact match "Starting."

Likewise, the character "$" will mark the end of a particular line.$ In this example the search will match any instance of "line." and it marks the end of that line. This means that "line," wouldn't match. If you had two instances of "line. line." The first instance of "line." would mark the end of that line and the second instance would be matched as separate match.

When used in combination, ^anchors will mark the beginning and end$ of a line. Taken literally, the previous anchors being used as regular expressions would find exact matches 'f "anchors will mark the beginning and end"; and all the text outside the anchors--both before and after--will not be considered a match.

### Quantifiers "*","?","{}","+"
Just as it sounds, quantifiers are used to identify how many occurrences of a particular series of characters are matched. 

"*" is considered a wildcard, because it will match an infinite number of occurrences and any character/s beginning from that position on. This means that a series of "cat.*" would match all combinations of the word cat, including the period, followed by any combination of characters. All of these combinations would match: "cat.0", "cat.txt", "cat.....", and "cat.cat".

"?" will match the character immediately preceding it exactly 0 or 1 times. This means that "cat.?" would not match the same instances seen with the "*" matching. In this case, the regex "cat.?" would match "cat." or "cat", but not "cat..."

The curly brackets "{}" give greater control over the number of occurences of a combination series. The syntax for using this quantifier will accept up to two values, so both "{3}" and "{3, 10}" are usage examples. They behave similarly, but there is a difference in how they are used. When only a single value is provided then the exression will match the provided series if it occurs exactly the same number of instances as the value provided inside the brackets. So "[aA]{3}" would match any combination of lower and upper case letter "a" up to 3 times. "aAa", "aaa", "Aaa", and "aAA" are all matches; but "a", "A", "aA" are not matches. Another caveat is that it only matches the first instance of that combination--meaning that the combination "aaAA" would only match on the first three characters in that set. 

When two values are provided in the curly brackets "{3, 15}" the lower and upper boundaries are set for the number of expected occurrences. What this means in practical terms is that the string being searched will have to have a minimum of 3 instances of the matching series and no more than 15. Given the set "[aA]{2,6}," the matching characters would need to have at least two occurrences of either lower or upper case a, and no more than 6. The string "aaaAAaa" would only match on the first 6 characters, and the last letter would not be considered a match.

"+" indicates that the character immediatly preceding the "plus" symbol would only match if they occur one or more times. The string "cat" would match "catt", "cattt", or "catttt"; but would not match "ca" or "caT"

### OR Operator "|", "[]"
Similar to how it's used in coding, the pipe symbol "|" indicates a binary matching sequence. This means that the expression will match the series on either the left side or the right side of the pipe, but not both. 

Using the square brackets works essentially the same as the pipe character, but there is a significant difference that leads into another important feature of using regex: "matching" vs. "capturing." When the pipe character is used, the "matching" value is *captured.* What does "capturing" mean? It means that the matching value is actually returned and can be accessed within functions. When the square brackets are used they will only "match" the characters specified, but they will not be returned and can not be accessed from a function.

### Character Classes "\d", "\w", "\s", "."
Character classes are used to match more general classes of characters. These are used to be less specific about the exact character, but more specific about the type of character. For example:

"\d" Will match on any single digit. So it's less specific about which digit it matches, since it will match *any* single digit; but it's more specifc about they type of character that will match. In other words, it will match *only* digits, but it will match *any* digit.

"\w" will match any word character, but is not limited to actual words. Regex is language agnostic for both coding and written language, so it doesn't know when a combination of letters/numbers/underscore are actual words or not. It just sees a combination of an alphanumeric value (including underscore) as a word. Examples of a "word" are "Somebody_20", but not "Somebody.20".

"\s" will match any single whitespace. An expression such as "[a\sb]" would match the combination "a b," and not "ab".

"." will match any individual character. This is similar to the "*" character, in that it will match *any* single character. It's important to be conscious of how wildcards such as "." or "*" are used in an expression since they are slower and less precise that using character classes. 

### Flags "m", "i", "g"

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
