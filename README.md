# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, January 12th, 2022, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20220112T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- D2286R5: Formatting Ranges
  - Review pending availability of proposed wording and continued targeting of C++23.
- [LWG3639: Handling of fill character width is underspecified in std::format](https://wg21.link/lwg3639)<br/>[LWG3576: Clarifying fill character in std::format
](https://wg21.link/lwg3576)
  - Review pending availability of an updated proposed resolution.
- [P2491R0: Text encodings follow-up](https://wg21.link/p2491r0)
  - Initial review.
- [P2498R0: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r0)
  - Initial review.


# Past SG16 meetings

- [December 15th, 2021](#december-15th-2021)
- [December 1st, 2021](#december-1st-2021)
- [November 17th, 2021](#november-17th-2021)
- [November 3rd, 2021](#november-3rd-2021)
- [October 20th, 2021](#october-20th-2021)
- [October 6th, 2021](#october-6th-2021)
- [September 22nd, 2021](#september-22nd-2021)
- [September 8th, 2021](#september-8th-2021)
- [August 25th, 2021](#august-25th-2021)
- [July 28th, 2021](#july-28th-2021)
- [July 14th, 2021](#july-14th-2021)
- [June 23rd, 2021](#june-23rd-2021)
- [June 9th, 2021](#june-9th-2021)
- [May 26th, 2021](#may-26th-2021)
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


# December 15th, 2021

## Agenda
- [P2361R4: Unevaluated strings](https://wg21.link/p2361r4)
  - Poll forwarding to EWG for C++23.
- [P1854R2: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r2)
  - Discuss and poll forwarding to EWG for C++23.
- [D2286R4: Formatting Ranges](https://wg21.link/p2286r4)
  - Review updates since the last telecon.

## Meeting summary
- Attendees:
  - Barry Revzin
  - Charlie Barto
  - Corentin Jabot
  - JeanHeyd Meneide
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tim Song
  - Tom Honermann
  - Zach Laine
- [P2361R4: Unevaluated strings](https://wg21.link/p2361r4)
  - PBrett explained that SG16 had previously reviewed this paper and that all prior feedback has
    been addressed.
  - PBrett thanked Corentin for quickly updating the paper in response to the prior review and for
    soliciting new feedback on the mailing list.
  - PBrett asked if there were any new comments.
  - Tom requested that a table be added to the prose section that summarizes the intended changes;
    though the effects can be determined from the wording, the impact is subtle with regard to
    things like where raw string literals are now allowed or disallowed.
  - Corentin agreed to do so.
  - Jens expressed a belief that there are no changes with regard to where raw string literals
    are and are not allowed.
  - Corentin agreed and noted that there were such changes in a previous revision, but that those
    changes have been removed.
  - **Poll 0: Forward P2361R4 "Unevaluated strings" to EWG with a recommended ship vehicle of C++23.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   4 |   0 |   0 |   0 |
      
    - Consensus (though with a smaller quorum than is usual due to abstention from late arrivals).
- [P1854R2: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r2)
  - Corentin summarized recent changes to improve the motivation and wording and to correct typos.
  - Corentin recalled that this paper was discussed in Belfast and in a recent telecon, but that the
    paper has not been polled since Belfast.
  - \[ Editor's note: Two polls were taken in Belfast as documented in the
    [minutes for the discussion of P1885](https://wiki.edg.com/bin/view/Wg21belfast/SG16P1885R0).
    The first was a poll to confirm the direction of the paper and the second was to make it dependent on
    [P1885 (Naming Text Encodings to Demystify Them)](https://wg21.link/p1885). Both polls had consensus.
    P1885 was recently approved via electronic polling by LEWG and is expected to be voted on during the
    next WG21 plenary. \]
  - Corentin explained that the paper proposes two changes:
    - Making non-encodable character literals ill-formed.
    - Adding restrictions to the characters that may syntactically appear in multicharacter literals.
  - Charlie asked if the proposal will break currently used methods to probe the literal encoding during
    constant evaluation.
  - PBrett replied that we now have a facility that avoids the need for such probing.
  - Charlie acknowledged the new facility and that its existence does reduce concerns, but that he still
    wanted to be sure about what the expectation is.
  - Corentin confirmed that such code may be broken and stated that this concern was discussed in Belfast
    and was the motivation for blocking this paper on adoption of P1885.
  - \[ Editor's note: Whether such code is broken in practice will depend on what implementors choose to
    do. The changes require a diagnostic to be produced, but implementors are free to implement that as
    a warning in which case compilation failure would only occur if warnings are elevated to errors. \]
  - Tom noted that P1885 recently passed LEWG electronic polling.
  - Corentin asked if the macros added to recent Microsoft Visual C++ releases to reflect the
    literal encoding are defined regardless of which `/std` options are passed.
  - Charlie confirmed that they are.
  - \[ Editor's note: As of Microsoft Visual C++ version 19.30, the `_MSVC_EXECUTION_CHARACTER_SET` macro
    is predefined to indicate the code page being used for the literal encoding. \]
  - Corentin noted that character probing mechanisms are not particularly reliable.
  - PBrett stated that only one implementation is expected to have to change behavior if this proposal
    is adopted and noted that the implementor in question is aware of the proposal and has so far not
    objected to the proposed change.
  - PBrett reported that prior wording feedback has been addressed.
  - Jens read the following proposed addition to \[lex.ccon\].
    - "If a multicharacter literal contains a *basic-c-char* representing a codepoint that is not
      encodable as a single code unit in the ordinary literal encoding, the program is ill-formed"
  - Jens noted that the difference between *basic-c-char* and *c-char* is that the former excludes escape
    sequences and asked if the prohibition against escape sequences was intended to apply to
    *universal-character-names* (UCNs) as well.
  - Corentin replied that the design is intended only to apply to visually ambiguous scenarios and that
    use of a UCN does not create visual ambiguity.
  - Jens noted that a UCN is not an escape sequence and that the paper prose discusses escape sequences,
    but not UCNs.
  - Corentin replied that he will update the prose to make it explicit that UCNs are not prohibited.
  - Jens pondered whether the previously read wording should state "UCS scalar value" in place of
    "codepoint".
  - Corentin replied that the distinction is not relevant after translation phase 1.
  - Jens opined that neither is actually needed and suggested rephrasing as,
    "... contains a *basic-c-char* that is not encodable as a single code unit ...".
  - Corentin agreed to make a change.
  - Tom pondered whether the parts of the note removed from \[lex.ccon\] that continue to be applicable
    to multicharacter literals should be preserved.
  - PBrett pointed out that the note is non-normative and that the relevant parts of it, that
    multicharacter literals have an implementation-defined value, are normatively specified elsewhere.
  - **Poll 1: Modify P1854R2 "Conversion to literal encoding should not lead to loss of meaning" to address
    wording feedback and forward the paper as revised to EWG with a recommended ship vehicle of C++23.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   5 |   0 |   0 |   0 |
      
    - Strong consensus in favor.
- [D2286R4: Formatting Ranges](https://wg21.link/p2286r4)
  - \[ Editor's note: D2286R4 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2286R4 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin reported that the LEWG chair is skeptical that there is sufficient time available for this
    proposal to be reviewed and adopted for C++23.
  - Tom reported that both SG9 and SG16 have planned time for review and that, assuming that both SGs
    forward the paper, further scheduling will be up to the LEWG chair.
  - PBrett reminded the group that SG16 had previously advocated for adding an explicitly deleted
    format specialization for `std::filesystem::path` to this paper and dropping the support proposed in
    [P1636R2 (Formatters for library types)](https://wg21.link/p1636r2) pending a future paper that
    addresses `std::filesystem::path` specifically.
  - PBrett stated that he wasn't sure if a later revision of the latter paper actually dropped that
    support.
  - \[ Editor's note: SG16 reviewed P1636R2 during its
    [2021-09-22 telecon](https://github.com/sg16-unicode/sg16-meetings/blob/master/README.md#september-22nd-2021);
    that revision remains the current revision.
    The poll taken then is recorded in
    [a comment in the related GitHub tracking issue](https://github.com/cplusplus/papers/issues/425#issuecomment-938167118). \]
  - Barry introduced the changes made since the last revision.
    - Hex escapes are now only used for ill-formed code unit sequences.
    - Hex escapes now use delimited escape sequence notation.
    - UCNs are now used for non-printable characters.
  - Jens asked if there is any further intention of reducing scope in order to maintain a target of C++23.
  - Barry replied that the intended scope is what is presented in this revision and that there are no
    current plans to further reduce scope.
  - PBrett asked if consideration was given towards dropping support for the debug format.
  - Barry replied affirmatively.
  - Jens stated that the escaping behavior needs to address the possibility of lone surrogates.
  - Tom asked if the expectation is that lone surrogates would be encoded in UCN notation.
  - Jens replied that UCN notation does not permit specifying surrogate code points.
  - Jens noted that the escaping behavior is described in terms of code points and that this differs from
    how string literals are specified; the latter is described in terms of code unit sequences.
  - Jens added that specifying escape behavior in terms of code points requires the ability to reconstruct
    code points from code unit sequences and noted that shift encodings may not have a clearly defined
    code point space.
  - Tom replied that translation to a UCS scalar value would still be possible, but may face implementation
    challenges.
  - Jens noted the dependency on Unicode properties and pondered how that applies to non-Unicode encodings.
  - Jens stated that "an implementation-defined equivalent of Unicode properties" could impose a
    documentation burden.
  - PBrett suggested that requirement could be met by documenting a methodology as opposed to an explicit
    table of equivalent Unicode properties for other character sets.
  - Corentin wondered whether newline characters should always be escaped.
  - Corentin noted that there are design questions regarding whether unassigned code points and private
    use area (PUA) characters should be escaped.
  - Corentin suggested that PUA characters should probably be escaped but that it is less clear how unassigned
    code points should be handled.
  - Corentin wondered what the performance cost would be for the requirement to check the `Grapheme_Extend`
    property for characters at the start of a string.
  - Corentin suggested that it may be desirable to specify escape behavior in terms of conversion to Unicode
    to ensure consistent behavior across implementations.
  - Tom asked how it was determined that the `Z` (`Separator`) and `C`(`Other`) values of the `General_Category`
    property suffice to define printable characters.
  - Corentin replied that those properties exclude all control, separator, and unassigned characters.
  - Corentin noted that there is a design decision to be made regarding which separators should be considered
    printable.
  - Corentin added that there is a trade off between getting a "right" result and potentially requiring a
    possibly large table of character properties.
  - Tom asked if the lookup for the `Grapheme_Extend` property is intended to identify combining characters
    for which a base character is not available to combine with.
  - Corentin confirmed that is the intent.
  - Charlie asserted a need for further elaboration of what is meant by "a code unit that is not a part of a
    valid code point".
  - Zach asserted that PUA characters should not be escaped and that they should be usable in the same manner
    as any other printable character.
  - Zach stated that Unicode specifies how sequences of invalid code units should be handled and that processing
    them should be left to QoI.
  - \[ Editor's note: See the
    "Constraints on Conversion Processes" and
    "U+FFFD Substitution of Maximal Subparts"
    sections of 3.9, "Unicode Encoding Forms", in
    [chapter 3 of Unicode 14.0](https://www.unicode.org/versions/Unicode14.0.0/ch03.pdf)
    for Unicode recommendations regarding handling of ill-formed code unit sequences. \]
  - Tom stated that his understanding is that the intent is to preserve the values of all bytes that contribute
    to an invalid code unit sequence.
  - Charlie mentioned that the Unicode standard refers to the
    [WhatWG encoding standard](https://encoding.spec.whatwg.org)
    for handling of ill-formed code unit sequences.
  - \[ Editor's note: It does so in the "U+FFFD Substitution of Maximal Subparts" section mentioned in the
    previous note. \]
  - Charlie noted a design question; how are invalid code unit sequences delimited?
  - Charlie suggested that it might be ok to discontinue consuming text after an invalid code unit sequence.
  - Charlie asserted a requirement for wording to prohibit considering code units following an invalid code unit
    sequence as themselves being part of the invalid code unit sequence if they could signify the start of a
    potentially valid code unit sequence.
  - \[ Editor's note: This is consistent with guidance in the
    "Constraints on Conversion Processes" section mentioned in a previous note. \]
  - Corentin asserted that replacement characters are not particularly helpful when trying to diagnose
    unexpected output; the actual byte or code unit values are needed.
  - Corentin stated that further discussion regarding handling of ill-formed code unit sequences is needed.
  - PBrett indicated that consensus for how to handle invalid code unit sequences is not yet clear and that
    there exists a design question of whether to emit replacement characters or preserve code unit values via
    hex escapes.
  - PBrett suggested it may be worth stating in
    [SD-8](https://isocpp.org/std/standing-documents/sd-8-standard-library-compatibility)
    that debug formatting is not stable.
  - Corentin noted that, because Unicode character properties are not stable, that we can't commit to stability anyway.
  - PBrett requested that Barry submit the draft revision as a P paper.
  - Barry agreed to do so, but reported that he had already edited it in response to the discussion.
  - Corentin asked if the group has concerns regarding handling of non-Unicode encodings.
  - PBrett replied that he would like to see wording, but that we are short on time.
  - **Poll 2: Modify D2286R4 to address design feedback, and forward the published paper as revised to LEWG with a
    recommended ship vehicle of C++23.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   2 |   0 |   1 |
      
    - Consensus.
    - N: Lack of wording.
    - SA: Lack of wording; concerned that there will be subtle issues that won't become apparent until wording
      is available.
- Tom announced that the next telecon will be held 2022-01-12 and that the agenda is expected to
  include review of an updated revision of
  [P2286 (Formatting Ranges)](https://wg21.link/p2286),
  review of an updated proposed resolution for
  [LWG3639 (Handling of fill character width is underspecified in std::format)](https://wg21.link/lwg3639) and
  [LWG3576 (Clarifying fill character in std::format)](https://wg21.link/lwg3576), and/or initial review of
  [P2491R0 (Text encodings follow-up)](https://wg21.link/p2491r0) and
  [P2498R0 (Forward compatibility of text_encoding with additional encoding registries)](https://wg21.link/p2498r0).


# December 1st, 2021

## Agenda
- [LWG3639: Handling of fill character width is underspecified in std::format](https://wg21.link/lwg3639)
- [P2286R3: Formatting Ranges](https://wg21.link/p2286r3)

## Meeting summary
- Attendees:
  - Barry Revzin
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
- \[ Editor's note: The agenda order was revised to accommodate attendee schedules. \]
- [P2286R3: Formatting Ranges](https://wg21.link/p2286r3)
  - Barry provided an introduction.
    - The goal is to add formatting support for types like tuple, pair, and vector.
    - A sed-like delimiter syntax is proposed to allow for unambiguous formatting of
      pair and tuple elements.
    - The delimiter syntax may be dropped for now in order to focus on fill and alignment.
    - The delimiter syntax could still be added for a future standard.
  - Zach mentioned that the Unicode Bidirectional Algorithm document defines a set of paired
    brackets that could potentially be used as matched delimiters.
  - \[ Editor's note: The Unicode Bidirectional Algorithm document is
    [UAX #9](https://unicode.org/reports/tr9).
    Paired brackets are defined via the UCD `Bidi_Paired_Bracket` and `Bidi_Paired_Bracket_Type`
    properties in
    [BidiBrackets.txt](https://www.unicode.org/Public/UCD/latest/ucd/BidiBrackets.txt). \]
  - Zach provided a brief introduction to how the term "character" gets used. Within the
    C++ standard, "character" generally means an object of type `char`, a "code point" represents
    some part of what we notionally think of as a character, and an "extended grapheme cluster" (EGC)
    represents a "glyph" or what we visually perceive to be a character.
  - Zach stated that we might be able to get away with specifying delimiters as "characters",
    but noted that such interfaces tend to become regarded as broken later.
  - Victor stated that, if the goal is to add some support in C++23, then custom delimiters should
    be dropped for now given concerns like how use of a digit as a delimiter could lead to problems.
  - Corentin agreed with Barry and Victor that custom delimiter support can be postponed in favor
    of a more comprehensive solution later.
  - Charlie argued strongly in favor of use of code points as delimiters given the lack of
    experience using EGCs in C++20.
  - Charlie noted that EGCs do not necessarily correspond to what you might navigate through in a
    word processor.
  - Charlie added that combining code points can be combined with bracket characters.
  - Charlie stated that most other languages just use code points for delimiters.
  - PBrett expressed concern about the choice of delimiters leading to format strings that are
    indistinguishable from line noise.
  - Barry noted that, without custom delimiters, the only newly required character is `:`.
  - PBrett acknowledged, but noted that a sequence of such characters is needed to navigate
    range hierarchies.
  - Barry agreed, but noted that subrange formatting wouldn't otherwise be possible.
  - PBrett suggested that a required custom formatter may be an improvement.
  - Barry asked for feedback on two questions.
    - Is everyone happy with use of `?` for the debug specifier?
    - Is everyone happy with the described quoting and escaping mechanism for string and
      character data?
  - Victor responded that `?` seems ok for the debug specifier.
  - PBrett asked if there are other use cases for which `?` might be desirable.
  - Tom noted that `?` is often used in conjunction with optional data.
  - Tom asked why the proposed specifier is called the "debug" specifier.
  - Barry responded that "debug" is consistent with Rust's description of its equivalent
    functionality.
  - Barry noted that Python uses "repr" for its equivalent.
  - Jens observed that `std::quoted()` already exists for use with iostreams.
  - Barry replied that using it would require an additional specifier like `Q`.
  - PBindels agreed that the "debug" name for the new specifier is confusing.
  - PBrett noted that the "debug" name would not be reflected in written format strings.
  - Charlie expressed a preference for "debug" over "repr" so that the latter can be
    preserved for compiler generated representations.
  - Jens asked for a summary of the escaping proposal.
  - Barry replied that the intent is to do what
    [{fmt}](https://github.com/fmtlib/fmt)
    does and deferred to Victor.
  - Victor stated that the escaping done by {fmt} was recently described in an email to
    the SG16 mailing list.
  - \[ Editor's note: that email is archived at
    https://lists.isocpp.org/sg16/2021/12/2874.php. \]
  - Victor noted that the paper should be updated to describe what {fmt} currently does.
  - Jens mentioned that the email states that code points in the range 0 through 0x100
    are formatted as hex escape of the form `\xhh`.
  - Victor clarified that this substitution only applies to non-printable characters.
  - Jens asked what characters are considered non-printable.
  - Victor replied that Unicode specifies a non-printable property and that Rust has a
    non-printable concept.
  - \[ Editor's note: Unicode does not specify a printable or non-printable property, but
    does specify many properties from which such properties could be derived. \]
  - Tom stated that there appear to be two specification questions:
    - What characters in the code point range 0 through 0x100 are considered non-printable?
    - How are non-printable characters escaped?
  - Tom expressed a preference for use of UCN notation for non-printable characters.
  - Corentin agreed; use hex escapes for invalid code units and UCN notation for characters.
  - Corentin suggested it might make sense to use hex escapes for non-Unicode encodings.
  - PBrett asked if it would be a problem to specify UCN notation now, but then switch to
    [P2290](https://wg21.link/p2290) delimited escape sequences later.
  - Jens stated that depends on other factors.
  - PBrett replied that it therefore seems quite important to make the right decision now.
  - Corentin indicated that there is no need to tie the choice of output format to the
    delimited escape sequences specified in P2290.
  - Corentin stated that P2290 will appear in the next EWG eletronic voting cycle.
  - Victor expressed reluctance towards P2290 delimited escape sequences due to increased
    verbosity and inconsistency with Rust.
  - Victor added that use of brace delimiters with `\x` is unusual.
  - PBrett encouraged use of delimited escape sequences for readability benefits.
  - Jens asked if it is intended that copy/paste work to produce a string literal that
    matches the formatted output.
  - Barry stated that would be a worthwhile goal.
  - Jens noted that it is therefore necessary to avoid potential munging with `\x`; this
    might require spliced strings.
  - Tom noted that such munging is a concern for human consumption as well.
  - \[ Editor's note: With regard to munging, consider `\xdeface`. Is that a single hex
    escape, a `\xde` escape followed by `face`, or something in between? \]
  - Jens agreed, but noted that a human might expect that only hex escapes with two digits
    will be produced.
  - Jens asserted that the ability to re-parse strongly suggests use of delimited escapes.
  - Jens pondered whether the escape mechanism might require an EBCDIC based implementation
    to transcode to Unicode in order to produce a UCN.
  - Jens stated that care is needed that deference to the Unicode DB for a non-printable
    property not result in a large dependency on the Unicode UCD.
  - Jens suggested an implementation should be permitted to escape all non-ASCII characters.
  - PBrett suggested that escape sequences could be limited to control characters.
  - Corentin reported experience with implementing an `isprintable()` function and noted that
    it does not require a large table.
  - Tom suggested that round tripping of an escaped string output should be possible with
    use of the `std::scan()` function proposed in [P1729](https://wg21.link/p1729).
  - Victor posted a link to an `is_printable()` implementation used in {fmt} and noted the
    small size of the tables used.
    - https://github.com/fmtlib/fmt/blob/master/include/fmt/ranges.h#L268-L395
  - Victor noted that limiting hex escapes to two digits avoids round trip concerns without
    requiring extra delimiters.
  - PBrett requested that the next revision of the paper include discussion of these concerns.
  - Corentin asked if the escape mechanism should be exposed as an independent facility.
  - Barry suggested that independent facility could just be `std::format()`.
  - PBrett observed that a standalone facility could be added later.
  - PBrett asked if SG16 should review an updated revision of this paper again.
  - Corentin replied affirmatively.
  - Jens agreed and noted a need to understand the escape mechanism.
  - Jens stated that the paper should also address non-Unicode platforms.
  - Corentin noted that, for `wchar_t`, a hex escape with only two digits is insufficient.
  - Tom noted that two digits is insufficient for `char` when `CHAR_BIT` is greater than 8.
  - Mark observed that the escape facility would be useful for dealing with file names.
  - Victor agreed.
  - **Poll 0: We recommend using universal character name escape sequences rather than
    numerical escape sequences for the debug representation of all non-printable characters.**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   6 |   2 |   2 |   0 |   0 |
      
    - Consensus in favor
  - **Poll 1: We recommend using brace-delimited numerical escape sequences as described in
    P2290 "Delimited Escape Sequences" for 'debug' formatting of invalid codeunits
    (including lone surrogates).**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   4 |   1 |   1 |   0 |
      
    - Consensus in favor
    - A: Delimited hex escape sequences do not exist in C++ yet and are not used elsewhere;
      but since they will only appear in cases of invalid code units, not SA.
  - **Poll 2: We recommend using brace-delimited universal character name escape sequences
    as described in P2290 "Delimited Escape Sequences" for 'debug' formatting of strings.**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   4 |   0 |   0 |
      
    - Consensus in favor
- [LWG3639: Handling of fill character width is underspecified in std::format](https://wg21.link/lwg3639)
  - Tom provided an introduction.
  - Victor stated that the proposed resolution is somewhat novel and doesn't match what has
    been implemented in {fmt}.
  - Victor noted the absence of a known use case.
  - Victor added that there is no good solution for when alignment is not possible.
  - Victor noted that option 3 allows changing behavior later.
  - Victor recommended proceeding with option 3; if the estimated width is not 1 then an exception may
    be thrown or some other UB may occur.
  - Tom asked what current implementations do.
  - Victor responded that {fmt} assumes an estimated width of 1.
  - PBrett argued against option 3 and provided U+3000 {IDEOGRAPHIC SPACE} as an example of a useful
    fill character with width other than 1.
  - PBrett suggested that an exception could be thrown if alignment requests cannot be met.
  - Zach recommended requiring an estimated width of 1 such that violations are diagnosed as ill-formed
    at compile-time and result in UB at run-time.
  - Zach expressed a desire to avoid paying the cost of checking the estimated width when it will
    virtually never matter.
  - Corentin expressed appreciation for PBrett's use case.
  - Corentin stated that the estimated width approach is known not to produce perfect results in general
    and that he is therefore not very concerned with how this issue is resolved.
  - Hubert expressed support for PBrett's use case.
  - Hubert noted the current absence of a wording mechanism to determine the number of fill characters
    to insert.
  - Corentin suggested we get implementation experience before proceeding and emphasized that option 3
    provides time to do so with the goal of doing better in a future standard.
  - PBindels agreed with restriction to an estimated width of 1 now, but with violations resulting in
    UB so that behavior can be changed later.
  - Victor agreed that PBrett's use case is interesting, but asserted that we should not hand wave a
    solution for it; we should properly explore support for it.
- Tom stated that the next SG16 telecon will be held on 2021-12-15 and will likely revisit LWG3639.
- Tom requested "+1" responses to
  [Corentin's post](https://lists.isocpp.org/sg16/2021/11/2862.php)
  to the SG16 mailing list with updates to his
  [P1854](https://wg21.link/p1854) and [P2361](https://wg21.link/p2361) papers by anyone that feels
  these papers are ready to poll forwarding to EWG.
- \[ Editor's note: such "+1" responses were provided in response to a
  [new post](https://lists.isocpp.org/sg16/2021/12/2888.php). \]


# November 17th, 2021

## Agenda
- [D1854R2: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r2)
  - New revision review.
- [P2361R3: Unevaluated strings](https://wg21.link/p2361r3)
  - New revision review; we last reviewed this proposal during the
    [2021-09-22 telecon](https://github.com/sg16-unicode/sg16-meetings#september-22nd-2021).

## Meeting summary
- Attendees:
  - Aaron Ballman
  - Charlie Barto
  - Corentin Jabot
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- \[ Editor's note: The agenda order was revised to accommodate scheduling conflicts. \]
- [P2361R3: Unevaluated strings](https://wg21.link/p2361r3)
  - Corentin introduced the recent wording changes and noted that the *unevaluated-string*
    production is not matched until after lexing, but is referenced from the wording for the
    preprocessor line control directive and the `_Pragma` operator as a means to impose
    constraints on their *string-literal* elements.
  - Corentin added that, for `asm` declarations, the only change now is to prohibit an
    encoding prefix.
  - PBrett requested confirmation that this represents a design change.
  - Corentin confirmed that it does.
  - PBrett asked what the ramification would be if EWG rejected such a change.
  - Corentin responded that there is no current implementation experience involving `asm`
    declarations that use an encoding prefix.
  - Corentin added that numeric escape sequences are still allowed in `asm` declarations
    but that their effect is unknown.
  - Aaron noted another change from the prior revision that was inspired by implementation
    experience; the paper now addresses user-defined literals (UDLs).
  - Jens observed that the change to the grammar for the preprocessing line control directive
    introduces an allowance for use of raw string literals.
  - Aaron stated this appears to be an oversight.
  - Corentin agreed.
  - Jens stated that use of *string-literal* should be avoided for the preprocessing line
    control directive if the grammar term doesn't apply.
  - Aaron noted that this is a pre-existing issue and asked how it should be repaired.
  - Jens asked how the C standard handles this.
  - Aaron replied that the C standard defines *string-literal* with an optional encoding
    prefix.
  - Corentin stated that the intent was not to enable new syntax, but asked if an allowance
    for raw strings would be problematic.
  - Jens responded that raw strings can contain new lines, but preprocessing directives are
    line based.
  - PBrett noted that such an allowance would introduce a new divergence from C.
  - PBrett observed that the current wording discusses *string-literal*.
  - Jens agreed that there is an existing issue in that the line control wording discusses
    *string-literal* where no such production is used.
  - Jens suggested retaining the current grammar so as to avoid an unintended change in meaning.
  - Corentin agreed to revert the use of *string-literal* in the proposed line control wording
    and to note the existing issue.
  - Jens requested that be included as an editorial note in the wording to ensure CWG considers
    it during wording review.
  - Jens requested that the proposed wording be rebased on the current draft so as to avoid the
    need for updates to \[lex.phases\] and \[lex.string\].
  - Jens requested that "encoding prefix" be styled as a grammar term in \[dcl.asm\].
  - Jens observed that the user-defined literal operator wording also allows use of raw string
    literals.
  - Jens noted that, in \[dcl.link\], the comparison of the recognized language linkages includes
    the quotes thereby requiring that a declaration be written as `extern "\"C\""`.
  - Corentin reported that Hubert also had a concern that it was not stated how to compare the
    literal contents in the wording.
  - Jens noted that *universal-character-names* (UCNs) can appear in an *unevaluated-string*, but
    that it isn't clear with respect to the comparison in \[dcl.link\] when that replacement
    occurs; `"\u0043"` and `"C"` should be handled equivalently.
  - Jens stated that it is unclear why the wording for \[cpp.pragma.op\] has been updated to strike
    handling of escape sequences.
  - Jens admitted a need to translate UCNs for string literals, but noted that doesn't happen here.
  - PBrett observed that doing so could change the meaning of existing code.
  - Jens agreed and noted that restoring handling of escape sequences will achieve the desired
    result; the preprocessing of the destringized string will expand UCNs.
- [D1854R2: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r2)
  - \[ Editor's note: D1854R2 was the active paper under discussion at the telecon.
    The agenda and links used here reference P1854R2 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin provided an introduction.
  - PBrett requested that the abstract be updated to summarize the problem the paper addresses, how it
    is solved, and what the impact is.
  - PBrett suggested that the proposed wording for \[lex.ccon\] consistently state,
    "in the literal's associated character encoding".
  - Corentin responded that there is no need to do so since multicharacter literals are no longer subject
    to use of an encoding prefix; their associated encoding is always the narrow literal encoding.
  - Jens agreed that indirection through an association is not required, but observed that the correct
    encoding is the "ordinary literal encoding", not the "narrow literal encoding".
  - Jens requested that "encoding prefix" be styled as a grammar term.
  - Discussion ensued regarding the goals of the paper and concluded with the following clarifications:
    - The proposal does **not** intend to prohibit a `c-char` from contributing more than one code unit to
      the calculation of a multicharacter literal value.
    - The proposal **does** intend to prevent a character literal from being **unintentionally** parsed as a
      multicharacter literal in visually ambiguous situations.
  - \[ Editor's note: Consider `'é'` in a UTF-8 encoded source file. If the source file is in Normalization
    Form C (NFC; `é` is U+00E9 {LATIN SMALL LETTER E WITH ACUTE}), then the expression would be an ordinary
    character literal. However, if the source file is in Normalization Form D
    (NFD; `é` is U+0065 {LATIN SMALL LETTER E} followed by U+0301 {COMBINING ACUTE ACCENT}), then the
    expression would be a multicharacter literal. The proposal seeks to avoid such visual ambiguity by
    restricting the individual written characters in multicharacter literals to those that only contribute
    a single code unit in the ordinary literal encoding. This suffices to reject the code in the NFD case
    (U+0301 isn't encodeable as a single code unit in any encodings that are used as the ordinary literal
    encoding in practice. \]
  - Corentin agreed to remove the restriction on UCNs from the wording added to the first paragraph of
    \[lex.ccon\] since use of a UCN does not produce visual ambiguity.
  - \[ Editor's note: Thus, the NFD case above can be explicitly written as `'e\u0301'`. \]
- Tom announced that the next telecon will be held on 2021-12-01 and that the agenda will include
  LWG3639 (Handling of fill character width is underspecified in std::format) and further review of
  P2361 and P1854 pending the availability of new revisions.


# November 3rd, 2021

## Agenda
- [D2071R1: Named universal character escapes](https://lists.isocpp.org/sg16/att-2805/d2071r1.html)
  - Continue review pending a revision update.
- [P1854R1: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r1)
  - New revision review.
- [P2361R3: Unevaluated strings](https://wg21.link/p2361r3)
  - New revision review; we last reviewed this proposal during the
    [2021-09-22 telecon](https://github.com/sg16-unicode/sg16-meetings#september-22nd-2021).

## Meeting summary
- Attendees:
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [D2071R1: Named universal character escapes](https://lists.isocpp.org/sg16/att-2805/d2071r1.html):
  - Tom noted that green highlight is missing in the wording for the feature test macro.
  - Jens stated that the Unicode standard divides name aliases into five types named
    *correction*, *control*, *alternate*, *figment*, and *abbreviation*, but that ISO 10646
    doesn't reflect this partitioning.
  - Steve reported that the aliases described in ISO 10646 appear to be mechanically produced from
    the Unicode standard's
    [NamesList.txt](https://www.unicode.org/Public/UCD/latest/ucd/NamesList.txt)
    file.
  - Steve noted that the names in
    [NamesList.txt](https://www.unicode.org/Public/UCD/latest/ucd/NamesList.txt)
    are distinguishable elsewhere in the Unicode DB which is why they are listed in capital letters
    in ISO 10646; additional names are listed in
    [NameAliases.txt](https://www.unicode.org/Public/UCD/latest/ucd/NameAliases.txt).
  - Jens stated that the ISO 10646 PDF does not retain some information from the Unicode files; for
    example, ISO 10646 specifies "NO BREAK HERE" as an informative alias for character code point
    0083, but omits the "NBH" abbreviation specified in
    [NameAliases.txt](https://www.unicode.org/Public/UCD/latest/ucd/NameAliases.txt).
  - \[ Editor's note: The aliases present for character code point 0083 in the Unicode names files are:

        NamesList.txt: "NO BREAK HERE"
        NameAliases.txt: "NO BREAK HERE" (control)
        NameAliases.txt: "NBH" (abbreviation)
      ISO/IEC 10646:2020 contains (the "=" introducer indicates an informative alias):

        <control>
        = NO BREAK HERE
    \]
  - Steve suggested that it may be necessary to refer to the Unicode standard for name aliases.
  - PBrett asked what the process would be for requesting changes to the ISO 10646 standard.
  - Jens replied that the process is the same for any ISO standard; contact the project editor.
  - Hubert suggested that an NB representative could provide contacts for filing an issue with ISO 10646.
  - Jens stated that the paper does not make it clear which Unicode name aliases are intended to be
    usable in these escape sequences.
  - Steve stated that ISO 10646 retains some of the Unicode name alias types as normative aliases,
    but that the rest are informative.
  - Steve added that the intended usable names from ISO 10646 are the
    *associated character name* and each *character name alias* preceded by ※.
  - \[ Editor's note: See ISO/IEC 10646:2020 section 34.3, "Character names list". It is currently
    assumed, but has not been verified, that the normative name aliases (those preceded by ※) correspond
    to the aliases present in NameAliases.txt with type *correction*. \]
  - Steve asked if there is an expectation to be able to use the name aliases listed in NameAliases.txt
    with type *control* since the relevant characters do not otherwise have an associated character name.
  - \[ Editor's note: All control characters are listed in NamesList.txt with "\<control\>" as the
    associated character name. \]
  - PBrett replied that names for some control characters already appear in the standard and provided
    "LINE FEED", "SPACE", and "BELL" as examples.
  - Jens noted that "SPACE" matches a normative name in ISO 10646, but that the others are problematic;
    "LINE FEED" is not present though "LINE FEED (LF)" is present as an informative alias, and "BELL" is
    only present as an informative alias.
  - Steve observed that the desired name for control characters might be the first alias listed in ISO 10646.
  - Steve asserted that the Unicode *alternate*, *figment*, and *abbreviation* alias types are not stable.
  - Tom observed that ISO 10646 appears to combine the Unicode control and abbreviation names to produce
    informative aliases like "LINE FEED (LF)", "new line (NL)", and "end of line (EOL)" and noted the
    inconsistent use of case.
  - Steve directed the group to the contents of
    [NamesList.txt](https://www.unicode.org/Public/UCD/latest/ucd/NamesList.txt).
  - Jens reported that the names listed in NamesList.txt match those in ISO 10646; it contains the same
    "LINE FEED (LF)", "new line (NL)", and "end of line (EOL)" aliases noted earlier.
  - Steve suggested that NamesList.txt may be parseable; an EBNF specification is present in
    [Unicode® NamesList File Format](http://www.unicode.org/Public/UNIDATA/NamesList.html).
  - Tom discovered that section 12 of ISO/IEC 10646:2020 has a list of names for control characters.
  - Jens observed that those names are present in a note and are therefore not normative.
  - Jens noted that these discoveries indicate that some of the names currently being used in the C++
    standard are not correct; "FORM FEED" should be used instead of "FORM FEED (FF)".
  - PBrett asked if the note in ISO 10646 can be normatively referenced from the standard.
  - Jens replied that a note can be added that matches the note in ISO 10646 for control names.
  - Tom noted that ISO/IEC 10646:2020 section 7.4 contains a reference to NamesList.txt; that introduces
    the possibility of referring to it via ISO 10646.
  - Jens stated that the desired names from ISO 10646 are the *associated character name* and
    *character name aliases* names.
  - Tom asked if the issue with missing names is limited to control characters.
  - Steve replied that it is.
  - PBrett volunteered to take care of getting an issue filed with ISO 10646 so long as someone is
    available to help define the concern.
  - Hubert asked what names other languages support.
  - Steve replied that he would research further.
  - Tom suggested that we should check what names the existing C++ implementations in Clang and Circle
    are actually using; those implementations may need refinement.
  - Steve replied that both use Corentin's name lookup implementation from
    https://github.com/cor3ntin/ext-unicode-db/tree/name_to_cp.
  - Discussion turned to other specification concerns.
  - Jens expressed concern about the standard having a floating reference to ISO 10646 and explained
    that this is problematic in this case since publication of a new ISO 10646 edition that contains
    new names would immediately render all implementations non-conforming.
  - Steve responded that the standard needs to specify a minimum ISO 10646 edition.
  - Jens agreed.
  - PBrett asked if the adoption of
    [P1949 (C++ Identifier Syntax using Unicode Standard Annex 31)](https://wg21.link/p1949)
    has this same issue since the introduction of new characters potentially makes new identifiers
    possible.
  - Steve replied that identifiers are at least guaranteed to be stable.
  - Tom replied that the character names and name aliases we want are likewise guaranteed to be stable.
  - Steve reported that there was originally a desire for a floating reference so that implementations
    could adopt newer ISO 10646 editions than is specified.
  - Jens confirmed that specifying a minimum edition with allowance for implementations to support
    newer editions is needed and possible thanks to stability guarantees.
  - Tom stated that, given that the paper is in line with prior guidance from both SG16 and EWG and that
    EWG is already scheduled to discuss the new revision on 2021-11-10, that he believes consensus for
    the revision exists in SG16 and that no further polls are needed.
  - Tom asked for dissenting concerns.
  - No such concerns were raised.
- [P1854R1: Conversion to literal encoding should not lead to loss of meaning](https://wg21.link/p1854r1):
  - Hubert suggested that the paper title should be changed to reflect the change the paper actually proposes.
  - Tom asked if Hubert would be willing to submit that feedback to the mailing list and the author.
  - Hubert agreed to do so.
  - \[ Editor's note: Hubert did so; the relevant email thread is archived at
    https://lists.isocpp.org/sg16/2021/11/2809.php. \]
- [P2361R3: Unevaluated strings](https://wg21.link/p2361r3):
  - No discussion due to lack of time.
- Tom stated that the next telecon will be 2021-11-17 and will continue discussion of P1854R1 and P2361R3.

  
# October 20th, 2021

## Agenda
- D2071R1: Named universal character escapes
  - Add named escape sequences to *universal-character-name* so that these escape sequences can be
    used everywhere, not just in string literals.
  - Use Unicode rules for matching names rather than requiring exact case-sensitive names.
- [P1885R8: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r8)
  - Continue discussions of issues raised on the LEWG and SG16 mailing lists.
  - Prohibit mapping to IANA encodings when `CHAR_BIT` is not 8?
  - Address special cases for IANA mapping purposes:
    - Is UTF-16 valid for ordinary strings when `CHAR_BIT` is >= 16?
    - Is UTF-16 valid for wide strings when `CHAR_BIT` is >= 16 and `sizeof(wchar_t)` is 1?
    - Is the underlying representation of a wide string required to match an encoding scheme for the
      encoding form when `sizeof(wchar_t)` is not 1?
    - Limit mapping of wide strings when `sizeof(wchar_t)` is not 1 to `other`, `unknown`, and the
      UCS/UTF variants?

## Meeting summary
- Attendees:
  - Charlie Barto
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- D2071R1: Named universal character escapes
  - Steve presented:
    - The most significant change is to make `\N{...}` a *universal-character-name* (UCN); this maintains
      consistency with the recent addition of `\u{...}` proposed in
      [P2290 (Delimited escape sequences)](https://wg21.link/p2290).
    - Implementation experience exists with both Clang and Circle.
    - Both implementations use Corentin's name lookup code.
    - \[ Editor's note: That code is presumably from Corentin's ext-unicode-db repository available at
      https://github.com/cor3ntin/ext-unicode-db/tree/name_to_cp. \]
    - Sean Baxter reported a 272K increase in the size of the Circle compiler binary following implementation.
    - EWG requested exact name matching.
    - Unicode recommends loose matching.
    - \[ Editor's note: where can one find a citation for this recommendation? \]
  - PBrett noted that the paper does not include the rationale for EWG's prior preferences.
  - Hubert stated that
    [P2290 (Delimited escape sequences)](https://wg21.link/p2290)
    was discussed in WG14 and noted feedback that curly braces are problematic on EBCDIC systems; though
    these characters are represented in all EBCDIC code pages customarily used for source code, these
    characters are not encoded the same way in all such code pages.
  - PBrett asked if a replacement syntax would be necessary.
  - Hubert replied that an additional syntax would suffice.
  - PBrett asked if multiple syntaxes is desirable.
  - Jens replied negatively.
  - Hubert noted that digraphs can't be used within string literals and that C++ removed support for
    trigraphs.
  - PBrett asked if there is experience in other languages using parenthesis, or perhaps both curly braces
    and parenthesis.
  - PBrett noted that all implementations will be required to support UTF-8 in C++23.
  - Hubert acknowledged the UTF-8 requirement and noted that UTF-8 support is useful for source transfer
    but not so much for native editing since local editors may not support it.
  - PBrett observed that an alternate escape syntax could be used in non-UTF-8 encoded source code.
  - Hubert acknowledged, but stated that doing so compromises readability.
  - Mark asked from chat: "how did format solve this?"
  - Hubert responded that `std::format()` is another such problematic case, though even more problematic
    because of the requirement to process the string according to the literal encoding.
  - PBrett noted that, if multiple syntaxes are supported, then people will use what they are most familiar
    with, probably curly braces due to use in other languages, and end up with non-portable code anyway.
  - PBrett opined that supporting a single syntax is the preferred trade off.
  - Hubert agreed that, if only one syntax is supported, that it should use curly braces.
  - Hubert stated that he was raising the issue because there are programmers that expect code
    to "just work" even when there are subtle mojibake issues.
  - Zach was relieved that there was not a request for a syntax that used only parenthesis.
  - Zach commented that we constantly struggle with available syntax, so we should not consume more than
    is necessary.
  - Jens opined that curly braces are members of the basic character set and used in strings elsewhere,
    so spending extra effort in this case seems unwarranted.
  - Jens requested that the paper be updated to note the concern.
  - Hubert noted that, in other cases of curly braces in string literals, other escape sequences can be used;
    that isn't an option for UCNs in string literals though.
  - Jens acknowledged and added that UCNs are also restricted to specifying characters that are not members
    of the basic character set outside of literals.
  - Jens suggested that the escape hatch is to not use this feature.
  - Tom noted that IBM can continue to use trigraphs.
  - Jens agreed with the added observation that such use makes the code non-portable.
  - **Poll 1: We should support both `\u{xxxx}` and `\u(xxxx)` (resp. `\N{ABCD}` and `\N(ABCD)`)
    for better support on EBCDIC systems and others where `{` and `}` are not consistently encoded
    in the character sets customarily used for source code.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   0 |   2 |   4 |   2 |
      
    - Consensus against.
  - Hubert requested that the SG16 chair inform the SG22 chair of this poll result for its
    relation to
    [P2290 (Delimited escape sequences)](https://wg21.link/p2290)
    and the corresponding proposal for WG14.
  - Jens requested that multiple wording options not be present in the paper going forward.
  - Steve stated that there are two remaining issues to poll, use of the
    UAX44-LM2 name matching algorithm and named escape sequences as UCNs.
  - Discussion turned to loose name matching.
  - Zach commented that code searches become more complicated when loose matching is allowed.
  - Jens stated that strong rationale is needed to justify a change of EWG's prior position.
  - Tom shared slides presented in Belfast that may have influenced EWG's position on loose
    matching.
  - \[ Editor's note: those slides illustrated that matching would succeed with cases like:

        ”\N{NOBREAKSPACE}”
        ”\N{NO BREAK SPACE}”
        ”\N{NO_BREAK_SPACE}”
        ”\N{NO-B_R-E-A_K-S P A C E}”
    \]
  - **Poll 2: Despite previous EWG feedback, we recommend the use of the UAX44-LM2 name
    matching algorithm.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   3 |   3 |   1 |   1 |
      
    - No consensus.
    - SA: I want to be able to easily grep for names; most other languages don't support
      loose matching.
  - Steve stated that he will change the paper to remove the recommendation for UAX44-LM2.
  - Tom interpreted this poll result as indicating that the compiler size concerns are
    not motivating.
  - Discussion turned to named escape sequences as UCNs.
  - Hubert noted that specifying named escapes as a form of UCN raises the issue that formation
    of a UCN via token pasting results in UB.
  - **Poll 3: Named escape sequences should be specified in the language as an alternative
    form of universal-character-name.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   5 |   3 |   0 |   0 |   0 |
      
    - Strong consensus in favor.
  - Tom requested that any wording review feedback be sent to the mailing list in advance of
    the next telecon.
- [P1885R8: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r8)
  - PBrett introduced the topics for discussion:
    - Whether the encoding querying functions should return `unknown` when `CHAR_BIT` is not 8.
    - How to handle wide strings for various values of `sizeof(wchar_t)` and `CHAR_BIT`.
  - Hubert suggested that decisions regarding how to handle `CHAR_BIT` when it is not 8 may have to
    be deferred to SG14 for embedded implementations.
  - Zach stated that `sizeof(wchar_t)==1` is problematic when `CHAR_BIT` is 8.
  - PBrett replied that there is a proposal to lift the restriction that currently requires that
    `wchar_t` be able to represent all characters of all implementation supported character sets;
    [P2460 (Relax requirements on wchar_t to match existing practices)](https://wg21.link/p2460).
  - Jens noted that we have discussed encoding schemes in the context of `wide_literal()` and that
    BE/LE appropriate results would be expected in that case, but we currently have consensus for
    a native endian result with no BOM semantics.
  - Jens raised a consistency concern; the paper currently erases the encoding endianness information
    for the UTF cases, but not for the UCS cases.
  - Jens stated that there are questions about wide-EBCDIC and endianness, but that those encodings
    don't currently exist in the IANA registry.
  - Jens noted that, at present, the only permissible IANA registered wide encodings when
    `sizeof(wchar_t)` is not 1 are UTF-16, UTF-32, UCS-2, and UCS-4.
  - PBrett asked Charlie for his impression of what the impact would be of returning UTF-16BE on
    Windows assuming a bigendian platform.
  - Charlie responded that Windows doesn't support any bigendian platforms, so it wouldn't matter
    right now; Windows programmers just assume UTF-16LE.
  - PBrett expressed concern about unexpected encoding names being returned and compared using
    other APIs.
  - Hubert observed that programmers may, or may not, want to see UTF-32LE vs UTF-32BE be returned
    for one Linux system vs another.
  - Steve raised the concern of a program externalizing an encoding name as UTF-16 and then providing
    UTF-16LE text instead of (the expected default of) UTF-16BE.
  - Steve mentioned in chat: "UTF-16 generally is supposed to imply BE. In practice it doesn't but,
    that's an inconsistency."
  - Charlie asked in chat: "isn't that just because the network byte order is BE?"
  - Jens replied in chat: "Steve: No. ISO 10646 encoding scheme "UTF-16" says
    "interpret BOM; if none is found, use big-endian"."
  - Jens continued in chat: "Steve: iconv does "interpret BOM; if none is found, use host endianness"."
  - Tom observed that, in the standard, the wording for string literals is written in terms of
    code units and encoding form and expressed a belief that programmers tend to work on code units
    rather than bytes; except for interfaces like `iconv()`.
  - Jens replied that previous polls supported an encoding scheme approach in order to support the
  - `iconv()` use case.
  - Jens stated that switching to encoding form would be a no-op for ordinary strings.
  - Jens added that concern about object representation seems wrong since it is so implementation specific.
  - PBrett expressed a desire to work with bytes and that object representation therefore matters for
    wide strings.
  - Hubert acknowledged the present inconsistency and noted the friction with encoding scheme.
  - Charlie stated that it is difficult to conceive of cases where the object representation encoding
    would differ from the native encoding.
  - Jens noted that proper byte access would currently require querying native endianness when presented
    with UTF-16; if the special case for UTF-16 were to be dropped, then behavior would be consistent.
  - Tom noted the benefit of being able to use UTF-16BE on little endian systems for encoding tagging purposes.
  - Jens observed that friction could be reduced by dropping support for wide strings.
  - Tom stated that we should re-poll the special case for UTF-16.
- Tom stated that the next telecon will be November 3rd and that we will plan to poll the special case
  for UTF-16 for P1885, and possibly look at updated wording for P2071.
- \[ Editor's note: since LEWG will be preceding with electronic polling of P1885R9 as is, SG16 will table
  further discussion of that proposal pending a new paper that argues for changes. \]


# October 6th, 2021

## Agenda
- [D2460R0: Relax requirements on wchar_t to match existing practices](https://wg21.link/p2460r0)
- [D1885R8: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r8)
  - Discuss and poll issues recently raised on the LEWG and SG16 mailing lists.

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [D2460R0: Relax requirements on wchar_t to match existing practices](https://wg21.link/p2460r0)
  - \[ Editor's note: D2460R0 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2460R0 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin presented:
    - Writing this paper was necessary to make progress on P1885.
    - The standard has been out of sync with at least one major implementation for many years.
    - The proposed wording transitions prior core language requirements to library preconditions.
  - PBrett commented that maintaining preconditions in the library wording seems correct, but that the
    wording should be changed to introduce library UB for characters that are not encodeable in a
    single code unit.
  - Corentin replied with a desire to agree on the design first and then address wording.
  - Hubert objected to the original paper title ("UTF-16 is standard practice") since UCS-2 is also
    non-conforming when used as the execution wide-character set if the execution character set
    contains more characters as happens when UTF-8 is the execution encoding.
  - Hubert agreed with the direction that PBrett suggested.
  - PBrett summarized; the direction is good, some refinement is needed, and some prose is needed to
    explain why claiming UCS-2 instead of UTF-16 does not suffice to avoid issues.
  - Jens and Hubert clarified that the prose should make it clear that the changes also allow use of
    UCS-2 when, e.g., UTF-8 is used as the execution encoding.
  - PBrett asserted that the prose should explain how the wording change accomplishes the goals of
    the paper.
  - PBrett asked if there is an existing core issue for concerns addressed by the paper.
  - Corentin replied that he was unable to find one.
  - Mark verified that there are no active CWG issues that mention UCS-2 or UTF-16.
  - **Poll 1: Add expanded motivation to D2460R0 and forward the paper so revised to EWG
    with a recommended ship vehicle of C++23.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   5 |   3 |   1 |   0 |   0 |
      
    - Strong consensus in favor.
  - Hubert asked if a feature test macro is warranted and noted the existence of `__STDC_MB_MIGHT_NEQ_WC__`.
  - PBrett suggested that SG10 (the feature test study group) review the need for a macro.
  - Tom noted that LEWG should review the paper since it adds library UB where none was possible
    previously.
  - Tom asked if anyone felt the need to review a revision of this paper in SG16 again.
  - No such desires were raised.
  - Corentin indicated that he will start a mailing list discussion for LEWG.
- [D1885R8: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r8)
  - \[ Editor's note: D1885R8 was the active paper under discussion at the telecon.
    The agenda and links used here reference P1885R8 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin presented:
    - The paper goals are limited to tagging known encodings used for interchange, not every possible
      encoding.
    - There is considerable history, some of it contradictory, mistakes have been made.
    - There are multiple encoding kinds; fixed width vs variable width, single byte vs double byte.
    - Wide interfaces are provided mostly for consistency with `char`-based interfaces.
    - There are few wide character encodings.
  - Hubert disputed the statement that there are few wide character encodings and indicated there are at
    least as many wide encoding variants as there are ISO-8859 variants.
  - Corentin expressed a desire for more information.
  - Hubert replied that, for every IBM documented CCSID encoding, there is one two byte and one four byte
    encoding; the narrow encoding is the odd one that uses a shift-state encoding.
  - Hubert noted that documentation is written in terms of character sets that are trivially encoded;
    encoding schemes are therefore not explicitly documented.
  - Tom recommended IBM's "Character Data Representation Architecture" documentation.
  - \[ Editor's note: Hubert later posted links to related IBM documentation to the SG16 mailing list in
    an email thread sith subject, "Structure of EBCDIC MBCS and wide EBCDIC"; an archive of that message
    thread is available at
    https://lists.isocpp.org/sg16/2021/10/2719.php. \]
  - Hubert noted that he usually consults ICU's converter explorer rather than IBM documentation.
  - \[ Editor's note: ICU's converter explorer is available at
    https://icu4c-demos.unicode.org/icu-bin/convexp. \]
  - Hubert noted that, for `iconv()`, use of the UTF-16 encoding results in BOMs being produced and
    consumed.
  - Jens presented:
    - An octet is not the same as a byte.
    - The cncoding form concept is applicable to non-Unicode encodings.
    - An encoding scheme encodes the output of an encoding form into a series of octets.
    - The "UTF-16" identifier is ambiguous because it may refer to either the encoding form or the
      encoding scheme.
    - The IANA registry specifies encoding schemes.
  - Tom asked if the use case presented for `iconv()` has defined behavior since it involves writing
    to objects of type `wchar_t` using pointers to `\[unsigned\] char`.
  - PBrett responded that objects of type `wchar_t` can be allocated and then passed to `iconv()` to
    read or write them.
  - Corentin asserted that the encoding form concept is not useful for users.
  - Tom stated that he remains unclear with regard to behavior for, e.g., UTF-16 in `char` when
    `CHAR_BIT` is 16.
  - Hubert replied that we take the hand wavy approach and avoid BOMs.
  - Zach stated that, as long as the encoding matches the bits produced, that he is satisfied; there
    needs to be a 1x1 corespondence between bytes.
  - Jens asserted that UTF-16LE or UTF-16BE should be returned.
  - PBrett replied that programmers won't expect that.
  - Tom suggested that we decide the behavior we want, and then make the wording match that.
  - Jens noted the desire to return UTF-16, but that the definitions in our normative references don't
    permit that.
  - **Poll 2: The values returned by the `literal()` and `wide_literal()` functions must indicate
    the encoding scheme associated with the object representation of ordinary and wide string
    literals respectively; UTF-16 & UTF-32 are interpreted as having native endianness, and the
    LE and BE forms are never returned.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   6 |   0 |   0 |   0 |
      
    - Strong consensus in favor.
  - **Poll 3: Notwithstanding the specification in ISO10646, we suggest to return UTF-{16,32}
    from `literal()` or `wide_literal()` with the understanding that string literals in the
    compiled program may not actually begin with a BOM and that library facilities
    \[e.g. `iconv()`\] may consume a BOM if present.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   8 |   1 |   0 |   0 |
      
    - Strong consensus in favor.
  - **Poll 4: Forward P1885 as revised to incorporate SG-16 feedback on object representation
    interpretation to LEWG with a recommended ship vehicle of C++23.**
    - Attendance: 8
    - No objection to unanimous consent.
- Tom stated that the next telecon will be October 20th.

  
# September 22nd, 2021

## Agenda
- [D2348R2: Whitespaces Wording Revamp](https://wg21.link/p2348r2)
- [P1636R2: Formatters for library types](https://wg21.link/p1636r2)
- [P2361R2: Unevaluated strings](https://wg21.link/p2361r2)

## Meeting summary
- Attendees:
  - Aaron Ballman
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Marina Oliveira
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Tomasz Kamiński
  - Victor Zverovich
- [D2348R2: Whitespaces Wording Revamp](https://wg21.link/p2348r2)
  - \[ Editor's note: D2348R2 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2348R2 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin stated that there are no design change between the R1 and R2 revisions.
  - Tom asked for confirmation that the only known behavioral change is that the VT and FF characters
    would be well-formed in comments rather than ill-formed no diagnostic required.
  - Hubert responded that the proposal also expands the set of allowed horizontal space characters
    in preprocessing directives.
  - Aaron asked if there is desire to recommend the proposal as a DR.
  - PBrett responded that there is no need to do so since the changes are effectively specification
    improvement.
  - Tom asked Hubert if all of the concerns he had raised on the mailing list have been addressed to
    his satisfaction?
  - Hubert responded that they have been.
  - **Poll 1: Forward D2348R2 to EWG as the recommended resolution of CWG2002 and CWG1655 and with
    a recommended ship vehicle of C++23.**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   6 |   1 |   0 |   0 |
      
    - Strong consensus in favor.
- [P1636R2: Formatters for library types](https://wg21.link/p1636r2)
  - PBrett stated that SG16 is reviewing this paper due to concerns Tomasz raised regarding
    quoting and localization in the formatting of `std::filesystem::path`.
  - Victor stated that we currently lack the tools to adequately address these concerns now.
  - Victor recommended removing support for `std::filesystem::path` from the paper for now.
  - Victor noted that planned range related enhancements will enable the desired quoting support.
  - PBrett observed that, if explicit support for `std::filesystem::path` is removed, then objects
    of that type will end up getting formatted as a comma separated list since it models a range.
  - Victor reported plans in place elsewhere to reject use of `std::filesystem::path` as a range.
  - PBrett noted that information can be lost when formatting a path as text.
  - Victor replied that transcoding is possible and that a quoted escape mechanism could be used for
    portions of a path that would not round trip through a transcoder losslessly.
  - Victor noted that use of the classic locale is a red herring as it has no effect on the output.
  - Tomasz noted the existence of two papers that overlap on these design questions.
  - Corentin expressed agreement with Victor that support should wait until there is an escaping
    mechanism available to losslessly preserve path contentss in formatted text.
  - Charlie noted that there may be cases where replacement characters might be preferred over of
    of an escaping mechanism that might interfere with further processing of the output.
  - Charlie cautioned against including `<format>` in lots of standard library headers since doing
    so could result in ABI problems if formatter templates are separately compiled.
  - Victor opined that `std::format` is effectively a generalized `to_string()` and that every type
    should be formattable.
  - PBindels noted that platform specific knowledge may be required to format paths.
  - Charlie remarked that confusion between the literal encoding and the system code page remain
    possible.
  - Charlie noted that Java has the benefit of only needing to compile the code that implements
    its string type once, but that C++ must do so for every TU that uses it.
  - Charlie added that, for Microsoft's implementation, the `<thread>` header includes `<format>`
    for chrono support.
  - Tomasz remarked that it is strange that including `<thread>` results in portions of `<format>`
    being included, but noted that the standard doesn't require that direct inclusion and that
    implementations should avoid it.
  - Charlie responded that `<thread>` including `<format>` is a quality of implementation issue,
    but noted that, for formatters, an extern template would be required. However, for
    `std::format`, the first argument is the format context and it probably can't be declared
    as an extern template.
  - PBindels asked why a platform wouldn't know what encoding is used by the filesystem.
  - Charlie responded that file names don't necessarily have an explicitly associated encoding.
  - Tom added that a path may have multiple associated encodings if it spans filesystems.
  - Charlie further added that additional problems occur with network filesystems that substitute
    characters for reserved character like `:` on Windows.
  - PBrett stated that, if the literal encoding is UTF-8, then the associated encoding of
    `std::string` is nominally UTF-8 and that the `string()` and `u8string()` members of
    `std::filesystem::path` should return the same content.
  - Victor responded that, on Windows, the `string()` member of `std::filesystem::path` returns
    a string encoded according to the system code page.
  - PBrett asked if a similar concern exists for `wchar_t`.
  - Steve responded affirmatively; Windows paths are a sequence of 16-bit code units, not UTF-16.
  - PBrett suggested a solution like the one adopted for locale dependent chrono fields; if the
    literal encoding is a UTF, then implementations can convert as best they know how.
  - Victor responded that the same resolution can be used and is simpler because
    `std::filesystem::path` already offers the necessary encoding conversion functionality.
  - PBrett presented a poll option that specifed conversion in terms of
    [[fs.path.fmt.cvt]](http://eel.is/c++draft/fs.path.fmt.cvt).
  - Charlie strongly agreed that formatting as if by the `u8string()` member of `std::filesystem::path`
    is the right thing to do.
  - Victor expressed a preference for a solution that preserves all information.
  - Tom proposed considering solutions from a text vs binary perspective with a goal to preserve
    binary representation so as to avoid data loss; programmers can perform conversion to text
    with their own preferred substitution when desired.
  - Victor agreed and noted a desire for a solution that maintains round tripping.
  - Tomasz suggested the possibility of multiple formatting options.
  - Charlie noted that use of an escape mechanism would solve the problem of conversions between
    libraries that work in narrow vs wide characters.
  - PBrett opined that it sounds like we need an actual proposal for how to format paths.
  - PBrett repeated the earlier advice to remove support for `std::filesystem::path` from the paper
    and encouraged the creation of a new proposal to support it before
    [P2286](https://wg21.link/p2286) is adopted.
  - Tomasz stated there is no urgency so long as
    [P2286](https://wg21.link/p2286) precludes handling `std::filesystem::path` as a range.
  - **Poll 1: Recommend removing the filesystem::path formatter from P1636 "Formatters for library types",
    and specifically disabling filesystem::path formatting in P2286 "Formatting ranges", pending a proposal
    with specific design for how to format paths properly.**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   5 |   5 |   1 |   0 |   0 |
      
    - Strong consensus in favor.
  - PBrett asked for a volunteer to write the suggested paper.
  - Victor volunteered.
  - PBrett volunteered to help with wording.
  - Mark asked rhetorically if solving the escaping problem also solves the unescaping problem.
- [P2361R2: Unevaluated strings](https://wg21.link/p2361r2)
  - Corentin presented:
    - Previously, all string literals were converted to the literal encoding in translation phase 5
      whether they corresponded to lexical strings or string literal objects.
    - The goal is to prohibit numeric escape sequences and conditional escape sequences in lexical
      strings, but not in string literals that initialize string literal objects. 
    - Support for UCNs and other character escapes is retained for all string literals.
    - There is currently implementation divergence regarding when encoding prefixes are or are not
      allowed.
  - Jens noted that the list of unevaluated string literals is missing the literal operator ID case.
  - Jens stated that, following [P2314](https://wg21.link/p2314), conversion and addition of a null
    character is now performed during translation phase 7.
  - Hubert noted that other proposals are changing nearby wording and that a rebase will likely be needed.
  - Hubert observed that wording is missing with regard to how to compare strings in cases for `extern "C"`.
  - Corentin replied that he will update the wording.
  - Hubert noted that the wording will need to address cases like `extern "\u0043"`.
  - Corentin acknowledged that the proposed wording will need some updates.
  - Corentin added that SG22 will review the paper soon and that he would like to target C++23.
  - Jens identified a grammar ambiguity; *unevaluated-string* and *string-literal* both match *s-char-sequence*.
  - Hubert noted that a similar case occurs with *header-name*.
  - Jens replied that the *header-name* case can be disambiguated by a preceding `#include` but that
    the preprocessor cannot disambiguate *unevaluated-string* and *string-literal* in, e.g., `static_assert()`.
  - Corentin replied that he'll find a way to address this without modifying the grammar.
  - Jens suggested retaining *string-literal* as the lexical term and then handling the different cases
    where the uses diverge.
  - Hubert stated that there are non-diagnostic concerns; for example with `asm` statements.
  - Corentin replied that an implementation can do whatever it likes with `asm` strings, such as passing
    them to an external assembler; the standard doesn't have to address such cases.
  - Hubert responded that the proposed change does reduce what the programmer can express, but that an
    implementation could, for example, do something different with an encoding prefix, issue a warning,
    and continue.
  - Hubert noted that following the introduction of `char8_t`, `u8""` string literals may no be accepted
    in some contexts they previously were.
  - Jens remarked that, for string literals, there is a distinct place where encoding conversion is
    specified; when initializing a string object.  For unevaluated string literals, there is no single
    location.
  - Corentin replied that he would work with Aaron to identify a wording solution.
  - PBindels asked if the proposal should be recommended as a DR.
  - Corentin stated no opinion on the matter.
  - Aaron replied that consideration as a DR is questionable.
  - PBindels clarified that doing so could make the life of an implementor easier by avoiding any need
    to fix conformance issues with rejection of encoding prefixes in earlier standard conformance modes.
  - **Poll 3: Acknowledging that we have limited time available, we support the direction for P2361R2
    and encourage further work.**
    - Attendance: 12

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   6 |   5 |   0 |   0 |   0 |
      
    - Strong consensus in favor.
- Tom announced that the next meeting will be on October 13th.
- \[ Editor's note: The next meeting ended up getting moved to October 6th due to scheduling conflicts. \]


# September 8th, 2021

## Agenda
- [D2348R1: Whitespaces Wording Revamp](https://isocpp.org/files/papers/D2348R1.pdf)
- [P2093R8: Formatted output](https://wg21.link/p2093r8)
- [P2361R2: Unevaluated string literals](https://wg21.link/p2361r2)

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Tom: Thank you to Peter and Steve for filling in during my absence.
- PBrett: Consensus from the polls taken during the last telecon held 
2021-08-25 and as posted to the mailing list are no longer tentative; no 
new dissenting opinions were raised.
- [D2348R1: Whitespaces Wording Revamp](https://isocpp.org/files/papers/D2348R1.pdf)
  - Corentin: Introduction:
    - Reversed prior intention to classify vertical tab and form feed
      as new lines.
    - Rebased on top of [P2314R2: Character sets and encodings](https://wg21.link/p2314r2).
    - Would like feedback about support for `\n\r` sequences; support can 
      be provided under implementat-defined behavior.
    - Jonathan Wakely would prefer not to use grammar terms in prose, 
      but unsure how to do that; perhaps Jens can advise.
    - Removed the restriction that non-space characters following a 
      vertical tab and form feed in a single-line comment render the code 
      ill-formed, no diagnostic required; addresses
      [CWG2002: Whitespace within preprocessing directives](https://wg21.link/cwg2002).
  - PBrett: The goal for now is that the wording reflect the design, it 
    doesn't need to be perfect.
  - Jens: In the new section \[lex.whitespaces\] there is a 
    horizontal-whitespace that has infinite recursion.
  - Corentin: The intent is to support a sequence of whitespace.
  - Jens: There is a general rule that we use a separate production for 
    sequences of characters.
  - Tom: *h-char-sequence* is such an example.
  - Jens: Yes, and *q-char-sequence*.
  - Jens: The lexical specification for *comment* is problematic due to 
    max munch; nothing prohibits `*/` appearing in the comment.  Something 
    is needed to address the intent previously expressed in the removed prose.
  - Jens: In the specification of *d-char*, line-break is not a single 
    character; it may be a sequence and therefore doesn't work following 
    "except".
  - Jens: *basic-s-char* has the same issue.
  - PBrett: Can we use a sequence of *line-break* characters?
  - Jens: No; order matters.
  - Jens: \[lex.pptoken\] hits a conflict between the requirement to 
    capitalize the first word of a sentence and sentences that start with a 
    grammar term; capitalizing the grammar term yields a different term, so 
    the prose must be modified to avoid grammar terms at the beginning of a 
    sentence.
  - Jens: Perhaps we should introduce a formal definition of *new-line* 
    to map to the grammar term.
  - Jens: There is a general substitution of the *line-break* grammar 
    term for *new-line* in the proposed wording.  Can we use *new-line* as the 
    grammar term and not introduce a *line-break* production?
  - Corentin: There is a desire to be able to discuss *new-line* 
    abstractly, like in simple escape sequences.
  - Jens: I'm wondering if we can avoid that in order to reduce the 
    wording churn.
  - Jens: P2314 intentionally did not touch *new-line*; it does update 
    places where a single new-line character is designated; like for simple 
    escape sequence.
  - PBrett: Other than for churn; is there motivation to avoid 
    replacing *new-line* with the grammar term?
  - Jens: Yes, the changes remove a definition for *new-line* which we 
    assume is needed by library, though I would be happy to be proven wrong.
  - Corentin: Library use of *new-line* must refer to the single Unicode 
    new-line character.
  - Jens: If *new-line* always designates Unicode new-line, then we can 
    keep *new-line* and use *line-break* for the grammar term.
  - Steve: Time format spec supports a `%n` for new-line character.
  - Jens: Could say it is equivalent to `\n`.
  - Jens: There may be interaction with references to the C standard 
    library.
  - Corentin: C uses "new-line" as a grammar and library term.
  - **Poll 1: Prefer to use the term *new-line* rather than *line-break* in the whitespace grammar production.**
    - Attendance: 10

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   0 |   4 |   3 |   1 |
      
    - No consensus for a change.
  - Hubert: With respect to EWG impact; the changes remove a 
    diagnosable issue involving vertical tab and form feed in preprocessor 
    directives.
  - Jens: That means we're removing a restriction and that is 
    evolutionary; the changes to [cpp.pre] on page 12 of the paper removes 
    the restriction.
  - Corentin: There is no place in the grammar to have a new-line in a 
    preprocessor directive.
  - PBrett: Let's have Corentin to resolve this issue and come back 
    with a revised paper.
- [P2093R8: Formatted output](https://wg21.link/p2093r8)
  - Victor presented slides:
    - Slides at 
      https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2021-09-08-p2093r8-presentation.pdf .
    - LLVM's `raw_ostream` uses a similar approach.
    - Added UB where SG16 requested it if invalid code units are 
produced by `std::print()`.
    - With [P2216: std::format improvements](https://wg21.link/p2216), the
      format string must be known at compile-time and therefore is
      associated with the literal encoding.
    - [LWG3576: Clarifying fill character in std::format](https://wg21.link/lwg3576)
      was recently resolved through use of the literal encoding.
    - If the format string does not match the literal encoding, it could
      fail to parse.
    - Consistency with `std::format` requires locale-independence.
    - Consistent with the
      [P2419: Clarify handling of encodings in localized formatting of chrono types](https://wg21.link/p2419)
      resolution for [LWG3565](https://wg21.link/lwg3565) where
      transcoding is performed if the literal encoding is a UTF.
  - PBrett: Use of P2419 as a wedge is questionable here since its 
    changes granted permission rather than mandating behavior.
  - Victor: We went with more relaxed wording due to concerns over user 
    provided locales; we could strengthen the behavior.
  - Hubert: Yes, we had weak consensus for use of literal encoding for 
    UTF-8, but that doesn't imply consensus for more general use.
  - Tom: I don't buy the argument that because the format string needs 
    to match literal encoding for compile time processing that that implies 
    the formatted result must be in the same encoding; though production in 
    a different encoding would impose overhead.
  - Tom: Use of the literal encoding as required for compile-time 
    parsing of the format string limits this being a precedent for similar 
    use of the literal encoding elsewhere.
  - PBrett: We discussed GB18030 recently and wide strings. Victor, are 
    you wedded to this being UTF-8 specific?
  - Victor: No.  UTF-8 is problematic in practice.  Different problems 
    occur for other encodings.  Worried about increasing scope though.
  - **Poll 2: Use of UTF-8 as the literal encoding is sufficient for \<print\> facilities to establish encoding expectations.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   3 |   2 |   1 |   0 |

    - Consensus in favor.
    - A: Against rationale: Still concerned that people are not going to use
      the faciility correctly, i.e. end up with mojibake anyway in corner
      cases that they won't find until later.  Would prefer solution that
      provides a stronger way to associate an encoding with the output, but
      there isn't an extant proposal to do that.
  - Charlie: I abstained for similar reasons.
  - Hubert: We did not read through the minor wording changes in 
    paragraph 31 and it would be good to do so quickly.
  - Hubert: Looks pretty good; are we clear that the UB only applies 
    after the first if?
  - Hubert: The order of the if statements is not correct; there are 
    subordination issues.
  - PBrett: In "If this requires transcoding", it is unclear what 
    "this" refers to.
  - Jens: Strike "then" in favor of a comma in "If this requires 
    transcoding then ..."
  - Jens: Remove the trademark symbol.
  - **Poll 3: Correct the P2093R8 wording for \[print.syn\].31 to remove ambiguities, and forward P2093 as revised to LEWG with a recommended ship vehicle of C++23.
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   4 |   2 |   0 |   0 |

    - Consensus in favor.
- [P2361R2: Unevaluated string literals](https://wg21.link/p2361r2)
   - Ran out of time; will discuss next time.
- Next telecon on 9/22 will review D2348R1 subject to a new revision, 
  [P1636 Formatters for library types](https://wg21.link/p1636), and
  [P2361 Unevaluated strings](https://wg21.link/p2361).


# August 25th, 2021

## Agenda
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)
- [P2419R0: Clarify handling of encodings in localized formatting of chrono types](https://wg21.link/p2419r0)
- [LWG 3576: Clarifying fill character in std::format](https://cplusplus.github.io/LWG/issue3576)

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Victor Zverovich
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)
  - Corentin presented
  - Steve: Is "basic source character set" a bug in comment grammar?
  - Corentin: maybe
  - Peter and Steve: Form feeds are used in sources
  - Corentin: no change proposed
  - Hubert: VT and FF don't end comments in clang or gcc.  Status quo is they
    may not be line breaks, although they may be whitespace

  - **Poll 1: Acknowledging that we have limited time available, we support the  direction for P2348R0 and encourage further work.**
    - Attendance: 7
    - No objections to unanimous consent
  - Peter: Please bring back the paper rebased on
    [P2314: Character sets and encodings](https://wg21.link/p2314), and add
    implementation notes.

- [P2419R0: Clarify handling of encodings in localized formatting of chrono types](https://wg21.link/p2419r0)
  - Charlie: Does this permit new things? If so it's appropriate to update
    feature test macro
  - Peter: Would have liked to include recommended practice in the wording
  - Charlie: Current wording is 'fine' because it has enough implementation
    defined wiggle room.
  - Hubert: If we are to improve the wording, it might just need to be a note
    rather than normative
  - Victor: Implementation coulde be in terms of `codecvt` facet, so it should
    work
  - Charlie: Concern if there's a list of locales, it might be a problemb if
    users customize facets of a locale derived from a system locale.

  - **Poll 2: Forward P2419 to LEWG as the recommended resolution of LWG 3565 and with a recommended ship vehicle of C++23.**
    - Attendance: 7

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   2 |   1 |   0 |   0 |
    
    - Consensus: Strong consensus in favour.

- [LWG 3576: Clarifying fill character in std::format](https://cplusplus.github.io/LWG/issue3576)
  - Charlie: MSVC processes codepoint, preserving the code unit sequence. libc++
    stores a code unit. Error handling in MSVC deals with ill-formed sequences
    transcoding later.
  - Hubert: Clarify as a note grapheme whether a cluster could include `{` or
    `}`
  - Charlie: Implementation difficult, as finding `{}` is straightforward,
    parsing a grapheme cluster is hard.
  - Peter: Doesn't like codepoint as it means combining characters are confusing
    in source.
  - \[ Editor's note: Contribution by Steve not recorded here \]
  - Victor stated in chat: We already talk about grapheme clusters in width
    estimation
  - Charlie: If we fill with a grapheme cluster, it's the first normative use of
    EGCs.  Some implementation difficulty. Varies over Unicode standard versions
    in some cases. Users have the ability to customize using formatters. Outside
    the normal range of use cases. A different format spec/library for multibyte
    fills? OK with etiher code unit or codepoint.
  - Corentin: Agree with Charlie, maybe use emoji, but rendering of that is
    complicated.  Doesn't see a use case for combined characters either.
  - Victor: Concerned about implementation experience with grapheme clusters as
    fill characters. Has had no requests for this functionality. Has had
    requests for codepoints. Code units would disallow box drawing characters.
  - Peter: We allow EGCs now for width, why shouldn't we allow them as fill
    characters?
  - Mark: We base on first character of cluster, specified as a heuristic. It's
    not a layout engine.
  - Charlie: Width is 'should' not 'must' (not mandatory)
  - Victor: We have to restrict the set of fill characters in any case. It might
    be theoretically better to use grapheme cluster, but has implementation
    concerns.  Way forward is to have a new facility for filling with grapheme
    clusters.
  - Corentin: Question for Charlie and Victor: If we say codepoint now, can we
    change to grapheme cluster later?
  - Charlie: Ict would probably break ABI. Heroic and disgusting hacks would be
    involved.
  - Victor: It would be a break for libfmt.
  - Hubert: Are we in agreement that there is an issue with the resolution as
    presented with it allowing `{}`? Do we need to discuss combining characters?
  - Charlie: I don't think so. Not a common use case and not actually totally
    unreasonable. Could use a *universal-character-name*.
  - Corentin: No value in protecting user from themselves in something they ask
    for.
  - Peter: Will, "Play stupid games, win stupid prizes," make it into the
    minutes?
  - Victor: Need to prevent characters disallowed by the grammar, but more than
    that is not necessary.
  - Mark: Clarify poll for non-Unicode encoding?
  - Charlie: MSVC doesn't treat UCS-2 properly, treats it as UTF-16. Do
    implementations have to deal with nonsense?
  - Peter: This happens after all the other phases of translation
  - \[ Editor's note: There was some discussion of polling options. \]
  - **Poll 3.1: Recommend that the proposed resolution for LWG3576 should be adopted, with the modification that the fill character must not contain '{' or '}' as part of the extended grapheme cluster.**
    - Attendance: 7
    
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   1 |   1 |   3 |   2 |

    - Consensus against.

  - **Poll 3.2: The format fill character should be defined as "any codepoint of the literal encoding other than '{' or '}'".**
    - Attendance: 7

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   1 |   0 |   0 |

    - Strong consensus in favour.


# July 28th, 2021

## Agenda:
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - Discuss and poll the proposed resolution.
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - PBrett presented
    - The standard is underspecified in terms of what happens with localized
      chrono substitutions
    - Proposed resolution is very narrow; limited to UTF-8 scenarios
  - Hubert: The direction makes sense, but the conversion to UTF-8 may not
    always be successful given the diversity of possible deployments.
  - Hubert: There should be some form of error handling policy; which one
  - Tom: The assumption is that there may not be characters that are in Unicode?
  - Hubert: No, the implementation may not have a map from the source charset to
    Unicode.
  - Charlie: Our implementation has `MultiByteToWideChar`, but it behaves in
    surprising ways for some encodings; some multibyte characters in some 
    encodings may not convert correctly.
  - Charlie: This doesn't permit requesting a non-UTF-8 encoding be used.
  - Victor: If 'L' is not specified, then the "C" locale is used and there is no
    issue.
  - Victor: The proposed wording only applies when `{:L}` is used.
  - PBrett: To clarify, there would be no way to preserve a non-UTF-8 encoding
    through `std::format()`.
  - Victor: Correct.
  - Charlie: The convention that the literal encoding affect `std::format()`
    behavior is currently limited; this widens that.
  - Charlie: The other place literal encoding is used is parsing the format
    string; which makes perfect sense.
  - Charlie: Widening this dependency on the literal encoding is concerning.
  - Charlie: I expect some Windows users to write code with UTF-8 literal
    encoding but to produce non-UTF-8 output.
  - Charlie: This may occur when logging text, the format string may just
    consist of format specifiers.
  - Victor: We also depend on the literal encoding for the "mu" character.
  - Victor: Even if text looks like ASCII, it may not be; confusables may be
    present or line drawing characters.
  - Steve: How does the library figure out what the literal encoding is?
  - PBrett: Implementation magic; the compiler knows and can communicate it to
    the library.
  - PBrett: Can we just specify that the locale text be transcoded to the
    literal encoding?
  - Charlie: The UTF-8 only solution avoids the need for a large transcoding
    library.  The non-UTF-8 case may not support representation and therefore
    require/request transliterating.
  - PBrett: In an implementation that supports CP1251 as locale, conversion to
    UTF-8 at least will be needed.
  - PBrett: We should allow implementations the flexibility to provide the right
    result if they know how to.
  - Charlie: This is mandating conversion in a specific circumstance; what
    happens when conversion is lossy?  We can't ensure convertibility to all
    code pages.
  - PBrett: The proposed resolution forbids doing the right thing for GB18030,
    which is able to represent all the characters.
  - Charlie: Right, the only encodings that support non-lossy conversion are
    Unicode ones.
  - Charlie: It is reasonable to support EBCDIC here.
  - Charlie: With regard to special characters like "mu", you can get mixed
    encodings regardless.
  - Charlie: This differs from width estimation which is always best effort
    since GUI presentation is not usually known.
  - Mark: This does pose a payload requirement on the implementation; not just
    implementation effort.
  - Mark: The overload on locale could be limited to 1; each locale could be
    required to provide UTF-8 translations.
  - Mark: The proposed resolution effectively requires a general purpose
    transcoding facility.
  - Mark: This might be best left to implementation-defined.
  - Hubert: There is a desire to allow conversion, but there is also a desire to
    avoid dependency on the output that locale facilities provide.
  - Hubert: The pre-computation method could be intrusive for deployment;
    limiting localedef to character sets with mapping to Unicode available.
  - Hubert: Perhaps guidance is to transcode when encoding information is known.
  - Charlie stated in chat: "if you support both `Russian.UTF-8` and
    `Russian.1251` then this is essentially saying that `format` will treat
    `Russian.1251` as `Russian.UTF-8` (assuming the actual content of the local
    facets is the same)"
  - PBrett: This is what I was trying to suggest in email.
  - PBrett: Only a burden on implementations if they support locale-specific
    encoding and if the locale specific encoding can be different from the
    literal encoding.
  - PBrett: Implementations that already support many encodings are already
    burdened with the transcoding facilities.
  - Victor: Agree with Peter; the "else" clause in the proposed wording should
    be relaxed; we should allow, but not require transcoding.
  - Steve: For most POSIX system, locales are an open system and may be extended
    by users (in potentially broken ways).
  - Steve: Implementations don't generally own the locale systems, so adding
    requirements there may not be implementable.
  - Steve: But, yes, we should allow implementations to do the best they can; we
    shouldn't mandate brokenness.
  - Charlie: Not a burden if transcoding is only needed for currently supported
    locales.
  - Charlie: Would be a burden if an implementation had to convert between two
    non-Unicode encodings.
  - Charlie: From an overhead perspective, probably not a big deal.
  - Charlie: A note may suffice.
  - PBrett stated in chat: "'L' = I want to be correct, not fast"
  - Corentin: Agree with Peter; avoid specifying transcoding
  - Corentin: options are to get output in locale specified, then convert to
    UTF-8, or to get UTF-8 directly.
  - Corentin: Implementations can hack this for `chrono` types; there aren't
    that many strings involved.
  - PBrett: Concerned about implementability since locales may be user-defined;
    implementations shouldn't have to engage in heroics.
  - Hubert: Locale systems have allowances; users can compile their own.
  - PBrett: Perhaps limit requirements to locales known by the implementation.
  - Hubert: Wording to an implementation-defined set of locales may work here.
  - Corentin: There is a limited amount of usefulness that can be extracted
    here; don't want to put too much effort here.
  - Corentin: `std::format()` isn't a great tool for localization; real
    localization requires swapping the order of fields.
  - Jens: Would like to ensure wording is more precise; need to specify which
    string literal encoding.
  - PBrett: Summarizing:
    1. Limit the requirement to implementation provided locales.
       - Locales with an implementation-defined set of strings.
    2. Permit implementation to "do the right thing"
    3. Require "as if" transcoding when the literal encoding is UTF-8.
    4. Permit "as if" transcoding when the ordinary literal encoding is not
       UTF-8.
  - Hubert: That seems to reflect consensus, but falls under "as if" rules.
  - Tom: Uncertain that we have consensus on dependency of UTF-8 literal
    encoding.
  - Victor: I thought we had consensus on that.
  - Mark: Am mildly infavor of requiring this when the literal encoding is
    UTF-8.
  - Hubert: That isn't implementable.
  - PBrett: Right, only implementable for locales the implementation provides.
  - Charlie: Implementations should be prohibited from transcoding to an
    encoding that is not Unicode (UCS-2 is not a Unicode encoding in this case).
  - Charlie: We don't want transliteration here.
  - Charlie: Should require UTF-8, permit UTF-7, UTF-EBCDIC, etc..., prohibit
    others.
  - Hubert: Prior polls had consensus for UTF-8, but not for others. Consensus
    would likely be similar for other Unicode encodings.
  - Tom: Concerned about that consensus.
  - PBrett: Concerned about consistency here; trying to rationalize the UTF-8
    focus.
  - \[ Editor's note: Some discussion of poll wording ensued \]
  - Corentin: Charlie, why the prohibition to "as if" conversion to other
    encodings?
  - Charlie: The goal is to avoid lossy conversions.
  - Corentin: Can we just prohibit lossy conversions?
  - Charlie: We could allow cases where the target encoding is not Unicode, but
    all of the characters are representable.
  - Charlie: The concern is wanting to avoid transliteration.
  - Corentin: I agree with that.
  - **Poll 1: Require implementations to make `std::chrono` substitutions with `std::format` as if transcoded to UTF-8 when the literal ecoding *E* associated with the format string is UTF-8, for an implementation-defined set of locales.**
    - Attendance: 9

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   6 |   2 |   0 |   0 |
    
    - Consensus: Consensus in favour.
    - Poll bikeshedding; Tom wants to apply to `wchar_t` cases.
  - **Poll 2: Permit such substitutions when the encoding *E* is any Unicode encoding form.**
    - Attendance: 9

        | SF  | F   | N   | A   | SA  |
        | --: | --: | --: | --: | --: |
        |   0 |   7 |   2 |   0 |   0 |

    - Consensus: Consensus in favour

  - **Poll 3: Prohibit such substitutions otherwise.**
    - Attendance: 9

        | SF  | F   | N   | A   | SA  |
        | --: | --: | --: | --: | --: |
        |   1 |   3 |   3 |   1 |   1 |

    - Consensus: No consensus
    - SA: This is an over constraint; should permit implementations to do best
      effort work.
    - Hubert: This requires invention for the case where a locale is defined
      outside the implementation without a mapping to the target locale.
- [P2348R0: Whitespaces Wording Revamp](https://wg21.link/p2348r0)
   - Ran out of time.
- Tom: Next meeting in two weeks, will revisit
  [LWG 3565](https://cplusplus.github.io/LWG/issue3565) if a paper is 
  available; [P2348R0](https://wg21.link/p2348r0) otherwise.


# July 14th, 2021

## Agenda:
- [P2295R5: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r5)
  - Review updated wording produced through collaboration between Corentin, Jens, Hubert, and Peter.
    - https://lists.isocpp.org/sg16/2021/04/2353.php
    - https://lists.isocpp.org/sg16/2021/06/2429.php
- [P2362R0: Make obfuscating wide character literals ill-formed](https://wg21.link/p2362r0)
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - Discuss and poll the proposed resolution.

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2295R5: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r5)
  - \[ Editor's note: D2295R5 was the active paper under discussion at the telecon.  The agenda and links
    used here reference P2295R5 since the links to the draft paper were ephemeral.  The published document
    is expected to differ from the reviewed draft revision as noted below. \]
  - PBrett presented.
    - Peter's presentation slides are available
      [here](https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2021-07-14-p2295r5-p2362r0-presentations.pdf).
    - The wording was revised based on feedback received from the SG16 mailing list.
    - Any wording changes approved today will appear in the revision of the paper that will be submitted for
      tomorrow's mailing deadline.
  - Tom noted that the existing wording regarding the introduction of new-line characters for end-of-line
    indicators only applies to non-UTF-8 encoding schemes with the proposed changes.
  - PBrett and Corentin explained that this is intentional; that end-of-line indicators are relevant for
    structured text (e.g., data sets), not for source files expressed as a sequence of code units.
  - PBrett and Corentin noted that new-line character sequences will be revisited with
    [P2348](https://wg21.link/p2348).
  - \[ Editor's note: A note was added to the final P2295R5 wording to explain that end-of-line indicators are
    not applicable to UTF-8 encoded source files and that new-line characters separate lines. \]
  - Hubert observed that some of the wording suggestions from the mailing list discussion had not been
    incorporated.
  - \[ Editor's note: Live editing of the proposed wording ensued, the discusion of which is not captured
    verbatim here.  Concerns discussed included use of "encoding scheme" vs "encoding", whether a plural form
    of "source file" should be used, methods to avoid use of the term "determined", and how to equate the
    sequence of UTF-8 code units with the elements of the translation character set. \]
  - Mark asked if the proposed wording handles CR/LF new-line sequences.
  - Hubert responded that [P2348](https://wg21.link/p2348) will address that concern.
  - **Poll: Forward D2295R5 with wording modifications as discussed to EWG for C++23.**
    - Attendance: 9
    - No objection to unanimous consent.
- [P2362R0: Make obfuscating wide character literals ill-formed](https://wg21.link/p2362r0)
  - PBrett presented.
    - Peter's presentation slides are available
      [here](https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2021-07-14-p2295r5-p2362r0-presentations.pdf).
  - Tom noted that the execution wide-character set is not necessarily Unicode; non-encodable characters are
    possible even when `wchar_t` is 32-bit.
  - Charlie noted that Visual C++ is technically not conformant since its 16-bit `wchar_t` is not able to
    store every possible locale dependent character in a unique `wchar_t` value.
  - Hubert explained that ISO C++ does not permit use of a multi-code-unit encoding for wide character and
    string literals.
  - Charlie asked what warning level Visual C++ requires for a warning to be issued for the cases proposed
    to become ill-formed.
  - Corentin responded, W2.
  - Tom asked Hubert how his implementation handles the multicharacter case.
  - Hubert reported that xlC encodes the last character (like gcc and Clang).
  - Wording review ensued.
  - Tom requested that the use of "character literal" removed in the proposed wording for \[lex.ccon\]p2
    be restored so that the note states, "... but does not determine the value of non-encodable
    **character literals** or multicharacter literals. ..."
  - PBrett agreed to do so.
  - Jens expressed a preference towards revising the paper title to remove the word "obfuscating" in order
    to avoid projecting bias.
  - Tom responded that the title is the author's prerogative, but reported having had a similar reaction to
    the current title.
  - Charlie asked if there is also motivation to make non-encodable character literals and multicharacter
    literals ill-formed as well.
  - PBrett stated that there is and that writing a paper to do so is on his todo list, but that the motivation
    for ordinary literals is different because they are used and do not suffer some of the problems that
    the wide variety do.
  - **Poll: Forward P2362R0 with title and wording modifications as discussed to EWG for C++23.**
    - Attendance: 9
    - No objection to unanimous consent.
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - Deferred to the next telecon due to time constraints.
- Tom announced that the next telecon will be held 2021-07-28 and that the agenda will include
  [LWG 3565](https://cplusplus.github.io/LWG/issue3565) and then [P2348](https://wg21.link/p2348).


# June 23rd, 2021

## Agenda:
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - Finish polling begun at the last telecon.
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - Discuss and poll the proposed resolution.
- [P2295R4: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r4)
  - Review updated wording produced through collaboration between Corentin, Jens, Hubert, and Peter.
    - https://lists.isocpp.org/sg16/2021/04/2353.php
    - https://lists.isocpp.org/sg16/2021/06/2429.php

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2093R6: Formatted output](https://wg21.link/p2093r6):
  - PBrett reviewed the polls taken at the last telecon.
    - \[ Editor's note: See the [June 9th, 2021](#june-9th-2021) summary for the prior polls. \]
    - Tom clarified the intent behind the "encoding expectations" terminology in the polls; it is intended to
      distinguish cases where there is a dependence on a particular encoding, but without tying that dependence
      to a particular mechanism for determining the existence of such a dependence.  As proposed, the paper
      currently imposes a UTF-8 encoding expectation when the literal encoding is UTF-8.
    - Hubert expressed being content with poll 5 relative to poll 4 since the determination of what constitutes
      a device with encoding expectations is left up to the implementation.
    - Hubert noted that it is ambiguous whether a file may constitute a device with encoding expectations and
      provided `/dev/tty` as an example.
  - Poll 2.1 discussion:
    - Victor stated that `std::format()` does not have an encoding expectation by itself but that string
      formatters must be encoding aware to honor field width specifiers.
    - Victor added that `std::print()` is special due to transcoding requirements.
    - Hubert noted that these polls address the abstract design extent.
    - Jens stated that, as currently specified, there is no implied encoding expectation, but there may be an
      expectation for the combined formatter outputs to be consistent.
    - Jens added that the format string might not contribute text to the final result; it might consist solely
      of field specifiers.
    - Jens concluded that concatenation of the output of two formatters that produce differently encoded text
      might produce text that is not consistently encoded and that nothing is provided to reconcile them.
    - Tom agreed and opined that diagnostics would be useful, but that it is not clear how to reconcile that
      with desired support for binary formatting.
    - Victor replied that he doesn't see any problems with combining binary and text and reiterated that the
      ability to do so addresses real use cases.
    - PBrett opined that the `<format>` and `<print>` facilities do not need to be consistent; the only time an
      encoding expectation should be present is when the output is directed to a device with an encoding
      expectation.
    - Jens asked if that implies that formatters must communicate the encoding of their output.
    - Victor replied that use of formatters to combine binary and text data is not dissimilar to existing uses of
      `std::ostream` or `printf()`; it is up to the programmer to ensure that use of formatters matches the
      intent.
    - Jens asked how a programmer determines what encoding is produced.
    - Victor replied that it is determined by the literal encoding.
    - PBrett replied that nothing in the standard states that though; not for `std::format()`.
    - Charlie stated that the Microsoft implementation assumes Unicode characters for the purposes of field
      width estimation, but that they could transcode to Unicode if the source encoding was known; but it is
      not known in general.
    - Charlie noted that the arguments passed to formatters are not transcoded.
    - Charlie added that format strings frequently consist of only invariant characters; effectively ASCII.
    - Charlie cautioned that the encoding of format strings must be known to the implementation in order for
      format string parsing to not misinterpret trailing code units of multibyte encoded characters.
    - Charlie noted that, for log files, it is not necessarily desirable to transcode to the system encoding.
    - Corentin portrayed `std::print()` as a two step process of formatting followed by transcoding and stated
      that there is a precondition on the output device being able to display the text, but noted that such
      a precondition does not imply a postcondition on `std::format()`.
    - Corentin stated that diagnostics would be limited because mojibake is not always detectable.
    - Hubert observed that the sentiment for the poll appears to be trending against it, but that we do have
      desire to avoid surprises with `std::print()`, or at least to say that we want some checking to be
      implemented.
    - Hubert suggested that the model of `std::print()` as a two step process of calling `std::format()` and
      then printing the result may be too limiting and that a more integrated design that provides
      `std::print()` more detailed information about formatting outputs may unblock further progress.
  - **Poll 2.1: P2093R6: `<format>` and `<print>` facilities should have consistent behavior with respect to encoding expectations for the output of formatters.**
    - Attendance: 9 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   1 |   1 |   5 |   1 |

    - Consensus: Strong consensus against.
  - Poll 7 discussion:
    - Victor asked if encouragement would be stated as a note in the standard.
    - Zach responded that LWG prefers normative encouragement of the form, "implementations should do X" and
      noted that such encouragement does not impose a requirement on implementors.
    - Zach added that it is important to follow Unicode guidelines.
    - Jens asked what the implication is to implementations that cannot implement the encouraged behavior.
    - Zach replied that, as proposed, all implementations would be able to implement it since transcoding is
      only prescribed for one Unicode form to another.
    - Victor noted that some implementations display a `?` rather than a U+FFFD replacement character.
  - **Poll 7: P2093R6: `<print>` facility implementors are encouraged to substitute U+FFFD replacement characters following Unicode guidance when output is directed to a device and transcoding is necessary.**
    - Attendance: 9 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   2 |   5 |   0 |   0 |   1 |

    - Consensus: Consensus in favor.
    - SA: The terminal will already handle this.
    - Tom noted that the device cannot handle this in the case where transcoding is necessary in order to
      direct the output to the device; e.g., when the device requires UTF-16.
    - Jens noted that specifying that the behavior is undefined but then encouraging a particular
      behavior is novel.
    - Zach agreed but noted that this is a case of "library UB", so kind of a special case.
  - Poll 8 discussion:
    - \[ Editor's note: the original poll was, "P2093R6: Neither `<format>` nor `<print>` facilities require
      an explicit program-controlled error handling mechanism for violations of encoding expectations." \]
    - Zach stated that the poll should be framed as a change to the status quo.
  - **Poll 8: P2093R6: `<print>` facilities must provide an explicit program-controlled error handling mechanism for violations of encoding expectations.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   3 |   3 |   3 |

    - Consensus: Strong consensus against.
  - Poll 9 discussion:
    - \[ Editor's note: The original poll was "P2093R6: Use of UTF-8 as the literal encoding is
      sufficient for `<format>` and `<print>` facilities to assume that the format string and
      output of all formatters is UTF-8 encoded." \]
    - Tom stated that the poll doesn't make sense as currently worded if formatters are allowed
      to format binary data.
    - Zach stated that his position may differ for standard formatters vs user provided formatters.
    - Zach added that the proposed heuristic already matches the behavior used to enable field
      width estimation.
    - Tom disputed the claim that field width estimation depends on the choice of literal encoding.
    - PBrett explained that field width is determined by code point values.
    - \[ Editor's note: [\[format.string.std\]p11](http://eel.is/c++draft/format#string.std-11) states:

          For a string in a Unicode encoding, implementations should estimate the width of a
          string as the sum of estimated widths of the first code points in its extended grapheme
          clusters.  The extended grapheme clusters of a string are defined by UAX #29.  The
          estimated width of the following code points is 2
          ...
          The estimated width of other code points is 1.
      \]
    - Charlie stated that Microsoft's implementation was designed around the literal encoding at
      least partially due to current technical limitations in the compiler.
    - Victor stated that the literal encoding is not a perfect indicator, but is the best that we
      have available.
    - PBrett agreed that we don't currently have anything better.
    - PBrett noted that use of the literal encoding does affect the cases where uses of `printf()`
      can be simply changed to `std::print()` without potentially unintended behavioral changes.
    - Zach compared use of the literal encoding to use of CMake; the least bad option.
  - **Poll 9: P2093R6: Use of UTF-8 as the literal encoding is sufficient for `<print>` facilities to establish encoding expectations.**
    - Attendance: 9

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   3 |   1 |   3 |   2 |   0 |

    - Consensus: Very weak consensus.
    - Corentin commented that LEWG sent these questions back to SG16 for clarification and
      weak consensus isn't really good enough.
    - PBrett suggested that perhaps use of an encoding tag could garner more consensus.
    - Zach reiterated that the status quo is to use the literal encoding to enable width estimation.
    - Jens replied that the standard does not connect literal encoding with width estimation.
    - \[ Editor's note: [\[format.string.std\]p10](http://eel.is/c++draft/format#string.std-10) states:

          For the purposes of width computation, a string is assumed to be in a locale-independent,
          implementation-defined encoding.  Implementations should use a Unicode encoding on platforms
          capable of displaying Unicode text in a terminal.
      \]
    - Zach responded that, regardless, implementations are relying on literal encoding.
    - Charlie replied that his implementation should probably be performing width estimation for
      other encodings like GB18030.
  - Poll 10 discussion:
    - \[ Editor's note: the original poll was "P2093R6: Use of a literal encoding other than UTF-8 is
      sufficient for `<format>` and `<print>` facilities to assume a particular encoding for the
      format string and output of formatters." \]
    - The weak results for poll 9 obviated the need to conduct this poll.
  - Poll 11 discussion:
    - \[ Editor's note: the original poll was "P2093R6: Support for implicit encoding conversions
      will only be possible when an encoding assumption is implicitly or explicitly present." \]
    - Victor preempted the poll by volunteering to add prose regarding how future extensions could
      enable implicit transcoding features.
    - Hubert noted that previous consensus was that `std::format()` and `std::print()` do not require
      the same encoding expectations.
    - Hubert added that it isn't clear how an implementation might take that into consideration when
      the implementation intent appears to be to pass the output of a `std::format()` call to a
      transcoding facility.
    - Corentin stated that LEWG time is more valuable than ours and, since we don't appear to have
      strong consensus, another meeting seems warranted.
    - Victor agreed with Hubert and Corentin that more common understanding is required.
    - Tom agreed and stated that it seems we are not yet ready to poll forwarding the paper.
    - PBrett pondered how consensus could be improved.
    - Zach suggested that those with positions on the margins could suggest ways in which their
      positions might be altered.
    - Zach noted that the current proposal and discussion has been on particular technical details and
      that progress might be made by focusing on, for example, a "Unicode context" as opposed to the
      choice of literal encoding.
    - Hubert requested a clear summary of how the implementation compares to the polls taken.
    - Hubert added that he would not oppose moving forward with behavior based on the choice of
      literal encoding.
    - Tom pondered whether Hubert's suggested escape mechanism for binary data would be helpful.
    - Victor requested more details on that mechanism, or perhaps a pull request, and stated that he
      has not seen something that sounds similar implemented elsewhere.
- [LWG 3565: Handling of encodings in localized formatting of chrono types is underspecified](https://cplusplus.github.io/LWG/issue3565)
  - Discussion postponed due to time constraints.
- [P2295R4: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r4)
  - Discussion postponed due to time constraints.
- Tom stated that the next meeting will be in 3 weeks, on July 14th.


# June 9th, 2021

## Agenda:
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - Continue discussion and poll for consensus on answers to the following questions:
    1) How should invalidly encoded text be handled when transcoding for the purpose of writing directly to
       a device interface?
    2) Is use of UTF-8 as the literal encoding a sufficient indicator that all input fed to `std::format()`
       and `std::print()` (including the format string, programmer supplied field arguments, and locale
       provided text) will be UTF-8 encoded?
    3) Is the literal encoding a sufficient indicator in general that all input fed to `std::format()`
       and `std::print()` (including the format string, programmer supplied field arguments, and locale
       provided text) will be provided in an encoding compatible with the literal encoding?
    4) What are the implications for future support of
       `std::print("{} {} {} {}", L"Wide text", u8"UTF-8 text", u"UTF-16 text", U"UTF-32 text")`?
- [LWG 3565: Handling of encodings in localized formatting of `chrono` types is underspecified](https://wg21.link/lwg3565)

## Meeting summary:
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - No initial discussion was held; the meeting proceded directly to candidate polls previously
    [communicated to the mailing list](https://lists.isocpp.org/sg16/2021/06/2430.php).
  - Poll 1 discussion:
    - Zach stated that programmers will expect `std::format()` and `std::print()` to behave the same way.
    - Victor stated that `std::print()` can be implemented using `std::format()`;
      `std::print()` is intended to be just `std::format()` with additional device dependent transcoding.
  - **Poll 1: P2093R6: `<format>` and `<print>` facilities should have consistent behavior with respect to encoding expectations for the format string.**
    - Attendance: 8
    - No objection to unanimous consent.
  - Poll 2 discussion:
    - \[ Editor's note: the original poll was "P2093R6: `<format>` and `<print>` facilities should have
      consistent behavior with respect to encoding expectations for the output of formatters." \]
    - Victor asked for confirmation that the "formatters" term in the poll refers to formatter specializations.
    - Tom confirmed that it does.
    - Zach asked for confirmation that formatters can be user provided.
    - Victor confirmed that they can be.
    - Hubert stated that a desire to bypass encoding constraints will require a concept for binary formatters
      and a corresponding proposal.
    - Jens expressed a belief that formatters are allowed to be agnostic with respect to use with `std::format()`
      vs `std::print()`.
    - \[ Editor's note: Jens observation prompted the addition of poll 2.2 to confirm matching design intent. \]
    - Victor stated that there is currently no mechanism proposed for a formatter to be informed as to whether
      it is being used with `std::format()` or `std::print()`.
    - Zach expressed confusion about the poll.
    - Hubert suggested this poll be deferred until after later polls concerned with the consequences of violating
      encoding expectations. 
  - **Poll 2.1: P2093R6: `<format>` and `<print>` facilities should have consistent behavior with respect to encoding expectations for the output of formatters.**
    - Per discussion; poll deferred until after later polls.
  - **Poll 2.2: P2093R6: formatters should not be sensitive to whether they are being used with a `<format>` or `<print>` facility.**
    - Attendance: 8
    - No objection to unanimous consent.
  - Poll 3 discussion:
    - \[ Editor's note: the original poll was "P2093R6: Regardless of format string encoding assumptions,
      `<format>` facilities (but not `<print>` facilities) may be used to format binary data." \]
    - Victor stated that support for binary data is a nice capability to have and is needed to match existing
      uses of `printf()`.
    - Steve noted that this poll is relevant for cases where transcoding is required.
    - Tom agreed and noted that the code author may not be aware of implementation performed transcoding.
    - Jens asked for reasons that a text facility would be used for binary data.
    - Victor responded that `printf()` is often used with binary data and noted that the format string does not
      necessarily contain text; it might solely contain field specifiers.
    - Tom noted that filenames may be formatted, but might not conform to encoding expectations.
    - Steve mentioned having also seen ostreams used with binary data.
    - Hubert noted again that additional design work would be needed for binary data to be transported through
      any implicit transcoding performed by `std::print()`.
    - Hubert added that control characters can be another source of binary data.
    - Zach suggested splitting the poll to address `<format>` and `<print>` separately so as to remove the
      parenthetical text.
    - Zach suggested that there may be a use case for standard formatters for binary data or for a "raw" print
      interface.
    - Victor suggested there may be some misunderstanding; that `std::print()` may be used with binary data
      with the result that garbage is displayed on the console.
    - Hubert politely disagreed due to the lack of an escape mechanism for binary data.
    - Jens agreed that some form of a non-text in-band signalling mechanism would be needed.
    - Victor clarified that his argument for preserving binary data is for the case where output is directed
      to a file.
    - Hubert noted that poll 3 and poll 10 are related and that consensus for poll 10 will require facilities
      related to poll 3.
  - **Poll 3.1: P2093R6: Regardless of format string encoding assumptions, `<format>` facilities may be used to format binary data.**
    - Attendance: 8 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   5 |   1 |   1 |   0 |   0 |

    - Consensus: Strong consensus in favor.
  - **Poll 3.2: P2093R6: Regardless of format string encoding assumptions, `<print>` facilities may be used to format binary data.**
    - Attendance: 8 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   2 |   1 |   3 |   1 |   0 |

    - Consensus: Weak consensus in favor.
    - A: No comment
  - Poll 4 discussion:
    - \[ Editor's note: the original poll was "P2093R6: `<print>` facilities exhibit undefined behavior when
      a format string or formatter output does not match encoding expectations." \]
    - Steve expressed a desire for behavior less severe than undefined behavior.
    - Victor expressed discomfort with undefined behavior as well, particularly that the poll applies to all
      `std::print()` invocations regardless of where the output is directed.
    - Hubert spoke in favor of the poll and noted that this establishes that an implementor or code reviewer
      can diagnose these cases; that can't happen if behavior is defined.
    - Jens agreed with Hubert, noted the existence of the precondition, and that a violation is "library UB"
      amd therefore less consequencial than core language UB.
    - Steve stated in chat: "OK, based on Hubert and Jens's comments, I'll withdraw my objections about UB.
      I'd like better terminology but this isn't the forum."
    - Jens stated that the paper would benefit from some prose that explains the intended model and that
      inconsistently encoded data can be stitched together.
    - Jens expressed distaste for preconditions being so specific to a corner case and professed desire for
      a good programming model.
    - Zach noted similarities with [P1868](https://wg21.link/p1868); the worst case outcome is mojibake
      displayed on the terminal; the damage is limited.
    - Zach stated that either UB or implementation-defined behavior would be fine for now, but that we may
      desire another failure mode where the behavior is more contained in the future; a behavior mode that
      reflects that something went wrong, but where the damage is localized.
    - Victor stated that he feels this poll overreaches; that the only concern is with regard to writing to
      a file vs a terminal and that, in practice, all that should happen is that the data is passed through
      or that replacement characters are substituted.
    - Hubert noted that files may correspond to special devices; e.g., /dev/tty.
    - Hubert stated that UB is a specification tool and noted that implementors are in a position to
      distinguish between polls 4 and 5, but that a code reviewer generally cannot.
  - **Poll 4: P2093R6: `<print>` facilities exhibit undefined behavior when an encoding expectation is present and a format string or formatter output does not match those expectations.**
    - Attendance: 8 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   2 |   4 |   0 |   0 |   1 |

    - Consensus: Strong consensus in favor.
    - SA: I think this is too broad and the impact is larger than necessary.
  - **Poll 5: P2093R6: `<print>` facilities exhibit undefined behavior when an encoding expectation is present and a format string or formatter output does not match those expectations and output is directed to a device that has encoding expectations.**
    - Attendance: 8 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   6 |   0 |   1 |   0 |   0 |

    - Consensus: Stronger consensus in favor relative to poll 4.
  - Poll 6 discussion:
    - \[ Editor's note: the original poll was "P2093R6: `<print>` facility implementors are encouraged
      to provide a run-time means for diagnosing format strings and formatter output that does not
      match encoding expectations." \]
    - Tom noted that this is not dependent on UB.
    - Hubert agreed.
    - Corentin expressed skepticism that this is implementable.
    - Hubert responded that the binary case is not well supported, but can be done and probably with 
      a reasonable result.
    - Hubert noted that it may be difficult for an implementation of this extension to distinguish the
      escaped binary data case.
    - Charlie noted that invalidly encoded data can be detected, but that mojibake cannot be.
    - Steve expressed desire for diagnostics for when the data doesn't match the encoding, but not for
      attempts to match mixed encodings.
    - Zach noted that heuristic warnings can result in false positives and false negatives.
    - Hubert observed that qualitative determination of good vs bad output may require a human.
  - **Poll 6: P2093R6: `<print>` facility implementors are encouraged to provide a run-time means for diagnosing format strings and formatter output that is not well-formed according to the expected encoding.**
    - Attendance: 8 (1 abstention)

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   4 |   0 |   2 |   1 |   0 |

    - Consensus: Consensus in favor.
    - A: I don't want double validation and this falls outside the standard.
- Tom stated that the next meeting will be in two weeks on June 23rd and that we will complete polling
  and discuss [LWG 3565](https://wg21.link/lwg3565).


# May 26th, 2021

## Agenda:
- [P2295R4: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r4)
  - Review updates intended to address prior SG16 feedback.
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - Discuss locale dependent character encoding concerns.

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
  - Zach Laine
- [P2295R4: Support for UTF-8 as a portable source file encoding](https://wg21.link/p2295r4)
  - \[ Editor's note: D2295R4 was the active paper under discussion at the telecon.  The agenda and links
    used here reference P2295R4 since the links to the draft paper were ephemeral.  The published document may
    differ from the reviewed draft revision. \]
  - PBrett provided an introduction.
  - Corentin presented and described the changes from R3 to the draft R4.
  - PBrett observed that the wording updates removed the prior definition for a *UTF-8 file* and added a new
    definition for a *UTF-8 source file*.
  - Tom recalled prior discussion that suggested there was no need to provide such a definition at all.
  - Jens confirmed and explained that the prior suggestion was to instead specify translation phase 1 in terms
    of a sequnce of characters instead.
  - Jens noted that there will be merge conflicts with
    [P2314](https://wg21.link/p2314).
  - Corentin asked if the merge conflicts can be dealt with after CWG reviews P2314.
  - Jens confirmed that they can be.
  - PBrett asked if progress can be made before P2314 is adopted into the working paper.
  - Jens confirmed that progress can be made.
  - PBrett asked Jens if he would like to see additional wording changes reviewed in SG16.
  - Jens replied that he would and noted that he had not received a response to all of the suggestions
    previously provided in his message to the mailing list available at
    https://lists.isocpp.org/sg16/2021/04/2353.php.
  - Jens observed that the proposed wording results in existing wording no longer applying to all source
    files.  For example, "Any source file character not in the basic source character set is replaced by
    the _universal-character-name_ that designates that character" now appears in a paragraph that doesn't
    apply to UTF-8 source files.
  - Corentin responded that this paper doesn't make sense without the changes from P2314.
  - Tom asked if the wording could be rebased on P2314 with a noted dependency on P2314.
  - Jens replied that it could be.
  - Hubert noted that the definition of a UTF-8 source file is problematic since the definition could apply
    to a file that just so happens to decode as UTF-8, but is not intended as a UTF-8 file.
  - PBrett responded that the following sentence specifies that encoding determination is
    implementation-defined.
  - Hubert acknowledged and suggested it might be helpful to reorder the sentences.
  - Hubert added that wording is still required to reflect intent that a file be interpreted as UTF-8.
  - PBrett agreed by way of an example; an implementation invoked without such intent may analyze a file,
    determine that it does not decode successfully as UTF-8, and then interpret it as, for example,
    Windows-1252, and do so without issuing a diagnostic.
  - Jens observed that the wording states that,
    "An implementation shall support UTF-8 source files",
    but there is no wording to require diagnosis of ill-formed UTF-8 source files.
  - Corentin responded that there is no such thing as an invalid UTF-8 file; either a file is valid UTF-8
    or it is not UTF-8.
  - Mark responded that there is a desire to have implementations produce a diagnostic if source files that
    are purported to be encoded as UTF-8 are not, in fact, valid UTF-8.
  - PBrett stated that there are three distinct requirements:
    - A requirement to support UTF-8 encoded source files.
    - A requirement for means to inform the implementation that all source files are to be assumed to be
      UTF-8 encoded.
    - A requirement that the implementation diagnose files that were assumed to be UTF-8 encoded but that
      contain (some) non-UTF-8 content.
  - Hubert offered some suggested wording in chat:
    - "An implementation shall provide for processing physical source files as having a UTF-8 encoding
      scheme without restriction, other than resource limits ([implimits]), upon the content of the
      physical source file."
  - Jens pasted previously suggested wording from the mailing list in chat:
    - "The encoding scheme of a physical source file is determined in an implementation-defined manner.
      An implementation shall support (possibly among others) the UTF-8 encoding scheme."
    - "If the encoding scheme of a physical source file is determined to be UTF-8, the physical source
      file shall consist of a well-formed sequence of UTF-8 code units as specified by ISO/IEC 10646."
  - Hubert expressed support for that wording but thought some additional updates would still be
    required to ensure diagnostics.
  - Corentin disagreed with removal of wording that requires that the scalar value of source file
    characters be preserved.
  - Jens responded that the scalar value preservation wording isn't required because the mapping to the
    translation character set already preserves characters.
  - Steve noted the existence of wording that uses the phrase "known to the implementation" and asked if
    that could be used to specify how source file encoding is determined.
  - Tom suggested that implementation-defined is preferred since that reflects a documentation requirement.
  - Hubert added that the "known to the implementation" wording is not intended to reflect that
    implementations can be wrong.
  - PBrett observed that Jens and Hubert would presumably like to see updated wording.
  - Hubert expressed a belief that the required wording has been identified and that he is onboard with the
    goal of preserving scalar value sequences from UTF-8 source files.
  - Corentin responded that he will bring back a revised paper with the suggested wording.
  - Steve informed the group that the EWG chair is considering dedicating a telecon to SG16 papers in the
    next month or so.
- [P2093R6: Formatted output](https://wg21.link/p2093r6)
  - PBrett reported a previous conversation with Victor in which Victor expressed that he felt he has the
    guidance he needs regarding handling of substitution characters and locale.
  - Victor presented slides:
    - The next question to be answered is whether it is ok to base behavior on the literal encoding.
    - Use of the literal encoding avoids race conditions with locale settings.
  - Discussion ensued regarding current dependencies on the choice of literal encoding and it was observed
    that, though the wording provided by
    [P1868](https://wg21.link/p1868)
    to specify estimated format field widths is not based on the literal encoding, at least one implementation
    is planning to only use the specified estimated widths when the literal encoding is UTF-8.
  - Hubert observed that field width estimation can apply to content from other than string literals.
  - PBrett provided an example; when `gettext()` is used, a literal is used for the message catalog lookup,
    but the result is not a string literal.
  - Hubert acknowledged the provided rationale, but noted that it does not address concerns raised and that
    he has seen many cases where use of locales works fine on UNIX systems.
  - Hubert added that this has the potential to bite existing users since code may appear to work correctly
    until it suddenly doesn't.
  - Victor replied that his goal is to make UTF-8 cases work as expected and that he is willing to accept
    some surprises in other scenarios.
  - Victor stressed that the intention is that, on UNIX systems, bytes are simply passed through.
  - Tom directed discussion towards the example code from the
    [telecon announcement](https://lists.isocpp.org/sg16/2021/05/2389.php).
  - Victor stated that he will request a LWG issue or author a paper to address handling of locale provided
    text.
  - \[ Editor's note: Victor requested an LWG issue that is now tracked as
    [LWG issue 3565](https://wg21.link/lwg3565). \]
  - Corentin stated that he is content with undefined behavior for cases where UTF-8 input is expected, but
    the input is not actually UTF-8 encoded.
  - Hubert responded that the format locale situation is rather urgent for EBCDIC environments.
  - PBrett stated that he is ok with the proposal because it won't break anything worse than it already is.
- Tom stated that the next telecon will be held on June 9th.


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
  - \[Editor's note: The chair's perception is that SG16's change in consensus is attributable to two factors:
    1) New information that arrived after the initial poll.
    2) SG16's original poll targeted C++23 while LEWG's poll targets C++23 and C++20 as a DR; some concerns
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
  - Tom suggested that an error handling facility might move us towards more consensus.
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
