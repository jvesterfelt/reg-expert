# Be a Reg-Expert

Imagine that you're a coder that is creating an application that needs to parse randomly sourced data and user input, and that your application needs to have the ability to recognize specific patterns. How would you accomplish this? Furthermore, imagine that your application needs to be able to validate the incoming data to be sure that it's in the expected format and doesn't contain any malicious data. How do we validate data formatting? Lastly, imagine that your application also needs to be able to find and replace certain words, characters, or phrases in a stream of data. Is it possible that there is a one tool that could handle all three of these examples? You bet there is! Regular expressions (generally referred to as regex) are very powerful tools that can make data parsing much easier and more efficient. Let's learn how regex works and see some examples of what it can do.

## Summary

In this tutorial we will be using a common regular expression (regex) that is used in many applications. We will be learning regex by breaking down the example regex into the different parts and explaining exactly how each section functions independently, and how it works in tandum with the other parts of the expression. Here is our example:

"/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/"

First, let's discuss the different features of regular expressions and then bring it all together with the breakdown of this expression.

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
In regex, an anchor is a character that indicates the start or end of a particular line. They can be used independently or together to allow greater control over the strictness of the search parameters. For example:

^Starting a line with the carrot character alone will search for all examples where the start of the line exactly matches "Starting". This means it would not match with "starting", "start", "STARTING, or any combination other than the exact match "Starting."

Likewise, the character "$" will mark the end of a particular line.$ In this example the search will match any instance of "line." and it marks the end of that line. This means that "line," wouldn't match. If you had two instances of "line. line." The first instance of "line." would mark the end of that line and the second instance would be matched as separate match.

When used in combination, ^anchors will mark the beginning and end$ of a line. Taken literally, the previous anchors being used as regular expressions would find exact matches of "anchors will mark the beginning and end"; and all the text outside the anchors--both before and after--will not be considered a match.

### Quantifiers "*","?","{}","+"
Just as it sounds, quantifiers are used to identify how many occurrences of a particular series of characters are matched. 

"\*" is considered a wildcard, because it will match an infinite number of occurrences and any character/s beginning from that position on. This means that a series of "cat.*" would match all combinations of the word cat, including the period, followed by any combination of characters. All of these combinations would match: "cat.0", "cat.txt", "cat.....", and "cat.cat".

"?" will match the character immediately preceding it exactly 0 or 1 times. This means that "cat.?" would not match the same instances seen with the "*" matching. In this case, the regex "cat.?" would match "cat." or "cat", but not "cat..."

The curly brackets "{}" give greater control over the number of occurences of a combination series. The syntax for using this quantifier will accept up to two values, so both "{3}" and "{3, 10}" are usage examples. They behave similarly, but there is a difference in how they are used. When only a single value is provided then the expression will match the provided series if it occurs exactly the same number of instances as the value provided inside the brackets. So, "[aA]{3}" would match any combination of lower and upper case the letter "a" up to 3 times. "aAa", "aaa", "Aaa", and "aAA" are all matches; but "a", "A", "aA" are not matches. Another caveat is that it only matches the first instance of that combination--meaning that the combination "aaAA" would only match on the first three characters in that set. 

When two values are provided in the curly brackets "{3, 15}" the lower and upper boundaries are set for the number of expected occurrences. What this means in practical terms is that the string being searched will have to have a minimum of 3 instances of the matching series and no more than 15. Given the set "[aA]{2,6}," the matching characters would need to have at least two occurrences of either lower or upper case ???a???, and no more than 6. The string "aaaAAaa" would only match on the first 6 characters, and the last letter would not be considered a match.

"+" indicates that the character immediatly preceding the "plus" symbol would only match if they occur one or more times. The string "cat" would match "catt", "cattt", or "catttt"; but would not match "ca" or "caT"

### OR Operator "|", "[]"
Similar to how it's used in coding, the pipe symbol "|" indicates a binary matching sequence. This means that the expression will match the series on either the left side or the right side of the pipe, but not both. 

Using the square brackets works essentially the same as the pipe character, but there is a significant difference that leads into another important feature of using regex: "matching" vs. "capturing." When the pipe character is used, the "matching" value is *captured.* What does "capturing" mean? It means that the matching value is actually returned and can be accessed by code. When the square brackets are used they will only "match" the characters specified, but they will not be returned and can not be accessed by code.

### Character Classes "\d", "\w", "\s", "."
Character classes are used to match more general classes of characters. These are used to be less specific about the exact character, but more specific about the type of character. For example:

"\d" Will match on any single digit. So, it's less specific about which digit it matches, since it will match *any* single digit; but it's more specifc about they type of character that will match. In other words, it will match *only* digits, but it will match *any* digit.

"\w" will match any word character; but is not limited to actual words. Regex is language agnostic for both coding and written language, so it doesn't know when a combination of letters/numbers/underscore are actual words or not. It just sees a combination of an alphanumeric value (including underscore) as a word. Examples of a "word" are "Somebody_20", but not "Somebody.20".

"\s" will match any single whitespace. An expression such as "[a\sb]" would match the combination "a b," and not "ab".

"." will match any individual character. This is similar to the "*" character, in that it will match *any* single character. It's important to be conscious of how wildcards such as "." or "*" are used in an expression since they are slower and less precise that using character classes. 

Another important part of using character classes are the negation operators of character classes, which are essentially the inverse of each of the character classes:

"\D" will match any *non-digit* character.
"\W" will match any *non-word* character.
"\S" will match any *non-whitespace* character  

### Flags "m", "i", "g"
Flags add another layer of functionality by allowing to specify how to handle the data being passed. 

"g", or "global", indicates how a search is performed. When it's used the expression will not search from the beginning of the dataset/string, but will begin from where the last search ended instead.

"i", or "insensitive", indicates that you want to treat the entire expression with case-insensitivity. This helps to reduce the clutter when specifying letter characters. For example, both "[a-zA-Z]" and "/[a-z]/i" accomplish the same thing--search for any single letter whether lower or uppercase.

"m", or "multi-line", when used in conjunction with "^" and "$" will mark the beginning and end of a line, rather than the entire data set/string.

### Grouping and Capturing "()"
As previously discussed, regular expressions allow for accessing the matching values when they are *captured*. By placing the series being searched within parentheses functions are able to access the values being returned. This allows for the matching values to be assigned to variables, and used programmatically. 

### Bracket Expressions "[]"
Square brackets define an individual set of criteria to be matched, and allow for building an expression that searches for multiple different sets of expressions. An expression such as "[a-d]|[t-z]" would match on either any single lowercase character between a-d, *OR* match on any single lowercase character between t-z. Similarly, an expression such as "[a-zA-Z]" will search for any single letter regardless of capitalization.

### Greedy and Lazy Match
The previously discussed quantifiers are examples of "greedy operators," since they will expand the search as far as they are allowed by the parameters provided. Conversely, using the "<>" symbols in a search will limit the search to just the parameters inside, making it a lazy search. Neither method is necessarily "wrong" or "right," but are both powerful when used with intent in a search.

### Boundaries "\b", "\B"
Boundaries are similar to the anchors discussed previously--they mark the boundaries defined by the terms of the search. "\b" will search for any whole word: "With this phrase" and expression "\bthis\b would match on the only the word "this" by itself. If the word were crammed in a stream of characters "adoifen*this*adiaoe" then it would not match. Just as "\b" will match only an individual word, it's "negation"--"\B"--will match only if the set is surrounded by whole words or whitespaces. 

### Back-references "\1", "\2", "\3", etc.
To understand the use of back-references it's important to first understand the concept of search groups discussed previously. With regular expressions a search group consists of the search criteria defined and contained within a set of parentheses "([a-z0-9]\i)". If you have multiple sets of searches that define different criteria in each set then you can use back references to essentially repeat a search set and avoid having to write out the pattern again. For example, a set of searches such as this "([a-z]{3})([0-9]{2})([a-z]{3})" could essentially be reduced using a back-reference: "([a-z]{3})([0-9]{2})\1". This reduces the work involved in creating a search, and it reduces the clutter in the search criteria making it easier to read and understand.

### Look-ahead and Look-behind "(?<=)", "(?=)"
For some more specific, and admittedly obscure regex tools, we have the look-ahead and look-behind references. These allow the search criteria to specifically find all references of a character *only when they are preceded or followed by the character in the look-ahead/look-behind.* With a look-ahead search, "a(?=b)", the search will match on all instances of the letter "a" as long as it is followed by the character "b"; *however*, the character "b" will *not* actually be a part of the match. Likewise, with the look-behind "b(?<=a)" will match any instances of the character "b" only when it's preceded by "a", but the "a" will *not* be a part of the match. 

The negation of the look-ahead and look-behind will do the inverse: "a(?!b)" will match on all instances of "a" only when it is *not* followed by "b"; and "a(?<!b)" will match "b" whenever it's not preceded by "a."

# Example Breakdown
Now that we've gone through the criteria used to define a regular expression, let's put it to practical use and break down the example provided at the beginning:

"/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/"

1. The two "/" characters at the beginning and the end are not actually search parameters--they mark the beginning and end of the regular expression.

2. As mentioned before: "^" marks the beginning of the string, and the "$" marks the end. Everything that matches the expression will need to fall within those two characters.

3. We have a total of 4 sets of searches: 
    * (https?:\/\/) is searching for either "http://" or "https://"
    * ([\da-z\.-]+) is searching for any combination of lowercase letters, digits, periods, or hyphens that occurs one or more times.
    * ([a-z\.]{2,6}) is searching for any combination of lowercase letters between 2 and 6 characters in length followed by a period.
    * ([\/\w \.-]*) is searching for any number and combination of words, periods, and hyphens that are preceded by a "/" character.

4. But there are also special search criteria embedded between those sets: 
    * "?" falls between the first and second sets of searches and indicates that the whole previous set may occur either 0 or 1 time exactly.
    * "\." falls between sets 2 and 3, marking the . between the domain and the geographical domain (.com, .ca, .uk, etc.).
    * "*\/?" finishes the search criteria, and will match on any number and combination of the previous search set and may or may not be finished with a "/" character at the end of the string.

Based on this breakdown what is our search expression going to identify? That's right! It will match on any string that is a valid URL (website address) of any length. Great work!

## Author
Jamie Vesterfelt is an aspiring full stack engineer that enjoys writing about coding and technology. Feel free to visit Jamie's [GitHub](https://github.com/jvesterfelt) and view his work, or reach out to talk tech or collaborate on projects.