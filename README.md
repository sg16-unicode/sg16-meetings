# SG16 Meeting Summaries

The next SG16 meeting is scheduled for Wednesday, August 29th, from 2:30-4:00pm EDT.

- [July 25th, 2018](#july-25th-2018)
- [July 11th, 2018](#july-11th-2018)
- [June 20th, 2018](#june-20th-2018)
- [May 30th, 2018](#may-30th-2018)
- [May 16th, 2018](#may-16th-2018)
- [April 25th, 2018](#april-25th-2018)
- [April 11th, 2018](#april-11th-2018)
- [March 28th, 2018](#march-28th-2018)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# July 25th, 2018

## Draft agenda:
- Discuss the Unicode support experience with Swift and WebKit representatives
  (tentative pending their availability).
- Review our issues list and start identifying goals for San Diego.

## Meeting summary:
- Attendees:
  - Artem Tokmakov
  - JeanHeyd Meneide
  - Mark Zeren
  - Tom Honermann
  - Zach Laine
- Tom announced that meeting with Swift developers was postponed due to scheduling conflicts and
  that, in the meantime, we'll focus on interaction with them over email.  \[Editor's note:
  Michael Ilseman and Dave Abrahams responded to the initial set of questions.  Their responses
  are available in the SG16 mailing list archive at
  http://www.open-std.org/pipermail/unicode/2018-August/000113.html \]
- Discussion then proceeded with review of the
  [SG16 issues list](https://github.com/sg16-unicode/sg16/issues).
- [Issue #2: Deprecate `std::ctype`, `std::ctype_byname`, `std::isupper()`, and `std::toupper()`](https://github.com/sg16-unicode/sg16/issues/2)
  - Zach suggested writing a direction paper regarding deprecation policies.
  - Artem, observing that the indicated functions are used by iostreams (e.g., by `std::uppercase`),
    suggested we just go the extra mile and deprecate iostreams to a mixture of approval and
    laughter.
  - Mark suggested that the issue scope be limited to previously identified functions.
  - Tom agreed and renamed the issue (previously "Deprecate text/string/character interfaces that
    are too broken to fix").
  - Zach mentioned that `isupper`, `isnum`, and `isalpha` are definitely broken for Unicode and
    expressed a preference that, if we're going to deprecate them, we should do so early in order
    to encourage replacement.
  - Zach went on to explain that replacements that properly handle Unicode must take locale into
    account in order to do title casing and case mapping correctly.
  - Tom asked for clarification - a code point based `toupper()` doesn't make sense?
  - Zach responded, no; more information is needed.
  - Tom asked, what about `isupper()`?
  - Zach answered, Unicode properties can answer that question, but are insufficient for doing
    case conversions.
  - Tom summarized, the take away is that interfaces in `<ctype>` and `<locale>` are definitely
    broken.
  - Mark added, yup, especially considering that `int` is signed.
  - Artem asked about support for UTF-8, UTF-16, and UTF-32.
  - Mark replied, yup, those are problematic.  Even for `char32_t` due to combining code points.
  - Tom stated this is not a high priority for C++20; no objections.
- [Issue #3: Uninitialized append for contiguous containers](https://github.com/sg16-unicode/sg16/issues/3)
  - Mark noted that [P1010](http://wg21.link/p1010) was not presented in Rapperswil; hopefully
    it will be in San Diego.
- [Issue #4: basic_string specification cleanup ](https://github.com/sg16-unicode/sg16/issues/4)
  - Mark mentioned that Tim Song recently proposed some clanup, but those changes don't address
    Mark's iterator invalidation concerns.
- [Issue #5: char8_t (WG21 P0482, WG14 N2231)](https://github.com/sg16-unicode/sg16/issues/5)
  - Tom stated that this is on target for C++20.  Tom has some minor wording changes to make per
    request from early LWG review.
  - Mark asked about the WG14 proposal.
  - Tom replied that WG14 is meeting again in October and that he hopes to have a revision
    ready to present.
- [Issue #6: Specify that char16_t and char32_t literals are UTF-16 and UTF-32 respectively](https://github.com/sg16-unicode/sg16/issues/6)
  - Tom indicated that the paper for this issue, [P1041R1](http://wg21.link/p1041r1), is ready
    for presentation in San Diego.
- [Issue #7: Modern terminology updates](https://github.com/sg16-unicode/sg16/issues/7)
  - Zach observed that this is something that could be done for C++20 since the changes won't
    impact implementors.
  - Tom agreed but lamented a lack of time for working on it now.
- [Issue #8: Explicitly disallow unnamed Unicode codepoints in http://eel.is/c++draft/lex.charset#2](https://github.com/sg16-unicode/sg16/issues/8)
  - Tom expressed a belief that this issue is complete.  Martinho discussed it with CWG members
    in Rapperswil and submitted a [pull request](https://github.com/cplusplus/draft/pull/2201)
    that was accepted as an editorial issue.
  - \[Editor's note: Tom was mistaken.  The accepted pull request addressed a terminology issue
    ("short name" vs "short identifier"); the concern tracked by this issue remains, though
    Martinho has a draft paper [D1139](https://github.com/sg16-unicode/sg16/blob/master/papers/d1139r0.md)
    that addresses it.\]
- [Issue #9: Requiring wchar_t to represent all members of the execution wide character set does not match existing practice](https://github.com/sg16-unicode/sg16/issues/9)
  - Artem summarized: the standard requires that all members of the execution wide character set
    be representable in a single `wchar_t` value.
  - Zach stated a preference for treating this as low priority.  Mark agreed.
  - Zach added that `wchar_t` is already a portability nightmare and there is therefore little
    incentive to try and fix it.  Mark agreed.
- [Issue #15: Add support for named Unicode character escapes](https://github.com/sg16-unicode/sg16/issues/15)
  - Tom indicated that the paper for this issue, [P1097R1](http://wg21.link/p1097r1), is ready
    for presentation in San Diego.
- [Issue #16: code_point_sequence\[\_view\]](https://github.com/sg16-unicode/sg16/issues/16)
  - Tom mentioned that Lyberta, the individual that filed this issue, had also discussed it on the
    mailing list.
  - Zack asked for clarification regarding what this issue is about.
  - Mark summarized: this is the question of whether a `text` type should have `begin()` and
    `end()` members that iterate over grapheme clusters or code points or whether the type should
    not be a range, but provide explicit access to EGC and code point ranges.
  - Tom added that Lyberta had also wanted to expose differences between encoding schemes and
    encoding forms, though it seems this was driven by purity of design goals rather than use
    cases.  Lyberta appeared to want to be able to, effectively, reinterpret cast a sequence of
    UTF16-BE code units (bytes) to a sequence of UTF-16 code units (`char16_t`).  But that doesn't
    work (portably) because bytes and `char16_t` might be the same size.
  - Mark commented, well that is fine, but don't put that in the standard then.  That's why we like
    C++; it lets you break the rules.
- [Issue #30: Unclear behavior for octal and hex escape sequences in Unicode character and string literals](https://github.com/sg16-unicode/sg16/issues/30)
  - Tom expressed a preference for making character literals like `u8'\x80'` well-formed; this
    matches existing practice.
  - Zach disagreed and presented the perspective that `u8`, `u`, and `U` literals should always
    produce well-formed UTF sequences.
  - Tom objected with the observation that `u8'\x80'` can't produce well-formed UTF-8 since it
    only produces a single code unit.
  - Zach suggested that perhaps `u8'\x80'` should be allowed, but `u8"\x80"` should not be.
  - Mark stated that both should be allowed because the programmer explicitly used a hex (or octal)
    escape sequence.
  - Zach objected saying that if he were to use an escape sequence that he wants the compiler to
    validate it.
  - Mark admitted seeing Zach's point.
  - Zach stated that, if a programmer wants to create an ill-formed sequence for some reason, then
    they should use `bit_cast` from a `char` sequence after creating the data.  The intent of adding
    a `u8` prefix to a string is to request well-formed UTF-8.
  - Tom disagreed and stated the intent of adding a `u8` prefix is to enable transcoding from the
    source character set to UTF-8.
  - Mark noted that this distinction is important due to planned changes for `char8_t`.
  - Tom disagreed and stated this is orthogonal since it is independent of the type system.
  - Tom noted that we can address this as a core issue or by writing a paper.
  - Mark said we should write a paper since there are different options for what the behavior
    should be.  Zach agreed.
  - Tom suggested that a core issue be filed to address the difference in what the standard states
    and in what current implementations actually do.  A separate paper can then address what the
    desired behavior is.
  - Zach stated that he doesn't think a defect report suffices to address this.
  - Tom stated that he'll file a core issue; Zach and Mark can follow up with a paper.
  - Mark mentioned that Martinho has a stake in this; that he wanted hex and octal escapes to be
    a back door.
  - JeanHeyd confirmed and agreed that hex and octal escapes should function as back doors.  If
    a programmer wants to ensure well-formed UTF, use `\u` or `\U` or (hopefully soon), `\N{}`.
- [Issue #31: std::text and std::text_view](https://github.com/sg16-unicode/sg16/issues/31)
  - Tom: On-going.
- [Issue #32: std::char_traits<char16_t>::eof() requires uint_least16_t to be larger than 16 bits (LWG#2959)](https://github.com/sg16-unicode/sg16/issues/32)
  - Tom summarized: All 16-bit values are valid UTF-16 code units.  This doesn't leave any room for
    a 16-bit value to be used to indicate EOF.  Implementations often use `0xFFFF` to indicate EOF.
    The result is spurious mismatches with `std::char_traits<char16_t>::eof()` when text encodes
    (valid) UTF-16 `0xFFFF` code units.
  - Zach observed that this isn't solvable without switching to a larger `int_type`.
  - Tom agreed but noted that it is an ABI break.
  - Tom added that libstdc++ made a change to minimize problems by mapping `0xFFFF` code units
    to `0xFFFD` when comparing against `eof()`, but this doesn't solve the problem.
- Tom asked what should be on the list for C++20.  Our `char8_t`, `char16_t` and `char32_t`
  literals are UTF-16/UTF-32, named escape sequences, and uninitialized string append proposals
  are underway.  We could make progress on other issues or work towards C++23 goals like
  `std::text` and `std::text_view`.
- Zach observed that the direction group would likely prioritize feature work over existing
  issues.
- Tom agreed and summarized, it sounds like prioritize features, resolve issues
  opportunistically.
- Zach then provided an update on Boost.Text.  He expects to have it ready for submission for
  Boost review soon; David Sankel has agreed to assist.
- Zach added that he got collation based text searching working and that it was fun because he
  could use Boyer-Moore searching for it.  He asked if any of us had used full collation based
  searching before.
- Artem responded that most people want linguistic searching; for example, searches for "frog"
  return "toad".
- Mark observed that linguistic searching goes a bit beyond Unicode.
- JeanHeyd asked if we should be considering exposing the Unicode character database.  Python
  and Java do \[Editor's note: and the next version of Swift will\].
- Tom was unsure and noted that programmers need for properties like "is number" and "is space"
  often have more strict constraints than Unicode; e.g., when parsing some mini-language.
- Zach added that, for full text processing, you're generally not looking at those properties
  either.
- Mark observed that adding the timezone database nearly made some committee members oppose the
  feature due to the extra 1MB or so of size.


# July 11th, 2018

## Draft agenda:
- Discuss what we want to learn from Swift and WebKit developers.
- Potentially review papers from the Rapperswil post-meeting mailing.
- Review issues list and start identifying goals for San Diego.


## Meeting summary:
- Attendees:
  - Artem Tokmakov
  - Mark Zeren
  - Tom Honermann
  - Victor Zverovich
- Apologies to JeanHeyd Meneide and Steve Downey; It seems technical issues with BlueJeans prevented
  them (and others?) from joining the meeting.  This issue and conflict with the World Cup semi-finals
  reduced attendance.
- Tom reconfirmed intent to rename our mailing list, but has not yet made progress on doing so.
- We then started reviewing some papers from the Rapperswil post-meeting mailing.
- [P0732R2: Class Types in Non-Type Template Parameters](http://wg21.link/p0732r2)
    - Tom asked if `std::text` and/or `std::text_view` should be literal types?
    - Tom noted this would require defining `operator<=>`.
    - Mark suggested adding a `std::text_literal`, but then asked about motivation:
      - `char8_t` allows differentiating encoding for standard mandated encodings.  Is there a need
        to track encoding through non-type template parameters?
      - [P0784](http://wg21.link/p0784) would enable dynamic allocation for literal types, so a
        separate (non-allocating) type may not be required.
    - Victor asked why `operator<=>` is relevant.  
    - Tom explained that `operator<=>` is required for non-type template parameters, but defining it
      for text is problematic because it would be either expensive, or wrong for many use cases
      (e.g., because it would be code unit or code point based).
    - Tom suggested that `std::fixed_string` may suffice since `std::text_view` could be layered
      on top.
    - Mark observed a solution would still be needed for encoding tagging then.
- [P1030R1: std::filesystem::path_view](http://wg21.link/p1030r1)
  - Tom mentioned that we had reviewed the earlier P0 revision during our
    [May 30th meeting](#may-30th-2018).
  - Tom noted that this revision addresses the concern we had with the `char` based interfaces
    requiring UTF-8 encoding.  However, it addresses this by replacing the `char` based interfaces
    with `std::byte` based ones.  This doesn't match existing practice for file name interfaces.
  - Tom mentioned that he would have liked to poll on this change, but since we didn't have a
    quorum, we would not do so.  The poll would have been to restore the `char` based interfaces,
    but to match the encoding requirements for `std::filesystem::path`.
- [P1100R0: Efficient composition with DynamicBuffer](http://wg21.link/p1100r0)
  - Tom wondered if Mark wanted to look at this as potentially related to
    [P1010](http://wg21.link/p1010).
  - Mark responded that he felt it isn't strongly related.
- We then discussed Victor's recent
  [follow up email](http://www.open-std.org/pipermail/unicode/2018-July/000103.html) regarding
  [P0645](http://wg21.link/p0645) and interpretation of field widths.
  - Mark stated that this is fundamentally a console problem, but that field widths are needed
    to implement programs like Eric Niebler's range based calendar example.
  - Mark also asked if we can specify that fill characters only consume one column of output.
  - Tom asked if we can rule out grapheme clusters as the unit of field width on the basis that
    the library must support non-Unicode encodings.
  - Victor suggested we could define a encoding agnostic concept of grapheme clusters.  For
    Unicode, the concept is a 1x1 match with grapheme clusters.  For other encodings, that concept
    might map to code points with no higher abstraction.
  - Tom replied that doing so is viable and that `text_view` would have to do so if its
    `Character` concept were to be redefined in terms of grapheme clusters.
  - Victor reiterated that he wants to implement both code point and grapheme cluster based
    approached and explore use cases.
  - Tom observed that the concerns are effectively equivalent for consoles and text editors;
    assuming use of a monospaced font.
  - Tom asked if `format` is intended as a `printf` replacement.
  - Victor responded, yes, but that doesn't mean that we have to replicate prior mistakes.
  - Tom suggested an experiment: Take Eric's calendar program and modify it to display emojis
    for holidays; e.g., U+1F384 Christmas Tree on December 25th.
- Discussion then turned to questions we'd like to discuss with the Swift and WebKit teams.
  - JeanHeyd (absent due to technical problems), provided the following five questions via Slack:
    - JM1: How many bug reports are related to users incorrectly choosing which layer of abstraction
         to work with for Strings (code units / code points / grapheme clusters)?
      - Tom attempted a clarification; since Swift strings are graphme cluster based, I think this
        question means, are users trying to do things at the grapheme cluster layer when they
        would be better served working at the code unit or code point level?
      - Mark posed the correlated question, how often do users try to work at code unit or code
        point level when they should just work at the grapheme cluster level?
    - JM2: Has the decision to use Extended Grapheme Clusters presented a problem (minor or major)
         in the usage?
      - Mark stated this should be the first question we ask.
      - Mark presented a different way of asking this question: What have been the best and worst
        results of this choice?
    - JM3: Has anyone ever wanted to pry underneath the string abstraction and perform their own set
         of text processing that wasn't supported by the language (e.g., retrieve code units / code
         points so they can do something that Swift did not let them do)? If so, does it happen often?
      - Tom stated the answer to the first question is clearly yes.  The second question is more
        about how often this happens and what the use cases are that motivate doing so.
      - \[Editor's note: a use case may be to work around differences in grapheme cluster boundaries
        in different Unicode versions depending on the version of Swift or the underlying version
        of ICU.\]
      - Mark expressed an interest in string builder use cases.  How are custom string builders
        created?
    - JM4: Has Swift ever considered exposing lower-level unicode database code point / script
         properties? CharacterSet seems to have some of that functionality, but has more ever been
         requested / asked for?
      - Tom expressed enthusiasm for this question.
    - JM5: There's some indication that putting the normalization form and such in the type system may
         prove beneficial. Has there been any progress on that front? We are looking to answer a
         similar question for C++ up-front, and picking one normalization form that might have the
         most up-front processing and performance benefits for typical users.
       - Mark rephrased as, what was the rationale for choosing the current design?
  - Tom then went over a list of questions he had come up with:
    - TH1: The Swift string manifesto is about 1 1/2 years old.  What have you learned since?
    - TH2: If you were starting over, what would you change?
      - Tom stated that this isn't a very useful question; it's too open ended.
      - Mark stated that bug reports are more intersting; What have you had to change?
    - TH3: How tied is the Swift string implementation to ICU?
      - Tom stated the intent of this question is to identify how much of ICU is needed to create
        a useful Unicode string class.
      - Tom added a second goal: to determine if the Swift developers would potentially be interested
        in replacing uses of ICU with standard C++ library features, if they existed.
    - TH4: Swift's string is locale insensitive (yay!).  Was a locale sensitive one considered?  Perhaps
         as a distinct type?
      - Tom stated the intent is to explore if a distinct type for localized strings might be useful
        (since locale is a run-time property not available at compile-time).
    - TH5: How often does string interpolation suffice vs using string formatting?
      - Tom asked Victor if he had considered string interpolation support when designing his `format`
        library.
      - Victor responded, yes, but with uncertainty regarding how to do it in C++ today.  Python started
        with a formatter and added interpolation later.  We could do likewise.
    - TH6: Has canonical string equality been...
      - A performance issue?
      - A surprise to users?
    - TH7: Have substrings turned out to work as well as hoped?
      - Tom noted that Swift substrings seem superficially similar to `std::string_view`, but with
        dynamic lifetime management of the underlying storage.
    - TH8: Are the results of string interpolation always dynamic?  Does Swift have a constexpr equivalent
         and, if so, do they work there?
    - TH9: Would you remove string.count() (returns "character" count) if you could?
      - Tom posed an additional question: How often do people use string.count() incorrectly?
    - TH10: Are the unicodeScalars, utf8, and utf16 views allocating?  Or are they lazy transformations?
    - TH11: There are a variety of "unsafe" methods.  Have they been problematic?
  - Mark suggested an additional question:
    - MZ1: Swift comparisons are provided.  Do users use them incorrectly?  Have they been a performance
           problem?
- Tom stated that our next meeting will be scheduled for July 25th.


# June 20th, 2018

## Draft agenda:
- Rapperswil recap.  Progress!
- Continue review of P0645R2 (Text Formatting), hopefully with
  Victor present if he can attend.
- Review the draft D1097R0 proposal:
  - https://github.com/rmartinho/sg16/blob/master/papers/d1097r0.md
- Discuss what we want to learn from the Swift and WebKit developers.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - JeanHeyd Meneide
  - Keld Simonsen
  - Mark Zeren
  - Martinho Fernandes
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- First order of business was to ensure that papers requiring updates following the Rapperswil meeting
  are submitted in time for the post-Rapperswil mailing.  Tom confirmed that P0482R4 had been submitted
  and correspondence with Hal confirmed that P1025R1 (adopted at Rapperswil) will be included in the
  mailing.  Though not discussed in Rapperswil, Martinho plans to submit a revision of P1041 for the
  mailing.
- [P0645R2](http://wg21.link/p0645r2) - Text Formatting
  - Victor started us off with a brief introduction of recent changes and review in Rapperswil.
  - Victor reported having read the summary of our previous meeting and discussion of P0645.
  - Discussion resumed regarding what field widths mean for multibyte encodings and combining characters.
  - Victor asked if basing field widths on grapheme clusters would be appropriate.
  - Zach provided an example of family emojis.  Consider 4 person code points separated by zero width
    joiners.  Each person code point combined with a ZWJ is a distinct grapheme cluster, but a single
    glyph may be used to display all four clusters.  So, grapheme clusters are not the right abstraction
    for field width.
  - Tom claimed that `format` should be used to format code units.
  - Peter suggested assuming one column per code point.
  - Keld asked about other libraries; are there any that use abstractions above code points for field
    formatting?
  - Tom stated that the competition is `printf` and iostreams.
  - Keld asked what ICU does.
  - Zach responded that he wasn't sure, but that Python uses code points for field formatting.
  - Discussion then moved on to other topics briefly.
  - Zach expressed enthusiasm for `format_to_n`.
  - Tom asked if mixed character encodings are supported.  For example:
    - `format("{}", u"text"); // execution character encoding for format string with UTF-16 argument.`
  - Victor stated that mixed encodings are not supported and result in compilation failure.
  - Zach observed that, if `char8_t` overloads were added, that, internally, `format` must consume
    code points.
  - Tom responded that this is true for any multibyte encoding, and therefore true in general for
    the execution and wide character encodings.
  - Victor agreed, but noted that operations other than fill and field formatting could be optimized
    to avoid looking at code points.
  - Peter asked if any multibyte encodings allow a NUL byte in trailing code unit sequences.  No
    such encodings were named.
  - Peter observed that, if an encoding library is used, `format` can always just read code points.
  - Zach offered to provide Victor code using code point iterators from Boost.Text that could be used
    to prototype code point based approaches.
  - Discussion briefly turned to portability of `wchar_t` and Keld's work to increase the number of
    C interfaces that do not rely on global program state; e.g., locale data.  Keld wants to improve
    support for working with multiple encodings in a single process.
  - Tom noted that such improvements are useful for our ideas around use of compile-time known
    internal encodings with transcoding to run-time determined encodings at program borders.
  - Tom asked how `format` handles signed and unsigned char; are they treated as integral/arithmetic
    or character types?
  - Victor replied that he didn't recall and would have to check.
  - Keld asked about reentrancy.
  - Victor responded that the only global state references are for locale data.
  - Keld recommended allowing strings to be tagged with encoding data.
  - Tom tried to bring discussion back to fill operations and field widths; are we agreed on use of
    code points for field fill/alignment?
  - Martinho asked how a code point approach works when writing to a fixed width buffer (of code units).
  - Victor mentioned that `format_to_n` takes a code unit count constraint.
  - Peter observed that a code unit count constraint can result in truncated code unit sequences.
  - Victor suggested that `format_to` could produce code points instead.
  - Steve asked how to avoid writing broken code; code points produced are likely going to be written
    to a code unit buffer anyway.
  - Keld stated that programmers like to write both code unit and code point code; perahps both
    should be supported.
  - Martinho claimed that truncated code unit sequences are probably not a large concern; buffers are
    generally larger than required anyway.
  - Discussion again drifted towards encodings that are known at compile-time vs run-time.
  - Keld asked what types are generally used for double byte character sets; Japanese, Chinese, ...
  - Martinho responded that those tend to be variable length encodings that switch between single byte
    and multibyte.
  - Tom agreed and mentioned ISO-2022 and escape sequences.
  - Discussion drifted back to code units vs code points.
  - Zach suggested that programmers will expect the output encoding to match the format string, but
    that code points are more consistent and natural.  If the `n` in `format_to_n` means something
    different than for field widths, that will be a problem.
  - Victor agreed that programmers will expect to be filling a code unit based buffer.
  - Tom observed that more discussion would be useful, but that we need to move on.
  - Zach recommended trying to support both code unit and code point based approaches and observe
    feedback and usage.
- [D1097R0](https://github.com/rmartinho/sg16/blob/master/papers/d1097r0.md) - Named character escapes
  - Martinho started by requesting feeback on:
    - name matching (currently more limited than described by
      [UAX44-LM2](https://www.unicode.org/reports/tr44/#UAX44-LM2))
    - lack of support for named character sequences.
  - Tom recommended adding a small section that summarizes what is actually proposed.  At present, the
    paper presents a number of options, but one must read the proposed wording to determine which
    options are actually proposed.
  - Tom expressed a preference for following the UAX44-LM2 for name matching.
  - Martinho responded with a dislike for the `U+1180 HANGUL JUNGSEONG O-E` exception and noted that
    none of the other languages he surveyed use `UAX44-LM2` for matching.
  - Keld noted existing APIs that allow specifying precision for matching.
  - Martinho clarified that general collation APIs don't apply here (because of the
    `U+1180 HANGUL JUNGSEONG O-E` exception).
  - Tom asked if we should propose this for C and everyone responded yes.
  - Tom mentioned the paper should address the potential for code breakage.  `"\N"` has a meaning now
    (it means `"N"`).
  - Tom asked if it is permissible to construct these escapes using macro concatentation.
  - Tom observed that `'_'` seemed to be missing in the definition of `c-char`.
  - Martinho stated that is intentional; `'_'` would be needed for `UAX44-LM2` matching, but that
    actual character names never use `'_'`.
  - Zach suggested adding a Tony Table to compare use of `\U` and `\N{}` escapes.
  - Tom suggested clarifying that `\N{}` escapes would not be permitted in identifiers.
  - Tom asked about interaction with raw string literals; `r-char-sequence` doesn't seem to include
    `universal-character-name`.
  - Martinho responded that `universal-character-name` escapes are not recognized in raw string
    literals; following existing precedent.
- Rapperswil recap:
  - Tom asked if Rapperswil attendees were able to connect with authors of previously discussed
    papers in order to deliver our feedback.
  - JeanHeyd reported that connections did not happen however:
    - P1030 was not discussed in Rapperswil.
    - P0882 was discussed in LEWG but not well received.  No need for follow up.
    - P0540 was discussed; LEWG feedback matched ours, so no need to follow up.
- We ran out of time to discuss what we want to learn from the Swift and WebKit developers.
- Tom asked about renaming the SG16 mailing list from `unicode` to `sg16-unicode`.  Both Tom and
  Martinho had been annoyed by the similarity to the `unicode.org` mailing list by the same name.
  No objections were raised; Tom will follow up with Keld.
- Tom noted that our next regularly scheduled meeting would fall on July 4th, a US holiday.  The
  next meeting will be scheduled for July 11th.

  
# May 30th, 2018

## Draft agenda:
- Discuss plans and goals for those attending Rapperswil.
- Review and discuss the following papers from the Rapperswil pre-meeting mailing:
  - P1030R0: std::filesystem::path_view 
  - P0540R1: A Proposal to Add split/join of string/string_view to the Standard Library
  - P0645R2: Text Formatting
  
## Meeting summary:
- Attendees:
  - JeanHeyd Meneide
  - Mark Zeren
  - Martinho Fernandes
  - Peter Bindels
  - Sergey Zubkov
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Administrative updates:
  - Tom reported that WG chairs were contacted regarding SG16 requests for paper reviews
    in Rapperswil.  WG chairs are predictably swamped and prioritizing as best they know
    how, but we may not get to present any of our papers.
  - Zach observed that Titus is concerned about the amount of time that LEWG will need for
    ranges, but that LWG should be more concerned.
  - Tom relayed that JF Bastien volunteered to arrange introductions with Swift and WebKit
    developers working on Unicode.  Tom reached out to arrange meetings, but hasn't heard
    back.  Apple developers are busy preparing for WWDC; Tom will reach out again soon.
  - Tom brought up the recent news that Microsoft has added beta support for UTF-8 as a
    system code page as of the Windows 10 April update.  Tom made some new contacts
    within Microsoft, but has not yet gotten any further information about Microsoft's
    goals or plans with this change.
- Rapperswil planning:
  - Tom asked for volunteers to standup for SG16 at the Saturday plenary in Rapperswil
    and give a brief update.  Martinho and JeanHeyd agreed to do so.
  - Tom asked for those who have attended meetings before to offer any advice they have
    for first time attendees.
  - Zach recommended spending some time in each of the WGs.  Each WG has its own personality;
  - It was noted that hanging around in WGs where one has a short paper in the queue creates
    opportunities to present earlier than the paper might otherwise be scheduled.  The
    P1025 (normative Unicode reference) and P1041 (char16_t/char32_t are UTF-16/UTF-32)
    papers are good candidates.
  - Zach also mentioned not to be afraid to ask questions and to try to read papers ahead of
    time.
  - Tom noted that anyone present in the room is allowed to vote in straw polls, but that
    polls in plenary are generally restricted to ISO members.  It was noted that Herb will
    make it clear when ISO membership is required to vote.
- [P1030R0](http://wg21.link/p1030r0) - std::filesystem::path_view
  - Martinho liked it, especially section 4.1 (Assume UTF-8 for char based interfaces).
  - Tom liked it with the exception of section 4.1.
  - Tom expressed a belief that the discussion in section 4.1 of how existing char based
    interfaces on Windows handle conversion to wchar_t for invocation of native filesystem
    interfaces is incorrect.  Tom's understanding is that char based strings are transcoded
    to wchar_t strings using the system code page.
  - Zach asked what is meant by ANSI encoding.
  - Tom explained that Microsoft has long referred to char based encodings collectively as
    ANSI encodings despite these encodings not reflecting an ANSI standard.
  - \[Editor's note: Microsoft's glossary of terms on MSDN describes the origin of the ANSI
    reference here.  It comes from a draft ANSI specification that was eventually standardized
    as the ISO-8859 family of encodings.  See the definition of "ANSI" at
    [https://msdn.microsoft.com/en-us/goglobal/bb964658.aspx#a](https://msdn.microsoft.com/en-us/goglobal/bb964658.aspx#a).
    Microsoft now officially refers to these encodings as "Windows code pages".\]
  - Zach initiated a discussion on compile-time vs run-time encodings.  Section 4.1 describes
    a scenario in which file paths are pasted into source code as string literals, but the
    existing interpretation of such strings, when used as paths at run-time, depends on
    run-time locale settings.
  - Peter mentioned that the Microsoft compiler now supports a `/utf-8` option that purports
    to define the source and execution character encodings.  However, that option really only
    affects how literals from the source code are translated to the execution character
    encoding (UTF-8 at compile time, but never UTF-8 at run-time (at least, not until the newly
    introduced beta support in Windows 10 that requires the user to opt in)).
  - Tom stated that we can't fix the compile-time vs run-time aspects of the execution character
    encoding.
  - Martinho countered that `char8_t` offers a solution for this - we know the compile-time
    and run-time encoding of `char8_t` characters and strings.
  - Tom suggested a response to the author: maintain consistency with existing code; `char`
    means "ANSI" encoding.  Use `char8_t` for UTF-8 (follow the changes to `path` proposed in
    the `char8_t` proposal.
  - Tom, Zach, and JeanHeyd all noted the presence of `#ifdef`s surrounding the `wchar_t` based
    interfaces in the proposed design.  We don't use `#ifdef` as specification for implementation
    defined features.
  - JeanHeyd noted that that `path_view` should not fight with the platform; don't propagate
    implementation defined behavior through interfaces to the programmer.
  - Martinho observed that there is no rationale for providing `wchar_t` based interfaces only
    for Windows; they are perfectly applicable to other platforms as well.
  - Zach stated that `path_view` should work the same as `path`; just as `string_view` does for
    `string`.  `path_view` should support the same set of constructors that `path` has and they
    should behave the same.  If there is a need for new constructors, they should be added to
    both `path` and `path_view`.
  - Zack noted that `path_view` should be explicitly constructible from `path`, not the other
    way around.  \[Editor's note: as currently specified, `path_view` is constructible from
    `path`, though the constructor isn't explicit.  Note that `string_view`'s corresponding
    constructor is also not explicit. \]
  - Further discussion regarding memory allocation and the behavior of the proposed `c_str`
    class ensued.  \[Editor's note: few details of this discussion were recorded.  From what
    I recall, consensus was that the memory allocation behavior should be implementation
    defined.\]
  - JeanHeyd asked how we should communicate our feedback to the author.
  - Zach replied with a preference for a direct person-to-person response.
  - JeanHeyd volunteered to deliver feedback.
  - Poll: Use execution character encoding for `char` interfaces, `char8_t` for UTF-8?
    - Unanimous consent.
- [P0882R0](http://wg21.link/p0882r0) - User-defined Literals for std::filesystem::path
  - Tom stated that SG16 concerns are limited to encoding issues; LEWG should address any
    other concerns; e.g., naming.
  - Peter noted that the paper punts on UTF-8 support pending a solution from the comittee for
    differentiating ordinary and UTF-8 string literals.  Fortunately, we have a solution for
    that in the works!
  - It was asked why the UDLs are not `constexpr`; the answer is because they produce `path`
    objects and the `path` constructor allocates.
  - Mark asked if the UDLs should produce `path_view` objects ala P1030 above and was rewarded
    with a round of yeses.
  - Peter observed that the UDL names are very generic (ha ha) and that the literal namespace
    proposed for them differs unnecessarily from existing precedent (e.g.,
    `std::filesystem::literals` vs `std::literals::filesystem`.  \[Editor's note: This design
    also results in the UDL declarations being visible following `using namespace std::filesystem`;
    this may be intentional.\]
  - Poll: Contingent upon adoption of `char8_t`, add `char8_t` based overloads?
    - Unanimous consent.
- [P0540R1](http://wg21.link/p0540r1) - A Proposal to Add split/join of string/string_view to the Standard Library 
  - Tom observed that the paper number and filename do not match.  \[Editor's note: Tom
    followed up with Hal and the author.\]
  - Everyone in unison, "non-member functions please!"
  - Tom asked if there were any concerns about split/join functions operating at the code unit
    level.
  - Martinho replied, no, those are useful operations for splitting/constructing grapheme
    clusters.
  - Zach expressed concern about increasing the surface area of string based interfaces.
  - Poll: Does adding these additional functions complicate future efforts due to increasing
    the set of functionality to replicate at code point or higher levels?<br/>
    \[ SF F N A SA \]<br/>
        5 1 1 0  0
- [P0645R2](http://wg21.link/p0645r2) - Text Formatting
  - Zach requested `char8_t` overloads.  \[Editor's note: Peter has been planning to work on
    adding `char16_t` and `char32_t` support.  There is an existing issue tracking support
    for `char16_t`: https://github.com/fmtlib/fmt/issues/698.  That issue notes that support
    for `std::numpunct<char16_t>` is missing; that would presumably be an issue for `char8_t`
    support as well.\]
  - Zach observed that formatting only works for trivial encodings in which one code unit
    equals one code point; otherwise, field alignments won't match up in displayed text.
  - Martinho responded that, if a font is missing a glyph for a combining character, then the
    combining character will likely be displayed as a separate glyph.  Text layout is required
    to display aligned text (e.g., depends on console, curses, etc...).
  - Tom asked how such display concerns can be addressed; `format` is not a text display tool.
  - Zach asked how field size is specified.  Code units?  Code points?  "Characters"?
  - Peter provided a link to an existing github issue concerning field size and UTF-8.
    - https://github.com/fmtlib/fmt/issues/628
  - Tom noted that we were out of time; we'll continue discussion next time and will invite
    Victor to join us.
- Tom stated out next meeting will be scheduled for three weeks from now on June 20th.  The extra
  week is to give everyone a break following Rapperswil.


# May 16th, 2018

## Draft agenda:
- Review and discuss papers in the Rapperswil pre-meeting mailing.
- Discuss plans and goals for those attending Rapperswil.

## Meeting summary:
- Attendees:
  - Bob Steagal
  - Corentin Jabot
  - Dalton Woodward
  - Florin Trofin
  - JeanHeyd Meneide
  - Mark Zeren
  - Martinho Fernandes
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- It was reported on Slack that Martinho's properly formatted UTF-8 P1041R0 paper
  was served up by open-std.org either without a `CharSet` header or with a
  Latin1 setting.  Tom contacted Hal and Keld.  Further discussion yielded a plan
  to update
  [SD-7](https://isocpp.org/std/standing-documents/sd-7-mailing-procedures-and-how-to-write-papers)
  to require UTF-8 for `.md` files and to configure the open-std.org web server to
  serve them with a `CharSet=UTF-8` header.
- Zach, Bob, and JeanHeyd shared some of their experience at C++Now.
- We then went on to review papers from the pre-Rapperswil mailing.
- [P1041R0](http://wg21.link/p1041R0) - Make char16_t/char32_t string literals be UTF-16/32
  - Tom noted a typo in the proposed wording changes for lex.ccon/4; a use of `UTF-8`
    where `UTF-16` was intended.
  - Given the encoding issues and lack of Markdown rendering support built into browsers,
    it was suggested that future papers, at least for now, be submitted in a pre-rendered
    format.
  - Martinho asked about getting the paper scheduled for discussion in Rapperswil.  Tom
    said he would forward SG16 polls on papers we discussed to WG chairs to communicate
    our position and request time in Rapperswil.  Tom will copy paper authors and expected
    presenters on this communication.
  - It was asked if there was any library impact.  Martinho responded no.  Tom noted having
    previously audited occurrences of `char16_t`, `char32_t`, `UTF-16`, and `UTF-32` and
    could not think of a case.
  - Zach suggested that, when presenting, it be emphasized that no implementation will need
    to make changes; that this is just standarizing existing practice.  Emphasize that there
    are no known implementations where the encoding used is not already UTF-16/UTF-32 and
    that a member of the C committee was consulted.
  - Poll: Those in favor of P1041R0?
    - Unanimous consent.
- [P1072R0](http://wg21.link/p1072r0) - Default Initialization for basic_string
  - Mark noted that P1072 is dependent on P1010 which is dependent on Richard Smith's P0593.
    This raised the question of prioritization and a request for SG16 to request that P0593
    and P1010 get time in Rapperswil so that progress can be made on P1072 in San Diego.  Tom
    agreed to make such a request; specifically to request that EWG entertain P0593 and that
    LEWG look at P1010 (and P1072 time permitting).
  - Mark went on to discuss applicability of P1072 to SG16.  Of particular concern are the
    issues caused by requiring null termination.  This is not a problem for `vector`, and
    hence not a concern expressed in P1010.
  - Mark pointed out that the design is used in real world code today.
  - Zach asked why `reserve()` doesn't suffice.  Mark explained the examples in the paper;
    that we currently either have to repeatedly update the size of the container with each
    addition, or eagerly resize the container and pay for an unused initialization.  The
    goal of the paper is to avoid both costs by enabling writing to excess capacity
    independently of updates to the container size.
  - Tom asked if option A is viable.  The concern is that const member functions must be
    thread safe.  A call to `resize_uninitialized()` makes uninitialized data available to
    const member functions.  Further, there is no event to indicate when the uninitialized
    data has been read and therefore no memory barier to function as a synchronization
    point.
  - Mark acknowledged that a two-phase commit approach is necessary to avoid UB.
  - Martinho observed that two-phase commit is not sufficient by itself because `basic_string`
    uses excess capacity to store a null terminator for the string; this is what allows
    the `data()` and `c_str()` member functions to be `const` qualified.  Overwriting the
    null terminator will cause UB for concurrently executing threads.
  - Mark advised SG16 to consider the consequences of providing implicit null-termination
    for string-like containers in the future.  An alternative approach would use string
    builders that append a null-terminator when they are collapsed.
  - Mark noted that the two-phase commit approach does at least allow the implementation to
    re-establish invariants (such as ensuring a null-terminator is present at the start of
    excess capacity following `insert_from_capacity()`.
  - Tom suggested an emplace-like solution might be preferred to enable preserving invariants.
  - Mark acknoledged a call-back/functor based solution would work (though it still doesn't
    address the over-written null-terminator issue).
  - Dalton asked whether making vector/string node-based containers such that data could be
    written to a new buffer and then swapped in.  This has the disadvantage of requiring that
    the current buffer be copied prior to performing the append.
  - Tom asked if any performance numbers were available.  What is the expected gain?
  - Mark responded that numbers are not available, but that Google has measured and claims the
    improvements make this feature worthwhile.  Estimate is a few percent improvement.
  - Corentin asked why not to use `vector` instead of `string`.
  - Mark responded that `string` is a vocabulary type.
  - Poll: Do we agree P1072R0 addresses a problem worth solving?
    - Unanimous consent.
  - Poll: Do we prefer option A, option B, or some option C?
    - A: 0
    - B: 2
    - C: 5
  - Mark clarified that option C, as discussed today, would be one of:
    - An emplace-like call with a call-back/functor.
    - A node-based swap.
  - Discussion moved into allocator interaction with node types.
  - Zach stated that swap is broken for PMR allocators.
  - Steve agreed and provided an elaboration; that the swap of the allocators doesn't swap
    the actual buffers.
  - Mark noted that moving a buffer between `vector` and `string` encounters complexities due
    to null-termination requirements.
  - Martinho asked how a small buffer optimized string is moved into a node type.
  - Dalton responded that you allocate.
  - Tom added, or the node type implements the SBO itself.
  - Mark expressed concern that an emplace-like call-back/functor approach may not work for
    the network use case of wanting to read data off the network directly into the buffer.
  - Zach suggested that, in a string builder approach, `vector` is the string builder.
  - Corentin expressed a preference for a specific string builder type rather than `vector`.
    Essentially a vocabulary type suited to the purpose.
- [P1025R0](http://wg21.link/p1025r0) - Update The Reference To The Unicode Standard
  - Steve briefly introduced the change as similar to what had been proposed, but not
    completed, for C++17.
  - Tom asked, why update the normative reference to specify each of Unicode 10, Unicode
    without a version indicator, and ISO 10646?
  - Steve answered, we need ISO 10646 for existing references; for example, the
    `__STDC_ISO_10646__` macro.  We want to reference the Unicode standard (in addition to
    ISO 10646) for stability guarantees and additional features.  We want to reference
    Unicode 10 to establish a minimum requirement, and the unversioned Unicode standard to
    enable implementors to adopt a newer version.
  - Tom suggested adding a non-normative note that implementors are allowed to use Unicode
    10 or newer; though they must use a corresponding version of ISO 10646.
  - Martinho stated that we need to make it clear that implementors must choose a specific
    Unicode release.
  - Tom asked if we should require a predefined macro that indicates the Unicode version.
  - Steve and Martinho both answered, maybe, but not yet as we don't actually depend on
    anything Unicode version dependent yet.
  - Poll: Those in favor of P1025R0:
    - Unanimous consent.
- Our next meeting will be May 30th; the week before Rapperswil.
- There is a WG21 administrative teleconference May 25th.
  - Tom will dial-in to give an update on SG16.  Martinho and JeanHeyd are encouraged to
    attend as well since they have papers to present.
- Those planning to attend Rapperswil:
  - Martinho, Corentin, Peter, JeanHeyd.
- Following the meeting, Martinho volunteered to present P1025R0 at Rapperswil since Steve
  will not be present.  Steve agreed.

## Assignments:
- Tom: Forward SG16 poll results to WG chairs and request time in Rapperswil.
- JeanHeyd: Research layering, concepts, required expressions, etc...
- Mark: Work on the basic_string specification cleanup paper.
- Tom and Zach: Work on a terminology update paper.


# April 25th, 2018

## Draft agenda:
- Review and discuss any draft papers targeting the Rapperswil pre-meeting mailing.
- Discuss plans and goals for those attending Rapperswil.

## Meeting summary:
- Attendees:
  - Tom Honermann
  - Zach Laine
  - Martinho Fernandes
  - JeanHeyd Meneide
  - Dalton Woodard
  - Sergey Zubkov
  - Steve Downey
  - Peter Bindels
  - Bob Steagall
- We started off with introductions from first time attendees Dalton and Sergey.
- Tom provided a few administrative updates:
  - A new sg16 repo was created under the sg16-unicode github org; the old std-text-wg
    repository is now retired.
    - https://github.com/sg16-unicode/sg16
  - A new sg16-papers repo was _not_ created under the assumption that it would be simpler
    to just use the new sg16 repository.
  - The old std-text-wg mailing list was removed; old emails were forwarded to the new
    mailing list.
  - The github projects that Tom was experimenting with have been removed in favor of
    tracking via github issues on the sg16 repository.
  - Alisdair provided some char8_t wording review; Mark is off the hook for doing so.
- We then did a round of status updates.
  - Steve provided a brief status update for the project to update normative
    references to ISO/IEC 10646 (https://github.com/sg16-unicode/sg16/issues/1).
    - Further discussion was postponed until after status updates.
  - Martinho provided a brief status update for the project to mandate that `char16_t`
    and `char32_t` literals use UTF-16 and UTF-32 encodings respectively
    (https://github.com/sg16-unicode/sg16/issues/6).
    - Further discussion was postponed until after status updates.
  - Zach provided an update on Boost text and reported having fun adding support for the
    Unicode bidirectional algorithm.
  - Jeanheyd reported that he is working on benchmarks and comparisons of Ogonek, Boost
    text, text_view, ICU, and other libraries.
  - We briefly discussed some of the work that Bob Steagal has been doing.  Bob had
    previously shared some UTF-8 conversion performance numbers with Zach and Tom.
    Bob had not yet joined the meeting, so Zach gave a brief overview.  When Bob later
    joined in, we discussed further (see below).
- We then returned to discussion on normative updates for Unicode standard references:
  - A productive discussion on Slack earlier in the day was helpful in setting
    direction.  At issue was how to handle UCS-2 and UCS-4 references in the
    standard since definitions of those terms would be lost by updating the
    normative reference to a recent standard.  It was confirmed that UCS-2 and
    UCS-4 are only referred to by the deprecated `codecvt` facets in annex D.
  - Tom had suggested in the Slack discussion that we could remove the deprecated
    features in C++20.  This would remove the existing references and avoid the need
    to retain any definitions for UCS-2 and UCS-4.
  - Zach noted that the standard practice for deprecation is to deprecate first and
    replace/remove in a future standard.
  - Steve noted that Debian code search reveals uses of the deprecated codecvt facets.
  - Martinho suggested the deprecated facets could be specified to use UTF-16/UTF-32
    instead of UCS-2/UCS-4.  This would be a technical break, but perhaps not a
    significant concern.
  - Tom noted that this would definitely break `codecvt_utf16` since it exists solely
    to convert between UTF-16 and UCS-2/UCS-4.
  - Steve stated that we can retain the old ISO/IEC 10646 reference for the deprecated
    UCS-2 and UTC-4 references, and use an updated reference for everything else.
  - Steve noted that LWG thought they had previously addressed the UCS-2/UCS-4 issue
    by deprecating existing uses, but since references still remain, the issue is not
    really addressed.
  - Tom asked how we should move forward.  With one paper addressing both the normative
    update and the UCS-2/UCS-4 references?  Two papers?  Perhaps three?
  - Zach expressed a preference to address separate concerns separately.
  - Tom expressed a preference for one paper with wording to address both issues.  The
    intent being that, if that approach were to fail, we could fall back to separating
    out the issues.  This preference is intended to avoid dependencies between the two
    issues; to avoid the case where we end up updating the normative reference, but not
    removing the UCS-2 and UCS-4 references, thus leaving undefined terms in the standard.
  - Sergey asked about the possibility of updating the deprecated facets to specify that
    the encoding conversion is implementation defined.
  - Tom: Someone (not sure who) had previously (not in this meeting) noted that there
    was already some implementation divergence regarding whether the codecvt facets
    actually do convert between UCS-2/UCS-4 vs UTF-16/UTF-32.
  - Martinho noted that the difference is unlikely to matter in real world usage because
    lone surrogates are unlikely to be present.
  - Peter countered that lone surrogates may appear in file names (on Windows where file
    names have 16-bit code units).
  - Zach stated that Windows no longer allows file names that are ill-formed UTF-16.
  - Tom noted he had heard this, but hasn't seen it confirmed.
  - Peter noted that WTF-8 exists to handle UCS-2 and malformed UTF-16.
  - Martinho stated that there is a difference between ill-formed UTF-16 and text that
    is not actually UTF-16.
  - We confirmed Steve had the guidance he felt he needed from the group to proceed
    as he deemed fit.
  - Steve stated that he will circulate papers when ready.
- We then returned to discussion on the character encoding for char16_t and char32_t
  literals.
  - Martinho have a quick overview of his draft:
    - https://github.com/rmartinho/sg16/blob/master/proposals/p0000r0_utf16_32_literals.md
  - Tom reported reaching out to the author of WG14 N2245
    (http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2245.htm).  That author confirmed no
    known C compiler implementations that don't use UTF-16/32.
  - Zach said the paper looks good and asked what happens with \u escapes in ordinary
    string literals today.
  - Tom stated that is implementation defined.
  - Zach and Martinho noted that there are potentially different results for escapes vs
    conversion from source encoding.
  - Tom suggested updating the character literal wording to use consistent naming with
    the updated string literal wording.
  - Tom also noted there would be a merge conflict with the char8_t proposal.
  - Martinho noted that he had also observed that.  He also observed that the term,
    "UTF-8 character literal" is defined but never referenced.  Martinho confirmed he
    will define character/string literals using char16_t/char32_t and UTF-16/32 terms to
    match the UTF-8 related definitions.
- JeanHeyd asked about where to create new repositories for new projects.
  - Zach and Steve both suggested creating personal repositories; we can transfer
    ownership later if/when it becomes appropriate.
- Steve observed that it would be helpful to use a consistent license for the
  works we produce.
  - JeanHeyd asked what license is preferred, CC0, Boost, MIT?
  - Zach stated a preference for avoiding CC0 because of legal complexities with
    "public domain".
  - Tom expressed no particular preference but observed that CC0 is more complicated
    from a wording perspective.
  - Peter stated we should use a license that is friendly to implementors.
  - Zach responded that fear of patent bombing prevents usage in some cases.
  - We settled on using the Boost license for group projects.
- Bob then provided an introduction and shared more specifics of his work.
  - He has been working on UTF-8 conversion performance improvements and shared some
    results that he will be presenting at C++Now.
  - Peter asked if more benchmarks could be added to Bob's tests.
  - Bob answered yes and noted that Zach did the work to integrate Boost text.
- Steve reminded everyone to request paper numbers for the pre-Rapperswil meeting now.
- We confirmed that the next meeting will by held on May 16th; three weeks from now
  so as not to conflict with C++Now.

## Assignments:
- JeanHeyd: Research layering, concepts, required expressions, etc...
- Mark: Work on the basic_string specification cleanup paper.
- Mark: Complete and submit on the uninitialized append for contiguous containers paper.
- Martinho: Complete and submit the UTF-16/UTF-32 string literals paper.
- Steve: Complete and submit the paper to update ISO/IEC 10646 normative references.
- Tom: Work with Zach on a terminology update paper.
- Zach: Work with Tom on a terminology update paper.


# April 11th, 2018

## Draft agenda:
- Identify champions to research and author papers for projects discussed in the last meeting:
  - Terminology modernization
  - Mandate char16_t and char32_t string literals be UTF-16/UTF-32.
  - Identify existing features to deprecate/replace.
  - basic_string specification cleanup.
  - uninitialized append for contiguous containers.
- Determine how to contribute to and collaborate on a common code repository; building from the ground up.

## Meeting summary:
- Attendees:
  - Tom Honermann
  - Steve Downey
  - Mark Zeren
  - Zach Laine
  - JeanHeyd Meneide
  - Nicole Mazzuca
  - Florin Trofin
- We first discussed some administrative updates:
  - We now have a mailing list at http://www.open-std.org/mailman/listinfo/unicode!  Thanks to
    JeanHeyd for an initial post summarizing our current projects and goals.
  - Our Slack channel has been renamed to reflect our new SG16 branding.  Thanks to Mark for
    taking care of that.
  - We have a new SG16 GitHub organization at https://github.com/sg16-unicode.  The old
    std-text-wg repo will be retired (but preserved).  Meeting summaries will now be tracked in
    a new `sg16-meetings` repository.  We'll create additional repositories as needed.
- We then spent a little time discussing how best to make use of the new GitHub org.
  - Tom created GitHub projects for the initiatives discussed in our last meeting and asked
    for feedback regarding tracking things that way.  None of us have much familiarity with
    GitHub projects, so there wasn't much feedback.  Some experimenting will be required.  Tom
    noted that task ownership seems to depend on creating issues associated with a git repo.
  - Nicole noted that, because we now have a central org, we can create numerous repos.
  - Steve mentioned that having a repository just for papers is very useful.
  - Tom suggested creating a "sg16" repo with a Readme.md that provides an overview of
    SG16 and other introductory text; for example, links to the mailing list and Slack.
    Basically, a repo to host the Readme.md file from the old `std-text-wg` repo.  We might
    also use this repo for general management purposes; e.g., to host GitHub issues used for
    project tracking.
  - Zach asked about where to host our mythical use cases doc and suggested an approach in
    which the use cases are stored as code rather than as documentation.  This could support
    testing the use cases with various implementations (for correctness, performance,
    expressiveness, etc...).  Should we decide to submit a use cases paper, the paper could
    presumably pull directly from the code.
  - It was mentioned that being able to share code samples on godbolt.org (or another Compiler
    Explorer host) would be helpful.  Nicole suggested we reach out to Matt Godbolt to see if
    he would be amenable to adding Unicode related projects such as `ICU`.  Matt has fulfilled
    similar requests in the past; e.g., for `range-v3`.
- We then moved on to identifying champions to research and author papers for projects discussed
  in the last meeting.  
  - Steve volunteered to work on updating normative references to ISO/IEC 10646 to a revision
    that isn't older than some committee members.
  - Tom and Zack agreed to work on terminology modernization.
  - Martinho wasn't present for the meeting, but had previously indicated interest in working on
    a paper to mandate that char16_t and char32_t string literals be UTF-16/UTF-32; he reconfirmed
    this on Slack after the meeting.  Tom volunteered to help try and identify any existing
    compilers that don't use UTF-16/UTF-32.
  - Mark reaffirmed his intent to work on basic_string specification cleanup.
  - Mark also reaffirmed his intent to work on uninitialized append for contiguous containers.
  - Noone volunteered to champion work on identifying existing features to deprecate/replace.
- We briefly discussed deprecation approaches using `std::toupper()` as an example.  It was
  acknowledged that eventual removal of this function may not be feasible due to widespread use.
  Likewise, automatic refactoring may not be feasible since a suitable replacement function
  might require multiple code points (either for context or for mapping).  Nicole noted that this
  is an example of a function that can remain useful, but has a name that does not communicate
  its limitations.  Deprecating it in favor of an appropriately named alternative (e.g.,
  `ascii_toupper()`) would support automatic refactoring.
- Our next discussion focused on further collaboration.
  - Tom again expressed a desire to bring our collective efforts together to enable collaborating
    on a reference implementation of features we'd like to see in a future TS.  Perhaps taking a
    bottom up approach to building it.
  - Zach noted that his `text` implementation and documentation are designed around three distinct
    layers: strings, Unicode, and text.
  - JeanHeyd expressed an interest in surveying `Ogonek`, `text`, `text_view`, etc... to identify
    overlap and further define layering opportunities.
- Tom then asked about recent reflector discussions regarding `string_view` and what we might
  learn from them that would be applicable to view/reference types we might design.
  - Zach noted a few guidelines:
    - Don't support default comparisons between different kinds of views (e.g., string_view and
      rope_view).
    - Don't provide operators that hide complexity.  For example, an operator+ for text/string
      views that would require allocation might be surprising.
    - Owning vs non-owning is more imprtant than shallow vs deep compare.
  - Mark mentioned that string_view cannot support intrinsic optionality because a null pointer
    state is observeable (via `data()`).
- We briefly discussed O(1) complexity requirements on `begin()`.
  - Tom mentioned that his `itext_iterator` types do not currently meet this requirement because,
    given an ill-formed initial code unit sequence, `begin()` may consume an unbounded number of
    code units.  The consumption is necessary to ensure that, in the case where the end of the
    underlying code unit sequence is reached before any code points are successfully decoded,
    that `begin() == end()` will hold.
  - Zach noted that his iterators don't encounter this situation because the `text` type ensures
    that the underlying code unit sequence is always valid.  His transcoding iterators also do
    not hit this because they produce a replacement character for each ill-formed sequence
    (presumably limited to a bound length).  This would be an issue for support of an error
    policy that simply skips ill-formed code unit sequences though.
- Florin requested that we make sure to keep IBM users in mind and that we work with people from
  IBM to ensure that what we propose won't be problematic for non-ASCII based systems.  Tom
  fervently agreed and indicated he has maintained contact with Hubert Tong.
- We finished by agreeing to two meetings to be held before the pre-meeting mailing deadline
  for Rapperswil.  The deadline is May 7th; we will meet ~April 18th and May 2nd~ [Post-meeting
  writeup correction: we will meet just once on April 25th].

## Assignments:
- JeanHeyd: Research layering, concepts, required expressions, etc...
- Mark: Review char8_t for LWG wording updates.
- Mark: Work on the basic_string specification cleanup paper.
- Mark: Work on the uninitialized append for contiguous containers paper.
- Martinho: Work on the UTF-16/UTF-32 string literals paper.
- Steve: Work on the paper to update ISO/IEC 10646 normative references.
- Tom: Forward emails from the old std-text-wg mailing list to the new one and retire it.
- Tom: Create new sg16 and sg16-papers repos and retire the old std-text-wg one.
- Tom: Work with Zach on a terminology update paper.
- Zach: Work with Tom on a terminology update paper.


# March 28th, 2018

## Draft agenda:
- Jacksonville recap.
- Divide and conquer: can we focus efforts on different support areas?
  - Views, ranges, code units vs code points vs EGCs.
  - Encoding, decoding, normalization, segmentation.
  - UCD and CLDR interfaces.
  - Localization, collation, case mapping.

## Meeting summary:
- Attendees:
  - Tom Honermann
  - Martinho Fernandes
  - JeanHeyd Meneide
  - Mark Zeren
  - Peter Bindels
  - Corentin Jabot
  - Nicole Mazzuca
  - Michael Spencer
  - Zach Laine
  - Florin Trofin
- This was our first official teleconference meeting as SG16.  We discussed
  and agreed on a number of steps to take as part of the transition from the
  informal std-text-wg group:
  - The recently added std-text-wg@googlegroups.com mailing list will be removed
    in favor of an isocpp sponsored mailing list on open-std.org once it is
    created.
  - Tom confirmed with Vinnie Falco that the C++ Alliance is looking into acquiring
    a paid Slack plan.  We'll continue using Slack for now, but will rename the
    existing "std-text-wg" channel to "sg16-unicode" or, if we can't rename it,
    migrate to a new channel with the new name.
  - We'll rename the existing std-text-wg github repo to "sg16-unicode".  After the
    meeting, JeanHeyd suggested that we should migrate to a repo not tied to a
    a personal account and Tom agreed to do so.
- We then went on to discuss future plans.
- Mark suggested that we plan to get together with Apple Unicode developers before,
  during, or after the San Diego meeting.  Mark previously worked with a number of
  Apple developers that work on Unicode and they have considerable expertise that we
  would love to have available.
- We then discussed ideas we could pursue for C++20:
  - Mark expressed interest in cleanup of the basic_string specification.  For example:
    - Fix long standing issues that were not fixed in C++11.
    - Cleanup iterator invalidation rules to match existing implementations.
  - Mark also expressed interest in adding an uninitialized append capability to
    vector and basic_string.
  - Mark suggested that we start researching whether and how the ISO standard can
    reference the Unicode standard.  Questions include:
    - How do we handle the different cadence of ISO C++ releases and Unicode releases?
    - Do we allow implementors to choose a Unicode version?
    - Would it suffice to reference other ISO/IEC standards such as ISO/IEC 10646 and
      ISO/IEC 14651 that reflect portions of the Unicode standard?
      - https://www.iso.org/standard/56921.html
      - https://www.iso.org/standard/68309.html
  - Tom remarked that ISO C and C++ do not specify the encoding of u"" and U"" string
    literals, but suspects that all current compilers encode them as UTF-16 and UTF-32
    respectively.  If this can be confirmed, then we could propose mandating UTF-16 and
    UTF-32 respectively to WG14 and WG21.
  - Tom expressed a desire to modernize the terminology used in the C++ standard.  In
    particular, replacing or clarifying uses of "character" and "character set" with
    more modern terms like "code unit", "code point" and "character encoding".  This
    will be necessary for future specification and gives us an opportunity to educate
    the committee on some of these distinctions.
  - Tom also suggested that we could review the standard for interfaces that are too
    broken to be fixed and deprecate them.  For example, `std::ctype::toupper()`.
    - Nicole suggested that, for `std::ctype::toupper()` in particular, we could propose
      new interfaces that provide the same behavior, but under names that make the
      limitations clear.  For example, `ascii_toupper()` or `basic_toupper()`.
  - Tom discussed the difficulties we face today in drafting wording updates and that,
    ideally, we would have some kind of tool that would allow us to edit a fork of the
    standard LaTex sources, and then build it such that only the sections that were
    modified would be present in the resulting document (with appropriate insert/delete
    markup).  In discussion with Richard Smith in Jacksonville, Richard noted that he
    has wanted something like that for some time.  A considerable benefit of such an
    approach is that it would make the process of updating wording for more recent
    drafts much simpler.
- We next discussed some goals for Rapperswil:
  - Tom will pursue getting char8_t through CWG and LWG; likely via a delegate.
  - Topics for SG16 to discuss in session:
    - What is our long term vision?
    - What might a TS contain?
  - Work group activities:
    - Identify use cases.  We've been talking about getting a solid list of common
      text manipulation use cases together for approximately forever now.  Perhaps we
      could devote some time to doing that work?
- Finally, Peter suggested that we could propose a library-in-a-week project for the
  upcoming C++Now conference, May 6th-11th.
- Tom noted that many of us have our own pet projects at the moment, many of which
  overlap considerably.  Tom has `text_view`, Zach has `text`, Martinho has
  `Ogonek`, JeanHeyd has his own `text_view`, Corentin has his own experiment with
  normalization, etc...  How can we best collaborate and execute on a shared vision
  for the standard?

## Assignments:
- Tom: Follow up on SG16 branding activities: new mailing list, github repo, and Slack
  channel rename.
- Mark: Review char8_t for LWG wording updates.
- Everyone: How do we decide to collaborate on a single vision?


# Prior std-text-wg meetings

Meetings held by the informal std-text-wg working group prior to the
formation of SG16 are available at:
- https://github.com/tahonermann/std-text-wg/blob/master/MeetingNotes.md
