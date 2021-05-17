# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.

# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, May 26th, 2021, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20210526T193000&p1=1440&p2=tz_pdt&p3=tz_mdt&p4=tz_cdt&p5=tz_edt&p6=tz_cest)).
The draft agenda is:
- [P2295R3: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r3)
  - Review updates intended to address prior SG16 feedback.
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - Discuss locale dependent character encoding concerns.

# Past SG16 meetings

- [May 12th, 2021](#may-12th-2021)
- [April 28th, 2021](#april-28th-2021)
- [April 14th, 2021](#april-14th-2021)
- [March 24th, 2021](#march-24th-2021)
- [March 10th, 2021](#march-10th-2021)
- [February 24th, 2021](#february-24th-2021)
- [February 10th, 2021](#february-10th-2021)
- [January 27th, 2021](#january-27th-2021)
- [January 13th, 2021](#january-13th-2021)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# May 12th, 2021

## Agenda:
- [P2295R3: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r3)
- [P2372R1: Fixing locale handling in chrono formatters](https://wg21.link/p2372r1)
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Tom Honermann
  - Steve Downey
  - Victor Zverovich
  - Zach Laine
- [P2295R3: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r3)
  - No discussion as the author was not present.
- [P2372R1: Fixing locale handling in chrono formatters](https://wg21.link/p2372r1)
  - \[ Editor's note: D2372R1 was the active paper under discussion at the telecon.  That paper
    was later published as P2372R1 without further modification.  The agenda and links used here
    reference P2372R1 since the links to the draft paper were ephemeral. \]
  - PBrett introduced the topic:
    - LEWG reached consensus for the direction proposed by
      [P2372R0](https://wg21.link/p2372r0) at its
      [2021-05-03 telecon](https://wiki.edg.com/bin/view/Wg21telecons2021/P2372#2021-05-03)
      with additional refinement to preserve locale dependent formatting for iostreams.
    - Since SG16 polls conduced at its
      [2021-04-28 telecon](https://github.com/sg16-unicode/sg16-meetings#april-28th-2021)
      did not agree with this direction, LEWG requested that SG16 review and conform or rebut
      the LEWG consensus.
  - Victor presented slides lightly updated from his prior LEWG presentation.
    - Victor's presentation slides are available
      [here](https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2021-05-12-p2372-presentation.pdf).
  - **Poll 1: Forward D2372R1 to LEWG for inclusion in C++23 and with the intent that it be applied retroactively to C++20.**
    - Attendance: 8

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   5 |   2 |   1 |   0 |   0 |

    - Consensus: Strong consensus in favor.
  - \[Editor's note: D2372R1 contains the LEWG requested update to preserve locale dependent formatting for
    ostreams.\]
  - \[Editor's note: The chairs perception is that SG16's change in consensus is attributable to two factors:
    1) New information that arrived after the initial poll.
    2) SG16's original poll targeted C++23 while LEWG's poll target's C++23 and C++20 as a DR; some concerns
       had been expressed regarding backward compatibility and migration.

    \]
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - Victor presented:
    - `std::print()` integrates `std::format()` with I/O.
    - R6 addresses recent LEWG feedback:
      - The proposed `std::print()` header was changed from `<io>` to `<print>`.
      - Additional rationale and clarifications were added regarding:
        - Substitution of replacement characters.
        - The choice to base behavior on the compile-time literal encoding.
        - ANSI escape sequences do not constitute a native device API.
        - Existing practice in Rust.
  - PBrett asked how substitutions would be performed for different kinds of ill-formed scenarios.
  - Zach stated that the Unicode standard documents recommended practice for substitution of
    replacement characters.
  - \[ Editor's note:
    [Unicode 13](http://www.unicode.org/versions/Unicode13.0.0)
    discusses substitution of replacement characters in
    section "U+FFFD Substitution of Maximal Subparts" of chapter 3.9, "Unicode Encoding Forms" and in
    chapter 5.22, "U+FFFD Substitution in Conversion". \]
  - Zach expressed a preference for implementations to be consistent in how replacement characters are
    substituted.
  - Hubert stated that an example should be added to the paper.
  - Hubert expressed a preference for `vprint_unicode()` to substitute replacement characters even
    when the output device is not Unicode.
  - Victor asked if that could be done as implementation-defined behavior.
  - Hubert responded, no; the goal is for the substitution behavior to be determinstic for
    `vprint_unicode()` regardless of the output device.
  - Victor replied that he would prefer that behavior to be optional.
  - Hubert replied that he would like to ensure that ill-formed inputs are not presented with
    no indication that something went wrong.
  - PBrett stated that, when writing to a Unicode device, a `U+FFFD` replacement character should
    be substituted and the device should then handle it as its designers intended.
  - Victor agreed with the substitution rationale for the device case since transcoding may be
    necessary, but disagreed for files due to a desire to avoid the validation overhead.
  - Hubert expressed a preference for the behavior of `vprint_unicode()` to be consistent across
    files and devices.
  - PBrett suggested that what Hubert desires is some kind of noisy failure, like a trap.
  - Hubert agreed and restated the goal as some kind of signal that encoding issues were
    encountered.
  - Steve stated that C++ programs do not typically interact directly with a device and that it
    is difficult to diagnose problems where the data can't be inspected en route.
  - PBrett asked if Steve had a suggestion.
  - Steve responded with a preference for a programatic error handling facility.
  - Zach stated that, in the case where UTF-8 source is copied to a UTF-8 sink, introduction of
    replacement characters could be surprising, but when transcoding is required, e.g., when the
    sink is UTF-16, then replacement characters are expected.
  - Zach suggested decomposing the problem; validate and handle errors first, then convert.
  - Charlie explained that, on Windows, the only ways to write Unicode to the console are to change
    the console encoding and write using the ANSI APIs, or to convert to UTF-16 and write using the
    wide APIs.
  - Charlie noted that, since the console encoding is a global property of the process, changing it
    within `std::print()` would require synchronization.
  - Zach suggested that it is reasonable to get mojibake in the ANSI case if the console encoding
    hasn't been correctly set.
  - Hubert responded that the global console encoding condition seems to be particular to Windows
    and worth addressing.
  - Charlie pondered the ramifications of writing to a stream opened in text mode.
  - Victor reiterated his stance on not wanting to pay validation costs except in cases where
    transcoding is necessitated.
  - **Poll 2: When \<print\> facilities must transcode formatting results for display on a device**
    **and, during that process, invalidly-encoded text is encountered, `std::print()` should replace**
    **the erroneously-encoded code units with U+FFFD REPLACEMENT CHARACTER.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   3 |   3 |   1 |   2 |   0 |

    - Consensus is in favor.
    - A: Not convinced that silently substituting replacement characters is always the right policy;
      an exception could be appropriate.  There are parallels with integer overflow.
    - A: Testing is difficult if substitution is device sensitive.
  - Charlie expressed support for a direction that would allow explicitly inhibiting use of the
    native device API but noted that, on Windows, that would mean the console encoding would have to
    be correctly set and the application would have to take care of buffering concerns.
  - **Poll 3: When \<print\> facilities need not transcode their formatting results for display**
    **on a device and invalidly-encoded text is encountered, `std::print()` should nevertheless**
    **replace the erroneously-encoded code units with U+FFFD REPLACEMENT CHARACTER.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   1 |   0 |   2 |   2 |   3 |

    - N: Undecided due to uncertainty; more consideration is needed.
    - A: Would prefer a UB approach that would enable sanitizers to diagnose these cases and remain
      conforming.
    - SA: There is lack of implementation experience for this direction, it imposes overhead, and there
      are terminals that accept bytes.
    - SA: A wide contract with validation does not make sense for high-performance I/O.
  - PBrett stated that there appear to be different audiences for `std::print()` and these audiences
    have different ideas of what is "obviously" correct:
    - For some, `std::print()` is a simple tool that enables a better Hello World.
    - For others, it is a high-performance I/O facility.
    - For yet others, it is a way to format bytes.
  - Tom suggsted that an error handling facility might move us towards more consensus.
  - PBrett noted that something like JeanHeyd's transcoding facilities could provide that.
  - Charlie agreed that integration of a familiar transcoding facility could work.
- Tom stated that the next telecon will be May 26th and that the agenda will again include
  [P2295R3](https://wg21.link/p2295r3) and
  [P2093R6](https://wg21.link/p2093r6).


# April 28th, 2021

## Agenda:
- [LWG3547: Time formatters should not be locale sensitive by default](https://cplusplus.github.io/LWG/issue3547)
- [P2093R5: Formatted output](https://wg21.link/p2093r5)
- [P2295R3: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r3)
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Charlie Barto was welcomed with a round of introductions.
- PBrett introduced the agenda.
- [LWG3547: Time formatters should not be locale sensitive by default](https://cplusplus.github.io/LWG/issue3547)
  - PBrett presented:
    - Peter's presentation slides are available
      [here](https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2021-04-28-lwg3547-presentation.pptx).
    - As currently specified, whether a format specifier is locale dependent is not obvious.
    - Floating point values are locale independent by default, but chrono values are not.
    - There is no systematic way to format locale-independent and locale-dependent chrono values.
  - Victor expressed a preference for chrono values being locale independent by default.
  - Victor explained that the current specification derived from existing specifiers used elsewhere.
  - Victor noted that, in some cases, specifiers are not available for locale independent formatting.
  - Victor reported success with a prototype implementation of the proposed resolution that performs
    locale independent formatting of chrono values unless a `L` specifier is present.
  - Charlie stated that changes to the format specifier syntax may have more implementation impact
    than just requiring changes to the implementation behavior.
  - \[ Editor's note: Discussion regarding the amount of time available to make changes before
    implementations of `std::format()` are shipped to users ensued.  That discussion is not recorded
    as it involved discussion of internal company time lines that have not yet been stated in
    public. \]
  - PBrett noted that there are two related issues:
    - 1: The format specification syntax.
    - 2: The behavior of the format specifiers.
  - PBrett explained that the proposed resolution addresses both concerns by making the format syntax
    consistent in requiring a `L` specifier to opt-in to locale dependent behavior.
  - Charlie noted that `std::format()` does not currently perform any transcoding operations today;
    not for format arguments, and not for text provided by a locale that uses a different character
    encoding than the literal encoding.
  - Charlie added that `std::format()` does need to be encoding aware for the purposes of field width
    estimation.
  - Corentin stated that the intent of the proposed resolution is to ensure that `std::format()` use
    consistent syntax to opt-in to locale dependent formatting and encouraged trying to address at
    least this concern.
  - Corentin added that LWG might agree on a resolution in a short time frame, but that there will
    not be a plenary poll until June.
  - PBrett stated that the resolution may be considered evolutionary.
  - Victor agreed and noded that the `L` specifier could be added for a future standard.
  - Victor asserted that we do need to decide what the default behavior is now.
  - Victor added that we could consider transcoding locale provided text and potentially detecting
    mojibake if it would be produced.
  - Victor noted that the format string is always a literal.
  - \[ Editor's note: In C++20, the format string may not be a literal, but
    [P2216](https://wg21.link/p2216), if adopted, will require a literal or other compile-time
    evaluated expression. \]
  - Zach asked for clarification regarding what is meant by "default behavior" and noted that the
    `%Ou` specifier is locale dependent, but that `%u` is not.
  - Victor responded that there are cases like `%T` that do not have locale independent forms.
  - \[ Editor's note: `%T` is locale dependent because the decimal point character potentially used
    for sub-second precision is provided by the locale. \]
  - Hubert stated that these concerns will be difficult to resolve quickly, are clearly evolutionary,
    and may require balloting.
  - Hubert added that there may also be issues with requiring the locale independent behavior to use
    English translations.
  - Tom noted that the basic source character set already has a bias in English.
  - Hubert responded that this goes further; we may potentially have to specify behavior in terms of
    `asctime()`.
  - Charlie commented that the text provided by the locale facet is currently produced by the
    operating system; changing that behavior may not be problematic.
  - Charlie added that adding new format specifiers will result in incompatibilities if code that
    uses those specifiers is run with an older library implementation that doesn't support them.
  - Charlie noted that, if support for compile-time format string checking is adopted via
    [P2216](https://wg21.link/p2216), then the format string will become part of the function template
    specialization; this may help to avoid library compatibility issues.
  - Charlie stated that there are multiple sources of locale information and that formatting of the
    chrono types is goverend by the Windows region settings.
  - Charlie noted that changes to the Windows region settings require a reboot.
  - Tom asked for confirmation that calls to `std::setlocale()` don't affect how chrono values are
    formatted.
  - Charlie confirmed that is correct.
  - PBrett asked if `std::format()` behavior is affected by changes to the global locale via
    `std::locale::global()`.
  - Charlie responded that the global locale does affect the behavior of format specifiers that
    include the `L` specifier.
  - Charlie clarified that the global locale will not affect parsing of the format string itself.
  - Corentin requested review of the proposed resolution.
  - Hubert noted that the wording requires that the "C" locale be used for field formats that do
    not include the `L` specifier regardless of whether a `std::locale` argument is passed.
  - Hubert noted that under the C++20 wording, implementations trying to accomodate this tentative
    future direction may be more able to ignore the global locale than an explicit locale argument.
    So, a change that maintains respecting the locale parameter is more compatible with C++20.
  - Tom responded that doing so would not be consistent with the other standard format specifiers.
  - Victor agreed and added that he would be strongly opposed to implicit use of a `std::locale`
    parameter.
  - Jens stated that a migration path to better behavior needs to be estalished and noted that
    the current situation is an interesting mess.
  - Jens suggested investigating how to increase consistency with the existing locale dependent
    format specifiers; e.g., for decimal point and digit group separator characters.
  - Jens added that there may be cases where it would be useful to be able to specify use of the
    "C" locale even when a locale is provided as an argument.
  - Jens observed that use of the "C" locale for the chrono `%p` specifier would be consistent
    with use of the "C" locale for floating point values.
  - Jens noted that the example in the proposed resolution does not match the proposed grammar;
    the `L` specifier should precede the _chrono-specs_ specifier, not follow it.
  - Jens stated that adding support for the `L` specifier is backward compatible from a standard
    evolution perspective.
  - Tom stated that a change to use the "C" locale in place of the global locale or a locale
    passed as an argument can be done as a non-abi breaking change.
  - Charlie agreed, but noted that some implementation tricks may be required to avoid potential
    conflicts with older libraries.
  - Zach stated that mixing different library versions is non-conforming anyway.
  - Corentin stated that the "C" locale is used as a proxy for the absence of a locale and suggested
    that a constexpr locale might be desired in the future.
  - Corentin asked Charlie if formatters can be modified without breaking ABI.
  - Charlie replied that they are templates, so modifications can result in ODR violations.
    Charled added that inline namespaces can be helpful in some cases.
  - PBrett asked for confirmation that use of a `L` specifier where one is not expected will result
    in a format exception being thrown.
  - Victor confirmed that is the case.
  - PBrett asked if the `L` specifier could be reserved now such that a format exception will be
    thrown if used, and then different behavior specified later.
  - Charlie responded that changing behavior to not throw in cases where an exception was previously
    thrown is fine so long as mixed library version problems are avoided.
  - Victor expressed agreement with Jens' prior comments.
  - Victor stated that behavior must remain consistent between `std::format()` overloads that do and
    do not accept `std::locale` arguments; the presence of the `std::locale` argument must not, by
    itself, affect behavior.
  - PBrett suggested that a paper that explores the alternatives may be required.
  - Corentin asserted that it must be possible to evolve the `std::format` format string so as to
    add new behaviors.
  - Corentin expressed distaste for the idea of a "no locale" specifier; that approach would still
    result in inconsistencies with number formatting.
  - Charlie agreed.
  - Jens conceded that challenging standardization work will be required if behavior changes from
    C++20 to C++23.
  - Jens asserted that the right to add format specifiers when a new standard is issued must be
    reserved, even if doing so causes implementation challenges.
  - **Poll 1: LWG3547 raises a valid design defect in \[time.format\] in C++20.**
    - Attendance: 11

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   7 |   2 |   2 |   0 |   0 |

    - Consensus: Strong consensus that this issue represents a design defect.
  - Hubert noted that, with regard to issues of consistency, the proposed resolution is a departure
    from existing interfaces such as `strftime()`.
  - **Poll 2: The proposed LWG3547 resolution as written should be applied to C++23.**
    - Attendance: 11

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   4 |   2 |   4 |   1 |

    - No consensus.
    - SA: Mitigation of behavior changes sensitive to string literal contents is very difficult and
      there are options available to deal with this problem in an additive way; this direction
      represents an unnecessary backward compatibility break.
  - Mark stated that the proposed resolution would have been great 18 months ago.
  - PBrett responded that we need to recognize when we make mistakes and own correcting them.
  - Corentin lamented the current state being another case of a bad default.
  - Tom suggested that the current behavior can be presented as intentional with the goal to maintain
    consistency with existing interfaces; new format specifiers can then be added in C++23.
  - PBrett suggested that an SG16 issue be filed and a volunteer found to work on it.
  - Victor responded that the behavior isn't sufficiently broken to make him want to spend time on it.
  - \[ Editor's note: Despite that lack of desire, Victor and Corentin quickly authored an initial
    draft paper that will become [P2372R0](https://wg21.link/p2372r0) once published. \]
  - PBrett volunteered to work on a paper.
- Tom and PBrett thanked Charlie for joining the telecon and encouraged him to continue attending.
- Tom stated that Victor had expressed interest in working on a potential `std::locale` replacement
  and asked if there were other volunteers interested in such work.
  - Victor responded that the motivation was provided by Hubert's example code included in the
    telecon agenda, that he is interested in conducting some implementation experiments, but that he
    does not have anything concrete in mind yet.
  - \[ Editor's note: Hubert's example is below.  In addition to the question of which locale is used
    in the formatting, there is a question of how encoding issues are handled.  The example depends on
    a locale to provide translations of AM/PM designators for a 12-hour clock.  What happens when the
    literal encoding is UTF-8 and the locale provides translations in Windows codepage 932?
    
        std::print("{:%r}\n", std::chrono::system_clock::now().time_since_epoch());
    \]
  - PBrett expressed interest in being involved.
- Tom stated that the next SG16 telecon will be held May 12th.
  - Tom added that the agenda will include further discussion of
    [P2093R5: Formatted output](https://wg21.link/p2093r5) and a return to
    [P2295R3: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r3).
  - PBrett asked if a CWG expert could review and comment on the updated wording for P2295R3.
  - Hubert agreed to do so.
  - Corentin requested a CWG expert also review the proposed wording in
    [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0).


# April 14th, 2021

## Agenda:
- [P2295R2: Correct UTF-8 handling during phase 1 of translation](https://isocpp.org/files/papers/P2295R2.pdf)
- [P2348R0: Whitespaces Wording Revamp](https://isocpp.org/files/papers/P2348R0.pdf)

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- PBrett introduced the agenda.
- [P2295R2: Correct UTF-8 handling during phase 1 of translation](https://isocpp.org/files/papers/P2295R2.pdf)
  - Corentin introduced:
    - This is a proposal to require that UTF-8 be one of the set of otherwise implementation-defined source file
      encodings.
    - With regard to ill-formed code unit sequences, there is no such thing; the source code is either valid UTF-8
      or it is not UTF-8.
    - Gcc does not validate its presumed UTF-8 input.
    - With regard to BOMs, the proposal does not impose any requirements other than that a BOM present in a UTF-8
      source file be ignored for the purposes of lexing.
    - An implementation may use the presence or non-presence of a BOM as part of its source file encoding determination.
    - The proposed wording will require updates for changes that will presumably be adopted from Jens'
      [P2314: Character sets and encodings](https://wg21.link/p2314).
    - This proposal follows Beman Dawes' earlier proposal,
      [N3463: Portable Program Source Files](https://wg21.link/n3463).
    - At present, the C++ standard has no requirement for a portable source file.
  - Tom stated that gcc will perform UTF-8 validation if both `-finput-charset=utf-8` and `-fexec-charset=utf-8` are
    specified.
  - \[ Editor's note: Tom was wrong (and since Tom is also the editor, he can be blunt like that); gcc only validates
    UTF-8 for string literals, and then only if `-fexec-charset=<encoding>` is specified. \]
  - Jens noted a capitalization issue in the wording; the sentence following the added note in \[lex.phases\]p1 has
    a capitalized "The" following a ";".
  - Jens asked why the note added to \[lex.phases\]p1 is just a note; the preceding prose provides a definition, but
    does not impose any requirements.
  - PBrett responded that, if an invalid sequence is present, then there is no sequence of Unicode scalar values.
  - PBrett asked if moving the note after the following sentence would resolve the concern.
  - Jens replied that it would not; that would define a UTF-8 source file and state that a well-formed UTF-8 source
    file must be accepted, but would impose no requirements on an ill-formed UTF-8 source file.
  - PBrett acknowledged that further wording work is needed.
  - Jens observed, and noted that the paper discusses, that implementations can accept source files that approximate
    UTF-8.
  - Hubert noted that a normative statement is needed to state that it is implementation-defined how a requirement
    for UTF-8 source files is specified.
  - PBindels suggested placing a requirement for well-formed input with the character set definitions.
  - Jens indicated no objection to clarification, but that he would like to see the ISO 10646 definition of
    "well-formed".
  - Steve observed that the note is stating that invalid UTF-8 sequences cannot happen in a well-formed UTF-8 
    source file.
  - Jens responded that there is a normative difference between something that cannot happen and something that is
    ill-formed; the latter requires a diagnostic.
  - Hubert asserted that the wording needs to establish intent; a sequence of bytes may happen to be well-formed
    UTF-8, but the wording needs to ensure that the bytes were intended to be interpreted as UTF-8.
  - PBindels summarized; we need to state there is an implementation-defined way to specify that a source file is to
    be interpreted as UTF-8.
  - Jens agreed.
  - JenaHeyd agreed from chat, "Yes, Hubert's definition is correct. You have to make it so the implementation has a
    way to mark/identify a source file as UTF-8, and then you can impose these requirements."
  - Corentin stated the intent; that the compiler determine the source encoding in an implementation-defined way,
    but that a source file that does not decode successfully is diagnosed as ill-formed.
  - Tom suggested specifying that the file must decode successfully as opposed to being well-formed.
  - PBrett stated that a branch is needed in translation phase 1 to distinguish the cases where the source file is
    encoded as UTF-8 vs some other encoding.
  - Zach suggested that a definition for a UTF-8 source file is unnecessary.
  - PBindels expressed concern that there may be a conflict between use of a BOM and a truly portable source file.
  - PBrett responded that the goal is that, if a source file is UTF-8 encoded, that there is a way to direct an
    implementation to process it as such.
  - Jens acknowledged and added that an implementation could require use of a command line option to opt-in to UTF-8
    encoded source files; that implies that the source file is not automatically portable, but is the best we can do.
  - Tom agreed and stated that the only way we could do better is to require a BOM everywhere and nobody wants that.
  - Zach noted that the only statement made regarding a BOM is that it can be ignored; presumably after encoding
    determination is complete so that the BOM doesn't interfere with translation phase 2.
  - Hubert noted that, once the encoding is determined to be UTF-8, a BOM is portably ignored.
  - PBrett encouraged assumption of non-hostile implementations; no implementation is going to require a BOM in order
    for a UTF-8 encoded source file to be processed as such.
  - Several relevant comments were made from chat:
    - Steve: "We want portable source code. If anyone requires a BOM, then portable source code needs one."
    - JeanHeyd: "If you put in a BOM and use -fexec-charset=SHIFT-JIS, the implementation can ignore the BOM and
      still read everything as SHIFT-JIS."
    - Hubert: "If you did that, the BOM is not a BOM..."
  - Jens suggested that the wording needs to establish when encoding determination happens; that should be the first
    step of translation phase 1.
  - Jens added that the wording should be consistent with regard to encoding vs encoding form vs encoding scheme.
  - Tom stated that, for UTF-8, encoding form vs encoding scheme doesn't matter, but that encoding scheme should be
    used if the intent is for the wording to be compatible with UTF-16 or UTF-32.
  - Hubert asserted that, since the context is byte oriented files, encoding scheme should be used.
  - Jens reiterated the necessary wording updates; the encoding scheme to use must first be established, then the
    source file can be validated and diagnostics issued if it fails to conform to the encoding scheme.
  - Jens added that the wording needs to prevent the current implementation-defined mapping to the internal encoding
    from being applied to UTF-8 source files.
  - PBindels asked if the added sentence in translation phase 2 regarding the "first codepoint" applies to each
    source file or just to the primary source file.
  - Tom and Corentin replied that translation phases 1 through 3 are performed separately for each source file.
  - Hubert suggested that translation phase 2 should discard a lead U+FEFF character regardless of the source file
    encoding.
  - Jens noted that the added translation phase 2 sentence doesn't make sense without the wording changes proposed in
    [P2314: Character sets and encodings](https://wg21.link/p2314)
    due to character translation to _universal-character-name_ in translation phase 1.
  - Tom noted that the wording changes in P2314 allow distinguishing a source file with a BOM and a source file that
    starts with a `\uFEFF` _universal-character-name_.
  - Jens clarified that, after P2314, a _universal-character-name_ isn't translated to a UCS scalar value until
    translation phase 3.
  - Hubert stated that it is a design question whether we want to treat a leading `\uFEFF` _universal-character-name_
    as a BOM.
  - PBrett asked PBindels if he is satisfied with the BOM design following prior discussion.
  - PBindels responded that he is, so long as we don't intentionally or unintentionally create the situation where
    UTF-8 source files end up requiring a BOM in practice.
  - PBrett asked if we should add normative encouragement not to require a BOM.
  - Hubert noted that, as wording updates are done, care must be taken to ensure we don't lose the wording that
    requires an implementation to accept a UTF-8 encoded source file whether it does, or does not, contain a BOM.
  - Tom asked about handling of differently encoded source files.
  - JeanHeyd replied in chat, "I think it's better to leave Encoding Identication to Tom's Paper on the subject."
  - Tom replied in chat, "Assuming I actually deliver on that threat..."
  - Hubert responded that the implementation must provide some means for standard headers (as opposed to header files),
    to remain usable when the implementation is running in UTF-8 mode.
  - Steve added in chat, "Which might be 7 bit ascii for those headers. Which is largely the case today."
  - **We wish to require implementations to support UTF-8 source files.**
    - Attendance: 10
    - No objections to unanimous consent.
  - **We wish to require implementations to be capable of accepting UTF-8 source files whether or not they begin with a U+FEFF byte order mark.**
    - Attendance: 10
    - No objections to unanimous consent.
  - Hubert reported that Clang allows non-UTF-8 encoded header names in `#include` directives in otherwise UTF-8
    encoded source files.
  - Steve stated that, since file names are not required to be representable in UTF-8, requiring strictly
    well-formed UTF-8 could have unanticipated consequences.
  - JeanHeyd asked in chat, "Does `\xFF` work in header-names as an escape?"
  - Corentin replied in chat, "unspecified".
  - Corentin explained his intent in requiring diagnosis of ill-formed UTF-8 input.
  - PBindels asked why it is useful to allow invalid UTF-8 in comments.
  - Corentin replied that Clang source code has comments explaining why invalid UTF-8 in comments is explicitly
    allowed and provided a link to the source code.
    - https://github.com/llvm/llvm-project/blob/main/clang/lib/Lex/Lexer.cpp#L3136-L3144
  - PBrett shared cases of copyright symbols appearing in otherwise ASCII files.
  - Tom noted that non-ASCII characters tend to appear in author, product, and company names in comments.
  - Hubert stated that source files that `iconv` will reject are undesirable.
  - **We wish to require implementations to have a mode in which they diagnose ill-formed UTF-8 source files (regardless of whether the ill-formedness is located in comments, header names or string literals).**
    - Attendance: 10

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   8 |   2 |   0 |   0 |   0 |

    - Consensus is strongly in favor.
    - SF: As it stands right now, people are already basically rolling the dice with their source files. This is
      strictly an improvement over the status quo, because now there is, at least, one entirely portable way to
      write source code.

  - Corentin asked about necessary wording to support both source files and non-files.
  - Hubert responded that (standard library) headers are not source files; source files are those things that
    are included by `#include` directives that do not name standard headers.
  - PBrett asked if the wording should be modified do discuss "input" as opposed to "files".
  - Hubert responded that such a change is not necessary.
  - Corentin pledged to bring back a revised paper.
- Tom stated the next telecon will be April 28th.


# March 24th, 2021

## Agenda:
- Continue discussion from the last telecon concerning:
  - [D2314R2: Character sets and encodings](https://wiki.edg.com/pub/Wg21telecons2021/SG16/d2314r2.html)
  - [D2297R1: Wording improvements for encodings and character sets](https://isocpp.org/files/papers/D2297R1.pdf)
- Discuss priorities and goals for C++23.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- [D2314R2](https://wiki.edg.com/pub/Wg21telecons2021/SG16/d2314r2.html) vs [D2297R1](https://isocpp.org/files/papers/D2297R1.pdf):
  - PBrett introduced the topic:
    - We are continuing discussion from the last telecon, but limiting discussion to new information.
    - Corentin posted
      [an email](https://lists.isocpp.org/sg16/2021/03/2182.php)
      that proposed a wording approach he hoped might bring consensus.
  - Corentin summarized the email.
  - Jens noted that the email proposed using "universal character set", but that term is not defined in
    ISO 10646, so a different term or a definition would be needed.
  - Jens added that a later reply suggested use of "Universal Coded Character Set" instead; that term is
    defined in ISO 10646 and appears to be isomorphic to the proposed "translation character set".
  - PBrett asked if there is consensus for this direction.
  - Corentin replied that there is an additional proposed change to replace use of "abstract character"
    with "element" in the definition of _universal-character-name_ (UCN).
  - Jens replied that he had already discontinued use of "abstract character" and that the members of
    the "translation character set" are denoted as "elements".
  - Tom asked for confirmation that the universal coded character set includes members corresponding to
    unassigned code points and was informed that it does.
  - Hubert noted that ISO 10646 uses "UCS" as an abbreviation for "Universal Coded Character Set".
  - Hubert reported an issue with the ISO 10646 specification of the UCS; it doesn't actually state
    what the UCS elements are.
  - Hubert added that the closest it comes to stating what those elements are is in "coded character".
  - \[ Editor's note: ISO 10646:2020 defines "coded character" in 3.8:
    
        coded character
        association between a character and a code point
    \]
  - Steve stated in chat: "code points seem to be elements of the UCS codespace. Coded characters would
    be elements of the UCS, but there aren't 'characters' that correspond to unassigned codepoints. IIUC."
  - Jens shared ISO 10646:2020, chapter 6, "General Structure of the UCS" and noted that the description
    includes a "canonical form" of the UCS that __uses__ the UCS codespace.
  - \[ Editor's note: ISO 10646:2020, chapter 6, "General Structure of the UCS" states:
    
        ...
        The canonical form of this coded character set – the way in which it is to be conceived – uses
        the UCS codespace which consists of the integers from 0 to 10FFFF.
        ...
    \]
  - PBrett observed that we don't seem to have consensus that the UCS can be used as Corentin proposed.
  - Hubert confirmed and stated that, if we went forward with this, CWG would likely have to change
    it; probably to what Jens has proposed.
  - Jens reiterated that, due to ISO rules, we are required to work with ISO 10646.
  - Corentin asked if Jens' latest draft still uses "character" in the definition of translation
    character set or if that had ben switched to "element".
  - Hubert confirmed that "character" is still used and shared the definition from the latest revision.
  - \[ Editor's note: that definition is:
    
        The translation character set consists of the following elements:
        - each character named by ISO/IEC 10646, as identified by its unique UCS scalar value, and
        - a distinct character for each UCS scalar value where no named character is assigned.
    \]
  - Jens stated that "character" had to be preserved for compatibility with existing wording that
    uses "character".
  - Hubert stated that we can't expect Jens to publish a paper that glosses over inconsistencies in
    the use of "character".
  - PBrett and Jens both agreed.
  - **Poll: Introduce the concept of a 'translation character set' which synthesizes characters for unassigned UCS scalar values.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   2 |   4 |   1 |   0 |   1 |

    - Consensus is in favor.
    - SA: The "translation character set" abstraction is unnecessary and the definition uses terminology
      incorrectly.
  - **Poll: Forward D2314R2 as presented on 2021-03-24 to EWG for inclusion in C++23.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   3 |   5 |   0 |   0 |   0 |

    - Consensus is in favor.
  - Jens stated that he will include poll results, note the objection, populate the revision section, and
    then submit the paper for the next mailing.
  - Corentin asked if a request for escalatation to quickly progress this paper could be made to the
    EWG chair since other papers will depend on it.
  - Tom replied that more motivation is needed to do so since no dependent papers have been forwarded from
    SG16 yet.
- Priorities and goals for C++23:
  - PBrett inroduced the topic:
    - A number of items were shared in the
      [agenda reminder email](https://lists.isocpp.org/sg16/2021/03/2200.php)
      that are candidates for prioritization for C++23.
    - We'll briefly review each; those that are nominated as a target for C++23 and for which a champion
      is identified will be added to the prioritization poll.
  - PBindels asked if we have a discrete vision for C++23.
  - Tom replied that that question is part of the motivation for this exercise.
  - [P1628: Unicode character properties](https://wg21.link/p1628):
    - Corentin stated that he does not plan to progress this paper for C++23.
    - Not nominated.
  - [P1629: Standard Text Encoding](https://wg21.link/p1629):
    - JeanHeyd stated that the scope could be reduced for C++23.
    - Steve reported good experience experimenting with the reference implementation and nominated it as
      a strong candidate for C++23.
    - Steve added that he would want to have the support for ranges included.
    - JeanHeyd replied that range support would probably be pursued via a different paper in order
      to avoid impeding progress on the core components.
    - Corentin stated that this paper would be ambitious for C++23.
    - Nominated; champion is JeanHeyd.
  - [P1729: Text Parsing](https://wg21.link/p1729):
    - Tom stated that he does not know Victor's plans for this paper.
    - Corentin opined that this paper isn't really an SG16 concern until encodings are involved.
    - PBrett responded that text processing in general is in the scope of SG16.
    - Not nominated; Victor was not present.
  - [P1854: Source to Execution encoding conversion should not lead to loss of information](https://wg21.link/p1854):
    - Corentin reported a request to include the wide literal encoding in the paper.
    - Corentin added that we voted to make this contingent on [P1855](https://wg21.link/p1855), but that
      paper is still making its way through LEWG.
    - Tom stated that we don't have to wait on
      [P1855](https://wg21.link/p1855)
      to be accepted to make progress on this.
    - Nominated; champion is Corentin.
  - [P1859: Standard terminology for execution character set encodings](https://wg21.link/p1859):
    - Steve stated that this paper has been mostly subsumed by other work.
    - PBrett asked if we should continue tracking this paper.
    - Steve replied that we should; at least until things in flight land.
    - Jens asked that the paper be reviewed to determine when/if it can be closed.
    - Not nominated.
  - [P1953: Unicode Identifiers And Reflection](https://wg21.link/p1953):
    - Corentin stated that priority of this paper depends on what SG7 does for C++23.
    - Not nominated.
  - [P2071: Named universal character escapes](https://wg21.link/p2071):
    - Jens noted that a paper revision is needed.
    - Tom acknowledged and reported plans to complete a revision soon.
    - Not nominated since this paper has already been forwarded out of SG16.
  - [P2295: Correct UTF-8 handling during phase 1 of translation](https://wg21.link/p2295):
    - Corentin nominated.
    - Nominated; champion is Corentin.
  - [Requiring wchar_t to represent all members of the execution wide character set does not match existing practice](https://github.com/sg16-unicode/sg16/issues/9):
    - Hubert noted that this will require corresponding changes for WG14.
    - JeanHeyd stated that other work he is doing in WG14 will help with this.
    - Nominated; champions are Tom and Corentin.
  - [std::to_chars/std::from_chars overloads for char8_t](https://github.com/sg16-unicode/sg16/issues/38):
    - Tom reported that this issue was raised from someone outside the committee.
    - Corentin stated that the concept of a number is complicated in Unicode.
    - PBindels noted that there are many different numbering systems.
    - PBrett suggested that the scope of `from_chars()` should be restricted to only parsing text that
      could be produced by `to_chars()`.
    - Jens stated that he had not considered other numbering systems, but had considered exposing the
      same functionality as for `char` for `char8_t` and UTF-8; this would suffice to provide portable
      ASCII support.
    - Nominated; champion is Peter Bindels.
  - [Publish an SG16 library design guidelines paper](https://github.com/sg16-unicode/sg16/issues/53):
    - PBrett suggested removing this from the candidate list since it doesn't target the standard.
    - Not nominated.
  - [Deprecate std::regex](https://github.com/sg16-unicode/sg16/issues/57):
    - PBrett noted that some NBs may object to such deprecation.
    - Nominated; champions are Peter Bindels and Peter Brett.
  - [Make wide multicharacter character literals ill-formed](https://github.com/sg16-unicode/sg16/issues/65):
    - Nominated; champion is Peter Brett.
  - [Improve portable ingestion of command-line arguments](https://github.com/sg16-unicode/sg16/issues/66):
    - JeanHeyd recalled discussion of
      [P1275](https://wg21.link/p1275)
      in San Diego.
    - Tom asked if anyone knew if Isabella is planning a revision.
    - JeanHeyd replied that further work is semi-dependent on his own transcoding work.
    - Tom noted that an alternate design sketch is present in the issue comments.
    - PBindels suggested a C++26 target due to lack of underlying existing functionality.
    - Not nominated.
  - [Alias barriers; a replacement for the ICU hack](https://github.com/sg16-unicode/sg16/issues/67):
    - Tom volunteered and summarized recent off-list discussion;
      [P0593](https://wg21.link/p0593) describes a `start_lifetime_as()` function that looks suitable
      for this, but it wasn't formally proposed.
    - Nominated; champions are Tom and Mark.
  - [Support for UTF encodings in std::format() and std::print()](https://github.com/sg16-unicode/sg16/issues/68):
    - PBrett proposed only addressing the easy cases; the ones that don't require implicit transcoding.
    - Corentin agreed and noted that Victor recently indicated intention to write such a paper.
    - Nominated; champions are Victor and Peter Brett.
  - [Specify what constitutes white-space characters](https://github.com/sg16-unicode/sg16/issues/69):
    - Tom stated that [P2295](https://wg21.link/p2295) intends to address this.
    - Corentin reported that he removed that section of the paper in a yet-to-be published revision
      to ensure it wouldn't delay progress on the core portion of the paper.
    - PBindels offered a comparison with [P1949](https://wg21.link/p1949) and noted this shouldn't be
      a difficult paper, though it may not be very important.
    - Hubert stated that there may be consensus issues with this since deferring to a Unicode definition
      of white-space character would introduce a lexing dependency on Unicode version.
    - Steve opined that this isn't terribly important until we have portable Unicode encoded source files.
    - Steve stated that it might help to clean up the specification though;
      [P1949](https://wg21.link/p1949) may have helped by stabilizing identifiers.
    - Corentin offered to send a message to the SG16 mailing list arguing for why this shouldn't be a
      priority.
    - \[ Editor's note: Corentin did follow up with
      [an email](https://lists.isocpp.org/sg16/2021/03/2207.php).
      \]
    - Not nominated.
  - [Specify what constitutes a new-line](https://github.com/sg16-unicode/sg16/issues/70):
    - Not nominated for the same reasons as the previous item.
  - [A portable mechanism to specify source file encoding](https://github.com/sg16-unicode/sg16/issues/71):
    - Tom expressed intent to work on this.
    - Jens asked that Tom prioritize [P2071](https://wg21.link/p2071) first.
    - Tom agreed to do so.
    - Corentin opined that this need not be a priority.
    - Nominated; champion is Tom.
  - Clarify the relationship between the literal and execution encodings:
    - Corentin proposed this additional candidate.
    - \[ Editor's note: An SG16 issue was
      [filed](https://github.com/sg16-unicode/sg16/issues/72)
      to track this addition. \]
    - Nominated; champions are Corentin and Jens.
  - PBrett summarized the polling method Tom described in the agenda email.
  - Tom suggested a simpler polling method; that everyone raise their hand for items that they felt most
    feasible and desirable for C++23.
  - \[ Editor's note: the poll results shown below have been reordered such that those that received the
    most votes are listed first. \]
  - **Poll: C++23 priorities.**
    - Attendance: 9

        | Votes | Candidate |
        | ----: | :-------- |
        |     6 | [P1854: Source to Execution encoding conversion should not lead to loss of information](https://wg21.link/p1854) |
        |     6 | [P2295: Correct UTF-8 handling during phase 1 of translation](https://wg21.link/p2295) |
        |     6 | [std::to_chars/std::from_chars overloads for char8_t](https://github.com/sg16-unicode/sg16/issues/38) |
        |     6 | [Make wide multicharacter character literals ill-formed](https://github.com/sg16-unicode/sg16/issues/65) |
        |     5 | [P1629: Standard Text Encoding](https://wg21.link/p1629) |
        |     5 | [Requiring wchar_t to represent all members of the execution wide character set does not match existing practice](https://github.com/sg16-unicode/sg16/issues/9) |
        |     5 | [Support for UTF encodings in std::format() and std::print()](https://github.com/sg16-unicode/sg16/issues/68) |
        |     4 | [Deprecate std::regex](https://github.com/sg16-unicode/sg16/issues/57) |
        |     4 | [Alias barriers; a replacement for the ICU hack](https://github.com/sg16-unicode/sg16/issues/67) |
        |     4 | [A portable mechanism to specify source file encoding](https://github.com/sg16-unicode/sg16/issues/71) |
        |     4 | [Clarify the relationship between the literal and execution encodings](https://github.com/sg16-unicode/sg16/issues/72) |
- Tom announced that the next telecon will be April 14th and the agenda will include
  [P2295: Correct UTF-8 handling during phase 1 of translation](https://wg21.link/p2295).
- Tom reminded participants from Europe of the pending switch to summer time and that the next telecon
  will be held an hour later than this one.


# March 10th, 2021

## Agenda:
- Continue discussion from the last telecon with updated draft paper revisions:
  - [D2314R1: Character sets and encodings](https://wiki.edg.com/pub/Wg21virtual2021-02/SG16/d2314r1.html)
  - [D2297R1: Wording improvements for encodings and character sets](https://isocpp.org/files/papers/D2297R1.pdf)

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- [D2314R1](https://wiki.edg.com/pub/Wg21virtual2021-02/SG16/d2314r1.html) vs [D2297R1](https://isocpp.org/files/papers/D2297R1.pdf):
  - Peter provided an introduction.
  - Corentin initiated discussion:
    - The primary disagreement concerns the introduction of "translation character set" instead of using Unicode
      terminology directly.
    - The proposed wording uses "abstract character" in a way that is explicitly prohibited by the Unicode standard.
    - \[ Editor's note: ISO 10646 does not define "abstract character"; it is only defined by the Unicode standard. \]
    - \[ Editor's note: Unicode 13, chapter 3.2, "Conformance Requirements", conformance clause C2 states:
      
          C2 A process shall not interpret a noncharacter code point as an abstract character.
          -  The noncharacter code points may be used internally, such as for sentinel values or delimiters, but
             should not be exchanged publicly.
      \]
    - \[ Editor's note: Later revisions of
      [D2314R1](https://wiki.edg.com/pub/Wg21virtual2021-02/SG16/d2314r1.html)
      replaced "abstract character" with "character" in the proposed wording. \]
    - We should prefer well known terminology and, in this case, not divert from the Unicode standard.
    - We should avoid using ambiguous terminology like "character".
    - The technically correct term is UCS scalar value.
    - The distinction between a character and a scalar value is not relevant for a lexer; lexing can be described
      using either form.
    - Thinking of lexing in terms of code units or scalar values may feel unintuitive, but that reflects how
      implementations actually work.
  - Hubert stated that his impression of Jens' intent in using character terminology is that source code is considered
    text.
  - Hubert continued; we tend to think of text as a sequence of characters, so it is not clear if a sequence of UCS
    scalar values constitutes text.
  - PBrett noted prior discussions that questioned whether C++ source code constitutes text since preservation of
    unassigned UCS scalar values, which do not correspond to characters, is required.
  - PBrett stated that the desired model is one that describes translation in terms of UCS scalar values.
  - Corentin agreed with Pter.
  - Steve also agreed with Peter and added that even a pedantic reading of lexing in the C++ standard should not depend
    on Unicode version.
  - Jens agreed with regard to avoiding dependence on Unicode version with the exception of recognizing
    identifiers since that requires
    [UAX #31](https://unicode.org/reports/tr31);
    translation must not otherwise be affected by Unicode version.
  - Jens disagreed that it is otherwise beneficial to expose UCS scalar values more widely in the standard.
  - Jens acknowledged the perspective that, due to the possibility of unassigned scalar values, C++ source may not be
    text, but opined that such cases will largely be introduced by _universal-character-name_s (UCNs).
  - Jens added that concerns regarding unassigned scalar values can be addressed in a foot note.
  - PBrett asked if there is a technical concern that motivates introducing "translation character set".
  - Jens replied that he did not think there is a technical requirement and acknowledged that translation could be
    described in the standard using UCS scalar values.
  - PBrett asked if Jens considers _universal-character-name_ an unattractive term and, if not, why UCS scalar
    value should be disfavored.
  - Jens replied that UCNs are used for a limited purpose and do not appear frequently in the standard; use of
    UCS scalar value for translation would require many more uses of that term..
  - Jens added that UCS scalar values denote an integer value and that is inconsistent with how lexing is described
    elsewhere.
  - Jens noted an example; proliferation of UCS scalar value leads to specifying "reinterpret_cast" as a sequence
    of numberic values.
  - Jens concluded that this debate concerns a presentation issue in the C++ standard.
  - Tom noted that it is not possible to distinguish between assigned and unassigned UCS scalar values without
    consulting a specific version of the Unicode standard.
  - Tom added that there are cases where a single abstract character is mapped to more than one UCS scalar value
    but where the standard must define behavior based on the UCS scalar value, not the character.
  - \[ Editor's note: Examples include compatibility characters such as
    the angstrom character (Å, mapped to U+00C5 and U+212B) and
    the ohm character (Ω, mapped to U+03A9 and U+2126). \]
  - Corentin summarized some of the concerns; Tom and Jens are concerned about describing translation in terms of
    UCS scalar values because those denote an integer.
  - Zach expressed uncertainty with regard to how use of UCS scalar value leads to having to describe lexing in
    terms of integers; implementations always represent characters using numbers.
  - Tom replied that source code read from a napkin or a blackboard doesn't go through a numeric translation; we
    think about lexing in terms of characters, not numbers.
  - Hubert stated that the goal is to require a mapping for translation without having to explicitly specify it.
  - Hubert added that there is less friction if UCS scalar values are used; that means that improving presentation
    in the standard should be the goal.
  - Zach asked to clarify how presentation would be confusing.
  - Hubert replied that translation is described assuming textual representation in the standard.
  - Zach asked if that could be addressed in some front matter text.
  - Hubert replied that he thinks it could be.
  - Corentin asked Jens if Hubert's suggestion would alleviate his concerns.
  - Hubert stated that, in terms of front matter, context matters; what would be needed is to state that the glyphs
    used in the specification are a proxy for UCS scalar values.
  - Zach suggested including such a statement with the description of the basic character set.
  - Jens replied that the basic character set concerns character sets rather than tokens and lexing.
  - Jens suggested that [[lex.pptoken]p2](http://eel.is/c++draft/lex.pptoken#2) may be a more appropriate location.
  - Jens acknowledged that there should be a blanket statement somewhere noting how the glyphs used in the standard
    are to be interpreted.
  - Tom returned discussion to Corentin's question regarding whether Hubert's suggestion would alleviate his concerns.
  - Jens replied that he finds it to be a useful clarification, but that he continues to believe that general readers
    are better served by use of an abstraction.
  - Jens added that use of UCS scalar value raises the question of assigned vs unassigned characters where we don't
    want to make a distinction and just state that some character is denoted here.
  - Jens again acknowledged that this is purely a presentation concern, not a semantic one.
  - Corentin stated that use of UCS scalar value may cause confusion for readers not familiar with the term, but
    noted that is exactly why character is not a good term; people have different ideas of what a character is, so
    use of UCS scalar value will force such readers to look up the definition in order to understand the intent.
  - PBrett noted that he knows of colleagues that think of code point as a character.
  - Hubert stated that his impression of Jens' perspective is that we don't want people paying attention to
    something that might be distracting if we can gloss over it.
  - Hubert expressed support for Corentin's perspective, implementors can't afford to gloss over such specification
    and must deep dive to determine intended behavior; UCS scalar value may be simpler.
  - Jens replied that he defined translation character set as precisely as he could.
  - Jens provided [[lex.pptoken]p2](http://eel.is/c++draft/lex.pptoken#2) as an example where there is mention of
    white-space characters that would require replacement written in terms of UCS scalar values, but where we do
    not have a specification.
  - Jens noted that he has been replacing use of colloquial names of characters with ISO 10646 U+XXXX short names.
  - PBrett suggested this paragraph requires an update regardless then.
  - Jens agreed and added that a definition of white-space should precede it.
  - Jens provided [[lex.pptoken]p3](http://eel.is/c++draft/lex.pptoken#3), as an additional example where there
    are many uses of "character".
  - PBrett asked to clarify that the concern is the many pre-exising uses of "character" in these clauses.
  - Jens replied that migrating away from "character" in this section would damage presentation.
  - Jens added that it feels like a category error to say, "if the next three UCS scalar values are ..."
  - Zach asked if colloquial terms could continue to be used with the previously suggested front matter.
  - Jens replied that doing so is ok normatively, but still feels like a category error.
  - Zach noted that in mathematical descriptions, an alternate notation is sometimes used because it is thought
    to be more convenient.
  - Zach noted that the proposed wording doesn't replace newline.
  - Jens replied that newline is special since it does not necessarily denote `\n`, it could be `\r\n`.
  - Tom added that it could also represent the end of a record in a z/OS data set.
  - Corentin suggested that the pre-existing concerns regarding newlines not be addressed in this paper.
  - Jens agreed and stated that he did not intend to address those.
  - Zach expressed a preference for retaining glyphs rather than swapping them out for U+XXXX short names and
    noted that "U+005C REVERSE SOLIDUS" is unambiguously less clear than "backslash `\`".
  - Tom suggested that both could be presented; "U+005C REVERSE SOLIDUS (\)".
  - Corentin agreed that "REVERSE SOLIDUS" is not a great name, but that including the U+XXXX short name removes
    ambiguity.
  - Steve expressed sympathy for Zach's point; people don't read this part of the standard because they think
    they know what it means and then end up surprised; you have to know what it means before you can understand
    the wording.
  - Steve agreed that, in terms of presentation, and as is seen in other standards, the redundancy of glyph,
    the U+XXXX short name, and the full name is helpful; if the glyph is known, the names can be skipped and if
    the glyph is unknown or ambiguous, then the names unambiguously identify the character.
  - Tom noted that we've discussed this question for an hour and suggested we poll it and then proceed to
    another topic.
  - Mark asked Jens if his concerns have been addressed.
  - Jens replied that he is still concerned about presentation.
  - Tom wondered if we might get inspiration from other language standards that describe lexing in Unicode terms.
  - PBrett responded that they all describe it in terms of characters, but that they are able to define character
    in a reasonable way.
  - Zach suggested adding a definition of "character".
  - Jens indicated no intention of renaming "character literal" and noted that, outside of lexing, translation
    is only concerned with tokens.
  - Zach asked what the ramifications would be if core language used "character" differently than library.
  - Jens opined that defining "character" and then not using it consistently would be worse than the status
    quo.
  - Hubert stated that defining "character" to suit this specific purpose is not a good idea and that it would
    be a drafting violation to use an inconsistent definition.
  - Steve observed that use of "character" in the library is equally as bad as in the core language.
  - **Poll: Introduce the concept of a 'translation character set' which synthesizes characters for unassigned UCS scalar values.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   1 |   4 |   0 |   2 |   2 |

    - No consensus.
  - Corentin asked for clarification regarding the desire for "translation character set"; specifically as to whether
    the term is useful or because UCS scalar value is an unattractive term.
  - Mark replied that "translation character set" allows existing implementations to remain conforming.
  - Hubert responded that both approaches have no impact on conformance and that this concerns a presentation issue.
  - Corentin agreed with Hubert.
  - Tom attempted to clarify Mark's point, that the abstraction acknowledges the possibility of multiple implementation
    techniques.
  - Tom expressed appreciation for that level of abstraction.
  - Hubert stated that whether implementations operate on scalar values or an "in-band transport" is observable;
    the C99 rationale was flawed.
  - Hubert added that it took us a long time to recognize the C99 model A limitations.
  - Tom asked what might lead people to change their vote.
  - PBrett replied that the sticking point for him is the materialization of characters.
  - Jens asked if that concern is more about the name "translation character set", or the use of "character" in the
    definition.
  - Jens asked if substituting "element" or another abstract term for "character" would help.
  - PBrett asked for an example of another character set that doesn't contain characters.
  - Jens replied that most character sets contain something like bell that isn't really a character.
  - Corentin opined that "element" would be an improvement, but since the elements would be equivalent to UCS scalar
    values, makes "translation character set" an unnecessary abstraction.
  - Tom asked if there is a way to avoid UCS scalar values that represent unassigned character from coming into play.
  - Corentin replied that he didn't think that was necessary; the mechanism described in Jens' paper is correct.
  - Hubert observed that discussion so far has been concentrated on objections to the proposed abstraction and asked
    what might help improve the case for UCS scalar values.
  - PBrett stated that he would prefer to have this paper with the proposed wording, than to not have it at all.
  - Jens suggested a poll to forward the paper with direction that core resolve the wording concerns and noted that,
    between himself and Hubert, they would be able to represent both sides of the issue.
  - Tom expressed support for that idea.
  - Mark agreed and noted that it may just be necessary for more people to weigh in on the matter.
  - Corentin stated that it seems kind of unfair to put that burden on core.
  - Tom asked if Corentin would be willing to research what additional wording changes would be necessary for Jens'
    paper to switch to use of UCS scalar values.
  - Corentin agreed to look into it.
  - \[ Editor's note: Corentin posted
    [suggested changes to the SG16 mailing list](https://lists.isocpp.org/sg16/2021/03/2182.php). \]
- Tom announced that the next telecon will be help March 24th.
- Tom noted that, due to daylight savings time changes, the next telecon will start an hour later for those in
  North America timezones.


# February 24th, 2021

## Agenda:
- [P2314R0: Character sets and encodings](https://wg21.link/p2314r0)
- [P2297R0: Wording improvements for encodings and character sets](https://wg21.link/p2297r0)

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Tom provided an introduction.
  - [P2314R0](https://wg21.link/p2314r0) and [P2297R0](https://wg21.link/p2297r0) overlap and compete
    in several ways.
  - The authors have been communicating with each other offline to ensure that their respective positions
    and the differences between the papers are understood.
  - Since the scope of [P2314R0](https://wg21.link/p2314r0) is smaller than
    [P2297R0](https://wg21.link/p2297r0), Jens will present first, we'll keep discussion to clarifying
    questions, then Corentin will present, then we'll open the floor to general discussion.
- [P2314R0: Character sets and encodings](https://wg21.link/p2314r0):
  - Jens presented.
    - C++ support for source code with characters outside the basic source character set uses model A
      from the "UCN models" subsection of section 5.2.1 in the
      [C99 rationale document](http://www.open-std.org/jtc1/sc22/wg14/www/docs/C99RationaleV5.10.pdf).
    - In model A, characters not in the basic source character set are implicitly converted to
      _universal-character-names_ (UCNs).
    - The (revised) paper proposes switching to a modified model C in which characters are converted
      to an internal encoding that is able to represent all supported characters as well as UCNs.
    - The model A approach is not reflective of how compilers work in practice.
    - The ISO requires that, when an ISO standard exists and suffices for a particular purpose, that
      it be used.  As a result, the proposed wording references ISO 10646 rather than the Unicode standard.
    - The terminology used in ISO 10646 differs from the terminology in the Unicode standard.
    - The C++ standard does not contain a normative reference to the Unicode standard today.
    - The standard conflates character sets and character encodings and this makes defining multibyte
      encodings problematic.
    - The wording is intended to separate the ideas of character sets vs character encoding.
    - Character sets are not mentioned except where normatively needed; their existence can be otherwise
      inferred from encodings.
    - The wording introduces a new _literal encoding_ term.
    - The literal encoding may not be compatible with the locale dependent execution encoding; this is
      consistent with the status quo.
    - An earlier revision of the paper removed _execution character set_ in proposed wording, but the
      term was revived for C compatibility.
    - Not all string literals denote the same thing; some denote an object, but others are used only at
      translation time.  For example, header names, `extern "C"`, and `_Pragma` directives.
    - Terminology changes:
      - _Basic source character set_ is renamed to _basic character set_.
      - _Basic literal character set_ describes aditional characters that are required to be representable
        in all literal encodings.
      - _Ordinary literal encoding_ specifies the encoding used to encode ordinary string literal objects.
      - _Wide literal encoding_ specifies the encoding used to encode wide string literal objects.
      - _Translation character set_ specifies the set of abstract characters corresponding to all possible
        characters encountered during translation; these map to UCS scalar values.
      - _Extended character set_ is removed.
    - The wording avoids the notion of a character being dependent on what Unicode version is used.
    - There are no intended behavioral changes other than one case involving stringizing extended
      characters; in that case, the standard currently specifies that a UCN is stringized, but that
      doesn't match existing behavior.
    - During translation phase 1, source characters are mapped to the translation character set.
    - In translation phase 3, UCNs outside of a header name or literal are converted to the translation
      character set.
    - There are a few questions regarding header names.
      - Implementations appear to replace UCNs in header names.
      - Extended characters don't work portably in header names.
    - Translation phases 5 and 6 could be collapsed, but are preserved to avoid renumbering translation
      phase 7.
    - The _translation character set_ members include both named characters and abstract characters for
      unassigned UCS scalar values.
    - The _basic character set_ is defined in terms of UCS scalar values and names.
    - The _basic literal character set_ consists of the _basic character set_ plus characters for
      alert, backspace, carriage return, and null.
    - Questions remain regarding the relationship between the literal encodings and the locale dependent
      execution encodings.
    - The C standard wording appears to require that characters used in a character or string literal
      must correspond to their encoding in the locale dependent execution encoding.
  - PBrett asked if the standard would be more clear if it referred to the Unicode standard instead of
    ISO 10646.
  - Hubert replied that the editorial standards that the ISO imposes is salient for use in C++ and that
    the Unicode method of terminology doesn't meet those standards.
  - Jens added that when we reviewed Unicode terminology a while back, we didn't find the Unicode terms
    very palatable.
  - Jens noted that references to the Unicode standards will be required at some point to satisfy
    dependencies that are not present in ISO standards.
  - PBrett observed that we don't have a guarantee that requirements don't change with new Unicode
    standards because of our planned dependence on [UAX #31](https://unicode.org/reports/tr31).
  - Jens agreed.
  - PBrett commented that the noted behavioral change regarding stringizing a UCN appears to be a bug
    fix and standardizes existing behavior.
  - Hubert expressed concern that the new wording for _basic literal character set_ may strengthen
    requirements to prohibit the same code unit value from meaning different things when it appears as
    a lead byte vs a trail byte.
  - PBrett stated that the core language is not dependent on locale, so discussion of execution character
    sets should be moved to library wording.
- [P2297R0: Wording improvements for encodings and character sets](https://wg21.link/p2297r0):
  - Corentin presented:
    - Corentin's presentation slides are available
      [here](https://docs.google.com/presentation/d/1PlCX8-0DbBXIr4OJU2jlec0Bwmd662udPP1tuENuTlI).
    - Jens' paper is good, but there are some areas of disagreement.
    - We agree on removing implicit production of UCNs in translation phase 1.
    - We should strive to better use terminology compatibile with Unicode.
    - It isn't clear that we all have the same mental model of translation.
    - There is disagreement with regard to Jens' _translation character set_ and that translation is not
      expressed using Unicode terminology.
    - Translation can be defined in terms of UCS scalar values; characters are not necessary.
    - An abstract translation character set solves a problem that doesn't exist if the right terminology is used.
    - The output of translation phase 1 should be a sequence of UCS scalar values.
    - UCS scalar value may not a great term; we can use an alias, but it should not denote a character or
      abstract character.
    - We agree on renaming _basic source character set_ to _basic character set_.
    - We disagree on the need for _basic literal character set_; we should pursue other means of handling
      the special requirements for alert, backspace, carriage return, and null.
    - The relationship between the literal encodings and locale dependent execution encodings have
      interesting ramifications:
      - `isalpha('a') // Can this ever return false?`
      - `isalpha('é') // Can this ever return false?`
    - It is ok to retain the status quo, but execution encoding concerns should be moved to library wording.
    - Raw string literal delimiters are restricted to the basic character set; perhaps that should be changed.
  - Hubert stated that EBCDIC code pages can't meet a requirement that all members of the basic character
    set are encoded the same in all supported locale encodings.
  - Jens noted the implication that we cannot even rely on a correspondence between the literal encoding and
    the execution encoding even for members of the basic character set.
  - Hubert stated that reducing the restrictions for raw literal delimiters would complicate tokenization.
  - Jens expressed a desire to poll a preference for abstract characters vs UCS scalar values.
  - Mark stated that header names effectively need to specify a sequence of bytes and it isn't clear that
    these should be called characters.
  - Steve noted that there is plenty of implementation-defined behavior involved in processing header names.
  - Jens stated that, with the current phrasing, a lone surrogate code point cannot be represented in a
    program since they are rejected as UCNs; but an implementation could allow that as an extension.
  - Jens opined that we should allow extended characters in header names.
  - Corentin noted that the status quo is maintained by both papers.
- Tom stated that the next telecon will be on March 10th and will continue this discussion.


# February 10th, 2021

## Agenda:
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm)
  - Continue discussion started at the last telecon and in
    [recent email discussion](https://lists.isocpp.org/sg16/2021/01/2049.php).
- [P2093R3: Formatted output](https://wg21.link/p2093r3)
  - Review Victor's updates since our
    [review of P2093R2 on 2020-12-09](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md#december-9th-2020).

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm):
  - JeanHeyd stated that he has not yet completed the benchmarks requested in the email discussion.
  - JeanHeyd shared code and demonstrated three possible signatures for the conversion functions:
    1) The form proposed in the paper.
       - `mcerr_t(const charX** ibegin, size_t* isize, charY** obegin, size_t* osize)`
       - Con: Each call requires writes to `*ibegin`, `*isize`, `*obegin`, and `*osize`.
    2) Iterator pairs passed by reference.
       - `mcerr_t(const charX** ibegin, const charX** iend, charY** obegin, charY** oend)`
       - Pro: Each call only requires writes to `*ibegin` and `*obegin`.
    3) Iterator pairs, begin passed by reference, end passed by value.
       - `mcerr_t(const charX** ibegin, const charX* iend, charY** obegin, charY* oend)`
       - Pro: Each call only requires writes to `*ibegin` and `*obegin`.
       - Con: No support for unbounded reads and writes.
  - Zach asked if, for #3, both `ibegin` and `iend` are required to be non-null.
  - JeanHeyd replied that they are.
  - Zach stated that, if null is passed for `oend`, that should allow unbounded writes, and if null is passed
    for `obegin`, that should allow counting code units.
  - JeanHeyd acknowledged and added that passing null for both would support counting and validation.
  - Tom noted the assumption that the count is returned via the return value in that case.
  - JeanHeyd agreed and noted that would require special error return values ike `(size_t)-3`.
  - PBrett asked if named constants would be provided for such error values.
  - JeanHeyd replied yes and that they already exist.
  - Jens requested that the paper clearly illustrate the three modes of operation (counting, validation,
    and conversion) and provide examples of each.
  - Jens noted that `iconv` does not support unbounded buffers.
  - Jens added that support for unbounded buffers would be novel and carries significant risk.
  - Jens observed that the arguments in the signatures presented differ from what is proposed in the paper.
  - JeanHeyd acknowledged and noted there is a lack of consistency in existing interfaces.
  - Jens suggested letting WG14 choose the argument order.
  - Tom noted that returning `size_t` with special error values makes for verbose call sites since
    there is no simple way to test for an error.
  - JeanHeyd agreed and noted that the proposed signature was designed to avoid that issue.
  - JeanHeyd added that a caller could check to see if all input was consumed to determine if an error
  - occurred.
  - Tom noted that these signatures don't include an `mbstate_t` parameter and therefore cannot support
    processing text one byte at a time as might be required to advance through buffer boundaries; for
    the `mbstate_t` taking variants, all bytes could be consumed without ensuring that an error condition
    is not present.
  - Tom suggested that optional parameters could be used to return counts of processed code units.
  - Corentin expressed a preference for the design in the paper for usability reasons and noted a dislike
    for using a return value to indicate both errors and counts.
  - Corentin stated that performance concerns should be subject to benchmarks indicating a problem, and
    that he is reluctant to compromise usability for small gains.
  - JeanHeyd noted that the design in the paper avoids using the return value for multiple purposes.
  - Zach wondered if the challenge with this interface is trying to do too many things and violating the
  - single purpose guideline; perhaps it would be worth having separate interfaces for validation and
    counting.
  - Zach added that examples of real world code would help to guide the design.
  - Zach asked if the interface offered a mechanism to request replacement characters for ill-formed input.
  - JeanHeyd replied that there are multiple possibilities for handling errors, but that WG14 felt the best
    approach is to leave error handling policy to the programmer.
  - JeanHeyd added that these interfaces are intended to be basic low level functionality and that more
    complex functionality can be added at a higher level.
  - Zach acknowledged that simplified wrappers could provide higher level error handling.
  - Jens asserted that interface choice should be based on informed performance behaviors and acknowledged
    that a complicated return value is undesirable.
  - Jens added that many C interfaces feel awkward from a C++ perspective due to the use of pointers and
    the need for manual error checking, and suggested that the focus be on getting the interface working
    and functional; ergonomics can be secondary.
  - Jens requested that the paper reflect opinions regarding separate validation and counting functions.
  - JeanHeyd stated that he would update the paper and bring back a revision for further review.
  - Corentin asked JeanHeyd what additional feedback he would like, what feedback WG14 might appreciate,
    and whether we should expect WG14 to consider our feedback.
  - JeanHeyd replied that WG14 will take WG21 feedback seriously.
  - JeanHeyd stated that the feedback provided so far has been useful; examples of usage will be a good
    addition to the paper.
  - JeanHeyd added that he'll take any questions or advice that he can't answer himself to WG14.
  - JeanHeyd noted that WG14 is open to adding potentially many functions, so separate interfaces could be
    a possibility.
  - Corentin expressed confidence that whatever interface is decided on will likely be reasonably usable
    and useful for C++, but that a dependency on WG14 is not required since WG21 can specify its own
    interfaces.
  - JeanHeyd agreed and noted that part of his intent in working with WG14 is to ensure that WG21
    implementors have the tools they need to implement future WG21 libraries.
  - Tom asked if the intent is that these interfaces be efficiently implementable using existing interfaces
    like `iconv` and `MultiByteToWideChar`.
  - JeanHeyd replied, yes.
  - Tom noted that optimizing these interfaces to work with little or no overhead over those interfaces
    should be a goal.
  - JeanHeyd agreed.
  - Tom asked how to seek to the next valid lead code unit when an error is encountered.
  - JeanHeyd replied that the simplest solution is to increment the input by one byte and to try again.
  - Tom observed that doing so would result in many error actions taken for a contiguous sequence of
    ill-formed code units, e.g., issuing many replacement characters; that conforms with Unicode, but
    Unicode guidance is to substitute a single replacement character for such sequences.
  - JeanHeyd replied that the caller could track consecutive errors and wait to apply an error policy until
    the ill-formed sequence has been fully consumed.
  - Tom agreed that would work and noted that we don't need to optimize for the error case.
- [P2093R3: Formatted output](https://wg21.link/p2093r3):
  - Victor presented:
    - Victor's presentation slides are avilable
      [here](presentations/2021-02-10-p2093r3-presentation.key).
    - Feedback provided during the last SG16 review was incorporated:
      - Additional motivation for `stdout` as the default output stream was added.
      - Appendix A was added with a comparison of behavior in other languages.
      - Other fixes and minor changes.
    - Six languages have been evaluated on Linux, macOS, and Windows.
      - The interesting case is Windows due to its use of a console encoding distinct from the system
        encoding.
      - Go, JavaScript, Python, and Rust were all able to produce correctly rendered output to the
        Windows console; C and Java did not.
      - When output was redirected to a file, Java and Python both tried to transcode to Windows-1251.
        - Java substituted replacement characters for unrepresentable characters.
        - Python threw an exception when attempting to convert unrepresentable characters.
    - The paper proposes following the behavior exhibited by C, Go, JavaScript, and Rust.
    - The only difference compared to `printf()` is special handling when writing to the console on Windows.
  - PBrett noted that, for Java, JavaScript, Python, and Rust, the internal encoding is always Unicode, but
    that is not the case for C and C++; this may indicate different behavior is warranted.
  - Victor agreed that there is a difference, but the proposal is to only special case writing to the
    Windows console when the execution encoding is UTF-8.
  - Corentin commented that, when writing to the console, the output is necessarily text, but when writing
    to a file, the output could be binary.
  - Jens noted how JeanHeyd's transcoding facilities could be used here; we can transcode so long as a
    target encoding is known.
  - Jens reiterated his desire for lower level functionality to be exposed such that general programmers
    would be able to implement similar functionality.  For example:
    - A facility to determine if output will be directed to a console; Tom showed how that can be done on
      several platforms and it is common for such customization to be done on POSIX systems for paging and
      color highlighting purposes.
    - Facilities to enable transcoding.  [P1885](https://wg21.link/p1885) enables identifying the execution
      character set; the remaining missing functionality is how to write directly to the console on Windows.
  - PBrett noted that we've discussed the desire to expose the low level functionality before.
  - Jens indicated that he is strongly opposed to forwarding this paper on without those independent lower
    level facilities.
  - Victor responded that he is willing to propose those lower level interfaces, but would prefer to focus
    on the text issues within SG16; the other facilities can be LEWG concerns.
  - Tom stated that functionality to write directly to a console is arguably an SG16 concern; though also
    arguably an SG13 concern.
  - Jens expressed concern about writing to the console being library black magic; he would like to be able
    to perform such writes without having to use formatting facilities, if desired.
  - Steve suggested that use of the Windows console is becoming more rare; software developers are probably
    the biggest users of it.
  - Steve asserted that the don't pay for what you aren't using principle applies; transcoding overhead may
    be undesirable, especially if it corrupts output.
  - Victor agreed and stated that he doesn't want to break anything; he just wants to do what `printf()`
    does with the one exception of writing directly to the Windows console in order to avoid Windows' builtin
    mojibake.
  - Steve suggested that direct writing could be considered QoI; the standard should not be specifically
    concerned with the Windows console.
  - Steve rephrased; we want to give Windows implementors permission, not a mandate.
  - Tom raised the question from the agenda email asking about future direction to integrate support for
    other character types.
  - Victor replied that it is straight forward for `char16_t` and `char32_t` since they can be simply
    transcoded to UTF-8, but that support for `wchar_t` is more complicated due to the need to actually
    transcode.
  - Tom replied that it isn't straight forward what the behavior should be when the executin character
    set is not UTF-8; consider EBCDIC.
  - PBrett opined that we don't have to solve this issue now.
  - Tom agreed, but expressed concern that design decisions made now might result in missed opportunities
    to do better than `printf()` in the future.
  - Zach commented that he does not want this paper delayed while awaiting proposals for the lower level
    interfaces encouraged by Jens.
  - Corentin stated that LEWG is busy and urgency is required if the proposal is to make C++23.
  - Corentin added that more features can be added later and that many desired features are not Unicode
    concerns.
  - Hubert claimed that the usefulness of a simple interface is nice and that the special cases needed
    here are not so disimilar to those required for `std::filesystem`.
  - Hubert observed that the proposal is both over specified and under specified; it is over specified
    for Windows, but under specified otherwise.

  - Hubert noted that the literal encoding and the locale encoding are distinct, and although
    [P1885](https://wg21.link/p1885)
    would allow differentiating them, we still have not standardized (in C or C++) facilities to transcode
    from the literal encoding.
  - **Poll: Forward P2093R3 to LEWG.**
    - Attendance: 9 (Hubert was present for discussion, but was not able to be present for the poll)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   4 |   2 |   2 |   0 |   1 |

    - Consensus is in favor.
    - SA stated opposition to progression without the lower level facilities also being made available.
    - Victor asked if it would still be helpful to propose those facilities separately.
    - SA responded, yes.
- Tom stated that the next telecon will be on February 24th and that the tentative topics are Jens'
  [P2314](https://wg21.link/p2314) and discussion of priorities for C++23.


# January 27th, 2021

## Agenda:
- Presentation and discussion with Jonathan Müller regarding his
  [lexy parser combinator library](https://github.com/foonathan/lexy)
  ([Tutorial](https://lexy.foonathan.net/tutorial), [Reference](https://lexy.foonathan.net/reference)),
  and the text and Unicode related challenged he faced, how he solved them, and what C++ standard
  language or library features he would have benefitted from.
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm)

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Daniela Engert
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Jonathan Müller
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tomasz Kamiński
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Presentation on lexy’s text and Unicode challenges by Jonathan Müller:
  - Jonathan's presentation slides are avilable
    [here](presentations/2021-01-27-lexy-presentation.pdf).
  - Part 1: Inputs and Encodings:
    - Jonathan presented:
      - Several classes are provided to handle input via ranges, strings, and buffers, each of which provides a
        reader class.
      - The reader class provides access to the input data independent of the specific input class.
      - Encoding classes provided for each of the supported encodings define traits and operations for an
        encoding.
      - The encoding classes are superficially similar to `std::char_traits`; they define a character type, an
        integer type to be used as an EOF sentinel, conversion operations from the character type to the integer
        type, secondary types that may be used with the encoding, and encode operations.
      - The supported encodings are:
        - Default: uses `char` as the character type, `int` as the integer type, and `-1` as the EOF value.
        - Raw: uses `unsigned char` as the character type, `int` as the integer type, and `-1` as the EOF value.
          `char` and `std::byte` can be used as secondary character types.
        - ASCII: uses `char` as the character type, `char` as the integer type, and `0xff` as the EOF value.
        - UTF-8: uses `char8_t` as the character type, `char8_t` as the integer type, and `0xff` as the EOF value.
          `char` can be used as a secondary character type.
        - UTF-16: uses `char16_t` as the character type, `std::int_least32_t` as the integer type, and `-1` as
          the EOF value.
          `wchar_t` can be used as a secondary character type if it has the same size as `char16_t`.
        - UTF-32: uses `char32_t` as the character type, `char32_t` as the integer type, and `0xffffffff` as the
          EOF value.
          `wchar_t` can be used as a secondary character type if it has the same size as `char32_t`.
      - Wish list:
        - The ability to determine the encoding of ordinary string literals.
        - The ability to convert between the original character types (`char`, `wchar_t`) and the newer types
          (`char8_t`, `char16_t`, `char32_t`) without the spectre of undefined behavior.
        - A library function to heuristically determine or guess the encoding for some input.
    - \[ Editor's note: Right at the start of Jonathan's presentation, one of the editor's sons showed up
      bleeding from having fallen while climbing over a fence.  Recovery was quick, and the editor was
      appreciative of the excellent slides that enabled him to fill in what he missed of the presentation. \]
    - Hubert noted that use of `0xFF` as the EOF value for the ASCII encoding could be problematic since `char`
      may be a signed type, but is probably ok if it is just an internal implementation detail.
    - PBrett observed that, for encodings with a larger integer type, buffer space may not be used efficiently.
    - Jonathan replied that buffers always store values in the character type, not the integer type.
    - Victor asked how ill-formed input that might have a character value that matches the EOF value is handled.
    - Jonathan replied that processing of such input will end prematurely.
    - PBrett stated that it seems reasonable for the library to require well-formed input.
    - PBrett asked if a library solution that provides a "blessed" cast operation for handling input in the
      secondary character types would suffice.
    - Jonathan replied that it would.
    - Corentin mentioned having discussed such a possibility with Richard Smith in the past, particularly with
      regard to the possibility of `constexpr` support.
    - Jonathan confirmed that `constexpr` support would be useful.
    - Steve stated that there is a need for that feature for historical interfaces that have `char*` parameters.
    - Jonathan acknowledged the need and explained that these interfaces accept either the primary or secondary
      type and use `reinterpret_cast` internally.
    - Hubert asked if these conversions are needed only in one direction or in both.
    - Jonathan replied that they are one directional; the user will not modify the text after handing it off and
      the library does not hold on to input beyond a call.
    - Jonathan added that, if a buffer is provided, the data is copied.
    - Jens explained that the reason that the `reinterpret_cast` results in undefined behavior is because the
      compiler can assume no aliasing of most types.
    - Corentin asked if a bless function could work at `constexpr` time.
    - Hubert replied that this is different than the `std::bless` that has been discussed in the past; to bless
      means to start the lifetime of an object.
    - Jens stated that there are two approaches we can consider:
      - Changing the alias rules and thereby prohibit related optimizations.
      - Extending the memory model in some way to enable such magic.
    - Mark noted that the anti-aliasing features of `char8_t` were a motivator for adopting the type.
    - Jens added that this is a research opportunity.
    - Jonathan obseved that undefined behavior seems to be ok for users for now.
    - Zach stated that he has also written a parser combinator library, but did so in a way that did not require
      use of `reinterpret_cast`.
    - Corentin noted from chat that [P1885](https://wg21.link/p1885) exposes the encoding of ordinary string
      literals.
  - Part 2: Unicode-Aware Rules:
    - Jonathan presented:
      - Parsing requires converting character input to integer input to check for EOF.
      - Comparing input to literal values also requires conversions.
      - The allowed conversions depend on the encoding in use.
      - Transcoding support is limited to conversion from ASCII to other encodings and assumes that the code
        point value in the target encoding matches the ASCII character code and is representable with a single
        code unit.
      - Matching of literal values is restricted to ASCII unless the literal has a `char8_t`, `char16_t`, or
        `char32_t` based type or if an explicit encoding is specified.
      - A rule is provided for matching a Unicode BOM.
      - A rule is provided for reading a code point for encodings other than default and raw.
      - Input is assumed to be well formed; no validation is performed.
      - Wish list:
        - Unicode character classification functions.
        - A `std::code_point` type.
        - Support for validating encoded input.
      - Features not actually needed for this part:
        - Decoding facilities.
        - Transcoding facilities.
    - \[ Editor's note: The editor's internet connection decided to take some time off just as Jonathan started
      presenting part 2.  It came back fairly quickly, but a few minutes of presentation were lost.  Gaps were
      again filled in thanks to the excellent slides. \]
    - Hubert asked what features would be desirable in a `std::code_point` type.
    - Jonathan presented lexy's `code_point` type and its `is_valid()`, `is_surrogate()`, `is_scalar()`,
      `is_ascii()`, and `is_bmp()` members.
    - PBrett observed that the desire is for something like Unicode properties.
    - Jens noted the much simpler requirements.
    - PBrett asked if higher level features are provided that could handle Unicode normalization.
    - Jonathan replied that there are not currently, but that adding such support seems feasible.
    - Zach noted that there are normalization equivalences, but also equivalence for collation purposes and
      that a lot of effort is required to get that working.
    - Corentin noted from chat that [P1628](https://wg21.link/p1628) provides support for Unicode character
      classification and that an implementation is available at
      https://github.com/cor3ntin/ext-unicode-db/blob/master/generated_includes/cedilla/properties.hpp.
  - Part 3: File Input:
    - Jonathan presented:
      - Buffers have an associated encoding.
      - Endian concerns, including handling of BOMs, are addressed when filling a buffer.
      - A function is provided for populating a buffer from a file.
      - File reading is done in binary mode and without encoding validation.
      - Wish list:
        - `std::read_file()`.
        - Endian conversion facilities.
        - Facilities to heuristically identify the encoding of arbitrary input.
    - Tom noticed that, if a BOM is not present, that big endian is assumed and asked if the default shouldn't
      be the native endian order for data in memory.
    - PBrett agreed that, for data in memory, yes, but for data at rest, big endian is the default.
    - Jonathan explaind that BOM assumptions are only used for files at present, so assuming big endian seems
      correct.
    - PBrett agreed that a `std::read_file()` function would be useful.
    - Jens stated in chat that support for endian conversions is in progress; [P1272R3](https://wg21.link/p1272).
  - Part 4: The `as_string` callback:
    - Jonathan presented:
      - When a production rule is matched, the parsed lexeme is passed to a functor that can receive it as
        a string-like type, a C string, or as a lexeme with associated reader class.
      - A lexeme is a range over the input.
      - Wish list:
        - Encoding facilities.
        - Transcoding facilities.
  - PBrett noted that Zach's [Boost.text](https://github.com/tzlaine/text) library does some of this.
  - Zach agreed and noted support for transcoding.
  - PBrett asked if support for grapheme rules had been considered.
  - Jonathan replied that he has considered such rules, but that such support requires the Unicode DB.
  - Mark asked if grapheme interfaces were available in the standard, whether they would be used.
  - Jonathan replied, yes and stated that he intends to implement more Unicode rules, but they are work.
  - Tom summarized one of his big take aways from the presentation is how encodings were handled; that
    support was limited to ASCII unless there was evidence in the type system for a more capable encoding.
  - PBrett stated that one of his big take aways is that a number of the items in the wish lists are
    already in the pipeline.
  - Jens agreed and noted that these are some of the easier items to address.
  - Jens noted that there would be clear benefit from access to Unicode DB character properties.
  - PBrett asked if Jonathan would make the slides available.
  - Jonathan agreed to do so.
  - \[ Editor's note: Jonathan did so and they are linked above. \]
  - Corentin stated that the ability to provide conversions between `char` and `char8_t` is something
    that we might be able to do for C++23.
  - PBrett suggested that one way to do that might be to take a span and return another span.
  - Steve agreed that the ability to perform such conversions would be useful, but wondered if it can
    be done without losing aliasing benefits.
  - Jens suggested postponing how to alias `char` and `char8_t` until a proposal is provided.
  - Zach commented that he and Jonathan made many similar choices in their implementations, but noted
    one point of difference; Zach tried to deduce the encoding all the time.
  - JeanHeyd observed that, with Corentin's [P1885](https://wg21.link/p1885), the literal encoding
    will be known.
  - JeanHeyd added that gcc trunk already has support for the predefined macro and that Clang and MSVC
    are making progress.
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm):
  - JeanHeyd presented:
    - The paper was presented to WG14 in November.
    - WG14 requested that additional conversion functions be provided to convert between UTF encodings.
    - The paper proposes conversion functions from the locale sensitive MB/wide encodings to UTF encodings.
    - Converters are provided that perform per-code-unit translation and per-string translation.
    - These functions avoid the historical issues with variable length encodings.
    - MAX macros are provided to avoid having to check for and handle insufficient output errors.
    - These functions differ from `iconv` because C doesn't have a locale or encoding tag suitable for
      specifying an encoding.
  - PBrett asked to verify that sizes are always expressed in code units in the paper.
  - JeanHeyd replied that they are.
  - PBrett observed that the historical designs returned a positive value to indicate the number of
    code units that were written.
  - JeanHeyd acknowledged and explained that a different design is proposed here because of ambiguities
    that arise with a return value of 0.
  - Steve asked how the number of code units that were consumed and written are returned.
  - JeanHeyd replied that the provided pointers are updated, so the caller can calculate.
  - Jens observed that the proposed interface always requires two modifications when some input is
    consumed and output is produced; an alternative would be a range where only the input is bumped.
  - JeanHeyd replied that convenience functions that provide that simpler interface could potentially
    be provided.
  - Jens asked for more explanation for the use of a pointer/size pair as opposed to a pointer/pointer pair.
  - JeanHeyd replied that null can be passed for the size.
  - Jens expressed concerns about security issues.
  - Tom stated that a null could be passed for an end pointer to accomplish the same goals; and the same
    security concerns.
  - PBrett suggested postponing further discussion until the next meeting.
- Tom stated that the next meeting will be February 10th and that
  [WG14 N2620](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm) will be top of the list.
- Tom thanked Jens for his recent draft paper proposing changes to the UCN model and that he would put
  that paper on the agenda soon.
- Tom added that he is thinking about dedicating an upcoming telecon to discussion of what we want to
  try and complete for C++23.


# January 13th, 2021

## Agenda:
- [P2246R0: Character encoding of diagnostic text](https://wg21.link/p2246r0)
  - And companion paper: [WG14 N2563: Character encoding of diagnostic text](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2563.pdf)
- SG16, SG22, and WG14 coordination.
  - Priority and owners for [SG16's open WG14 issues](https://github.com/sg16-unicode/sg16/issues?q=is%3Aissue+is%3Aopen+label%3Awg14).
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm)

## Meeting summary:
- Attendees:
  - Aaron Ballman
  - Corentin Jabot
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Tom stated that his paper to clarify guidance regarding use of BOMs in UTF-8 text was submitted
  to the UTC and given paper number L2/21-038.
  - The submitted paper is available at https://www.unicode.org/L2/L2021/21038-bom-guidance.pdf.
- [P2246R0: Character encoding of diagnostic text](https://wg21.link/p2246r0):
  - Aaron provided an introduction:
    - The basic problem is that we have features that require source code fragments to be reproduced in diagnostics
      without clear specification or limits regarding how that should be done.
    - Depending on the various encodings in use, accurate representation of the original source code may not be
      possible.
    - The degree to which these fragments are preserved and reproduced should be a QoI issue.
    - WG14 approved the C version of this paper
      ([WG14 N2563: Character encoding of diagnostic text](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2563.pdf)).
    - The wording changes for the C standard have a little additional cleanup;
      some uses of "may" were changed to "should".
    - A goal is to keep the C and C++ standards aligned.
  - PBrett asked if the proposed changes might be considered editorial.
  - Hubert opined that considering them editorial would be contentious.
  - Aaron responded that the changes should not be considered editorial.
  - PBrett asked if there is anything evolutionary about the changes.
  - Aaron replied that he didn't think so, but that EWG participants may have a different perspective; for example,
    a desire to define a character set for diagnostics, though he would be surprised.
  - Steve noted that we have parallel work in progress to specify translation within the standard in terms of a
    Unicode encoding.
  - Hubert observed that the standard currently specifies different requirements for the `static_assert` declaration
    and `#error` directive vs the `[[deprecated]]` and `[[nodiscard]]` attributes; the former require the message to
    reproduce the text while the latter specify normative encouragement.
  - Hubert noted that the status quo is not that diagnostics are QoI; there are requirements on the text produced, so
    changes could impact implementations.
  - Hubert observed that the `#error` directive requires reproducing preprocessing tokens, potentially including string
    literals, at an earlier phase of translation than, for example, `static_assert`.
  - Hubert requested that the paper clarify how diagnostics produced at different translation phases be handled.
  - Aaron stated that he was not aware of a requirement that diagnostics be textual; an implementation that presented a
    frowny face or a graphical image of the source code would be conforming.
  - PBindels chimed in from chat to state that
    [Evoke](https://github.com/dascandy/evoke) emits emoji for its error state and that he felt called out.
  - Victor also chimed in from chat to suggest to PBindels that emoji is still text and that Evoke should emit a gif
    with a relevant meme.
  - Hubert responded that there is a requirement if the standard states one; the implementation must have some means to
    present a message.
  - Aaron asked if a change to the prose was desired.
  - Hubert responded affirmatively; that he would like to see a change of the rationale to clarify that there is no
    increase in requirement for some representation of the text in comparison to the status quo. 
  - Aaron agreed to make such a change.
  - Corentin recalled earlier discussions regarding translation phase 1, string literals always being in execution
    encoding, and whether `static_assert` might require special handling.
  - Corentin expressed contentedness with the paper as presented and stated that the standard should not have to specify
    how a string literal is presented.
  - Aaron agreed with one exception; `#error` is specified solely in terms of preprocessing tokens.
  - Corentin acknowledged; a string literal is a token in that case and `#error` processing occurs before conversion
    to the execution character set in translation phase 5.
  - Hubert noted that the status quo is that preprocessing tokens are limited to the basic source character set due to
    translation phase 1 converting other characters to UCNs.
  - Hubert added that we have direction that might change this, but that this paper should not be held up because of
    that; Jens' effort may need to consider this though.
  - Hubert observed that the standard does not specify how an implementation represents text in the execution character
    set, but that it needs to acknowledge that a translation is required when producing a diagnostic.
  - Aaron asked if some string literals, such as those used in attributes, should even undergo translation to the
    execution character set.
  - PBrett replied that an implementation performs conversion to the execution character set and therefore has the means
    to undo the conversion.
  - Steve noted that an implementation presumably will retain access to the original source code; a reverse map to the
    original text suffices in the worst case.
  - Hubert stated that it isn't necessarily true that a compiler can easily map from a converted string literal back to
    the original text after translation phase 5.
  - Mark noted that, with regard to attributes, they can include arbitrary expressions, not just string literals.
  - Corentin stated that this discussion is expanding the scope of what is required and repeated his opinion of the
    paper being acceptable as presented.
  - Corentin added that, with respect to string literals, that programmers be able to rely on them being consistently
    converted; consistency is important for reflection and other compile-time programming facilities.
  - Steve opined that some of this discussion is well in to QoI territory; if a compiler can't display source code in a
    sensible manner to the programmer, then all bets are off.
  - Hubert stated that he would be happy with changing the current uses of "shall" to "should" via this paper, but that
    it isn't strictly necessary at this time; we don't want to exclude any execution environments.
  - Aaron agreed.
  - Hubert added that the wording for `#error` should be changed to match.
  - **Poll: When diagnostic messages quote a portion of source code, the preservation of text semantics is merely a quality of implementation concern.**
    - Attendance: 11

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   5 |   2 |   2 |   0 |   0 |

    - Consensus is in favor.
  - **Poll: We agree with removing the specific character set from static_assert along the lines of P2246.**
    - Attendance: 11
    - No objections to unanimous consent.
  - **Poll: Forward P2246 to EWG**
    - Attendance: 11
    - No objections to unanimous consent.
- SG16, SG22, and WG14 coordination:
  - Aaron introduced:
    - SG22 will have its first meeting soon.
    - Any WG21 papers targeted to SG22 will be forwarded to WG14 and SG22 will evaluate whether the paper is
      appropriate for both groups.  Authors will then submit papers to WG14.
    - SG22 will assist with finding people to present at WG14 meetings on behalf of WG21 authors that are
      unable to attend a WG14 meeting.
    - WG14 does not currently have a study group that focuses on text issues.
    - WG14 participants tend to be passionate about character sets.
- Review of [SG16's open WG14 issues](https://github.com/sg16-unicode/sg16/issues?q=is%3Aissue+is%3Aopen+label%3Awg14):
  - [Issue #62: WG14 N2594: Disallow mixed string literal concatenation](https://github.com/sg16-unicode/sg16/issues/62):
    - JeanHeyd reported that [WG14 N2594](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2594.htm)
      was adopted for C2x and that this issue can be closed.
    - JeanHeyd noted that there was a request for a follow up paper to allow mixed literals with defined
      semantics.
    - Aaron added that the [sdcc](http://sdcc.sourceforge.net) compiler implements mixed string literals with
      useful semantics.
  - [Issue #56: WG14: Improve support for Unicode characters in identifiers](https://github.com/sg16-unicode/sg16/issues/56):
    - Steve volunteered to look at this.
    - Tom commented that WG14 generally likes to see two implementations before adopting a feature and that
      a change to the C++ standard generally counts as one.
    - Aaron confirmed and noted that more implementations increases the motivation for standarizing existing
      behavior.
    - Corentin asked if compatibility with C++ is considered good motivation.
    - Aaron replied that it is seen more as weak motivation.
  - [Issue #55: WG14: Named universal character escapes](https://github.com/sg16-unicode/sg16/issues/55):
    - Tom stated that it is still on his plate to get a revision of
      [P2071](https://wg21.link/p2071) submitted to WG21.
    - PBrett suggested that SG22 be included on the next revision of the paper.
    - Tom agreed.
  - [Issue #54: WG14: Make char16_t/char32_t string literals be UTF-16/32](https://github.com/sg16-unicode/sg16/issues/54):
    - Tom noted that this is standardizing existing practice.
    - JeanHeyd volunteered to own this.
    - PBrett volunteered as backup if JeanHeyd becomes too busy with his other efforts.
  - [Issue #5: WG14 N2231: char8_t: A type for UTF-8 characters and strings](https://github.com/sg16-unicode/sg16/issues/5):
    - Tom stated that he is actively working on this.
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm):
  - Tom apologized to JeanHeyd, but stated that discussion of this paper would have to wait until
    the next telecon.
- Tom stated that the next telecon will be held January 27th.  The agenda will include a presentation
  and discussion of Jonathan Müller's Lexy parser combinator library and, of course, JeanHeyd's
  [WG14 N2620](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm)
  postponed from today's meeting.


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
