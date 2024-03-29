# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, April 10th, 2024, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20240410T193000&p1=1440&p2=tz_pdt&p3=tz_mdt&p4=tz_cdt&p5=tz_edt&p6=tz_cest)).

Draft agenda:
- TBD.


# Past SG16 meetings
- [March 13th, 2024](#march-13th-2024)
- [February 21st, 2024](#february-21st-2024)
- [February 7th, 2024](#february-7th-2024)
- [January 24th, 2024](#january-24th-2024)
- [January 10th, 2024](#january-10th-2024)
- [Meetings held in 2023](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md)
- [Meetings held in 2022](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# March 13th, 2024

## Agenda
- [P1729R4: Text Parsing](https://wg21.link/p1729r4).
- [P3154R0: Deprecating signed character types in iostreams](https://wg21.link/p3154r0).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Braden Ganetsky
  - Eddie Nolan
  - Elias Kosunen
  - Fraser Gordon
  - Jens Maurer
  - Mark de Wever
  - Nathan Owens
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
- A round of introductions was held for new attendee Braden Ganetsky.
- [P1729R4: Text Parsing](https://wg21.link/p1729r4):
  - Elias explained that prior feedback has been addressed and that the paper is expected
    to be ready for a forwarding poll.
  - Elias reviewed the revision history and the changes requested by SG9.
  - Elias stated that support for stdin will be provided in a future paper; similar to
    how `std::print()` was proposed after `std::format()` was adopted.
  - Elias proceeded to review each section of the paper.
  - Eddie noted that the comment in the example in section 3.2, "Reading multiple values at once",
    appears to be missing `values()` following `operator->`.
  - \[ Editor's note: The comment appears to be intentional in only referring to `operator->`,
    but incorrect in stating, "will throw if it doesn't contain a value"; a call to
    `std::expected<T>::operator->()` exhibits UB if `has_value()` is not true. \]
  - Tom asked, while looking at the example in section 3.4, "Reading multiple values in a loop",
    if all result values are definitely assigned.
  - Elias explained that the scan result is returned by value and that there is no way to
    provide an object that is referenced within the result object.
  - Tom asked, while looking at the example in section 3.6, "Scanning a user-defined type",
    if the use of `std::expected` is required or whether another `std::expected`-like type
    could be used.
  - Elias replied that a concept-like approach is used in the reference implementation.
  - Braden asked if it will be surprising to programmers that `std::scan` reports errors via
    `std::expected` where as `std::format` uses exceptions.
  - Elias responded that a failure to parse input provided at run-time is expected and therefore
    a different category of error than what is expected when formatting.
  - Victor agreed with Elias and stated that this is a reasonable design.
  - Mark asked what happens if the scan format string is not valid.
  - Elias replied that the format string is constant evaluated and, if not valid, renders the
    program ill-formed.
  - Mark commented that both throwing an exception and returning a `std::expected` value that
    holds an error type in response to an invalid format string can suffice to produce a
    compile-time error.
  - Elias proceeded to review section 4, "Design".
  - Robin requested that, in section 4.2, "Format strings", in the discussion of whitespace,
    the word "currently" in "Those code points are currently" be struck since the Unicode
    stability policy ensures these won't change.
  - Robin observed that the list of whitespace code points appears to be missing some
    characters; U+000B LINE TABULATION for example.
  - Elias responded that the ASCII line includes a range of code points that includes that
    character.
  - Tom suggested it would be more clear for the list to include all of the
    [`Pattern_White_Space`](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=%5B%3Apattern_white_space%3A%5D&g=&i=)
    characters individually.
  - Elias continued review in section 4.3.2, "Fill and align", and explained the behavior
    for scanning of centered text without an explicit width; an unambiguous width cannot be
    inferred based on surrounding fill characters.
  - Tom referenced the `rH` example that scans `"*42**"` with a `"{:*^}"` format specification,
    noted that the final `*` character is not scanned, and asked for confirmation that the
    example won't roundtrip with what `std::format()` produces with an explicit field width.
  - Elias confirmed.
  - Victor suggested double checking how the
    [Python parse project](https://pypi.org/project/parse/)
    handles that situation.
  - Elias responded that he had checked at one point, but would need to do so again.
  - \[ Editor's note: The "Format Specification" section in the
    [Python parse project description](https://pypi.org/project/parse/)
    states:

      > Note that the “center” alignment does not test to make sure the value is centered -
      > it just strips leading and trailing whitespace.

    \]
  - Victor pondered whether it is possible to roundtrip in general without field width
    information and suggested the possibility of not supporting scanning of center aligned
    text without an explicit field width.
  - Elias agreed that such cases could be disallowed.
  - Jens questioned whether it might be a good to scale back the options for scanning.
  - Jens noted that there are already some asymmetries and provided an example;
    `std::format()` produces a specific whitespace sequence while `std::scan()` will
    consume arbitrary whitespace.
  - Jens suggested that use of a regular expression to consume fill characters might
    provide a more practical approach.
  - Elias asked if Jens' suggestion is intended just for handling of center alignment or
    for all field widths.
  - Jens clarified that the goal would be for the `r5` example to have a format specifier
    that consumes an arbitrary number of fill characters.
  - Jens stated that perhaps the `r7` example would not be covered by this idea since it has
    an explicit field width.
  - Jens opined that the `r5` example and all those that follow it are a little concerning;
    particularly with regard to centering.
  - Elias responded that section 6.2, "`scanf`-like `[character set]` matching" discusses
    potential future support for matching regular expressions and discarding characters.
  - Elias stated these future directions would cover Jens' suggested approach, but
    acknowledged that a format specifier option would be convenient.
  - Jens stated that full regular expression support would invite complication.
  - Mark asked if dynamic field widths are supported.
  - Elias replied that they are explicitly disallowed.
  - Elias reported that there was a poll in LEWGI that supported compatibility with
    `std::format` as a guiding principle.
  - Elias acknowledged that formatting and scanning are different.
  - Jens agreed and stated that compatibility makes sense as long as it makes sense.
  - Victor stated that symmetry with `std::format()` is not a goal, but that providing a
    replacement for `scanf()` is a goal and the motivation for many of these use cases.
  - Jens replied that he is not aware of features in `scanf()` that would allow for
    skipping over fill characters.
  - Victor acknowledged the lack of such general features but that the use cases apply
    when the fill character is a space character.
  - Victor asked if iostreams supports skipping fill characters when scanning.
  - General uncertainty was expressed.
  - Jens reported that it appears that example `r5` cannot be parsed with `scanf()`.
  - Tom stated that it sounds like there is some homework to be done.
  - Jens suggested that homework be done and that review continue at a future telecon.
  - Tom agreed.
  - Eddie moved on to section 4.3.3, "Sign, '#', and '0'", and stated that ignoring
    '+' and '-' signs or leading '0' characters would not be desirable by default,
    but could be useful in conjunction with the sign and '0' format options.
  - Elias responded that, in his experience, it is more important to have a clean design
    space than it is to have compatible format strings and that he preferred to not
    allow those flags in order to avoid confusion.
  - Victor agreed with Elias.
  - Elias explained that there is an additional roundtrip asymmetry when formatted text
    exceeds an explicit field width; scanning the text with an explicit field width won't
    consume all of the formatted text.
  - Elias noted that section 4.3.5.2, "Design discussion: Separate flag for thousands
    separators" will be removed; it was unintentionally left in.
- [P3154R0: Deprecating signed character types in iostreams](https://wg21.link/p3154r0):
  - Elias introduced the paper by explaining that the `signed char` and `unsigned char`
    inserters and extractors behavior is surprising because those types are treated as
    character types but are often used as the underlying types of `int8_t` and `uint8_t`.
  - Alisdair asked how `std::format()` handles these types.
  - Elias responded that they are formatted as integer types.
  - Jens suggested updating section 1, "Motivation", to add a `std::format()` example for
    each of the `std::cout` examples.
  - Alisdair asked about the long term intent and whether these functions might be defined
    as deleted or specified to have different behavior after a deprecation period.
  - Alisdair asserted that deprecation should be a transitional state; features should not
    stay deprecated indefinitely.
  - Elias expressed a preference for defining them as deleted due to concerns about just
    switching to new behavior.
  - Victor expressed strong support for deprecation and stated that these functions are a
    common source of errors.
  - Victor noted that the existing behavior will remain available but will require an
    explicit cast to a `char`-based type.
  - Jens stated that a plan to deprecate in C++26, to define these functions as deleted for
    C++29, and to define them with new behavior for C++40 or so could make sense.
  - Jens expressed strong support for defining these functions as deleted as either a final
    or further intermediate step.
  - Jens requested gathering some implementation experience by modifying a C++ standard
    library to define these functions as deleted and then compiling some real world projects
    to see if any latent bugs are discovered.
  - Jens opined that deprecation is a LEWG concern and that SG16 should offer a recommendation
    on use of `signed char` and `unsigned char` as character types.
  - Alisdair pondered an option to change the behavior to implementation-defined or unspecified.
  - **Poll 1: Recommend reserving `signed char` and `unsigned char` for use as integer types, not character types.**
    - Attendees: 11 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   7 |   2 |   0 |   1 |   0 |
    - Consensus in favor.
    - A: I would like to see the results for the experiment Jens suggested first.
  - **Poll 2: Forward P3154R0 with the suggested modifications to the motivation section to LEWG for C++26.**
    - Attendees: 11 (3 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   2 |   1 |   1 |   0 |
    - Consensus in favor.
    - A: The direction is more a matter for LEWG.
  - Those that abstained from the second poll reported being uneasy with the poll because
    the proposed change to deprecate these features is not an SG16 concern.
  - Tom explained that his intention with forwarding polls is to confirm that there are
    no outstanding SG16 concerns that are not either addressed or discussed in the paper;
    these polls are not intended to state a position on matters that do not fall under SG16's
    purview.
- Tom reported intent to cancel the scheduled 2024-03-27 SG16 meeting since the WG21 meeting
  in Tokyo will have just concluded and we'll all be busy catching up with our regular lives.
- Jens expressed support for that cancellation.
- Tom reported that he has historically scheduled SG16 meetings for the 2nd and 4th Wednesday
  of each month, but that meetings from now through 2024-10-24 were scheduled for every two
  weeks; whether inadvertently or intentionally with now forgotten intent remains a mystery.
- Tom indicated an inclination to stick with that schedule for now and requested that anyone
  that will encounter attendance difficulties because of it let him know.
- Tom announced that the next meeting is scheduled for 2024-04-10 and that there are a
  number of papers awaiting review.


# February 21st, 2024

## Agenda
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html).
  - Identify updates needed for UAX #31 changes in Unicode 15.1.0.
- [LWG 4043: "ASCII" is not a registered character encoding](https://wg21.link/lwg4043).
- [LWG 4044: Confusing requirements for std::print on POSIX platforms](https://wg21.link/lwg4044).

## Meeting summary
- Attendees:
  - Eddie Nolan
  - Fraser Gordon
  - Jens Maurer
  - Nathan Owens
  - Peter Bindels
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html):
  - Tom provided a brief introduction:
    - Unicode 15.1.0 introduced changes to
      [default identifier syntax](https://www.unicode.org/reports/tr31/#Default_Identifier_Syntax)
      to allow U+200C (ZERO WIDTH NON-JOINER) and U+200D (ZERO WIDTH JOINER) in identifiers.
    - We can choose to accept these changes or to adopt a profile that retains the prior
      behavior.
    - Regardless, the removal of
      [UAX31-R1a](https://www.unicode.org/reports/tr31/#R1a)
      necessitates an update to
      [\[uaxid.def.rfmt\]](http://eel.is/c++draft/uaxid.def.rfmt)
      in
      [Annex E](http://eel.is/c++draft/uaxid).
  - Steve stated that it makes the most sense to defer to Unicode for valid identifier syntax and
    for individual projects to decide what constitutes a reasonable identifier.
  - Steve asserted that following Unicode guidance should not be an on-going discussion for WG21.
  - Jens reminded the group that we decided to defer to Unicode explicitly so that we would not
    have to decide what is a valid identifier.
  - Robin explained that this topic is on the agenda because there was a change to UAX #31 and
    Annex E now has dangling-ish references.
  - Robin reported that the change made to default identifiers was a simplification and that
    [UTS #55 (Unicode Source Code Handling)](https://www.unicode.org/reports/tr55/)
    gives general guidance for identifiers.
  - Robin noted that the provided guidance suggests adopting a profile from
    [UAX #31 section 7.1](https://www.unicode.org/reports/tr31/#Mathematical_Compatibility_Notation_Profile)
    to allow additional characters that are not included in default identifiers.
  - Robin stated that some implementations already allow those characters and that formally adding
    them to C++ should probably be pursued by a separate paper.
  - Tom noted that those additional characters are for some mathematics symbols.
  - Steve agreed that is something to consider, but is unrelated to the current issue.
  - Tom asked if anyone had an argument to offer for why we should not accept the UAX #31 updates.
  - No such arguments were offered.
  - Tom asked for a volunteer to update annex E.
  - Steve volunteered.
  - Robin expressed interest in collaborating on a paper to adopt the
    [Mathematical Compatibility Notation Profile](https://www.unicode.org/reports/tr31/#Mathematical_Compatibility_Notation_Profile). 
  - Tom requested that Steve send updated wording to Jens to be included in the proposed resolution.
  - Jens stated that the proposed resolution will require approval from EWG due to the minimum version
    requirement.
- [LWG 4043: "ASCII" is not a registered character encoding](https://wg21.link/lwg4043):
  - Tom provided a brief introduction:
    - Users expect "ASCII" to be a recognized encoding name, existing converters recognize
      it, the proposed resolution is that it be recognized as an alias of "US-ASCII".
  - Fraser asked if it is known why "ASCII" isn't already an alias for "US-ASCII" in the
    [IANA character set registry](https://www.iana.org/assignments/character-sets/character-sets.xhtml).
  - Tom guessed that it is due to historic confusion regarding "extended ASCII"
    character sets.
  - Tom shared a link to the IANA character set reference and quoted the first paragraph
    in chat.
      > These are the official names for character sets that may be used in
      > the Internet and may be referred to in Internet documentation.  These
      > names are expressed in ANSI_X3.4-1968 which is commonly called
      > US-ASCII or simply ASCII.  The character set most commonly use in the
      > Internet and used especially in protocol standards is US-ASCII, this
      > is strongly encouraged.  The use of the name US-ASCII is also
      > encouraged.
  - Steve noted that the IANA registry includes a "csASCII" alias.
  - Fraser opined that this sounds like a historic issue.
  - Steve recalled that some special handling for "cs" prefixed names was adopted.
  - Tom replied that the `std::text_encoding::id` enumerators use the "cs" prefixed aliases
    with the "cs" prefix removed.
  - Tom asked if anyone is opposed to adding the proposed "ASCII" alias.
  - Jens noted that implementations already have lattitude to add additional names.
  - Jens agreed we should add this particular alias, but not as a precedent for adding
    additional aliases later.
  - Peter stated that ASCII is deserving of special consideration and is recognized
    around the world.
  - Victor opined that the motivation in the LWG issue is a little weak, but that he
    isn't opposed.
  - Tom reported that `iconv()` and ICU will already recognize it and opined that users
    will expect it to be recognized.
  - Steve noted that implementors don't need our approval to add this alias.
  - **Poll 1: Approve the addition of "ASCII" as an alias for the US-ASCII IANA encoding.**
    - Attendees: 9
    - No objection to unanimous consent.
- [LWG 4044: Confusing requirements for std::print on POSIX platforms](https://wg21.link/lwg4044):
  - Victor introduced the issue:
    - Jonathan Wakely implemented support for `std::print()` in libstdc++ and encountered a
      significant performance issue due to how he interpreted the standard wording.
    - When discussing `std::print()` in SG16, we didn't consider POSIX streams as a
      "Native Unicode API".
    - Private correspondence with Jonathan clarified the intent and resolved the performance
      issues.
  - Victor guided discussion through the proposed wording.
  - Victor highlighted the removal of the POSIX and `isatty()` related wording as the important change.
  - Victor suggested that the moved text that encourages implementations to diagnose invalid code units
    be removed.
  - Eddie agreed with striking the wording regarding diagnosing invalid code units.
  - Eddie noted that checking for ill-formed code unit sequences imposes overhead.
  - Steve asserted that `isatty()` is fragile and that its use complicates debugging since it leads to
    file redirection changing program behavior.
  - Eddie asked Steve for clarification.
  - Steve replied that `isatty()` is fragile because it is easy to cause `isatty()` to return false
    when the output is still going to the terminal.
  - \[ Editor's note: Compare the behavior of `ls` vs `ls | cat` on Linux for example. \]
  - Eddie opined that tools should check the `NO_COLOR` environment variable.
  - Steve insisted that `isatty()` is too low level for what `std::print()` is intended to do.
  - Tom expressed support for dropping the wording regarding diagnosing invalid code units.
  - Tom asked if the wording should state something else regarding the behavior when invalid code unit
    sequences are present but concluded that likely falls under implementation-defined behavior related
    to use of the native Unicode API.
  - Jens asked if the Windows checks for code directed to a console have similar overhead concerns as
    calls to `isatty()` on POSIX systems.
  - Victor replied affirmatively but noted that there is no known alternative at present.
  - Victor stated that the check could become a no-op in the future if it becomes possible to check
    for use of a Unicode code page instead.
  - Victor summarized that we can either do the wrong thing quickly or the right thing slowly.
  - Jens expressed agreement for striking the wording regarding diagnosing invalid code unit sequences.
  - Peter opined that the wording appears to be written from a Windows point of view and seems quite
    strange from a POSIX perspective.
  - Peter suggested that the wording could discuss Windows specifically.
  - Jens replied that Windows is specifically addressed in a note.
  - Tom acknowledged that Peter has a valid point; the "native Unicode API" is only needed when writing
    directly to the stream is insufficient to produce the right result.
  - Eddie advised caution regarding discounting the possibility that writing directly to the stream
    could produce the right result on Windows.
  - Tom noted that Microsoft does ship versions of Windows that only support UTF-8 as the active
    code page and offered HoloLens as an example.
  - Steve asked if implementors need this guidance.
  - Victor replied that they do and that it took considerable exploration to determine exactly which
    functions were needed to achieve the right results.
  - Jens commented that this is one of those rare places in the standard where we try to tell
    implementors what to do rather than just specifying the required behavior.
  - Jens stated that the wording needs to be sufficient to guide implementors to the right result.
  - **Poll 2: Approve the LWG 4044 proposed resolution with the wording about diagnosing invalid code units removed.**
    - Attendees: 9
    - No objection to unanimous consent.
- Tom announced that the next meeting will be on 2024-03-13; the week before the Tokyo meeting.
- Tom requested suggestions for any papers or issues that need SG16 review prior to Tokyo.


# February 7th, 2024

## Agenda
- Updates from the Unicode liaison from the UTC #178 meeting.
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html).
- [P2845R6: Formatting of std::filesystem::path](https://wg21.link/p2845r6).
- [P3070R0: Formatting enums](https://wg21.link/p3070r0).

## Meeting summary
- Attendees:
  - Eddie Nolan
  - Jens Maurer
  - Mark de Wever
  - Nathan Owen
  - Peter Bindels
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Updates from the Unicode liaison from the UTC #178 meeting:
  - Robin shared the following updates:
    - Draft meeting minutes are available at https://www.unicode.org/L2/L2024/24006.htm#178-0.
    - Character assignments may now be specified on a provisional basis to facilitate early feedback
      and development; this is particularly useful for font development.
    - ICU will not expose characters in alpha or beta status.
    - Product releases should not include support for provisional character assignments.
    - Alpha review for Unicode 16.0 started yesterday; background material is available at
      https://www.unicode.org/review/pri497/pri497-background.html.
    - Unicode 16.0 will specify new normalization behavior that might invalidate optimization
      techniques used by some implementations.
    - A conformance testsuite is available that exercises the new normalization behavior.
    - There was a minor update to
      [UTS #55](http://www.unicode.org/reports/tr55/)
      for case insensitive identifiers.
    - \[ Editor's note: See the changes to
      [section 3.1.1, "Normalization and Case", in the 2024-01-03 proposed update of UTS #55](https://www.unicode.org/reports/tr55/tr55-4.html#Normalization-Case).
       \]
    - Fraser Gordon was nominated and confirmed to chair the Terminal Text Working Group.
    - The ICU technical committee has created a new Inflection Working Group.
  - Tom noted that the new Inflection WG would presumably be relevant to the
    Message Formatting Working Group.
  - Robin agreed.
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html):
  - Tom explained that, following decisions made during the
    [2024-01-10 SG16 meeting](https://github.com/sg16-unicode/sg16-meetings#january-10th-2024),
    we now need to select a Unicode version for the standard to refer to.
  - Steve proposed using the version that was current when designs were being evaluated and wording
    drafted.
  - Steve observed that doing otherwise might result in references that don't exist in the normatively
    referenced version or that behavior or features might have changed.
  - Steve stated that, for most features adopted during the C++23 development cycle, that would
    probably be Unicode 15.
  - Robin reported that Unicode 15.1.0 has material differences due to changes inspired by SG16 and
    the
    [UTS #55 (Unicode Source Code Handling)](https://www.unicode.org/reports/tr55/)
    effort that impacted the `XID_start` and `XID_continue` properties.
  - Robin noted that Unicode 15.1.0 also has changes for EGC segmentation for Indic scripts, shared
    a link to the
    [Sample Grapheme Clusters table in UAX #29 (Unicode Text Segmentation)](https://www.unicode.org/reports/tr29/#Table_Sample_Grapheme_Clusters),
    and referenced the Devanagari *kshi* example (क्षि).
  - Robin observed that the current undated reference currently resolves to Unicode 15.1.0.
  - Eddie indicated a desire to ensure that implementors can defer to ICU for normalization and be
    free to choose which ICU version they use.
  - Eddie reported that, following discussion with Zach, he was convinced to use the latest Unicode
    version which is currently 15.1.0.
  - Eddie stated that implementors should be able to use different Unicode versions for the core
    language and the standard library.
  - Steve pointed out that there are multiple options for an ICU version to defer to; if they choose
    to defer to one supplied by the platform, then they could get stuck with an old version.
  - Eddie replied that is motivation for implementors not to defer to a platform supplied version or
    for granting permission for use of an older version.
  - Steve noted that Linux distributors like RedHat support the installation of new compiler versions
    on older OS releases.
  - Steve reported having encountered issues due to use of old versions of some platform supplied
    libraries.
  - Steve stated that we need to allow time for implementors to adapt to changes to the normatively
    referenced version.
  - Tom asked Jens if he will want EWG to review the choice of normative Unicode version reference.
  - Jens replied that this issue has wide visibility and that the related GitHub issue is tagged for
    EWG and LWG as well as SG16.
  - Jens added that LWG can forward any concerns they have to LEWG.
  - Jens stated that CWG will only be involved to vet the actual wording changes and the guarantees
    regarding availability of character names as needed for the core language.
  - Mark commented that, if libc++ were to start relying on ICU, that such reliance would likely be
    expected to be satisfied by a distibution provided by the target platform.
  - Mark stated that use of ICU would likely be determined on a per-feature basis.
  - Eddie argued that such expectations suggest standardizing the lowest version that still covers
    everything in the standard.
  - Jens noted that, at present, that lowest version is the most recent Unicode version due to the
    undated reference in C++23.
  - Jens expressed being comfortable with specifying Unicode 15.0.
  - Jens stated an expectation that implementors will likely honor the resolution of this CWG issue
    for C++23 if it is approved as a DR.
  - Jens suggested that some implementors might choose to warn on use of features from newer
    Unicode versions.
  - Robin reported that it is possible to subdivide ICU to include only necessary components.
  - Robin added that it shouldn't be assumed that an implementor needs to rely on a version
    distributed with the platform.
  - Steve stated that ICU has support for symbol versioning and that this would allow an implementor
    to distribute their own version such that it will not conflict with other versions.
  - Jens suggested that future paper authors be encouraged to comment on whether implementations
    should or should not rely on ICU for particular features and the potential to get stuck with a
    dependency on an older version.
  - Jens advocated for collecting opinions from implementors.
  - Robin asserted that specifying Unicode 15.1.0 will help to position implementors for future
    upgrades.
  - Steve claimed it would be useful to give implementors advanced notice.
  - Tom asked if anyone knows what ICU version Microsoft provides and whether any implementations
    defer to it today.
  - Mark reported that Microsoft relies on the platform ICU version for timezone data, but not for
    `std::format()` related features.
  - \[ Editor's note:
    [Microsoft's ICU documentation](https://learn.microsoft.com/en-us/windows/win32/intl/international-components-for-unicode--icu-)
    does not report an ICU version, but does indicate that only C APIs are exposed due to the lack
    of a stable ABI for C++. \]
  - Steve asserted that we should not use a normative reference for a version prior to Unicode 14.0.
  - Steve stated that wording review would be necessary to determine if Unicode 13.0 matches the
    required features and intended semantics for recently adopted papers.
  - Eddie asked whether SG16 would be ok if, for
    [P2729 (Unicode in the Library, Part 2: Normalization)](https://wg21.link/p2729),
    implementors wanted to use the version of ICU provided by the platform.
  - Tom replied that he thinks implementors have options available to them to meet requirements;
    they might not love any of the options, but they do exist.
  - Steve asserted that we need to make it clear to implementors that they must use consistent
    implementations of the Unicode algorithms.
  - Eddie agreed and disclosed that there is also an unpublished proposal for segmentation.
  - Eddie reported that there is a long history of security vulnerabilities that occured due to
    use of parsers that interpreted the same text inconsistently.
  - Robin informed the group that ICU does not provide default tailoring support.
  - Steve responded that the base tailoring algorithms are not terribly difficult to implement but
    that some data is required.
  - **Poll 1: Recommend specifying Unicode 15.1.0 as the minimum Unicode version for C++23 (as a DR) and C++26.**
    - Attendees: 9
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   5 |   1 |   0 |   0 |
    - Consensus in favor
  - Tom stated that, with regard to Unicode versions being consistent across the core language
    implementation and the standard library, that it doesn't seem feasible to not allow divergence.
  - Steve commented that problems caused by a mismatch are unlikely to be worse than processing text
    from other sources.
  - Eddie noted that it is common to use Clang with libstdc++ and libc++ and that EDG does not
    provide a standard library implementation.
  - Mark reported that different people tend to work on the compiler and the standard library and
    that the versions of each can be mixed; requiring a consistent Unicode version would be very hard.
  - Steve took a devil's advocate role and suggested that, perhaps such cases are just not conforming.
  - Steve stated that it is not required for all deployments to be conforming; non-conforming is not
    the same as useless.
  - Steve opined that the standard should still acknowledge the possibility of mismatched versions.
  - Robin noted that the standard library does not currently require a normative reference to Unicode
    for any of its features at the moment.
  - Jens expressed a preference for treating the C++ standard as a unit and only normatively require
    a single Unicode version with allowances for use of a later version.
  - Tom agreed, but stated a desire to provide programmers the ability to query the version in use.
  - Jens replied that preprocessor behavior is impacted by Unicode version and that it is therefore
    unclear how useful a feature test macro would be.
  - Steve suggested that we might be getting ahead of ourselves in asking what we would use a feature
    test macro for.
  - Jens posited that a library version query utility of some kind might be more useful than a feature
    test macro.
  - Jens stated that certain features can just be avoided for core language.
  - Jens opined that it could be useful to write a `#error` directive based on Unicode version.
  - Tom concluded that we should avoid specifying a feature test macro and an explicit allowance for
    the core language and standard library to use different Unicode versions until more need is
    identified.
  - Tom stated that he will forward the CWG issue with the above poll.
- [P2845R6: Formatting of std::filesystem::path](https://wg21.link/p2845r6):
  - Victor introduced the recent changes.
    - The `path-format-spec` now supports a `g` option to enable formatting a path as a generic path.
  - Discussion in chat confirmed that `/` is used as the path separator when formatting a generic
    path and that the native path separator is used otherwise.
  - **Poll 2: Forward P2845R6 to LEWG.**
    - Attendees: 9
    - No objection to unanimous consent.
- [P3070R0: Formatting enums](https://wg21.link/p3070r0):
  - Victor explained the motivation for the new feature:
    - This allows defining a `format_as()` function rather than writing a `std::formatter`
      specialization.
    - This approach is simpler and more efficient at run-time.
  - Jens asked if an alternate type presentation can be requested in the format specifier.
  - Victor replied that a `std::formatter` specialization is required to do that.
  - Tom asked if the format specifier has to be `{}`.
  - Victor replied that it doesn't, that the format specifier is parsed according to the
    mapped type; the type returned by the `format_as()` customization point.
  - Jens asked if `format_as` is an existing customization point.
  - Victor replied that it is not; it is new with this proposal.
  - Eddie observed that the proposed functionality seems useful for many types, but that
    the proposal is restricted to enumeration types.
  - Victor responded that it is extensible to other types, but is limited to enumeration
    types for now due to lack of experience with other types.
  - Mark asked how field widths are handled.
  - Victor replied that they are handled the same as for the mapped type.
  - Eddie asked for confirmation that, as proposed, an attempt to use this feature for a
    type other than an enumeration type will fail.
  - Victor confirmed the intent, but noted that the proposed wording is currently missing
    a constraint.
  - Jens asked if the mapping is applied recursively and what happens if `as_format()`
    returns another enumeration type.
  - Victor replied that it should work, but that he needs to check and then update the
    paper accordingly.
  - Peter observed that this approach doesn't solve the problem of wanting to format the
    name of an enumerator.
  - Victor agreed that mapping an enumerator value to a name still has to be explicitly
    written but that reflection would make that easy.
  - **Poll 3: Forward P3070R0 to LEWG.**
    - Attendees: 9
    - No objection to unanimous consent.
- Tom announced that the next meeting will be on 2024-07-21 and that the agenda is TBD.


# January 24th, 2024

## Agenda
- [P3045R0: Quantities and units library](https://wg21.link/p3045r0).
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html).

## Meeting summary
- Attendees:
  - Billy Baker
  - Corentin Jabot
  - Eddie Nolan
  - Elias Kosunen
  - Fraser Gordon
  - Lauri Vasama
  - Mark de Wever
  - Mateusz Pusz
  - Nathan Owen
  - Jens Maurer
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [P3045R0: Quantities and units library](https://wg21.link/p3045r0):
  - Mateusz provided an introduction:
    - There is a need for some unit types to have both a basic unit symbol and one that includes characters
      that are not in the basic literal character set.
    - The proposed design allows specifying multiple symbols.
    - We need to decide how these different symbols are specified.
  - Tom asked what character types need to be supported.
  - Corentin recalled an LWG issue concerning the symbol used to print `std::chrono::duration` values with
    a microseconds period and that the issue was resolved in favor of allowing the implementation to choose
    between two symbols.
  - \[ Editor's note: See
    [LWG #3094 (§\[time.duration.io\]p4 makes surprising claims about encoding)](https://wg21.link/lwg3094)
    and the current wording in
    [\[time.duration.io\]p(1.5)](http://eel.is/c++draft/time.duration.io#1.5).
    \]
  - Corentin suggested that precedent could be followed here.
  - Corentin opined that there is not much motivation for `wchar_t`, `char16_t`, and `char32_t`.
  - Mateusz responded that there was only one such case to be addressed for the chrono library but there are
    many such cases for the units library.
  - Mateusz added that there is a desire to allow programmers to restrict formatting to basic characters so
    as to avoid non-basic characters being written in some cases.
  - Mateusz acknowledged that removing the need for multiple symbols would simplify the design.
  - Victor agreed with Corentin and argued for a design that is simple and prioritizes Unicode.
  - Victor stated it should not be necessary to spell out symbols for all five encodings.
  - Victor concurred that the `std::chrono::duration` example is a good model to follow.
  - Tom expressed skepticism regarding an implementation-defined approach since the units library is designed
    to be user extensible.
  - Tom expressed a preference to specify a design that will work for user code.
  - Corentin replied that the symbols for the unit types defined by the standard library could be
    implementation-defined.
  - Corentin observed that passing arbitrary string literals as template arguments could cause compatibility
    issues if a program includes translation units built with different choices of the ordinary literal
    encoding.
  - Corentin shared https://godbolt.org/z/8frTvfvoE as an example that demonstrates the concern.
  - \[ Editor's note: The concern is that a string literal like `"µ"` might be differently encoded such
    that the specialization `prefixed_unit<{"µ", "u"}, ...>` might not coincide across translation units. \]
  - Corentin expressed uncertainty regarding catering to programmers that want to avoid seeing non-ASCII
    characters.
  - Mateusz replied that the concern isn't just for reading the formatted output but that people need to be
    able to write the characters as well.
  - Mateusz reported that there is no standard for ASCII-only symbol names.
  - Steve agreed that the choice of ordinary literal encoding can create portability problems.
  - Steve advised caution regarding potentially requiring the ordinary literal encoding to be able to
    accommodate characters not in the basic literal encoding.
  - Elias observed that specifying the symbols as implementation-defined would cause problems for exchange
    of text.
  - Steve noted that C++23 requires a conforming implementation to support UTF-8.
  - Tom agreed, but noted that the UTF-8 requirement is for the encoding of source files and that the
    ordinary literal encoding need not support UTF-8.
  - Steve observed that the proposed design would therefore be unimplementable for some implementors.
  - Mark opined that it would be useful to specify alternate symbols for implementations to use.
  - Corentin asserted that ordinary character and string literals can't be used as template arguments due to
    the possibility of inconsistent ordinary literal encoding.
  - Mateusz pondered whether a Unicode encoding should be used for all the symbols.
  - Corentin replied that he thinks that is necessary to avoid compatibility problems.
  - Steve observed that the compiler can't correct for such incompatibilities because this is effectively a
    linkage concern.
  - Elias asked if there is a compelling reason for the symbol names to be provided as template arguments.
  - Mark replied that the motivation is to enable a succinct programming style as opposed to specializing a
    trait.
  - Victor opined that the symbol is data and should not be specified as part of the type.
  - Victor argued that moving the symbol out of the type system would make the design less fragile.
  - Victor stated that macros can be used to provide a succinct programming style.
  - Steve raised a concern that making data part of the type can lead to accidental ABI freezes where, for
    example, misspellings can't be fixed.
  - Steve noted that such a design limits future extension possibilities as well.
  - Tom asked Mateusz how moving the symbols out of template arguments would impact the design.
  - Mateusz replied that users appreciate the terseness the current design allows and stated that exposing
    macros as part of a standard interface would not be desired.
  - Mateusz acknowledged such a change would be possible though.
  - Elias cautioned that we don't have an alternative design in front of us to consider and that makes it
    difficult to evaluate relative benefits.
  - Mateusz stated that strong types are important to the design.
  - Mateusz suggested A CRTP-based design could work.
  - Victor stated that it seems problematic to have the symbol text be part of the identity of the type.
  - Victor suggested that tag types would be more appropriate.
  - Mateusz reported that he ran into difficulties when considering tag types but that he needs to explore
    some more.
  - Mateusz stated that use of tag types would change the interface considerably.
  - Steve returned discussion to support of multiple encodings and asserted that use of transliteration
    should be avoided since it can produce surprises like "Ω" (U+03A9 GREEK CAPITAL LETTER OMEGA) getting
    converted to "O".
  - Tom summarized his impression of where the discussion has been leading:
    - The proposal authors should explore alternatives to passing symbols as template arguments.
    - There does appear to be a need to specify symbol alternatives for different encodings.
    - A method of specifying a symbol alternative in a UTF form and another as an ordinary string literal
      should suffice to support all five encodings.
  - Victor reiterated that exploration of alternative designs should include the option of
    implementation-defined symbol selection.
  - Tom replied that there is still a need to specify symbol selection for user-defined units.
  - Corentin agreed that there appears to be consensus for a fallback symbol to be used when the preferred
    symbol is not representable.
  - Corentin expressed uncertainty regarding consensus for a user opt-in to use of a fallback symbol.
  - Mateusz directed discussion toward use of '_' to indicate a subscripted character in cases where
    Unicode lacks a corresponding character.
  - Steve stated that subscripted characters in Unicode exist solely for compatibility with legacy character
    sets and that subscripting and superscripting are considered markup.
  - Corentin opined that if subscripting and superscripting can't be done uniformly everywhere, then it
    should not be done anywhere.
  - Corentin suggested consulting with Robin.
  - Corentin wondered whether the ISO standards on units suggest a solution.
  - Jens stated that he doesn't think there is a portable way to represent physics symbols in ordinary
    string literals.
  - Jens suggested that it should be possible to allow a user to insert markup for support of subscripting
    and superscripting.
  - Jens questioned whether support for non-ASCII characters should be provided at all since plain text
    can't represent the desired formatting.
  - Mateusz replied that others have provided similar feedback such as the ability to produce LaTeX.
  - Mateusz stated that he doesn't know how to do that with `std::format` or `std::print` though.
  - Corentin agreed with Jens that users will want more capabilities and that these symbols are intended
    for display in a terminal.
  - Steve suggested that, since the library is intended to support user-defined units, perhaps the unit
    symbols defined by the standard library should be restricted to the basic literal character set and
    programmers can use whatever characters from the actual ordinary literal encoding that they like for
    their own unit types.
  - Steve commented that the symbol is significant in the type system.
  - Jens agreed that it is and that units need to be preserved such that
    `2*speed_of_light == speed_of_light`.
  - Victor agreed with Jens that we shouldn't put too much effort into pretty formatting since users can
    perform their own formatting.
  - Victor asserted that the main purpose of the library is to provide the unit primitives as opposed to
    nicely formatted output.
  - Mateusz asked if `std::format` could potentially take a tag type to differentiate behavior.
  - Victor replied that the way to differentiate behavior would be to write separate formatters.
  - Jens noted that the way to opt-in to such differentiated behavior is to wrap types accordingly.
  - Jens suggested updating the narrative of the paper to demonstrate how to produce nicely formatted
    output for these types.
  - Jens indicated that it would be nice to be able to specify custom formatting with a terse syntax.
  - Mateusz expressed uncertainty regarding how, for example, a `std::vector` of these types could be
    formatted in a custom way.
  - Jens acknowledged uncertainty regarding whether the `std::vector` formatters could handle that.
  - Jens observed that a `std::vector` wrapper could presumably apply a corresponding wrapper to its
    elements.
  - Jens suggested that an inability to do so might imply a deficiency in `std::format` that might
    be worth addressing and stated that an HTML formatter shouldn't require reinventing `std::format`.
  - Eddie opined that, even if formatted symbols are only used for debug-like scenarios, Unicode
    support is useful and should be a goal.
  - Mateusz reported that none of the units libraries that he is aware of provide such extensive
    formatting capabilities.
  - Jens opined that such capabilities are not needed for the standard either but that it would be
    useful to illustrate what a solution might look like.
  - Steve asked for additional topics that would benefit from discussion.
  - Mateusz asked for preferences regarding the return type of `unit_symbol()`.
  - No opinions were offered.
  - Mateusz stated that adding additional iostream manipulators is probably not desireable and recalled
    that previous discussion settled on just providing `std::format` support.
  - Tom asked Victor if there is an SG16 concern regarding section 13.4.1,
    "Controlling width, fill, and alignment".
  - Victor replied that the behavior should be consistent with other formatters and that any reason to
    deviate should be discussed.
  - Jens asked for confirmation that nested formatting works with ranges.
  - Mark and Victor both confirmed.
  - Mateusz stated that the proposal uses nested `{}` braces for formatting of subentities.
  - Victor expressed opposition to use of `{}` for nesting because it closes off syntax space that could
    be used for other extentions.
  - Victor noted that there are other delimiters that can be used.
  - Mateusz stated that the parse context isn't copyable, so there isn't a portable way to handle nesting.
  - Victor replied that implementation is straight forward using implementation internals.
  - Jens noted that, for the purposes of standardization, it doesn't matter if the subentity selection is
    portably implementable using existing implementations.
  - Corentin stated that the proposed approach doesn't support localization.
  - Tom noted that message formatting capabilities would be required for that.
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html):
  - Tom apologized for the lack of time for further review of this issue.
- Tom announced that the next meeting will be 2024-02-07.


# January 10th, 2024

## Agenda
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html).
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Jens Maurer
  - Mark de Wever
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Robin announced that the planned 2024-01-24 SG16 meeting overlaps with the UTC #178 meeting and
  that he will therefore be unable to attend.
- [CWG 2843: Undated reference to Unicode makes C++ a moving target](https://cplusplus.github.io/CWG/issues/2843.html):
  - Jens provided an introduction:
    - Undated references refer to the latest edition of such references.
    - The ISO prefers undated references.
    - WG21 negotiates the use of dated references with the ISO editors based on the fact that conscious effort is
      required to align wording and semantics with new editions.
    - The C++23 draft is still undergoing editorial changes in conjunction with the ISO.
    - The C++ standard used to have a normative reference to ISO/IEC 10646, but the reference was redirected to the
      Unicode Standard following additions that required features that are not specified in ISO/IEC 10646.
    - \[ Editor's note: The change of normative reference was made via
      [P2736R2 (Referencing The Unicode Standard)](https://wg21.link/p2736r2). \]
    - ISO/IEC 10646 is not identical to the relevant portions of the Unicode standard.
    - The ISO has so far not complained about the C++ standard's use of the Unicode Standard despite the ISO
      generally preferring to refer to ISO standards.
    - The undated reference to the Unicode Standard is "live"; which means that, as soon as a new Unicode Standard
      is published, the reference automatically refers to that edition.
    - That implies that a conforming implementation of C++23 that uses Unicode 15 becomes non-conforming the moment
      that Unicode 16 is published.
    - Changes to Unicode algorithms could impose ABI breaks that create difficulties for implementors.
    - The proposed resolution is to require conformance with Unicode 15.
    - It has also been suggested that a minimum Unicode version be specified with an allowance for implementors to
      use a more recent version.
    - A reference to a particular Unicode version is benficial even if an allowance is made for use of a later version.
    - Specifying both an undated and a dated reference would be weird.
  - Alisdair stated that issuing a DR has a similar effect to publication of a new edition of an undated reference,
    but differs in that the change happens under the auspices of WG21 rather than being imposed by an unaffiliated
    third party.
  - Jens clarified that DRs are not ISO publications and that WG21 so far has not made use of the ISO procedures for
    issuing technical corrigenda for defects or amendments for enhancements.
  - Robin objected to the notion of the Unicode Consortium being an unaffiliated third party and noted the formal
    liaison relationship with SC22.
  - Steve opined that fixing the Unicode version to Unicode 15 is probably fine for C++23.
  - Jens replied that C++23 is done with the exception of editorial changes being coordinated with the ISO and that
    any action taken for this CWG issue will target C++26.
  - Steve reported that he tends to start observing use of new Unicode features within four to six months of the
    publication of a new Unicode version.
  - Steve stated that new emoji are often the first new feature observed and that such text needs to be correctly
    processed.
  - Steve asserted that waiting for the next C++ standard for support of a new Unicode version isn't viable.
  - Steve agreed with the approach of specifying a minimum version with an allowance for implementors to upgrade
    at their discretion.
  - Steve advised against implementors using different Unicode versions for different C++ standard conformance
    modes since doing so would invite ODR violations.
  - Corentin expressed agreement with Steve's comments.
  - Corentin asserted that implementors need to be able to keep up with the Unicode Standard at a faster pace
    than the C++ standard can.
  - Corentin stated that it is likely not viable to support different Unicode versions for different C++ standard
    conformance modes.
  - Corentin reported having tried to support multiple Unicode versions in a private project and that it didn't
    work well.
  - Corentin noted that the Unicode Standard has a good history of maintaining backward compatibility and that
    changes made often address defects for which fixes are desirable.
  - Corentin agreed that a dated reference in the C++ standard is useful to facilitate references to specific
    sections by number and name.
  - Corentin opined that guidance for implementors to handle or avoid ABI issues in accordance with Unicode
    stability policies would be useful.
  - Corentin suggested that a note that expresses that intent would be helpful.
  - Corentin reported that Clang releases have stayed current with the most recent Unicode versions and will
    continue to do so.
  - Alisdair expressed alignment with Jonathan's suggestion for the version of the Unicode standard to be
    implementation-defined for defect reporting purposes.
  - Alisdair stated a preference for not requiring a minimum version so that implementors can provide options
    to enable backward compatibility with previous releases while remaining conforming.
  - Eddie noted an advantage of an undated reference is that it avoids potential opposition to updating the
    normative reference to a newer version due to ABI concerns.
  - Eddie explained that `std::format` already has the potential to lock in at compile-time features from the
    Unicode Standard that don't have a stability policy.
  - \[ Editor's note: Eddie later
    [clarified on the SG16 mailing list](https://lists.isocpp.org/sg16/2024/01/4097.php)
    some misconceptions regarding `constexpr` and `std::format`; implementors have flexibility to isolate ABI
    concerns using `if constexpr`. \]
  - Eddie agreed that it would be a good idea to provide guidance to implementors regarding how to isolate
    ABI concerns.
  - Robin recognized that, in the real world, modern compilers support C++11 despite C++11 no longer being an
    active ISO standard, and projects are still developed with it.
  - Robin cautioned that, if the version of the Unicode standard is tied to the C++ standard version, then
    projects using an older C++ version could be using a 10+ year old Unicode version and that possibility is
    even more concerning than having to wait three years to use a newer version.
  - Robin emphasized the Unicode Standard's stability guarantees.
  - Robin noted that implementations of a Unicode algorithm impose a limit on what Unicode versions are
    compatible.
  - Steve provided an example of such limitations; extended grapheme clusters (EGCs) were introduced after
    the initial Unicode release and the use of such features imposes a minimum version that is required.
  - Robin noted in the chat that EGCs were introduced in Unicode 5.1 in April of 2008.
  - Corentin expressed support for specifying a minimum Unicode version for portability reasons.
  - Corentin stated that he is not concerned about ABI issues at this point and asserted they haven't been a
    practical issue for Unicode concerns so far.
  - Mark replied that libc++ does have an ABI issue that will need to be resolved; there is a table that needs
    to have an ABI tag applied to it.
  - Mark expressed support for implementations being able to use newer Unicode versions because that is useful
    for users.
  - Mark stated a preference for an implementation-defined version rather than one which must be adhered to.
  - Alisdair indicated that he would be content to have market pressures determine compatibility.
  - Alisdair stated a desire for an allowance for a conforming implementation to support use of an older
    Unicode version for compatibility with prior C++ standard versions.
  - Alisdair stated in chat:
    "Conversely, I would not object to a “recommended practice” to set the floor, rather than making it normative".
  - Eddie asked if there is an ABI impact from `std::format` width estimation changes.
  - Mark replied that the width estimation in libc++ is `constexpr` as an implementation detail.
  - Tom expressed a belief that width estimation has to be performed with run-time field values.
  - Corentin acknowledged that the C++ standard may need to refer to a minimum Unicode Standard version just
    to be able to refer to certain features.
  - Corentin asserted that there are ways that implementors can hide things behind ABI and that this includes
    use in `constexpr` context.
  - Jens agreed with Alisdair that the Unicode version actually used in a particular language mode should be
    implementation-defined.
  - Jens disagreed about not specifying a definite minimum version.
  - Jens explained that core language features like named universal characters (`\N{...}`) require a minimum
    Unicode version in order to write portable code.
  - Jens asserted that features that can't be reliably used across implementations should be removed.
  - Jens observed that a consistent version of the Unicode Standard is required in order for the C++ standard
    to be consistent.
  - Jens opined that the C++ standard should not reference different Unicode versions for the core language
    and the standard library.
  - Tom asked if it might make sense for the minimum Unicode Standard version required for implementations to
    conform to the C++ standard to be different from the normative dated reference.
  - Jens replied negatively.
  - Jens stated that the formal text needs to provide the right guarantees even if implementors all do what
    we consider to be the right thing; the formal text must be sufficient to write portable programs.
  - Jens noted that the ISO will not permit the introduction of an alias for a normative reference.
  - Jens expressed uncertainty where a Unicode version conformance requirement should be specified, but stated
    that is likely a solvable problem.
  - Jens observed that identifiers have a forward compatibility guarantee thanks to the Unicode Standard
    stability policies for XID start and continue properties.
  - Steve reported that his organization builds their internal toolchain using system supplied libraries and
    noted this could produce a non-conforming implementation due to building with older Unicode libraries.
  - Steve indicated he is ok with that result though.
  - Steve noted that the Unicode Standard is a coherent specification and that mixing parts from different
    versions of it can produce non-sensical results.
  - Steve described "ABI problems" as shorthand for lots of different problems, some of which, like virtual
    function table layout differences, are catastrophic while other cases, like fast math enabled vs disabled,
    are not.
  - Alisdair stated that he has been persuaded by Jens' arguments that a dated reference to the Unicode Standard
    in the C++ standard with the actual version being implementation-defined is a good direction.
  - Alisdair opined that it is still important for implementors to be able to provide backwards compatibility
    and that he would prefer normative guidance for use of the normative dated reference to be the minimal
    version supported by an implementation.
  - Gordon explained that the ISO prefers undated references because ISO standard editions effectively disappear
    when superceded and asked for clarification that the Unicode Consortium handles this differently.
  - Robin confirmed that release of a new Unicode Standard does not obviate the preceding ones and provided
    a link to https://www.unicode.org/versions in the chat.
  - Robin asked for Jens to confirm that, with regard to named universal characters, whether the concern is in
    regard to upgrading compilers.
  - Jens explained that implementations might want to issue a portability warning for use of a name that was
    added in a later Unicode Standard than the dated version from the C++ Standard.
  - Jens reported that he wants to be able to rely on all character names from, e.g., Unicode 15, being available
    for use across all C++ implementations.
  - Robin asked if the same concern applies to identifiers.
  - Jens confirmed that it does.
  - Robin explained that, as long as the C++ standard specifies a minimum version and that implementations are
    permitted to use a newer version, then he is content; he would not be content with the C++ standard
    specifying a maximum version though.
  - Steve noted that implementations are free to accept ill-formed code as long as a diagnostic is issued.
  - Alisdair asked whether a feature test macro with predictable values can be specified.
  - Jens noted that the C++ standard currently provides the `__STDC_ISO_10646__` macro with a date value.
  - Corentin replied that the existing macro can't be relied on at compile-time because it is shared between
    the core language and the standard library.
  - Robin reported that the Unicode Standard does not have a stability policy for the format of the Unicode
    version but stated that such a policy could be proposed.
  - Jens replied that the year and month of the release date suffices assuming the Unicode Consortium doesn't
    start shipping new releases at a rate higher than once a month.
  - Tom summarized his perception of the emerging consensus:
    - The C++ standard should have a single dated reference to the Unicode Standard for consistency purposes.
    - A minimum Unicode version should be specified as normative guidance or as a mandatory requirement.
    - The actual Unicode version in use by an implementation should be implementation-defined and allowed
      to be newer than the minimum version.
    - The Unicode version in use by an implementation may differ for the core language vs the standard
      library; separate feature test macros may be required to identify the implementation-defined version.
  - Jens noted that the minimum version may be increased in future C++ standards to accommodate references
    to features introduced in newer versions.
  - Tom observed that some effort will be required to identify the minimum Unicode version required for the
    C++ standard.
  - Suggestions were made to specify Unicode 15 as the minimum version.
  - **Poll 1: Recommend having a dated reference to Unicode in the "Normative references" and add
    permission to implement an implementation-defined version.**
    - Attendees: 10
    - No objection to unanimous consent.
  - **Poll 2: The standard shall specify a mandatory minimum Unicode version.**
    - Attendees: 10
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   5 |   1 |   1 |   0 |
    - Consensus in favor
    - A: I would prefer to allow implementations to use older Unicode versions and still be considered
      conforming; implementations will do so regardless.
  - Steve summarized the consensus: we recommend having a dated reference to the Unicode Standard in the
    "Normative references" section, a minimum version requirement, and an allowance for implementors to
    use an implementation-defined later version.
  - Jens stated that he will update the proposed resolution for the CWG issue to reflect the SG16
    consensus.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0):
  - Tom thanked Corentin for agreeing to defer discussion of this paper.
- Tom reported that the next meeting will be in two weeks and will continue review of Mateusz' paper
  as well as additional followup on the CWG issue.


# November 29th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#november-29th-2023.


# October 25th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#october-25th-2023.


# October 11th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#october-11th-2023.


# September 27th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#september-27th-2023.


# September 13th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#september-13th-2023.


# August 23rd, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#august-23rd-2023.


# July 26th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#july-26th-2023.


# July 12th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#july-12th-2023.


# June 7th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#june-7th-2023.


# May 24th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#may-24th-2023.


# May 10th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#may-10th-2023.


# April 26th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#april-26th-2023.


# April 12th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#april-12th-2023.


# March 22nd, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#march-22nd-2023.


# March 8th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#march-8th-2023.


# February 22nd, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#february-22nd-2023.


# February 1st, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#february-1st-2023.


# January 25th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#january-25th-2023.


# January 11th, 2023

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2023.md#january-11th-2023.


# December 14th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#december-14th-2022.


# November 30th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#november-30th-2022.


# November 2nd, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#november-2nd-2022.


# October 19th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#october-19th-2022.


# October 12th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#october-12th-2022.


# September 28th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#september-28th-2022.


# September 14th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#september-14th-2022.


# August 24th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#august-24th-2022.


# July 27th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#july-27th-2022.


# June 22nd, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#june-22nd-2022.


# June 8th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#june-8th-2022.


# May 25th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#may-25th-2022.


# May 11th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#may-11th-2022.


# April 27th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#april-27th-2022.


# April 13th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#april-13th-2022.


# March 9th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#march-9th-2022.


# February 23rd, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#february-23rd-2022.


# February 9th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#february-9th-2022.


# January 26th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#january-26th-2022.


# January 12th, 2022

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md#january-12th-2022.


# December 15th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#december-15th-2021.


# December 1st, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#december-1st-2021.


# November 17th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#november-17th-2021.


# November 3rd, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#november-3rd-2021.

  
# October 20th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#october-20th-2021.


# October 6th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#october-6th-2021.

  
# September 22nd, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#september-22nd-2021.


# September 8th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#september-8th-2021.


# August 25th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#august-25th-2021.


# July 28th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#july-28th-2021.


# July 14th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#july-14th-2021.


# June 23rd, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#june-23rd-2021.


# June 9th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#june-9th-2021.


# May 26th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#may-26th-2021.


# May 12th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#may-12th-2021.


# April 28th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#april-28th-2021.


# April 14th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#april-14th-2021.


# March 24th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#march-24th-2021.


# March 10th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#march-10th-2021.


# February 24th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#february-24th-2021.


# February 10th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#february-10th-2021.


# January 27th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#january-27th-2021.


# January 13th, 2021

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#january-13th-2021.


# December 9th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#december-9th-2020.


# November 11th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#november-11th-2020.


# October 28th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#october-28th-2020.


# October 14th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#october-14th-2020.


# September 23rd, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#september-23rd-2020.


# September 9th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#september-9th-2020.


# August 26th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#august-26th-2020.


# August 12th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#august-12th-2020.


# July 22nd, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#july-22nd-2020.


# July 8th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#july-8th-2020.


# June 17th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#june-17th-2020.


# June 10th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#june-10th-2020.


# May 27th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#may-27th-2020.


# May 13th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#may-13th-2020.


# April 22nd, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#april-22nd-2020.


# April 8th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#april-8th-2020.


# March 25th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#march-25th-2020.


# March 11th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#march-11th-2020.


# February 26th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#february-26th-2020.


# February 5th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#february-5th-2020.


# January 22nd, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#january-22nd-2020.


# January 8th, 2020

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#january-8th-2020.


# December 11th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#december-11th-2019.


# November 20th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#november-20th-2019.


# October 23rd, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#october-23rd-2019.


# October 9th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#october-9th-2019.


# September 25th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#september-25th-2019.


# September 4th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#september-4th-2019.


# August 21st, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#august-21st-2019.


# July 31st, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#july-31st-2019.


# June 26th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#june-26th-2019.


# June 12th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#june-12th-2019.


# May 22nd, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#may-22nd-2019.


# May 15th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#may-15th-2019.


# April 24th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#april-24th-2019.


# April 10th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#april-10th-2019.


# March 27th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#march-27th-2019.


# March 13th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#march-13th-2019.


# February 13th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#february-13th-2019.


# January 23rd, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#january-23rd-2019.


# January 9th, 2019

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md#january-9th-2019.


# December 19th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#december-19th-2018.


# December 5th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#december-5th-2018.


# October 17th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#october-17th-2018.


# October 3rd, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#october-3rd-2018.


# August 29th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#august-29th-2018.


# July 25th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#july-25th-2018.


# July 11th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#july-11th-2018.


# June 20th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#june-20th-2018.


# May 30th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#may-30th-2018.


# May 16th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#may-16th-2018.


# April 25th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#april-25th-2018.


# April 11th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#april-11th-2018.


# March 28th, 2018

See https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#march-28th-2018.


# Prior std-text-wg meetings

Meetings held by the informal std-text-wg working group prior to the
formation of SG16 are available at:
- https://github.com/tahonermann/std-text-wg/blob/master/MeetingNotes.md
