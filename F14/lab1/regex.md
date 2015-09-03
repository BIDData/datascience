## Regular Expressions

#### Basic Expressions

The simplest regular expressions are alphanumeric strings, e.g., `/pattern/`,
will match the substring `"pattern"`.

#### Wild Cards and Quantifiers

The character `.` matches any character, so for example, the pattern `/.ed/`
will match all of `"sed"` and `"bed"` and `"1ed"`.

Quantifiers match the preceding expression multiple times.  There are several
quantifier expressions:

* `*` matches the preceding expression 0 or more times 
* `?` matches the preceding expression 0 or 1 times
* `\{n\}` matches the preceding expression `n` times, where `n` is a number
* `\{m,n\}` matches the preceding expression `m` to `n` times, where `n` is a number.

Combine wild cards with quantifiers to match arbitrary strings, e.g., `/.*ed/`
matches all of `"sed"`, `"ed"`, and `"foo bar baz ed"`.

#### Grouping

You can cause an regular expression to be treating as one thing for quantifiers
by surrounding it with `\(...\)`. For example `/\(foo\)\{3\}/` matches 'foofoofoo'.

#### Character Sets

Sometimes `.` is too powerful a wildcard, and what you really want is to match
some characters but not others.  Character sets let you do that.  A character
set is composed of square brackets around the characters you want to match.

For example, `[AEIOU]` matches any uppercase vowel.  You can also invert the
character set with a `^` after the `[`, i.e., `[^AEIOU]` matches anything BUT an
uppercase vowel.  For convenience, you may also list character ranges, e.g.,
`[A-Z]` or `[0-9]`.

#### Beginning and End of a String

You can match the start and end of a string with `^` and `$`, respectively.  As
we will see with `sed`, regular expressions are often evaluated line
by line over a file, and in these instances `^` and `$` refer to the start and
end of the line.

#### Alternation

You can match one or more alternatives with `\|`. For example `/foo|bar/` matches
both `foo` and `bar`. If you only want part of the regular expression to have
alternatives, you can use `\(...\)`. For example `/\(Li\|U\)nix/`
matches both `Linux` and `Unix`.

### Programs other than `sed`

The above guide describes _POSIX Basic Regular Expressions_ which are used by `sed`.
Many regular expression tools, such as `egrep` and [Python's re module](https://docs.python.org/2/library/re.html),
use a syntax based on "extended" regular expressions.
In this style of regular expression, there is no backslash before `|`, `(`, `)`, `{`, or `}`,
so one must write `/(Li|U)nix/` instead of `/\(Li\|U\)nix/`. Instead, putting a backslash before
a nonalphanumeric character always matches that character only.

Although there are standards for regular expressions, in practice, there is a lot of minor
variation in the features and syntaxes that regular expression libraries support, so you
should try to consult documentation for the tool you are using.
