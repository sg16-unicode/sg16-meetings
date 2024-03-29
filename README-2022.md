# SG16 2022 Meeting Summaries

This document contains summaries of SG16 meetings held during 2022.

- [More recent SG16 meetings](#more-recent-sg16-meetings)
- [December 14th, 2022](#december-14th-2022)
- [November 30th, 2022](#november-30th-2022)
- [November 2nd, 2022](#november-2nd-2022)
- [October 19th, 2022](#october-19th-2022)
- [October 12th, 2022](#october-12th-2022)
- [September 28th, 2022](#september-28th-2022)
- [September 14th, 2022](#september-14th-2022)
- [August 24th, 2022](#august-24th-2022)
- [July 27th, 2022](#july-27th-2022)
- [June 22nd, 2022](#june-22nd-2022)
- [June 8th, 2022](#june-8th-2022)
- [May 25th, 2022](#may-25th-2022)
- [May 11th, 2022](#may-11th-2022)
- [April 27th, 2022](#april-27th-2022)
- [April 13th, 2022](#april-13th-2022)
- [March 9th, 2022](#march-9th-2022)
- [February 23rd, 2022](#february-23rd-2022)
- [February 9th, 2022](#february-9th-2022)
- [January 26th, 2022](#january-26th-2022)
- [January 12th, 2022](#january-12th-2022)
- [Meetings held in 2021](#meetings-held-in-2021)


# More recent SG16 meetings

Meeting summaries for meetings held more recently than 2022 are available at
- https://github.com/sg16-unicode/sg16-meetings/blob/master/README.md


# December 14th, 2022

## Agenda
- [D2675R1: LWG3780: The Paper (format's width estimation is too approximate and not forward compatible)](https://wg21.link/p2675r1)
  - [LWG #3780: format's width estimation is too approximate and not forward compatible](https://cplusplus.github.io/LWG/issue3780)
  - [FR-007-012 22.14.2.2 \[format.string.std\] codepoints with width 2](https://github.com/cplusplus/nbballot/issues/409)
- [FR-020-014 5.3 \[lex.charset\] Replace "translation character set" by "Unicode"](https://github.com/cplusplus/nbballot/issues/422)

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Tom Honermann
  - Victor Zverovich
- [D2675R1: LWG3780: The Paper (format's width estimation is too approximate and not forward compatible)](https://wg21.link/p2675r1):
  - \[ Editor's note: D2675R1 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2675R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - PBrett summarized the changes in the draft R1 revision.
  - Corentin summarized an
    [email sent by Victor](https://lists.isocpp.org/sg16/2022/12/3623.php)
    that demonstrated behavior in which a wide character was rendered such that it
    overlapped an adjacent character because the terminal treated the character as
    a narrow one but the font in use rendered it as a wide character.
  - Corentin pointed out that the demonstrated behavior implies that character width
    cannot be determined by looking at a rendered character in isolation since the
    character rendering may exceed the bounds of a terminal cell.
  - Victor acknowledged it was a mistake to categorize the relevant characters as
    having a width of 2; the initial error was due to observing the rendered character
    without an adjacent character.
  - Victor expressed appreciation for the systematic approach proposed in the paper
    and that it appears to improve behavior.
  - Victor stated that it is difficult to interpret the screenshots currently in the
    paper.
  - PBrett suggested that it might be helpful to provide more constructive feedback
    to paper authors regarding how presentation can be improved.
  - Corentin explained that he had asked for contributions of screenshots from others
    since he did not have convenient access to the wide range of terminals that are
    used in practice.
  - Corentin reported that rendering issues that occur with just one or a small subset
    of terminals are common and asserted that we should not concern ourselves with
    such cases.
  - Corentin stated that he has not found cases that are contrary to the proposal and
    that have consistent behavior across the sampled terminals.
  - Victor, referring to an
    [email that Tom sent to the SG16 mailing list](https://lists.isocpp.org/sg16/2022/12/3621.php),
    reported having performed some further analysis with the attached source code and
    provided some constructive feedback.
  - \[ Editor's note: The mailing list software appears to have ignored, misplaced, or
    otherwise omitted the source code that was attached to that email. \]
  - Tom stated that we could spend additional time discussing the pros and cons of the
    screenshots but that doing so might not be a good use of our time.
  - Corentin opined that it would not be a good use of our time and agreed to remove
    most of the screenshots.
  - Jens summarized his understanding of the paper; that the standard currently specifies
    explicit code point ranges and the paper proposes changes to better align behavior
    with various terminals.
  - Tom voiced agreement.
  - Jens expressed concern that it is late in the release cycle for such changes.
  - PBrett replied that this addresses a defect.
  - Corentin noted that
    [LWG issue 3780](https://cplusplus.github.io/LWG/issue3780)
    already exists.
  - Tom explained that we can choose between recommending this as a change for C++23 or
    as a DR to be addressed in C++26.
  - PBrett expressed a preference for addressing this in C++23.
  - Victor noted that there already is consensus that width estimation is best effort and
    likely to change in the future.
  - Victor stated that there is not an urgent need to rush this into C++23 but that we
    might as well add it now if we agree the paper is ready.
  - Corentin explained that his motivation for targeting C++23 is to ensure that behavior
    varies as expected with whatever Unicode version is in use by an implementation.
  - Corentin noted that the situation will grow worse over time as the explicit code point
    ranges in the standard deviate further from existing practice as that practice changes
    with new Unicode releases.
  - **Poll 0.1: Forward D2675R1
    "format's width estimation is too approximate and not forward compatible",
    with improved presentation, to LEWG as the recommended resolution of LWG3780
    and NB comment FR-007-012.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   0 |   0 |   0 |
    - Unanimous consent.
  - **Poll 0.2: Recommend that D2675R1 be applied to the C++23 working paper.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   4 |   0 |   0 |   0 |
    - Unanimous consent.
- [FR-020-014 5.3 \[lex.charset\] Replace "translation character set" by "Unicode"](https://github.com/cplusplus/nbballot/issues/422):
  - Tom asked what new information has become available since we last discussed and
    polled this topic during the
    [2021-03-24 SG16 meeting](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md#march-24th-2021).
  - PBrett responded that the existence of an NB comment may constitute new information.
  - Corentin stated that removal of the "translation character set" term will require
    addressing the imprecise use of the term "character".
  - Corentin reported that the Unicode Standard states that an unassigned character must
    not be treated as a character and that treating one as such could be a Unicode
    conformance concern.
  - Corentin requested an indication of support for this direction before devoting the
    considerable time drafting a paper would require.
  - Jens noted that we don't claim conformance with the Unicode Standard; we only use it
    as a reference.
  - Tom opined that the current use of "character" does not constitute a Unicode
    conformance concern.
  - Tom asserted that a paper to address the imprecise use of "character" would be quite
    valuable regardless of any changes with respect to "translation character set".
  - PBrett expressed support for making changes with regard to "translation character set"
    either in C++23 or sometime after the use of "character" is addressed.
  - Corentin noted that the Unicode Standard intentionally does not define "character".
  - Corentin indicated that the paper he would write would address the core language, but
    not the standard library since addressing both would require such a significant effort.
  - PBrett asked if these changes could be done editorially.
  - Jens replied that there is potential for friction with the C standard since it also
    uses the term "character".
  - Tom reported that Ken Whistler recommended reviewing
    [UTR #17 (Unicode Character Encoding Model)](https://www.unicode.org/reports/tr17)
    for terminology to use.
  - Corentin replied that he would review it.
  - Corentin noted that, after translation phase 1, the elements of the translation
    character set are all Unicode scalar values because surrogate code points are not
    allowed and asked what terminology should be used.
  - Tom replied that, in an offline discussion, he had suggested to Corentin that we prefer
    "code point" in general discussion and reserve "scalar value" for use as a form of
    qualifier to restrict code point allowances.
  - Jens requested a paper that describes the desired end state before considerable effort
    is put into producing wording.
  - PBrett replied that doing so implies rejecting the NB comment.
  - Jens replied that, without a paper, rejection is the only option as there can be no
    consensus for a specific change.
  - Tom noted that there is very little time left for making changes to C++23.
  - **Poll 1.1: Encourage further work on expressing the semantics of C++ lexing in terms
    of the terminology defined in the Unicode Standard.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   1 |   0 |   1 |   0 |
    - Strong consensus.
    - A: I'm concerned about interaction with the C standard and introducing inconsistency
      between core wording and library wording.
- [D2736R0: Referencing the Unicode Standard](https://wg21.link/p2736r0):
  - \[ Editor's note: D2736R0 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2736R0 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin noted that the previous feedback was to try to ensure that the change of
    reference would have no normative impact on behavior.
  - Corentin explained that there is a design question regarding the `__STDC_ISO_10646__`
    predefined macro; the macro is specified by the C standard as having a value that reflects
    the date of a ISO/IEC 10646 standard.
  - Corentin reported that there are known issues with the macro; compilers can't predefine it
    because the value to define it to is determined by the C standard library.
  - Corentin stated that the macro is only useful to distinguish between old 16-bit Unicode
    and modern 21-bit Unicode.
  - Corentin suggested that the C++ standard could specify it to have an implementation-defined
    value like it does for `__STDC_VERSION__`.
  - Corentin suggested another alternative would be to specify it as having a Unicode version
    date instead.
  - PBrett suggested specifying it to have a value that matters.
  - Corentin explained that implementations that use a 16-bit `wchar_t` can't define this macro
    to any relevant Unicode or ISO/IEC 10646 standard.
  - Jens replied that in those cases, he would expect the macro to be defined for the last
    ISO/IEC 10646 standard that had a 16-bit code point space.
  - Jens suggested the value should just reflect the size of `wchar_t`.
  - Corentin noted that the macro also reflects whether values of `wchar_t` correspond to a
    Unicode encoding; which could be locale dependent.
  - Tom summarized three possibilities:
    - `wchar_t` has an associated encoding that is not a Unicode encoding; the macro is not
      defined.
    - `wchar_t` is 16-bit and the associated encoding is UCS-2; the macro is defined to reflect
      an obsolete ISO/IEC 10646 standard.
    - `wchar_t` is 32-bit and the associated encoding is UTF-32; the macro is defined to reflect
      a relatively current ISO/IEC 10646 standard.
  - Jens opined that this requires coordination with WG14.
  - PBrett asked if we can deprecate the macro.
  - Jens replied that we can choose to deviate from the C standard but noted that the macro can
    be useful.
  - PBrett asked about Corentin's previous suggestion to just state that the macro has an
    implementation-defined value.
  - Jens opined that the macro has some value.
  - Jens noted that the C++ standard has library wording that states that all elements of the
    wide character set are representable as values of `wchar_t` and that the presence of the
    macro definition in core wording is suggestive of applicability to wide character and
    string literals.
  - Tom suggested some compare and contrast analysis with the C standard.
  - Corentin stated that it isn't clear to him that WG14 knows what this macro is intended for.
  - Corentin pondered deprecation, but not as a part of this paper.
  - Corentin reported that code searches revealed few references to the macro that are sensitive
    to the macro value; most code just checks if the macro is defined.
- Tom announced that the next two telecons are scheduled for 2023-01-11 and 2023-01-25 and
  will be followed by the WG21 meeting in Issaquah in early February.


# November 30th, 2022

## Agenda
- [P2713R0: Escaping improvements in std::format](https://wg21.link/p2713r0)
  - [US 38-098 22.14.6.4p1 \[format.string.escaped\] Escaping for debugging and logging](https://github.com/cplusplus/nbballot/issues/515)
  - [FR 005-134 22.14.6.4 \[format.string.escaped\] Aggressive escaping](https://github.com/cplusplus/nbballot/issues/408)
- [P2693R0: Formatting thread::id and stacktrace](https://wg21.link/p2693r0)
  - [FR-008-011 22.14 \[format\] Support formatting of thread::id](https://github.com/cplusplus/nbballot/issues/410)
- [FR-010-133 \[Bibliography\] Unify references to Unicode](https://github.com/cplusplus/nbballot/issues/412) and<br/>
  [FR-021-013 5.3p5.2 \[lex.charset\] Codepoint names in identifiers](https://github.com/cplusplus/nbballot/issues/423)
- [P2675R0: LWG3780: The Paper (format's width estimation is too approximate and not forward compatible)](https://wg21.link/p2675r0)
  - [LWG #3780: format's width estimation is too approximate and not forward compatible](https://cplusplus.github.io/LWG/issue3780)
  - [FR-007-012 22.14.2.2 \[format.string.std\] codepoints with width 2](https://github.com/cplusplus/nbballot/issues/409)
- [FR-020-014 5.3 \[lex.charset\] Replace "translation character set" by "Unicode"](https://github.com/cplusplus/nbballot/issues/422)

## Meeting summary
- Attendees:
  - Charles Barto
  - Corentin Jabot
  - Jens Maurer
  - Mark de Wever
  - Mark Zeren
  - Nathan Owen
  - Peter Brett
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2713R0: Escaping improvements in std::format](https://wg21.link/p2713r0):
  - Tom reported that the paper implements the previous guidance provided for
    [US 38-098](https://github.com/cplusplus/nbballot/issues/515)
    during the
    [2022-10-19 SG16 telecon](https://github.com/sg16-unicode/sg16-meetings#october-19th-2022)
    and for
    [FR 005-134](https://github.com/cplusplus/nbballot/issues/408)
    during the
    [2022-11-02 SG16 telecon](https://github.com/sg16-unicode/sg16-meetings#november-2nd-2022)
    so all that should be needed is to confirm the paper via a poll.
  - Tom noted that some minor wording feedback was provided in a
    [post to the SG16 mailing list](https://lists.isocpp.org/sg16/2022/11/3586.php).
  - Victor presented the paper and further wording review commenced.
  - **Poll 1: P2713R0: Forward to LEWG as the recommended resolution of US 38-098 and FR 005-134
    amended with discussed wording changes.**
    - Attendees: 10
    - No objection to unanimous consent.
- [P2693R0: Formatting thread::id and stacktrace](https://wg21.link/p2693r0):
  - Corentin provided an introduction.
  - Victor reported Bryce's rationale for SG16 review; there were questions about wide string
    support.
  - Victor noted that the `ostream` inserters for `stacktrace_entry` and `basic_stacktrace`
    do not support wide ostreams, so the lack of support for `std::format` is consistent.
  - Corentin stated that there is no guarantee that `std::thread::id` will be formatted
    consistently for `char` and `wchar_t`.
  - Jens, referring to the proposed \[stacktrace.format\] wording, noted that "must" is not
    allowed in normative wording.
  - Victor asked what should be used instead.
  - Tom suggested "mandates" or "requires".
  - Victor explained that the wording intent is that a non-empty *format-spec* evaluated at
    compile-time render the program ill-formed and result in a format error exception if
    evaluated at run-time.
  - Jens suggested wording the requirements in terms of format string validity.
  - Charles noted that a thread ID is a handle on Windows.
  - Charles stated that his only concern is whether additional header inclusion might be
    required but the proposal looks fine otherwise.
  - Jens suggested dropping the "The syntax of format specifications is as follows" sentence
    in the wording for `formatter<thread::id, charT>`.
  - Tom stated that any changes to require wide character support for stacktrace or consistent
    text representation for `std::thread::id` would be out of scope.
  - **Poll 2: P2693R0: Forward to LEWG as the recommended resolution of FR-008-011.**
    - Attendees: 10
    - No objection to unanimous consent.
- [FR-010-133 \[Bibliography\] Unify references to Unicode](https://github.com/cplusplus/nbballot/issues/412) and<br/>
  [FR-021-013 5.3p5.2 \[lex.charset\] Codepoint names in identifiers](https://github.com/cplusplus/nbballot/issues/423):
  - Corentin explained that authoring a paper to address these NB comments is on his todo list.
  - Corentin invited offers to help with a paper.
  - Jens stated that it will be important to understand how the change to the normative reference
    impacts how wording is interpreted throughout the standard.
- [P2675R0: LWG3780: The Paper (format's width estimation is too approximate and not forward compatible)](https://wg21.link/p2675r0):
  - Corentin provided an introduction.
    - Victor had initially identified a range of code points that specify characters to be
      considered as having an estimated width of two.
    - That code point range corresponds to Unicode 13 and has not been updated for more recent
      Unicode Standard versions.
    - Analysis of source code and behavior in existing terminals inspired the current proposal
      to derive the code point ranges from the Unicode character property database.
  - Victor expressed mixed feelings regarding the proposal; though the idea is favorable,
    consulted sources indicate that the Unicode properties don't predict how characters are
    displayed particularly well.
  - Victor indicated support for consideration of the Unicode width property, but that code
    point ranges that are ambiguous should be retained.
  - Victor stated that all of the code points that change from an estimated width of two to
    an estimated width of one are rendered with a width of two in his environment, so those
    cases appear to constitute a regression.
  - Victor acknowledged that the proposal looks like a good step in the right direction.
  - Victor raised U+2E9A as an example; it is an unassigned character in a block for which
    characters are assumed to have a width of two and it is rendered as a wide unassigned
    character.
  - \[ Editor's note: In Unicode 15.0,
    [U+2E9A](https://util.unicode.org/UnicodeJsps/character.jsp?a=%E2%BA%9A&B1=Show)
    is a reserved unassigned character in the
    [CJK Radicals Supplement block](https://www.unicode.org/charts/PDF/U2E80.pdf)
    and its `East_Asian_Width` property value is `N` (Neutral).
    \]
  - Corentin replied that terminals that display such characters as wide characters are
    non-conforming.
  - Corentin argued that use of the Unicode character database is justified by the lack of
    anything obviously better.
  - Corentin asserted that estimated width is necessarily an approximation at present.
  - Corentin stated his goal with the proposal is to prioritize a principled solution with
    predictability.
  - Zach observed that there appear to be some contradictions and pondered how they might be
    resolved.
    - There is a desire to be forward compatibile and to defer to the Unicode Standard.
    - There is a desire to consider certain unassigned code points as wide until they are
      assigned a width by the Unicode Standard.
  - Corentin stated that existing behavior should be evaluated before choosing to deviate
    from Unicode.
  - PBrett observed that wide divergence can be observed between different rastorizers and
    stated that he does not relish the idea of identifying the subset of behavior that is
    exhibited in the wild.
  - Victor expressed skepticism regarding the feasibility of relying only on Unicode.
  - Victor stated that Unicode conformance doesn't apply to this situation.
  - Victor cautioned that the traditional Windows console behavior should not be used as a
    reference as it exhibits notoriously poor behavior.
  - Corentin indicated an intent to update the paper with references to the scripts used
    to collect data and evaluate behavior.
- [FR-020-014 5.3 \[lex.charset\] Replace "translation character set" by "Unicode"](https://github.com/cplusplus/nbballot/issues/422):
  - Discussion was postponed due to lack of time.
- Tom reported that the next meeting will take place on December 14th, 2022.


# November 2nd, 2022

## Agenda
- NB comment processing.

## Meeting summary
- Attendees:
  - Charles Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Mark de Wever
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [FR 005-134 22.14.6.4 \[format.string.escaped\] Aggressive escaping](https://github.com/cplusplus/nbballot/issues/408):
  - Corentin explained that the direction polled for
    [US 38-098](https://github.com/cplusplus/nbballot/issues/515)
    during the
    [October 19th, 2022 SG16 meeting](#october-19th-2022)
    suffices to resolve this issue.
  - Victor agreed that the prior poll result is consistent with the first option of the proposed change.
  - **Poll 1: \[FR 005-134\]: SG16 recommends accepting the comment in the direction presented in the
    first bullet of the proposed change and as recommended in the polls for US 38-098.**
    - Attendees: 8
    - Unanimous consent
  - Corentin asked if anyone is preparing wording for US 38-098.
  - Hubert replied that no wording was provided with the comment.
  - Victor noted that the proposed change for US 38-098 did have the suggestion to replace "logging"
    with "technical logging".
  - Hubert replied that the direction polled didn't include that change.
  - Tom stated that wording will be left up to LWG without a volunteer.
- [GB-031 5.2 \[lex.phases\] Clarification of wording on new-line and whitespace](https://github.com/cplusplus/nbballot/issues/432):
  - Tom lamented Peter Brett's absence.
  - Tom recalled recent
    [discussion on the SG16 mailing list](https://lists.isocpp.org/sg16/2022/10/3495.php)
    that suggested a possible misunderstanding regarding feedback provided during the
    [2022-09-09 CWG review](https://wiki.edg.com/bin/view/Wg21telecons2022/Teleconference2022-09-09)
    of a draft of
    [P2348R3](https://wg21.link/p2348r3).
  - Corentin explained that CWG was dissatisfied with the amount of churn involved in the paper and
    preferred an approach that addresses whitespace issues during translation phase 1.
  - Corentin expressed disagreement with that approach and stated that he doesn't plan to pursue it.
  - Corentin acknowledged that an issue exists.
  - Steve expressed support for fixing the issue eventually but that he is weakly against doing so
    via an NB comment since, though the risk is low, late fixes can have unintended consequences.
  - Jens disagreed with Corentin's summary of the CWG review, specifically with the claim that CWG
    wanted all whitespace issues to be addressed in translation phase 1.
  - Jens explained that what CWG requested was for translation phase 1 to translate all accepted
    new-line forms to a single new-line character in the translation character set.
  - Jens reported that CWG determined that the form of a new-line expressed in an input file is
    not observable by a program, not even in a raw string literal.
  - Jens agreed with Corentin's claim that CWG recommended against the churn proposed in the paper.
  - Jens explained the status quo, that translation phase 1 does not currently allow a UTF-8 encoded
    input file to have a new-line sequence other than U+000A (LINE FEED); the wording prohibits the
    use of U+000D (CARRIAGE RETURN) followed by U+000A (LINE FEED) as a new-line indicator.
  - Jens noted that
    [US 3-030](https://github.com/cplusplus/nbballot/issues/475)
    requests a change that matches the CWG feedback.
  - Tom asked Corentin if Jens' explanation was helpful.
  - Corentin replied that he doesn't want to object to progress but that he lacks bandwidth to work
    on the issue himself.
  - Corentin offered to share the source to
    [P2348](https://wg21.link/p2348)
    to anyone interested in working on a revision.
  - Steve stated that, based on the intended scope, he would not object to CWG's preferred direction.
  - Steve volunteered to look into producing a revision of P2348 if Corentin makes the source
    available.
  - Tom stated that Jens' comments suggest a path forward of rejecting this comment in favor of
    pursuing US 3-030.
  - Jens suggested that further action await a revision of P2348 and that this NB comment be
    handled procedurally as not having consensus for a change.
  - Corentin noted that P2348 went through the committee pipeline and doesn't need to be rushed.
- [FR-009-024 Annex E \[uaxid\] Shorten contents and integrate with \[lex.name\]](https://github.com/cplusplus/nbballot/issues/411):
  - Tom mentioned that this issue was briefly discussed with the discussion of
    [US 64-132](https://github.com/cplusplus/nbballot/issues/542)
    during the
    [October 19th, 2022 SG16 meeting](#october-19th-2022).
  - Corentin stated that it is not yet clear that we understand
    [UAX #31](https://unicode.org/reports/tr31)
    sufficiently well to declare conformance.
  - Corentin asserted that, assuming retaining annex E is desirable, additional work is needed
    to evaluate conformance against a specific version of UAX #31, but it isn't clear which
    version that evaluation should be performed against.
  - Corentin claimed that it is not clear that annex E is necessary or useful.
  - Corentin noted that it would be useful to note some of the associations in
    [\[lex.name\]](http://eel.is/c++draft/lex.name).
  - Steve replied that the burden of conformance is the same regardless of where it is stated.
  - Steve added that he is disinclined to abandon attempting to state conformance.
  - Steve asserted that, similarly to undefined behavior, it is hard to find answers for things
    that are not explicitly stated in the standard.
  - Steve claimed that statements regarding what is and is not intended to be conforming are
    useful.
  - Steve noted that the placement of the conformance statements in an annex avoids interactions
    with normative wording.
  - Jens reported that the reference to UAX #31 in the
    [bibliography](http://eel.is/c++draft/bibliography)
    specifically refers to revision 33 and Unicode 13.
  - Jens asserted that it is preferable that the C++ standard specify the syntax of identifiers
    itself rather than by deference to Unicode.
  - Jens expressed support for expanding annex E to include statements of conformance for other
    Unicode requirements in a future standard.
  - Jens noted that some of the clarifications made to UAX #31 for Unicode 15 were directly
    inspired by the initial attempt to state conformance in annex E and that such a feedback
    cycle is a valuable result.
  - Jens stated that annex E doesn't require significant maintenance and, since it is
    non-normative, a failure to update it would not be highly consequential since it has no
    implementaiton impact.
  - Corentin stated that the Unicode standard is defined as a complete set and is not intended
    or designed to support cherry picking different versions of its parts.
  - Corentin provided normalization as an example of Unicode specification that is defined
    across multiple parts of the Unicode Standard.
  - **Poll 2: [FR-009-024]: SG16 recommends rejecting the comment on the basis that explicit
    indication of Unicode requirement conformance, non-conformance, or inapplicability is useful.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   1 |   0 |   1 |
    - Consensus.
- [FR-010-133 \[Bibliography\] Unify references to Unicode](https://github.com/cplusplus/nbballot/issues/412)
  and <br/>
  [FR-021-013 5.3p5.2 \[lex.charset\] Codepoint names in identifiers](https://github.com/cplusplus/nbballot/issues/423):
  - Corentin explained that the C++ standard currently references four distinct Unicode versions
    for various purposes but that implementations, Clang specifically, intend to adopt behaviors
    from newer Unicode versions as releases occur.
  - Corentin described a technical inconsistency that results from the disjoint version references:
    - The range of UCS scalar values that can be expressed in a *universal-character-name* (UCN)
      is determined by the ISO/IEC 10646 version.
    - The set of character names recognized for a *named-universal-character* (NUC) are likewise
      determined by the ISO/IEC 10646 version.
    - The set of UCS scalar values allowed in an *identifier* is determined by the `XID_Start` and
      `XID_Continue` properties defined in the referenced
      [UAX #44](https://unicode.org/reports/tr44)
      version.
    - If the version of UAX #44 referenced corresponds to a newer version of the Unicode Standard
      than the associated version for the referenced version of ISO/IEC 10646, then there will
      exist some identifiers that can be spelled as, for example, `x\u1234` but not as
      `x\N{NAME_FOR_1234}`.
  - Steve expressed concern that updating the referenced versions might break section references.
  - Corentin replied that he checked all references and only found one section reference; the
    reference for the Unicode replacement character in
    [\[ostream.formatted.print\]](http://eel.is/c++draft/ostream.formatted.print)
    specifically references chapter 3.9 of the core specification for Unicode 14.
  - Steve stated that the bibliography is intended to reflect what the author was reading when
    writing the C++ standard.
  - Corentin agreed and noted that normative changes should be made as necessary when the versions
    referenced in the bibliography are updated.
  - Steve noted that such concerns will be more important for future library features that have
    a deeper dependence on the Unicode Standard.
  - Tom noted that the ISO requires references to other ISO standards to reference the most recent
    version and asked if that applies to non-ISO standards as well.
  - Jens replied that the ISO prefers undated references.
  - Jens explained that outdated ISO versions don't really exist from the ISO perspective since a
    newer version is intended to replace a previous version; references to previous releases are
    somewhat like dangling pointers.
  - Jens noted that, practically speaking, older versions do exist and that we do refer to older
    versions when necessary; like we have to do for UCS-2.
  - Jens further explained that a dated reference is used for C since normative changes are very
    likely required to accommodate a newer version.
  - Corentin explained that, at present, there is a mix of specific version references and floating
    references and that some are normative and some are non-normative.
  - Corentin stated that the only change that would have a normative impact is for named character
    sequences.
  - Jens stated that the Unicode Standard is referenced for cases where the needed subject matter
    is not present in an ISO standard.
  - Jens noted that ISO prefers referencing ISO standards when possible.
  - Jens suggested that the project editor should have more insight into the rules provided by ISO
    regarding references to ISO standards vs the Unicode Standard.
  - Corentin clarified that the NB comment is not asking to only refer to the Unicode Standard; it
    is asking that named character sequences be made consistent with other uses of Unicode
    functionality.
  - Jens noted that the character names are present in ISO/IEC 10646, but that the properties
    needed for identifiers are not.
  - Hubert suggested that, when a reference is needed to the Unicode Standard, that the version
    aligned with ISO/IEC 10646 be referenced.
  - Hubert stated that implementations can then veto that in favor of newer versions and that
    no one would complain.
  - Hubert raised the option of asking the project editor to make a request to the ISO that
    the scope of ISO/IEC 10646 be expanded to include the additional Unicode features that we
    need.
  - Hubert expressed a preference towards referencing ISO/IEC 10646 for terms and definitions
    because the ISO's practice tends to be more stringent than the Unicode Consortium's.
  - Corentin repeated his goal to improve consistency; that the references be updated so that
    the character names and XID properties be sourced from the same reference.
  - Hubert asked why the reference for extended grapheme cluster is non-normative.
  - Jens replied that he thinks
    [UAX #29](https://unicode.org/reports/tr29)
    is only referenced to satisfy normative encouragement for an implementation direction.
  - Charlie expressed agreement with Jens' recollection.
  - Hubert stated that normative encouragement should require a normative reference.
  - Jens agreed that is probably true.
  - Corentin asserted that, as more support for Unicode is added to C++, there will be more
    need for references to the Unicode Standard that can't be satisfied by ISO/IEC 10646.
  - Jens admitted he was surprised when he first joined SG16 to learn that ISO/IEC 10646
    specifies a subset of the features present in the Unicode Standard.
  - Tom asked if changes to reference the Unicode Standard version that is aligned with the
    referenced ISO/IEC 10646 version would resolve the concern.
  - Jens noted that the current reference to ISO/IEC 10646 is undated.
  - MarkZ suggested the right approach would be to just reference the Unicode Standard.
  - Corentin suggested that the next action be to coordinate with the project editor to
    better understand our options.
  - Steve suggested it might be best to state that implementations should use the
    Unicode Standard version that aligns with their version of ISO/IEC 10646.
  - Tom stated that the
    [Unicode FAQ](https://unicode.org/faq/unicode_iso.html)
    explicitly states which Unicode Standard version is aligned with each ISO/IEC 10646
    version and asked if ISO/IEC 10646 is similarly explicit.
  - Jens checked and reported that it is not, but that it embeds links that are version
    specific.
  - Corentin stated that the highest priority is to provide consistent references and that
    we can rely on forward compatibility guarantees.
  - Jens noted that, though we do understand and appreciate the Unicode stability guarantees,
    we are obligated to verify that those commitments are honored.
  - **Poll 3: \[FR-010-133\]\[FR-021-013\]: SG16 requests that the project editor discuss with the
    ISO the option of eschewing references to ISO/IEC 10646 in favor of the Unicode Standard
    both for technical consistency and release frequency.**
    - Attendees: 9 (1 abstention)
    - Objection to unanimous consent.
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   0 |   1 |   1 |
    - Weak consensus
    - SA: Use of the ISO/IEC 10646 document benefits from ISO governance.
    - SA: Would prefer to explore expansion of ISO/IEC 10646 to include more components of Unicode.
  - Hubert indicated he might work with his NB to raise comments on the next ballot of
    ISO/IEC 10646 to request that it expand its scope.
  - MarkZ suggested that quality issues could also be reported to the Unicode Consortium.
  - MarkZ noted that interoperation with other languages and runtimes might be improved by
    aligning with the Unicode Standard.
  - **Poll 4: \[FR-010-133\]\[FR-021-013\]: SG16 recommends resolving these comments by restricting
    all references to the Unicode Standard to the version that corresponds to the referenced
    version of ISO/IEC 10646.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   3 |   0 |   3 |   0 |
    - No consensus.
    - A: It doesn't benefit the community to reference a Unicode version that is outdated by the
      time the standard is published.
  - Steve suggested that it might be helpful to explore different guarantees for core language vs
    the standard library.
  - Hubert agreed that it is conceivable that use of different Unicode Standard versions for the
    core language and the standard library would be ok.
- Tom reported that the next meeting will take place on November 30th.


# October 19th, 2022

## Agenda
- NB comment processing.

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [US 2-029 3.35 \[defns.multibyte\] Give context for "execution character set"](https://github.com/cplusplus/nbballot/issues/474)
  - Steve presented the concern:
    - The definition of multibyte character refers to the locale dependent execution character set.
    - Changing this might be difficult, but removing the reference to "execution character set" might
      help.
  - Hubert stated that the use of "multibyte character" in the library wording is consistent with the
    definition.
  - Tom asked if Hubert is suggesting that this is not a defect.
  - Hubert responded affirmatively.
  - Steve stated that he would agree if the definition was in the library section.
  - Jens explained that there used to be a terms and definitions section in the library wording but
    that ISO required it to be merged with the section in the core wording back in the C++17 time frame.
  - Hubert noted that the only use of "multibyte character" is in the library wording.
  - Corentin responded that there are indirect uses of it via "multibyte string" and "NTMBS" in the
    definition of the `main` function in
    [\[basic.start.main\]](http://eel.is/c++draft/basic.start.main).
  - Corentin noted that all uses of it are intended to refer to the locale encoding.
  - Tom asked if it would make sense to strike the term so that it is inherited from the C standard.
  - Jens expressed a preference not to do so.
  - Steve stated that doing so might have unintended consequences.
  - Tom summarized the sentiment expressed so far; we're leaning towards this not being a defect but
    that there are opportunities for improvement via editorial changes.
  - Tom suggested that any such editorial changes be left up to the CWG.
  - Jens replied that the CWG is likely to decline to make any changes without a proposed change.
  - Corentin asked if an editorial pull request could be submitted.
  - Jens replied affirmatively.
  - Hubert stated that the concern that Corentin raised regarding use of "multibyte character" with
    `main` is an issue.
  - Jens asserted that would be a different core issue.
  - **Poll 1: \[US 2-029\] SG16 suggests to consider this issue as "not a defect", but to improve
    the presentation by editorially moving the definition of "multibyte character" to
    [\[multibyte.strings\]](http://eel.is/c++draft/multibyte.strings).**
    - Attendees: 8
    - No objection to unanimous consent.
  - \[ Editor's note: Corentin submitted a pull request that implements the polled direction at
    https://github.com/cplusplus/draft/pull/5910. \]
- [US 38-098 22.14.6.4p1 \[format.string.escaped\] Escaping for debugging and logging](https://github.com/cplusplus/nbballot/issues/515):
  - Hubert presented the concern:
    - The feature description claims to provide a larger scope than it serves; the design doesn't
      suffice to address all logging scenarios.
    - It is not clear that the escaped string is required to be usable as a string literal.
  - Victor opined that the proposed change to replace "logging" with "technical logging" makes sense.
  - Victor expressed a preference against the second bullet regarding visually distinguishing
    equivalent text that is differently encoded.
  - Victor stated that the primary motivation for the feature was to produce a character sequence
    that would not interfere with the formatting of ranges.
  - Victor noted that the feature has existing experience with both Python and Rust and that the
    chosen design is modeled after Rust.
  - Victor asserted that the proposed change to allow for future addition of alternative escaping
    methods is unnecessary since other extension methods are already available.
  - Jens stated that the concern seems mostly related to the first sentence of
    [\[format.string.escaped\]](https://eel.is/c++draft/format.string.escaped):
      > "A character or string can be formatted as *escaped* to make it more suitable for debugging or for logging".
  - Jens continued; and the request is to make it clear that the escaped result shall be valid for
    interpretation as a string literal and that "logging" be replaced with "technical logging".
  - Hubert agreed, but noted there is still a question of whether visually distinct output is desired.
  - Hubert reiterated; the first priority is that the escaped result is a valid string literal, and
    a secondary priority is that text that might not be visually distinct be made so.
  - Jens stated that the minimal change would be to change that first sentence.
  - Jens noted that no actual defect has been identified.
  - Hubert stated that SG16 may not be the best place to fully resolve the comment; the question of
    extension remains and is more of a LEWG consideration.
  - Jens suggested that, for LWG's benefit, SG16 should propose a change to that first sentence.
  - Corentin stated that NB comment FR-005-134 similarly states that the intent of the feature is
    not clear.
  - Corentin asserted there are further questions regarding the escaping of grapheme clusters and
    that it is not clear what is intended to be escaped and for what purpose.
  - Corentin expressed concern that the currently specified behavior of escaping all combining
    characters disadvantages some languages more than others and provided Korean as an example.
  - Victor acknowledged that US 38-098 and FR-005-134 both state that the intent is not clear, but
    noted that their proposed resolutions are not in agreement.
  - Victor agreed with Corentin that users of scripts that require more use of combining characters
    should not be penalized.
  - Victor stated that the Python form of the feature does not escape combining characters and that
    can result in interference with range separators.
  - Victor noted that the original proposal only escaped lone combining characers and acknowledged
    that the switch to the Rust approach might have gone too far.
  - Hubert disagreed with the notion that a failure to escape does not harm the technical debugging
    use case.
  - Mark reported experience with use cases where text content is only available via an image;
    perhaps a screen shot captured with a phone.
  - Mark stated that he has only experienced a need for escaped characters in cases where the text
    was not correctly encoded.
  - Mark noted it is a valid question as to whether the standard library should default to producing
    visually indistinct text.
  - Tom stated that a goal of maximizing visual distinction would require escaping all characters not
    in the basic character set.
  - Corentin replied that it would be terrible to escape all non-ASCII characters but that doing so
    would not be worse than escaping all combining characters.
  - Corentin expressed a preference towards either maximizing escaping or minimizing it.
  - Hubert stated that the scripts like Korean provide strong motivation for a minimally escaped form.
  - Hubert noted that there are still valid reasons for wanting a visually distinct form via an easy
    opt-in.
  - Victor reiterated that the primary goal of the escaped form was to avoid interference with the
    formatted range output.
  - Victor suggested that desires for other use cases be pursued via new papers rather than NB comments.
  - Victor asserted that it is useful to have ill-formed code units escaped.
  - Mark expressed a preference towards not escaping combining characters due to the readability harm
    it would impose on scripts like Korean.
  - Corentin asserted that all use cases can't be satisfied with this single facility but that
    extensions can satisfy more post-C++23.
  - Corentin expressed a preference towards a default that maintains readability for more languages
    and that more extensive escaping can be pursued separately.
  - Hubert opined that a sequence of combining characters that immediately follow an escaped character
    is sufficient evidence of an error to justify escaping them.
  - Corentin repeated that it is useful to escape non-printable characters.
  - Corentin stated that the grapheme breaking algorithm is potentially expensive, but then backtracked
    with an observation that it is sufficient to check for the `Grapheme_Extend=Yes` character
    property to identify combining characters that may need to be escaped.
  - **Poll 2.1: \[US 38-098\] SG16 agrees that the formatted code units in the escaped string are intended
    to be usable as a string literal that reproduces the input.**
    - Attendees: 8
    - No objection to unanimous consent.
  - **Poll 2.2: \[US 38-098\] SG16 agrees that the escaped string is intended to be readable for its textual
    content in any Unicode script.**
    - Attendees: 8
    - No objection to unanimous consent.
  - **Poll 2.3: \[US 38-098\] SG16 agrees that separators and non-printable characters
    ([\[format.string.escaped\]p(2.2.1.2)](https://eel.is/c++draft/format.string.escaped))
    shall be escaped in the escaped string.**
    - Attendees: 8
    - No objection to unanimous consent.
  - **Poll 2.4: \[US 38-098\] SG16 agrees that combining code points shall not be escaped unless there is no
    leading code point or the previous character was escaped.**
    - Attendees: 8
    - No objection to unanimous consent.
  - Tom stated that he would provide examples for each of the polls when reporting the SG16 consensus
    once the NB comment github repository is populated.
  - Tom suggested that anyone that works on proposed wording include examples.
- [US 64-132 Annex E.4 Whitespace and pattern rules](https://github.com/cplusplus/nbballot/issues/542):
  - Tom noted that FR-009-024, if adopted, will make this NB comment moot.
  - Corentin explained the motivation for the FR-009-024 comment; that the annex is light on information,
    that many of the requirements don't apply to C++, and that the ones that do could be noted in
    [\[lex.name\]](http://eel.is/c++draft/lex.name).
  - Steve responded that an explicit record of a negative answer to a question is useful.
  - Steve explained that it would be difficult to identify Unicode requirement conformance information
    if it was spread throughout the standard wording.
  - Tom observed that differing opinions are clearly present with regard to the utility of the annex
    and stated that, due to time constraints, discussion will be limited to US 64-132 for now; discussion
    of FR-009-024 will be scheduled for a future meeting.
  - Steve expressed an expectation of agreement that UAX #31 is intended to apply to general purpose
    programming languages.
  - Hubert expressed a desire for more details and noted that conformance is not currently claimed.
  - Tom provided a link to Unicode document
    [L2/22-179](https://www.unicode.org/L2/L2022/22179-uax31-36-draft-6-post-pri450.pdf);
    it contains highlighted markup of the changes that were accepted for Unicode 15.
  - Tom noted the changes added to the beginning of chapter 4, "Pattern Syntax":
      > Most programming languages have a concept of whitespace as part of their lexical
      > structure, as well as some set of characters that are disallowed in identifiers but have
      > syntactic use, such as arithmetic operators. Beyond general programming
      > languages, there are also ...

    and the changes to the "Modifications" section at the end of the document:
      > - Section 4, Pattern Syntax
      >   - Clarified that this section is applicable to programming languages.
  - Jens observed that the NB comment is missing a reference to the updated Unicode document that
    clarifies applicability to general purpose programming languages.
  - Jens suggested that the annex could state that
    [\[lex.name\]](http://eel.is/c++draft/lex.name)
    defines a profile.
  - Hubert expressed a preference to continue claiming non-conformance pending a clear specification
    of a conforming profile.
  - Steve expressed contentedness with a change to just claim non-conformance.
  - Jens observed that consensus appeared to be aligning with the proposed change from the NB comment
    as opposed to the one proposed in
    [P2653R0 (Update Annex E based on Unicode 15.0 UAX 31)](https://wg21.link/p2653r0).
  - Steve asked if such a change could be applied editorially.
  - Tom opined that it could be.
  - Jens expressed a desire for CWG to review first and stated that, if a paper revision can be made
    available quickly, that he would schedule it for CWG review later in the week.
  - Steve agreed to prepare a revision.
  - **Poll 3: \[US 64-132\] SG16 agrees with resolving the issue in the direction presented in the
    comment.**
    - Attendees: 8
    - No objection to unanimous consent.
- Tom discussed plans for the next SG16 meeting:
  - Review of the GB and FR draft NB comments identified 7 comments for SG16 to review
  - It is not yet known if additional NB comments from other NBs will require review.
  - The next meeting is scheduled for 2022-11-02.
  - Once an agenda is sent, please discuss in email in advance of the meeting in order to reduce
    review time during the meeting.


# October 12th, 2022

## Agenda
- Michael Kuperstein: Internationalization From the Perspective of Defect Analysis
- NB comment processing.

## Meeting summary
- Attendees:
  - Charles Barto
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Mark Zeren
  - Michael Kuperstein
  - Nevin Liber
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Tomasz Kamiński
  - Victor Zverovich
- Michael Kuperstein: Internationalization From the Perspective of Defect Analysis
  - \[ Editor's note: Michael's slides are available at
    https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2022-10-12-i18n-presentation.pptx. \]
  - Michael provided a brief introduction:
    - He has been working for Intel since 1996.
    - He has been working in Intel's localization group since 2001.
  - Slide 1: Internationalization From the Perspective of Defect Analysis
  - Slide 2: Venn Diagram
  - Slide 3: Defects in Localized Software
    - The defect breakdown presented is from an analysis performed in 2011.
    - Internationalization and localization defects are usually found by the localization team.
    - Localization defects can often be fixed by the localization team; as a result, localization
      teams tend to maintain their own defect database.
    - Localization defects that require a fix by a development team tend to first be reported in
      a defect database maintained by the localization team and then migrated to another team's
      defect database.
  - Slide 4: World-Readiness Defect Types
    - Most localization defects are due to UI, Layout, or formatting issues.
    - The next largest category of defects are due to translation issues.
    - Defects due to non-translated and embedded strings make up the next largest two categories.
    - Defects due to encoding issues make up the smallest defect category, but are very important.
    - For software developers, internationalization and localization support is a small part of
      their total effort, but an important part.
  - Slide 5: Code Scans: I18N Issues by Volume
    - The top two categories of issues found by code scans are hard-coded strings and hard-coded
      formatting.
  - Slide 6: I18N Issues by Volume – Honorable Mentions
    - A consistent internal locale insensitive representation of dates is necessary to prevent
      failures.
    - Steve confirmed that the general shape of relative error counts presented matches his
      experience.
    - Steve reported that products he has worked on avoid localized formatting of dates so as
      to avoid confusion; likewise, "." is consistently used for decimal point.
  - Slide 7: More than 150 string formatting functions in C/C++ on Windows
    - Charlie noted that most of those 150 functions wrap a common underlying formatting function.
    - Corentin suggested bumping the number to 151 now that `std::format()` has been standardized.
  - Slide 8: Defaults: Fall into the pit of success
    - Use of UTF-16 made it easier to produce the right results on Windows.
    - A string class that basically does the right thing makes it easier to get the right result.
    - The goal is to guide developers towards doing the right thing.
    - Many programmers like string interpolation.
    - ICU discussion:
      - Charlie reported that the ICU included in Windows doesn't expose the C++ interface.
      - Michael noted that, in .NET languages, programmers can choose either ICU or the native
        Windows NLS subsystem for localization, but programmers generally use the default.
      - Charlie asked if ICU is mostly present for transcoding purposes.
      - Michael replied that he doesn't believe that to be the case since .NET interfaces can
        defer to ICU for more localization purposes.
      - Michael expressed a belief that ICU is more deeply integrated on Apple systems.
      - PBrett asked what defect category would best be associated with cases where programmers
        incorrectly attempt to produce translated strings via concatenation.
      - Michael expressed uncertainty, suggested "other", and noted that such issues are very
        common but not called out specifically in the slides.
      - Michael acknowledged that, for some applications, issues due to concatenation are one of
        the most common problems, but that doesn't happen to be the case for Intel.
      - Michael reiterated that making sure programmers fall into the pit of success is important.
  - Slide 9: Quick Intro to BCP 47 Language Tags and Fallback
    - Spoken language is not relevant for text presentation; written language, or script, is.
    - Chinese has two forms of written language; simplified and traditional.
    - It is important to specify fallback locales; otherwise, a request for zh-SG when it is not
      available may result in a default language like English rather than zh-CN.
    - Specifying a hierarchy of fallbacks such as zh-Hans and zh-Hant is recommended.
    - Since C++ locales don't appear to provide locale fallbacks, it may be necessary to supply
      support for all of them; perhaps by providing the same locale data for, e.g., zh-CN and
      zh-SG.
    - Steve noted that English is a better fall back than blank strings or the "tofu" character.
  - Slide 10: User Language Selection Choices
    - The .NET languages wrap locale info in a `CultureInfo` type.
    - They also allow various components of a locale to be selected from different locales.
    - Programmers can create their own custom cultural definitions.
    - Thread specific locale selection is infrequently used; it is more common to supply a
      locale object locally when constructing a string for presentation.
    - Browsers have multiple language settings; one for the browser UI itself and another for
      the requested page language.
  - Slide 11: Date formatting
    - Use ISO 8601 for date formatting and store times relative to UTC internally.
    - Convert dates to the appropriate locale for presentation.
    - Likewise, use one encoding internally and convert for presentation and at program
      boundaries.
    - Hubert asked if Michael had any opinions on the use of ISO week days and numbers.
    - Michael responded that he has no opinion on that.
  - Slide 12: The Famous Turkish “İ” Problem
    - Locale sensitive uppercasing may translate "i" to "İ" (dot retained on uppercase I).
    - Locale sensitive lowercasing may translate "I" to "ı" (dot omitted on lowercase i).
    - This is why it is important to test with Turkish locales!
    - Various languages offer locale invariant or case insensitive case folding operations.
    - ICU collation solves many of these problems when used correctly.
    - Some form of collation should be used for file name matching.
    - Hubert asked if it would generally be expected for a file with an uppercase dotted I
      like "FILE.GİF" to match a request for files named with a ".gif" extension.
    - Michael responded affirmatively; that would generally be desired.
    - Tom observed that such use cases may be more aligned with a form of transliteration.
    - Corentin responded that Unicode case folding as defined in
      [UAX #35](https://unicode.org/reports/tr35)
      handles that case, but that standard C++ doesn't provide an interface.
  - Slide 13: Formats (numbers, dates, etc.) are not as straightforward as they appear
    - ICU's message formatting abilities handle all of these.
    - Corentin noted that currency symbols should not be locale dependent and that C++
      got this wrong.
  - Slide 14: Many other things can go wrong when dealing with international users
    - Handling plural forms is important; the .NET languages do not handle plural forms
      or gendering.
  - Slide 15: JavaScript i18n Objects and Namespaces
    - JavaScript only provides a small number of builtins; i18n is a separate package.
    - Current browser versions provide the JavaScript i18n namespace; polyfill is required
      for older browser versions.
    - Since the language doesn't provide it as a builtin, there are thousands of i18n
      packages available.
  - Slide 16: .NET Culture Aware Classes and Namespaces
    - The .NET languages provide a relatively complete solution that is improving each year.
    - The .NET fundamentals documentation is extensive.
    - Resource files are easy for .NET languages and can be provided in a number of formats.
    - The .NET languages support gettext-like methods for retrieving translated strings.
  - Slide 17: Resource File Formats
    - Some resource file formats are differentiated by encoding.
  - Slide 18: Read All Lines From a File
    - Some languages provide more ergonomic interfaces.
  - Slide 19: Byte Order Mark (BOM) and Endian descriptions
    - On Windows, the default encoding used to be a locale dependent "ANSI" encoding, but
      modern editors are more likely to default to UTF-8.
    - C and C++ don't provide interfaces for file encoding detection and it isn't easy to
      implement well.
  - Slide 20: Character Count vs Byte Count
    - Character counts tend to be close to code unit count for many languages for text
      encoded in UTF-16.
    - It is not easy to obtain a count of characters.
    - Corentin asked when it is useful to count characters.
    - Michael responded that a number of cases exist and provided an example of a buffer for
      which the user is told how many more characters they can expect to type; Twitter is an
      example for which both characters and bytes are counted.
  - Slide 21: Character Encodings (Incomplete List)
    - In C and C++, `char` doesn't have a strongly associated encoding.
    - PBrett asked how often the lack of a strongly associated encoding leads to defects.
    - Michael responded that it is not as much of a problem as it used to be, but that there
      are still many locale dependent "ANSI" encoded files to be found.
  - Slide 22: RTL Text Detection
  - Tom asked the group what stood out to them from the presentation.
    - PBrett noted that C++ doesn't make it easy to write programs that are locale insensitive
      internally but locale sensitive at program boundaries.
    - Michael noted that `gettext()` provides an example of how plural forms can be handled.
    - Jens observed that, with `std::format()`, we're still far away from providing proper
      localization support; it doesn't yet lead to the pit of success.
    - Tom noted that the possibility of extending `std::format()` creates opportunity.
    - Michael noted that formatting is often used for internal uses that don't require
      localization or translation.
    - Steve stated that the experiences reported closely match his experience at Bloomberg.
- NB comment processing.
  - NB comment processing was postponed due to lack of time.
- Tom reported that he would not be available for the previously scheduled 2022-10-26 meeting
  and suggested rescheduling meetings for 2022-10-19 and 2022-11-02 with the intent to focus
  on addressing NB comments in advance of the Kona meeting; there were no objections.


# September 28th, 2022

## Agenda
- [LWG #3767: codecvt<charN_t, char8_t, mbstate_t> incorrectly added to locale](https://cplusplus.github.io/LWG/issue3767)
- [LWG #3412: §[format.string.std] references to "Unicode encoding" unclear](https://cplusplus.github.io/LWG/issue3412)
- Handling ill-formed Unicode in the library
  - See prior [mailing list discussion](https://lists.isocpp.org/sg16/2022/09/3369.php).

## Meeting summary
- Attendees:
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [LWG #3767: codecvt<charN_t, char8_t, mbstate_t> incorrectly added to locale](https://cplusplus.github.io/LWG/issue3767):
  - Victor provided an introduction.
    - There are four `std::codecvt` facets specified for `std::locale` that are not
      intended to be locale dependent.
    - This appears to be the result of an oversight; when `char16_t` and `char32_t` were
      added, new specializations were presumably added to match the existing `char` and
      `wchar_t` ones but are not actually locale dependent.
    - When `char8_t` was added, new specializations that convert between `char16_t`/`char32_t`
      and `char8_t` were added and the old specializations were deprecated.
    - The overhead of the unnecessary facets is probably minimal.
    - The presence of the unnecessary facets is confusing from a design perspective.
    - The proposed resolution removes the specializations that are not actually locale
      dependent from `std::locale`.
    - The proposed resolution also makes the `std::codecvt` constructors publicly accessible
      so that specializations can be constructed without declaring derived classes.
  - PBrett stated that the
    [email that announced the meeting agenda](https://lists.isocpp.org/sg16/2022/09/3427.php)
    noted that it would be helpful to understand what overhead is imposed by these additional
    facets in practice and asked if it had been measured.
  - Victor replied that he had not measured and that the design ramifications were of more
    concern to him.
  - Victor volunteered to perform some measurements and described how implementations manage
    the facets; via a dynamically allocated array.
  - Tom responded with his understanding that at least some implementations statically allocate
    the facets and just register pointers.
  - Steve asked if the proposed changes would cause existing programs to break at run-time.
  - Victor replied that the presence of the facets can be queried at run-time.
  - Tom stated an expectation that, for some implementations, complete removal of these
    specializations might result in link failures.
  - Steve expressed appreciation for the desire to remove these facets based on them not
    actually being locale dependent.
  - Victor suggested that these facets could be deprecated instead.
  - PBrett asked if the `std::codecvt` destructor should be virtual.
  - Victor expressed an expectation that a virtual destructor is inherited from a base class.
  - PBrett asserted the destructor should be declared with `override` in that case.
  - Hubert opined that these questions are more of a concern for LEWG and do not fall under
    SG16's purview.
  - Jens suggested an SG16 perspective that these facets are not locale dependent and therefore
    should not vary by locale.
  - Jens noted that these facets have been present for more than one standard cycle and removal
    could result in silent behavior change.
  - Jens asserted that experience should be obtained regarding the effects of removal before
    moving forward with a change.
  - Jens noted that those removal effects are LEWG concerns.
  - Victor agreed regarding SG16 scope for concerns.
  - Victor volunteered to investigate what the consequences of removal would be.
  - **Poll 1: SG16 agrees that the codecvt facets mentioned in
    LWG3767 "codecvt<charN_t, char8_t, mbstate_t> incorrectly added to locale"
    are intended to be invariant with respect to locale.**
    - Attendance: 7
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   3 |   0 |   0 |   0 |
    - Consensus: unanimously in favor.
- [LWG #3412: §[format.string.std] references to "Unicode encoding" unclear](https://cplusplus.github.io/LWG/issue3412):
  - Hubert explained that the term "Unicode encoding" is used in several places in
    the standard, but with no formal definition.
  - Tom provided two perspectives:
    - "Unicode encoding" refers to only those encodings specified by the Unicode
      standard and ISO/IEC 10646; UTF-8, UTF-16, and UTF-32.
    - "Unicode encoding" refers to any encoding that maps the entirety of the
      Unicode code space and therefore includes, for example, UTF-7 and UTF-EBCDIC
      in addition to UTF-8, UTF-16, and UTF-32.
  - PBrett asked if there is an industry term that describes the latter perspective.
  - Hubert replied that he is not aware of one.
  - Tom replied that he had briefly looked for one in the Unicode standard when
    drafting the agenda email but did not find one.
  - Hubert stated that, for the debug formatting output introduced by
    [P2286 (Formatting Ranges)](https://wg21.link/p2286),
    that a stateless encoding was assumed.
  - Tom expressed support for restricting "Unicode encoding" to just those encodings
    that are defined in the Unicode Standard.
  - Tom noted that, if motivation arises to support additional encodings as Unicode
    encodings, that a paper can argue for relaxing the restrictions.
  - **Poll 2: SG16 recommends that
    LWG3412 "§[format.string.std] references to 'Unicode encoding' unclear"
    should be resolved by replacing references to "Unicode encoding" with
    "UCS encoding scheme".**
    - Attendance: 7
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   5 |   0 |   0 |   0 |
    - Consensus: unanimously in favor.
  - Tom asked Hubert if he would be willing to research other uses of "Unicode encoding"
    to see if they should be similarly changed.
  - Hubert agreed to do so and to open new LWG issues as appropriate.
  - Jens suggested that a proposed resolution can address all such issues.
  - PBrett raised concern about use of GB18030 with `std::print()`.
  - Hubert noted that we don't currently use the "Unicode encoding" terminology in
    conjunction with `std::print()`.
  - \[ Editor's note: Overloads of `std::print()` for `wchar_t` and other character
    types are not currently provided; the wording in
    [\[print.fun\]p2](http://eel.is/c++draft/print.fun#2)
    currently restrits the enhanced Unicode behavior to UTF-8. \]
  - Hubert suggested we proceed with the pragmatic solution for now.
  - Tom noted that, for GB18030, the latest version no longer requires use of the
    Unicode Private Use Area (PUA), and is therefore more likely to be considered
    acceptable as a "Unicode encoding" in the colloquial sense.
  - Tom stated that the issues are likely sufficiently complicated though that inclusion
    via a new paper is justified.
- Handling ill-formed Unicode in the library:
  - Mark summarized the two issues raised during prior
    [mailing list discussion](https://lists.isocpp.org/sg16/2022/09/3369.php):
    - One of the examples in
      [\[format.string.escaped\]p3](https://eel.is/c++draft/format.string.escaped#3)
      is incorrect; `s5` should have a result value of
      `["\x{c3}("]`, not `["\x{c3}\x{28}"]`.
    - It is not specified how ill-formed code unit sequences should be handled for
      purposes of width estimation and formatting of debug output.
  - Victor responded that, for debug format output, the goal is to avoid loss of
    information but that concern doesn't apply to width estimation.
  - Tom stated that the issue with the example is editorial since examples are
    non-normative.
  - PBrett suggested that the width estimation issue can be addressed via an
    NB comment or an LWG issue.
  - Tom opined that specifying the behavior for invalid code unit sequences is
    reasonable.
  - Victor agreed and noted that this is actually a C++20 issue.
  - PBrett noted that performance overhead may be potential motivation for not
    specifying the behavior of ill-formed input.
  - Victor responded that this concern only applies to width estimation; optimizations
    can still be employed.
  - Jens stated that, for formatting of debug output, it is clear that the intent is
    not to lose information.
  - Tom agreed that the intent in that case is clear and well-specified; the remaining
    issue is width estimation for ill-formed code unit sequences.
  - Jens asked what should be displayed for such ill-formed code unit sequences.
  - Tom replied that such questions depend on replacement character policy.
  - Jens asserted that the width estimate should be derived from the characters that
    will actually be displayed.
  - Victor suggested that research is needed to determine what happens in practice.
  - Tom noted that the input string has to be processed to calculate the estimated width,
    so what terminals and such do with ill-formed code unit sequences doesn't
    necessarily matter.
  - Victor agreed and asked if the standard specifies a replacement character.
  - Tom responded that he did not think it does.
  - Tom suggested that the desired resolution is probably to apply
    [PR-121](https://www.unicode.org/review/pr-121.html)
    policy 2 with the Unicode replacement character substituted for the ill-formed
    sequence.
  - Victor replied that substituting a replacement character might not be easy and might
    impose overhead.
  - Jens suggested that the best answer might be that the estimated width is unspecified.
  - Mark volunteered to file an LWG issue for further follow up.
- Tom stated that the next meeting is scheduled for October 12th and that the agenda is
  expected to include a presentation by Michael Kuperstein unless preempted by a need to
  start addressing NB comments.


# September 14th, 2022

## Agenda
- Report on the on-going interactions between WG21 and the Unicode Consortium.
- Report on the backward compatibility impact of
  [P1949 (C++ Identifier Syntax using Unicode Standard Annex 31)](https://wg21.link/p1949).
- Continued discussion of
  [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - Mark Davis
  - Michael Kuperstein
  - Peter Bindels
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- A round of introductions was held in honor of new attendees.
- Report on the on-going interactions between WG21 and the Unicode Consortium:
  - Tom provided an introduction and presented prepared slides.
  - \[ Editor's note: Tom's slides are available at
    https://github.com/sg16-unicode/sg16-meetings/blob/master/presentations/2022-09-14-WG21-UC-collab-p1949-presentation.odp. \]
  - Unicode Message Format Working Group (MFWG):
    - Tom presented his understanding of the group's progress as previously relayed to him
      by Peter Brett as Peter was unable to attend the meeting.
      - Progress is on-going.
      - A draft specification is available.
      - The specification is complicated.
      - The features provided subsume those currently available in ICU.
      - Implementations are available in Javascript and Rust.
      - The design might not integrate well with `std::format()`.
    - Mark elaborated on the group's work.
      - A tech preview will be available in an upcoming release of ICU; In Java first with
        C++ support to come later.
      - The current specification (2.0) supercedes previous work.
      - The design is intended to minimize dynamic processing.
      - In support of higher level processes, the design enables formatting to a data model
        that is then formatted to a string.
      - Formatting is sensitive to surrounding characters.
    - Robin stated that, with regard to dynamic and static formatting models, the previous
      1.0 specification could be used to produce a statically checked implementation via
      code generation.
    - Michael noted that most formatting needs involve simple cases and that the interfaces
      provided must support difficult cases without complicating the simple cases.
    - Mark replied that making simple things simple is a goal, but that challenges naturally
      arise.
    - Mark provided an example of such challenges; some languages have gendered forms of
      sentences that should be tailored for the user.
    - Mark further emphasized the desire to cater to those cases while maintaining simplicity.
    - Tom noted an implication; that locale is insufficient by itself for producing a message;
      information about the recipient is needed.
    - Mark acknowledged, but noted that gender should not be imposed; formatting should reflect
      the diversity of recipients.
    - Michael reflected on how these concerns are expressed in social media.
    - Mark noted the concerns apply in any case where a particular user is the target of a
      message.
    - Mark added that western speakers are not often aware of these concerns.
  - Unicode Source Code Ad Hoc Group (SCWG):
    - Tom presented the group's progress and on-going activities.
      - The group started meeting in late 2021.
      - A liaison relationship between ISO SC22 and the Unicode Consortium might be established.
      - Proposed updates to
        [UAX #9](https://www.unicode.org/reports/tr9/tr9-46.html) and
        [UAX #31](https://www.unicode.org/reports/tr31/tr31-37.html)
        were accepted for Unicode 15.
      - On-going work includes:
        - Establishing principles for source code as text.
        - Considerations for language designers.
        - A new UTS.
      - A new group will be formed to focus on issues of character confusability.
    - Mark commented that the updates adopted for Unicode 15 were done to address
      some fairly obvious deficiencies.
    - Robin categorized the updates as non-normative clarifications.
    - Steve stated that
      [annex E](http://eel.is/c++draft/uaxid)
      should be updated to reflect these clarifications.
    - Steve noted such an update would only modify non-normative wording.
    - Hubert cautioned that the updates must be consistent with prior intent and noted
      there was a desire not to speculate on uncertain interpretations at the time.
    - Hubert stated that we tend to favor normative text when there is a conflict with
      non-normative text.
    - Mark noted that non-normative text may better explain the intent of normative
      wording.
    - Robin described in more detail some of the on-going work:
      - There will be a new UTS that will be a one-stop shop for source code.
      - Much of the focus concerns display of source code in the presence of
        bidirectional text or invisible characters.
      - Considerations for language design.
      - Considerations for language evolution; for example, migrating a language from
        immutable identifiers to default identifiers.
    - Mark explained the intent to define a suite of standard profiles that language
      designers can choose from in order to provide a simple set of options that
      encompass complicated concerns.
    - Corentin noted that most language designers are not qualified to determine what
      characters should be used for what purposes and that it is important to understand
      the consequences of changes.
    - Corentin expressed a desire for the Unicode Consortium to make decisions about
      character use; for example, for what characters are allowed in an identifier.
    - Mark reiterated that the goal is to make choices as easy as possible.
    - Mark noted that language designers have to make choices for backward compatibility
      purposes and provided the example of maintaining use of '_' in identifiers.
    - Mark explained that providing well-defined profiles allows language designers to
      better understand the implications of combining profiles.
    - Mark stated that some profiles will offer the option of removing characters that
      are otherwise in a default included set.
    - Robin acknowledged Corentin's concern and agreed with not wanting language designers
      to be burdened with having to consider individual characters.
    - Robin stated that characters in these profiles won't be added to `XID_Start` and
      `XID_Continue` because those properties are required to be universal.
    - Tom noted that this work was partially motivated by the C++ migration from immutable
      identifiers to default identifiers and the effort required to appreciate the
      consequences.
    - Mark reflected on the difficulties encountered by backward incompatible changes made
      for XML 2.0 relating to C1 control characters.
    - Robin offered assurances that a new UAX #31 revision will make the consequences of
      such choices more clear.
    - Steve noted limitations imposed by concerns we don't have control over and provided
      the examples of separate compilation and linkers; identifiers might be written in
      normalization form C (NFC) but a linker might just interpret it as a sequence of
      bytes.
    - Mark responded that requiring NFC is a good solution for a lot of matching cases that
      also arise outside of programming languages.
    - Robin lamented the problems that occur by burdening users with NFC requirements and
      asserted that programmers can help.
    - Steve noted that programs can validate NFC quickly.
    - Mark agreed and noted that hits to the slow path during NFC validation are infrequent.
    - Tom stated that the Unicode Consortium will form a new group to address character
      confusability in order to take that security burden off the programmer.
    - Mark responded that the Unicode Standard provides some data regarding confusable
      characters but is limited to cases where glyphs for a single code point might be
      confused with a sequence of multiple code points; maps between code point sequences
      are not currently provided.
    - Mark noted that confusability is often dependent on the font being used, that
      programming languages tend to use a reduced set of characters, and that programmers
      tend to use fonts that avoid some confusability issues.
    - Robin explained that major changes to confusability analysis will be handled by the
      new group and that smaller issues will likely follow the existing processes.
    - Michael asked if the confusability work will focus more on usability or security.
    - Mark responded that both are important and that improving one often helps with the
      other.
    - Corentin mentioned that visual markup for confusability can impact usability and
      noted that VS Code currently highlights all non-ASCII characters that might be
      confused with an ASCII character.
    - \[ Editor's note: Following the meeting, Robin Leroy shared an example of current
      VS Code highlighting as exhibited by Compiler Explorer (Compiler Explorer uses
      VS Code as its editor). The example code contains Russian text and many of the
      characters in that text are highlighted as confusable characters despite the
      surrounding context. The highlighting creates significant distraction that makes
      the text difficult to read. See https://gcc.godbolt.org/z/zK7GPo9hW. \]
    - Mark acknowledged the concern and stated that efforts will be focused on avoiding
      markup that isn't helpful.
    - Robin commented that he has a note in his working draft that states "don't do what
      VS Code does".
    - Mark suggested a thought exercise; imagine using an editor that highlights all
      Latin characters that look like characters in other lanugages.
    - Robin explained that mixed script identifier support is important and provided
      `HTTPЗапрос` as an example in which an identifier is composed of
      names that originate from different languages.
    - \[ Editor's note: HTTPЗапрос can be translated as HTTPRequest. \]
    - Michael expressed support for a code library that provides confusability analysis.
    - Mark replied that ICU provides confusability data but noted that application of
      that data necessarily requires understanding text structure.
- Report on the backward compatibility impact of
  [P1949 (C++ Identifier Syntax using Unicode Standard Annex 31)](https://wg21.link/p1949):
  - Tom provided an introduction.
    - [SG16 issue #79](https://github.com/sg16-unicode/sg16/issues/79)
      tracks reports of backward compatibility impact.
    - [Clang defect report #54732](https://github.com/llvm/llvm-project/issues/54732)
      tracks Clang user reports; four users have reported impact, but the number of
      projects represented by them is unknown.
    - Robin maintains code that was impacted.
    - Robin conducted a survey of character usage in identifiers and published
      [L2/22-102 (A survey of non-XID identifier usage in program text)](https://www.unicode.org/L2/L2022/22102-non-xid-ident-usage.pdf).
  - Robin explained that his code that was impacted is in a hobby project.
  - Robin described the survey he conducted and reported that it identified impacted
    code in a number of projects.
  - Robin reported that the SCWG intends to provide standard profiles for optional
    inclusion of select mathematical symbols and emoji in identifiers.
  - Robin noted that the main character differences between immutable and default
    identifiers is the selection of allowed mathematical symbols and emoji characters.
  - Corentin expressed concern that, if C++ were to add support for user-defined
    operators as Swift did, we don't want to end up in a situation where characters
    previously allowed in identifiers become candidates for use as operators.
  - Robin reiterated that there is no intent to add these characters to `XID_Start` or
    `XID_Continue`; that they are only being considered for standard profiles.
  - Robin reported that the rationale for the proposed mathematical notation standard
    profile for default identifiers considers existing use in languages such as Julia
    and Swift that support user-defined operators.
  - Robin stated that relevant experts from other members of the Unicode Consortium
    are reviewing that rationale.
  - Steve expressed sympathy towards use of mathematical symbols in Mathematica and that
    doing similarly in C++ means using those symbols in identifiers since algorithms are
    typically implemented as functions in C++.
  - Steve stated that the subscript and superscript characters are problematic since many
    fonts don't support those characters.
  - Michael asked what motivates programmers to want their code to look like mathematical
    equations.
  - Steve responded that, in mathematics heavy fields like physics simulation, it is
    desirable for the code to match equations in other documents.
  - Michael expressed uncertainty whether that is reasonable and reported that his closest
    experience has involved equations in Mathematica.
  - Michael noted that typesetting languages like TeX are able to render such characters
    appropriately but that he wasn't sure about common programming language editors.
  - Steve responded that such concerns may be limited if code is not widely shared or
    reused.
  - Steve asserted that depending on a finicky environment is ill-advised.
  - Corentin expressed a belief that language designers don't want to make such decisions
    and that implementors should not offer such extensions.
  - Tom responded that different recommendations are appropriate for, for example, general
    purpose languages vs domain specific ones.
  - Corentin agreed.
  - Steve stated that defining standard profiles helps to provide sensible options.
  - Steve suggested that profiles also provide a clearly defined feature for which
    implementors can be lobbied for an extension that could then be standardized based on
    adoption.
  - Hubert replied that common extensions are not necessarily good evidence of widely used
    or appreciated extensions.
  - Steve agreed with not wanting to make decisions on individual characters; that an appeal
    to authority is desired.
  - Robin agreed with not placing the burden of evaluating individual characters on language
    designers.
  - Corentin asked about the anticipated timeline for this work.
  - Robin responded that a draft is expected in November, that feedback from the UTC will
    then be provided, and that the work is targeting next September's Unicode release.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0):
  - Tom apologized for the lack of time available to continue discussion of this paper.
- Tom stated that the next meeting will be held on September 28th and asked for opinions
  regarding what to prioritize next.
  - Corentin replied that continued discussion of P2626 is not a high priority right now.
  - Corentin stated that there is a need to update the standard to use and reference the
    current Unicode version.
  - Corentin stated that work is needed to improve estimated field widths.
  - Corentin stated that the escape string format added via
    [P2286 (Formatting Ranges)](https://wg21.link/p2286)
    needs additional work to handle combining characters in extended grapheme clusters.
  - Hubert cautioned that concern is warranted regarding debug strings getting corrupted
    during copy/paste operations.
  - Steve stated that Bloomberg will be filing an NB comment to update annex E.
  - Hubert stated that he will be filing an NB comment about `std::format()` debug strings.
  - Tom pondered the possibility of requesting that NB comment authors send copies of relevant
    NB comments to us when they submit them so that we can start work on them sooner.
  - \[ Editor's note: Tom reached out to Herb and he arranged for all SGs to get early access
    to NB comments. \]
  - Tom reported that the next meeting will focus on LWG issues and that the following meeting
    will likely include a presentation from Michael.


# August 24th, 2022

## Agenda
- Initial planning for Kona.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Initial planning for Kona.
  - Tom stated that there will likely be NB comments for SG16 to address and that they are
    unlikely to be available in a timeframe that would allow us to discuss them before the
    Kona meeting begins.
  - Tom explained that, if few people will be present in Kona, that he is inclined not to
    reserve a room, but rather to have both in-person and remote attendees join a Zoom
    meeting for discussions.
  - PBrett suggested that any such meetings should be planned for early morning Kona time
    in order for remote attendees in Europe and the US east coast to be able to attend.
  - Jens explained his current plans and expectations for room setup and audio capabilities.
  - Jens cautioned that the conference wifi may not handle many in-person attendees using
    Zoom at the same time.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0):
  - Corentin presented the paper.
    - `char8_t`, `char16_t`, and `char32_t` are useful for their encoding assurances, but
      lack support in the standard library.
    - Unfortunately, we can't just assume UTF-8 with `char`-based types and avoid use of the
      UTF variants.
    - Some form of interconvertibility between `char`, `wchar_t`, and the UTF character types
      is needed for the latter types to be incrementally adopted.
    - Copying the content of an array of one character type to an array of another character
      type just because existing code needs to access it by the latter type is expensive.
    - None of the current language facilities enable zero cost interconvertibility.
    - The proposed functions are intended to have a narrow contract.
    - The names of the functions are intended to reflect the partitioning of character types
      that are always used with UTF data and other character types.
    - The functions are intended to provide interoperability in constant expressions.
    - The `basic_string_view` and `span` interfaces are provided for convenience.
    - The alias barrier based conversion operations that ICU uses are non-conforming, probably
      don't work reliably, and probably can't be made to work in the C++ core language.
    - \[ Editor's note: See
      [SG16 issue #67](https://github.com/sg16-unicode/sg16/issues/67)
      for more background information regarding the ICU alias barriers. \]
    - An interoperability solution is needed for the UTF character types to be adopted in
      practice.·
  - Victor asked how the proposed functions would work on a system where, for example,
    `wchar_t` is not the same size as `char16_t`.
  - Corentin responded that the functions are constrained such that the source and target
    types must have the same size and alignment; a call is ill-formed otherwise.
  - Victor requested that the paper be updated to explicitly state early in the paper what
    properties of the types must match for the operations to be well-formed.
  - Hubert stated that there are memory model concerns that may make this feature not
    worth pursuing; the proposed functions provide a very sharp feature.
  - Tom asked Corentin why he felt SG1 might want to review the paper.
  - Corentin responded that his understanding is that SG1 is generally consulted regarding
    the C++ abstract machine, the memory model, and concurrency concerns.
  - Jens explained that the concerns the paper raises have more to do with the object model
    than the memory model and that these concerns fall more under CWG than SG1.
  - Jens noted that
    [P2590 (Explicit lifetime management)](https://wg21.link/p2590),
    a paper with related concerns, was reviewed by LWG and CWG, but not by SG1.
  - Jens added that
    [P2590](https://wg21.link/p2590)
    completed work that began with
    [P0593 (Implicit creation of objects for low-level object manipulation)](https://wg21.link/p0593)
    and that paper also targeted LWG and CWG.
  - Corentin asked if the paper represents a good direction.
  - Hubert stated that the proposed semantics are such that, if these functions were called
    to replace a subobject, that the enclosing complete object would be destroyed.
  - \[ Editor's note: Hubert provided a reference to the relevant wording in
    [\[basic.life\]p1](http://eel.is/c++draft/basic.life#1)
    in a follow up
    [post to the SG16 mailing list](https://lists.isocpp.org/sg16/2022/08/3359.php). \]
  - Hubert repeated his assertion that the proposed semantics have sharp edges.
  - Hubert noted that there are on-going concerns involving `start_lifetime_as()` and base
    classes.
  - Jens commented that the complete object would only be saved from destruction if there is
    a *provides storage* relationship
    ([\[intro.object\]p3](http://eel.is/c++draft/basic#intro.object-3)
    between the subobject and the target type.
  - Jens suggested that a better approach might be to add `constexpr` support to
    `start_lifetime_as_array()`.
  - Jens added that it might be possible for `start_lifetime_as_array()` to offer additional
    guarantees in cases where an underlying type is shared.
  - Tom stated that there is a complicated relationship between the core language
    possibilities and how that impacts the library interface possibilities.
  - Tom expressed a preference for specifying an ideal library interface that then drives
    the core language needs.
  - Hubert expressed uncertainty with regard to how to word restrictions around usage of an
    enclosing object following a change of type for a subobject; use or destruction of the
    subobject via the enclosing object would have to be avoided.
  - Corentin said he would try to address that.
  - Corentin stressed that, once an object's type is changed, the memory for that object
    cannot be accessed as though an object of the previous type is there.
  - Hubert reiterated that a change of type for a subobject becomes very complicated.
  - Jens asked if the paper includes examples that are reflective of how this facility would
    be used in something like real world code.
  - Jens noted that the mailing list discussion indicated that conversion in one direction
    must be followed by a conversion back.
  - Corentin expressed uncertainty regarding what limitations must be imposed and voiced an
    assumption that, since the character types are trivial, there is more flexibility.
  - Jens stated that the core language has moved towards objects of a trivial type being
    destroyed at the same point as other types; in the past objects of a trivial type could
    be accessed after their point of destruction until their storage was destroyed.
  - Jens noted that there may be wording that states that destruction of a trivial object
    where an object of another type is present results in undefined behavior and provided
    [\[basic.life\]p6](http://eel.is/c++draft/basic.life#6)
    as a reference.
  - Tom described his understanding of how constant evaluation works in terms of
    interterpretation of an AST; constant evaluators can currently rely on the type system;
    changing the type of an object could lead to undefined behavior within the evaluator.
  - Hubert agreed with Tom's description and stated that multiple implementors should be
    consulted.
  - Corentin suggested that such problems might be avoided via dependence on an underlying
    type relationship.
  - PBrett asked why the object type is so problematic and why, if a region of memory
    contains bytes that represent UTF-8 encoded text, it can't simply be accessed as an
    array of `char8_t`.
  - Tom explained that constant evaluation is based on the C++ object model and that the
    concept of memory regions don't apply there.
  - Corentin further explained that compiler optimizers use
    [type based alias analysis (TBAA)](https://en.wikipedia.org/wiki/Alias_analysis#Type-based_alias_analysis)
    to eliminate re-reading memory and
    [dead stores](https://en.wikipedia.org/wiki/Dead_store)
    (writes to memory that will never be observed according to the abstract machine)
    based on the type system.
  - PBrett suggested that such alias restrictions could be removed.
  - Hubert responded that doing so would impact performance.
  - Jens noted that `char8_t` raised the abstraction level in C++ but not in C since
    `char8_t` is a type alias of `unsigned char` there.
  - PBrett stated that the issue with the object model must be solved in order to specify
    a zero cost abstraction.
  - Hubert explained that there is a trade off; using both `wchar_t` and `char16_t`
    increases costs, but the latter provides encoding and portability guarantees.
  - PBrett opined that this suggests that use of the UTF character types is not zero cost.
  - Jens responded that C++ opted to add those types as fundamental types in order to
    support overload resolution.
  - Hubert explained the competing costs; restricting aliasing improves performance at the
    cost of having to workaround the type system.
  - Jens noted that `memcpy()` can be used to workaround the type system.
  - Tom noted that `memcpy()` can even be optimized away in some cases.
  - PBrett pondered whether the abstractions adopted for UTF character types were the
    right choice and noted that a library facility could have provided the same encoding
    guarantees while using `char` internally.
  - Tom explained that doing so wasn't an option for `char8_t` since UTF-8 string literals
    were already part of the core language.
  - Steve explained that we use the type system to annotate how a block of memory is used
    and that `char8_t` provided the ability to annotate a block of memory as holding UTF-8
    data.
  - Steve asserted that making the UTF character types aliasing types would impose costs
    like those he has seen with code that loops over `std::byte`; the aliasing behavior
    hurts code generation.
  - Steve noted that there are good libraries available that do use `char` and translate
    between code units and code points.
  - Corentin stated that the choice to make `char8_t` a non-aliasing type was intentional
    and that any such change would further harm adoption.
  - Corentin asserted that a way to use `char8_t` with historic `char`-based interfaces
    is needed or it just won't get used, but we'll still be left with the problems that
    motivated its introduction in the first place.
  - Corentin opined that strong types are needed to support the
    [Unicode sandwich model](https://nedbatchelder.com/text/unipain/unipain.html#35).
  - Corentin expressed a belief that this is solvable, implementable, and therefore should
    be specified.
  - Jens suggested that an alternative UTF-8 design could have been based on something like
    `std::span<char8_t>` over a sequence of `unsigned char`.
  - Jens opined that code unit types are not particularly interesting since an individual
    code unit by itself conveys little meaning.
  - Jens noted that the proposed library interfaces have rough edges and expressed
    skepticism regarding a need for anything UTF specific since the underlying functionality
    is not encoding dependent.
  - Steve agreed that the desire expressed in the paper is a special case of the problem
    where we want to get objects of one type out of a region of memory that holds objects of
    another type.
  - Steve also agreed that the underlying storage for a text type is not interesting; the
    interface provided is.
  - Steve noted that none of the suggested library solutions would have avoided the string
    literal concerns.
  - Hubert provided a list of what he termed "a few uncomfortable facts":
    - Reading object representations is allowed but the existing wording is not satisfactory
      and fixing it will be hard.
    - Implementations don't always follow the standard; for example, Clang's support for
      placement new is non-conforming.
    - Implementations sometimes implement behavior that can't be expressed in the standard.
    - Determining that wording is sufficient requires that multiple implementations are
      completed based on the wording.
  - Corentin, referring to earlier discussion regarding the possibility of making
    `start_lifetime_as_array` constexpr, noted that, since the memory location is provided by
     a parameter of type `void*`, any original source object type information is not present.
- Tom reported that the Unicode Source Code Ad Hoc Group suggested that SG16 author a paper
  to discuss the issues that have been reported following adoption of
  [P1949](https://wg21.link/p1949)
  for C++23 as a defect report and the migration from
  [immutable identifier syntax](https://unicode.org/reports/tr31/#Immutable_Identifier_Syntax)
  to
  [default identifier syntax](https://unicode.org/reports/tr31/#Default_Identifier_Syntax)
  in order to assist implementors with migration techniques, particularly in light of the
  intent for a future Unicode standard to introduce to default identifiers some currently
  excluded characters that are included in immutable identifiers.
  - Jens stated that he would like to understand more about the issues reported and requested
    that it be added to the agenda for a future meeting.
  - Hubert expressed an interest in understanding more about the discussion going on between
    WG21 and the Unicode Consortium.
  - Steve volunteered to add writing such a paper to his todo list.
  - Tom said he would file an SG16 issue to track the reported issues and submission of a paper.
  - \[ Editor's note: Tom filed
    [SG16 issue #79](https://github.com/sg16-unicode/sg16/issues/79). \]
- Tom stated that the next SG16 meeting is scheduled for September 14th and will likely
  include further discussion of
  [P2626R0](https://wg21.link/p2626r0)
  and the above requests for more information about the identifier issues and collaboration
  with the Unicode Consortium.


# July 27th, 2022

## Agenda
- [WG14 N3016: Unicode Length Modifiers v3](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3016.pdf)

## Meeting summary
- Attendees:
  - Eskil Steenberg
  - Hubert Tong
  - Jens Maurer
  - Marcus Johnson
  - Peter Brett
  - Tom Honermann
  - Victor Zverovich
- [WG14 N3016: Unicode Length Modifiers v3](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3016.pdf):
  - PBrett introduced the topic and invited Marcus to present his paper.
  - Marcus discussed the motivation for the paper; the desire to be able to easily format
    text in a Unicode encoding.
  - Tom provided a summary of the WG14 review of the paper during the recent WG14 meeting.
  - PBrett described how `gettext()` is used; a string in the string literal encoding is
    provided and a string in the current locale encoding is produced.
  - Tom stated that there is effectively a contract that the string produced by
    `gettext()` is encoded in the current locale encoding.
  - PBrett confirmed.
  - PBrett asked how `printf()` would handle formatting a UTF-16 encoded argument.
  - Tom replied that the existing practice for `wchar_t` based arguments is to convert them
    to the current locale encoding.
  - Tom asked if motivation exists for an alternative behavior.
  - Jens asked for an example of alternative behavior.
  - Tom replied that the string literal encoding could be used to guide conversions instead
    of the current locale and noted that this would match the behavior chosen for
    `std::format()` when the string literal encoding is a Unicode encoding.
  - Tom explained that such behavior would require preserving the string literal encoding
    for each translation unit and then somehow passing that information to `printf()`.
  - Jens noted that `std::printf()` and `gettext()` have different encoding expectations; the
    former expects the formatting string to be in the current locale encoding while the latter
    expects something else.
  - \[ Editor's note: The
    [GNU gettext man page](https://man7.org/linux/man-pages/man3/gettext.3.html)
    states:
      > The msgid argument identifies the message to be translated. By
      > convention, it is the English version of the message, with non-
      > ASCII characters replaced by ASCII approximations.
    \]
  - PBrett stated that it is rare in his experience for a string literal to be passed as the
    format string to `printf()`.
  - Victor replied that in the code base he works on, approximately 50% of `printf()` calls
    pass a string literal.
  - Tom surmised that Victor's experience may reflect an assumption of UTF-8 as both the
    string literal encoding and the locale encoding.
  - Victor replied that third party libraries are more likely to not assume UTF-8.
  - Jens asked if there is motivation to introduce a `u8printf()`.
  - Tom replied that adding such an interface is an option.
  - Jens expressed belief that we have consensus that the future is UTF-8 and that
    transcoding operations should occur at program boundaries.
  - PBrett expressed acceptance of library UB as a result of passing a format string to
    `printf()` that is not encoded in the expected encoding.
  - Jens asked how `printf()` implementations recognize the '%' character today.
  - Hubert responded that `printf()` is required to be locale sensitive and that the code
    point value of the '%' character may vary across encodings.
  - Eskil professed that implementations simply search for a code unit that matches the
    ASCII encoding of '%'.
  - Jens argued that is an unlikely implementation choice for an EBCDIC-based system.
  - Hubert explained that the '%' character encoding is non-varying across EBCDIC code
    pages so a simple search for a code unit that matches the EBCDIC encoding works on
    such systems.
  - Jens surmised that, for implementations that support a locale encoding that is
    unrelated to the string literal encoding, there must exist a compile time decision
    regarding calls to `printf()`.
  - Hubert responded affirmatively and stated that the `printf()` family of functions have
    multiple entry points on z/OS.
  - \[ Editor's note: The z/OS C run-time library provides EBCDIC-based implementations
    and ASCII-based implementations. The latter exist to support an ASCII environment on
    z/OS systems. See IBM's
    [Enhanced ASCII support documentation](https://www.ibm.com/docs/en/zos/2.3.0?topic=table-enhanced-ascii-support). \]
  - PBrett reported having seen cases where, if `printf()` was not locale sensitive, the
    results produced would not have matched expectations.
  - Tom agreed that we have established that the format string must match the locale encoding.
  - Eskil stated that, ideally, the string literal and locale encodings would match.
  - Hubert agreed but noted that the locale encoding is controlled by the program user as
    opposed to the program author.
  - Eskil observed that character conversions are not desirable in all cases and provided
    production of a JPEG header as an example.
  - Jens noted that there is no current proposal to implicitly convert the `printf()` format
    string to the locale encoding.
  - Eskil and others agreed that such a proposal would be ill-advised.
  - PBrett concluded that the current `printf()` behavior matches the needs of the paper; it
    must alreadly be locale encoding aware, so conversion between UTF encodings and the locale
    encoding is reasonable.
  - Hubert agreed assuming requisite functionality as proposed in JeanHeyd's transcoding
    facilities.
  - Hubert stated that it would be necessary to specify how transcoding errors are handled.
  - Tom expressed a belief that the C standard already specifies how such errors are handled
    via delegation to functions like `wcrtomb()`.
  - Hubert responded with a belief that the C standard requires that well-formed multibyte
    strings and well-formed wide strings always be interconvertible without loss.
  - Tom expressed surprise that such a requirement exist.
  - PBrett noted that the wording would need to specify whether the precision flag applies to
    code units, code points, or extended grapheme clusters (EGCs).
  - PBrett stated that additional flags could select either code units, code points, or EGCs.
  - PBrett asserted that the grapheme break algorithm is not too onerous a requirement.
  - Tom asserted that the precision flag must specify code units for consistency with other
    uses of precision flags and that written code units should not split code points or EGCs.
  - Hubert explained that the number of code units read from the input must not exceed the
    specified precision for security reasons.
  - Discussion ensued regarding the possibility of buffer overflows and existing uses of
    the precision flag.
  - Victor asked if the precision flag currently specifies the maximum number of input
    characters when performing wide character conversions.
  - Hubert responded affirmatively but suggested verifying.
  - PBrett noted that, for existing uses, code units is equivalent to characters.
  - Tom explained his understanding of the precision flag; that if the precision is *X*,
    then up to *X* code units are read, but only the complete code unit sequences are written.
  - Hubert responded that, if the input string had *X* code points, but the number of code
    units to write differs, then the same number of characters written would not match *X*.
  - PBrett asserted that it is common to use the precision to limit output.
  - Tom checked https://cppreference.com and reported that it claims that the `%s` specifier
    uses the precision to limit the maximum number of bytes to write.
  - Eskil expressed a preference towards designing for the future and that legal output
    always be produced.
  - Hubert checked the C standard and reported that the precision specifies the maximum
    number of output code units in the target encoding and that partial characters are not
    written.
  - Victor summarized; the precision is the amount of output to write and the remainder of
    what was read is discarded.
  - PBrett asserted that programmers expect the precision to express display width.
  - Hubert responded that existing behavior hasn't matched that expectation for as long as
    multibyte encodings have existed.
  - Hubert pondered whether field width has a meaning in this case.
  - PBrett replied that field width fills and that precision truncates.
  - PBrett asserted that what code authors really want is the ability to specify display
    width.
  - Tom asked if there is agreement that `printf()` does not currently have the ability to
    specify display width.
  - PBrett and Eskil responded negatively.
  - Discussion ensued regarding EGCs and display width.
  - Eskil expressed a preference that the C standard provide base level functionality and
    that additional functionality be built as libraries.
  - Eskil asserted that there isn't always a single best solution.
  - Hubert noted that, with regard to code points vs EGCs, splitting an EGC can produce
    misleading output.
  - PBrett noted that virtually all programs need to interact with text in some capacity.
  - Eskil stated that some capabilities are fundamental and provided the example of
    formatting a number.
  - Eskil stated that, with regard to string types, there are uses for a size+pointer
    string type, a size+buffer string type, a size+capacity+buffer string type, a
    string-with-allocator string type, and more.
- Tom indicated that the next meeting is scheduled for August 10th and that the agenda is
  yet to be determined.


# June 22nd, 2022

## Agenda
- Continue discussion of survey questions for the 2023 C++ Developer Survey.
  - Revise, add, and remove questions from the
    [draft survey document](https://docs.google.com/document/d/1lRU7uErn2Vc7LOGG2H3PrzCvmf69u8S_v-43by_Vb9c/edit?usp=sharing).

## Meeting summary
- Attendees:
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- Continue discussion of survey questions for the 2023 C++ Developer Survey:
  - \[ Editor's note: The active revision at the start of the meeting can be viewed by selecting
    `File` | `Version history` | `See version history`, then selecting the version named
    "pre 2022-06-22 meeting", then clicking the rightward facing triangle next to the version
    name to "expand detailed versions"; this latter step is necessary to exclude detailed edits
    that otherwise interfere with numbering of the questions. \]
  - Tom asked attendees to nominate questions to be removed from consideration.
  - PBrett suggested removing Q1 (What character encoding(s) do you use for source files?) since
    we already have consensus for moving towards UTF-8 encoded source files.
  - PBrett asked how answers to Q1 would affect our decision making.
  - Jens concurred and asked hypothetically whether responses would entice us to, for example,
    add a translation phase 1 option to support GB18030 as we are doing for UTF-8 via
    [P2295 (Support for UTF-8 as a portable source file encoding)](https://wg21.link/p2295).
  - Jens noted that implementations that support non-UTF-8 source files will continue to support
    them and argued that there is nothing to be done within the standard.
  - Hubert suggested an alternative formulation that asks which scripts programmers are using in
    their source files and for which they might be using specific encodings.
  - Jens noted that
    [P2528 (C++ Identifier Security using Unicode Standard Annex 39)](https://wg21.link/p2528)
    assumes that everyone is using Unicode for their source file encoding and that encoding does
    not imply which scripts are being used.
  - Jens stated that use of a particular encoding such as ISO8859-1 does restrict what scripts
    can be used and that such information could potentially be used in confusability analysis.
  - Jens suggested the question could probe which scripts are used in conjunction with a
    non-Unicode encoding.
  - PBrett noted the existence of the Big-5 encoding and that it is being phased out in favor of
    GB18030 and UTF-8.
  - PBrett asked if we are at risk of discussing whether support for additional encodings should
    be mandated.
  - Hubert responded negatively and stated that the question is intended to probe the extent to
    which substantial use of non-Unicode encodings remains.
  - Tom stated that it sounds like we have not identified a use case for this question.
  - Tom struck Q1 from the draft document.
  - PBrett expressed uncertainty as to what Q2 (What character encoding(s) do you use for string
    literals?) is intended to ask and stated that it might be interpreted as asking if `L`, `u8`,
    `u`, or `U` prefixed literals are being used.
  - Tom replied that the question is intended to ascertain what encodings are being used for the
    encoding of ordinary (non-prefixed) literals in order to learn about trends occurring in the
    ecosystem.
  - Hubert noted that we now assume that if string literals are UTF-8, then the locale encoding
    is as well.
  - PBrett expressed a feeling of persistent saltiness over that assumption.
  - Jens stated that only `std::format` is currently pushing us towards Unicode in this way.
  - Tom stated that we seem to have no use case for this question.
  - Tom struck Q2 from the draft document.
  - PBrett suggested removing Q10 (How are the project(s) that you work on organized for
    Unicode normalization?) on the basis that few programmers are aware of Unicode normalization.
  - Tom responded that the question is intended to provide input regarding whether normalization
    should be reflected in the type system.
  - Steve stated that it doesn't matter for most programmers, but that it matters immensely for
    a few.
  - PBrett suggested it is not a good candidate question if we believe it impacts few programmers.
  - Tom struck Q10 from the draft document.
  - PBrett opined that Q13 (Do your project(s) use regular expressions for which the search
    pattern is not known at compile-time?) is important to determine if programmers create regular
    expressions using user input.
  - PBrett stated that it probes whether
    [CTRE](https://compile-time-regular-expressions.readthedocs.io/en/latest)
    is a suitable replacement for `std::regex`.
  - PBrett stated that Q14 (Which regular expression languages do you use?) appears to duplicate
    Q12 (What libraries do you use for regular expression support?).
  - Tom replied that Q14 is intended to ask which regular expression languages are being used; for
    example, which of the six languages supported by `std::regex` are being used.
  - Hubert stated that Q12 could be useful to determine whether collation support is useful and
    noted that use of POSIX languages may imply better locale support needs.
  - Jens observed that programmers might use those languages for other reasons.
  - PBrett replied that programmers tend to use whatever language the regular expression facility
    they are already using supports.
  - Tom struck Q14 from the draft document.
  - Jens asserted that Q15 (Do you use the signed char or unsigned char types for text processing?)
    is not interesting.
  - Hubert asked if that concern is motivated by the lack of standard library support.
  - Jens replied that iostream supports signed and unsigned char types.
  - Tom stated that the question is intended to help determine whether these types should be used
    exclusively as small integer types as opposed to character types.
  - Jens opined that programmers should use `char`, `char8_t`, etc... for character types.
  - PBrett noted that `unsigned char` is commonly used as a character type in C.
  - Tom stated that this reflects a policy issue regarding whether we intend to extend the standard
    library to support use of these types for text and stated we have no such intent.
  - Jens agreed, noted that the aliasing is unfortunate, and expressed support for not making the
    situation worse.
  - Tom struck Q15 from the draft document.
  - Jens expressed support for asking programmers how they support internationalization and
    localization.
  - PBrett suggested dropping Q19 (What libraries do you use for collation?).
  - Jens countered with a suggestion to merge
    Q17 (What libraries or operating system features do you use for language translation?),
    Q18 (What libraries do you use for localization?), and Q19.
  - Tom agreed to do so.
  - Tom pondered whether it is worth asking about prohibition of standard library facilities.
  - PBrett responded that we can infer avoidance of the standard library when programmers state
    that they use, for example, ICU, but not the standard library facilities.
  - Steve stated that the explicit locale capabilities present in `std::format` are representative
    of what programmers want.
  - PBrett asked about adding a free form field for programmers to state how they support
    localization.
  - Tom responded that it is difficult to extract data from free form entries.
  - Steve stated that it is useful to know that no one uses, for example, `stdcoll()`.
  - Tom asked if the "discourage or prohibit" language should be retained.
  - Jens replied negatively and stated that we want to know what they do use.
  - Hubert stated that Q16 (Do you use the C and C++ locale features?) is useful to know if, or
    to what extent, programmers depend on the C and C++ locale for identification purposes.
  - Tom agreed to simplify Q16.
  - Tom pondered what we would use the responses to questions about languages and scripts for.
  - PBrett replied that Visual Studio Code has
    [UAX#9 HL4](https://unicode.org/reports/tr9/#HL4) features intended to help with display of
    bidirectional text in source files; that information could be used for SG15 guidance.
  - Jens stated that the standard allows identifiers, literals, and comments to be written in
    many kinds of scripts; support for languages such as Japanese is intentional.
  - Jens added that he favors developing guidelines to encourage features like those that
    Visual Studio Code offers.
  - Tom noted that guidance will be forthcoming from the Unicode Source Code Ad-Hoc Group.
  - PBrett concluded that it sounds like we already know we want to support these features;
    the data could help establish urgency.
  - Jens agreed, but noted that implementors can decide for themselves what is and is not urgent.
  - Tom struck Q3 and Q4 from the draft document.
  - Tom opined that Q5 (Do you use characters other than the basic character set in identifiers)
    is probably irrelevant following the adoption of
    [P1949 (C++ Identifier Syntax using Unicode Standard Annex 31)](https://wg21.link/p1949).
  - Steve indicated that language specific concerns are best addressed in a code style guide.
  - Tom struck Q5 from the draft document.
  - Discussion ensued regarding poll bias and privacy concerns.
  - PBrett suggested we could ask which region of the world respondents are located in.
  - Jens replied that such a question might be one that the Standard C++ Foundation is interested
    in asking anyway; it may not need to be included within our quota of questions.
  - Hubert suggested it would be useful to emphasize culture as opposed to geographical location.
  - PBrett expressed a preference for asking which nation the respondent is in.
  - Tom suggested asking respondents what their native language is.
  - Jens replied negatively; there are many languages spoken in India.
  - Tom proposed striking Q6 (Do the projects you work on limit locale selection in deployment
    environments to those that use a specific character encoding?) on the basis that mainframes
    aren't going away any time soon.
  - Tom struck Q6 from the draft document.
  - PBrett suggested merging
    Q7 (What libraries do you use for text processing?),
    Q8 (How are the project(s) that you work on organized for text processing?), and
    Q9 (If your project(s) convert text to and from an internal encoding, what encoding(s) are
    used for the internal encoding?) based on an expectation that use of framework libraries like
    QT sufficiently answer these questions.
  - Jens noted that we already have agreement that we want utilities to convert to/from UTF-8 and
    possibly UTF-16.
  - Tom asked for clarification that such agreement is relative to locale dependent encodings.
  - Steve replied yes, but also to other specified encodings.
  - PBrett asserted that these questions have already been probed by JeanHeyd.
  - Tom explained that Q7 (What libraries do you use for text processing?) is really intended to
    ascertain what features are supported via non-standard libraries because the standard does
    not provide adequate support for them.
  - Jens suggested asking that question instead.
  - Tom agreed to rephrase Q7 accordingly.
  - Jens suggested asking what text processing features people most need; whether that be
    transcoding, Unicode algorithms, or something else.
  - Jens noted that regular expression support could be added to that list differentiated by
    compile-time vs run-time support.
  - Steve asserted that a laundry list would be ok.
- Tom stated that the next meeting is scheduled for July 13th but that we need new papers.


# June 8th, 2022

## Agenda
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/b37ca29e4d5802aeccaf3fe14568ee7427b2c19e/presentations/2022-06-08-d2572r0.html)
  - Final review pending the availability of an updated revision.
- Discuss survey questions to suggest for the 2023 C++ Developer Survey
  - Review questioned and topics suggested in the
    [mailing list discussion](https://lists.isocpp.org/sg16/2022/06/3214.php).

## Meeting summary
- Attendees:
  - Charlie Barto
  - Hubert Tong
  - Inbal Levi
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/b37ca29e4d5802aeccaf3fe14568ee7427b2c19e/presentations/2022-06-08-d2572r0.html)
  - PBrett lamented the lack of a published revision with a "P" designation and change
    history that reflects the evolution of the design and wording.
  - Tom stated, in response to preferences expressed by Victor on the mailing list,
    that he will add a drafting note regarding the change of "specifier" to "option"
    in the description of the *align* grammar production so that LWG will be sure to
    review.
  - Jens requested that the drafting note regarding note renumbering be removed since
    the LaTeX machinery will handle that automatically.
  - Tom stated that he would add a note following the format examples that mentions
    that the clown face emoji has an estimated length of two.
  - PBrett suggested adding an example with a formatting argument that contains a
    character with an estimated width other than one; essentially an example that
    swaps the fill character and formatting argument in example `s7`.
  - Jens requested that note X be modified to drop "estimated" and to replace
    "width of the fill character" with "width of **any** fill character".
  - Jens expressed distaste for the existing wording in
    [\[format.string.std\]p11](http://eel.is/c++draft/format.string.std#11)
    that states "estimated width of ... UCS scalar values"; UCS scalar values are not
    characters.
  - Hubert noted a missing "the" in the same paragraph;
    "the sum of **the** estimated widths".
  - **Poll 1: Revise D2572R0 "std::format() fill character allowances" as discussed,
    and forward the paper so revised to LEWG as the recommended resolution of LWG3576
    and LWG3639.**
    - Attendance: 8 (2 abstention)

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   3 |   0 |   0 |   0 |

    - Consensus in favor.
- Discuss survey questions to suggest for the 2023 C++ Developer Survey
  - PBrett proposed separating the survey questions into two categories:
    - The form of the source code; how the source code is written.
    - The facilities used to perform text processing.
  - PBrett suggested that questions about tools might comprise an additional category.
  - Inbal suggested asking for input on what topics most urgently require solutions in
    the standard.
  - Tom replied that a free form question could be used for that and that the current
    developer survey presents such free form responses as a word cloud.
  - PBrett asserted that the questions should address the topics we most want to learn
    about.
  - PBrett suggested asking what facilities programmers are using in place of standard
    facilities like `std::regex` and `std::locale` that are known to have significant
    design issues.
  - Hubert noted that the standard notion of locale encompasses both interface and
    locale identification; a programmer may use `std::locale` or the C locale facilities
    for locale identification, but then use alternate facilities for locale dependent
    behavior.
  - PBrett pondered whether the facilities programmers actively use to support
    internationalization and localization is one of the topics we are most ignorant of.
  - Hubert responded that there is speculation that programmers avoid the standard
    facilities but that we don't have data to confirm that.
  - Steve stated that Bloomberg actively avoids the standard locale related facilities.
  - Victor suggested it might be helpful to ask if programmers are intentionally using
    the standard locale facilities and noted that many do so inadvertently.
  - Victor noted that the questions need to consider C and C++ locale facilities as
    distinct facilities.
  - PBrett suggested structuring the questions as:
    - "Do you provide internationalization support", and
    - "If so, how do you provide internationalization support".
  - Victor stated that those questions should include multiple selection responses
    that include C, C++, POSIX, etc...
  - PBrett suggested adding ICU and other popular packages.
  - PBrett asked for additional topics that we might be particularly ignorant about.
  - Steve suggested asking if programmers are still having to work with multiple character
    encodings within their main application and, if so:
    - whether they transcode at application boundaries and work exclusively with Unicode
      internally, or
    - whether they work directly with data in whatever character encoding it is provided in.
  - PBrett suggested it would be useful to know how often programmers use regular
    expressions where the pattern is not known until run-time.
  - Victor pondered whether Hana coerced Peter to ask that question.
  - PBrett responded that she did not, but that the question does concern whether and to
    what extent CTRE is a suitable substitute for `std::regex`.
  - Steve agreed that it would be useful to understand what the requirements for a
    replacement are.
  - Charlie stated that a replacement would need to be more ABI resilient but that there is
    no need to pass compiled regular expression objects across module boundaries.
  - Steve suggested asking which regular expression languages programmers are using.
  - PBrett responded that question requires an "I don't know" response option.
  - Tom asked if it would be helpful to know how many programmers are using `TCHAR` in
    Windows environments.
  - Charlie reported suspicion that many programmers are still using that.
  - Tom wondered what we might do with such data if we had it.
  - PBrett suggested it would be interesting to know what libraries programmers are
    using for Unicode algorithm support and string classes.
  - Tom asserted that that question would need to be multiple choice with an
    "other" option.
  - Tom recalled one of the questions Peter had suggested on the mailing list,
    "what language(s) do you use in identifiers and comments?", and asked whether the
    question was intended to probe the languages used or whether characters outside the
    basic character set are being used.
  - PBrett replied that the interest is in the language; the goal is to find out which
    scripts are being used.
  - Tom recalled one of the questions Zach suggested,
    "How often do you use multiple Unicode normalization forms in the same program?"
    and commented that this is similar to the encoding question; whether programmers
    normalize at program boundaries or not normalize at all.
  - Steve stated this is an important consideration for deciding if normalization
    belongs in the type system.
  - Tom mentioned that Zach also posed questions about collation support.
  - Steve replied that collation needs depend on context; data in a database is likely
    to be ordered in a locale independent manner but may need to be reordered for
    presentation in a user's locale.
  - Inbal asked if serialization is within the purview of SG16.
  - Tom replied that it could be for producing and consuming text formats.
  - Inbal stated that, given a list of keywords, it would be possible to scrape
    stackoverflow.com for related questions.
  - Tom wondered about asking if programmers place locale constraints on their users;
    for example, whether they require use of UTF-8.
  - Hubert responded that such a question won't garner a 100% yes answer, so may not
    be so helpful.
  - Tom replied that it might be useful to help guide where we invest effort; if lots
    of products support non-UTF-8 environments, then we know to focus more broadly.
  - Hubert agreed with that perspective.
  - PBrett stated that a transcoding facility remains high on our priority list and
    asked if the question about internal encodings and translation at program boundaries
    was intended to probe actual need.
  - Tom responded that he had not thought about that relationship concretely.
  - Steve suggested that question is more related to how many programmers need to
    operate directly on text in multiple encodings and if facilities are needed to do so.
  - Hubert stated that gathering interest in a rope class would be useful.
  - Tom asked if that would be for the case of stringing together blocks of text that are
    differently encoded.
  - Hubert responded affirmatively.
  - PBrett noted such a type is also useful in cases where buffers are in different places.
  - Tom pondered what we would do with data regarding which character types are in use; for
    example, whether we would choose not to focus on `char32_t` as anything other than a
    code point type.
  - Steve suggested asking if programmers use `signed char` and `unsigned char` for text as
    opposed to for use as small integers like `int8_t` and `uint8_t` or for other forms of
    bit manipulation.
  - Hubert responded that `unsigned char` is likely used for UTF-8.
  - Victor responded that `unsigned char` is often used for `uint8_t` and that this causes
    formatting confusion.
  - Inbal asked if C and C++ compatibility is important.
  - Tom replied that it is helpful to decide if we need low level C utilities that are
    exposed via C++ wrappers.
  - Tom added that JeanHeyd has been pursuing the approach of getting low level facilities
    for transcoding through WG14 before continuing work on transcoding support in WG21.
  - PBrett raised the question of which kind of C string interfaces are important;
    null terminated vs Pascal strings.
  - PBrett mentioned WG14 Annex K and noted that Microsoft can't ship it due to conflicts
    with their historical secure function implementation.
  - Hubert returned to the topic of localization and stated it would be useful to know if
    programmers customize locale formatting or just rely on default formatting.
  - Tom stated that he will draft a Google doc with an initial set of questions based on
    this discussion that we can all comment on and contribute to.
  - Further discussion ensued regarding stability vs the need to evolve and fix defects.
- Tom stated that the next meeting will be on 2022-06-22 and that, if we make good progress
  refining and suggesting survey questions in the interim, then we'll probably continue this
  discussion then.


# May 25th, 2022

## Agenda
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/ad0a0ed160ef6216954c699ba5b8497190eaf29c/presentations/2022-05-25-d2572r0.html)
  - Continue review pending the availability of an updated revision.
- [L2/22-072R: Proposal for amendments to UAX#9 and UAX#31](https://www.unicode.org/L2/L2022/22072r-uax9-uax31-amd.pdf)
  - Review for familiarity and relevance to
    [P1949: C++ Identifier Syntax using Unicode Standard Annex 31](https://wg21.link/p1949).

## Meeting summary
- Attendees:
  - Charles Barto
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
- In honor of a new attendee, a round of introductions was conducted.
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/ad0a0ed160ef6216954c699ba5b8497190eaf29c/presentations/2022-05-25-d2572r0.html)
  - Tom presented the paper.
  - Robin pointed out a spelling error; "IDIOGRAPHIC" -> "IDEOGRAPHIC" (two occurrences).
  - Charlie explained that the ABI mitigation technique discussed in the
    "Future considerations and ABI" section relies on persistence of at least the fill character
    portion of the format string but such persistence is not otherwise currently required
    because the format string is evaluated at compile-time.
  - Charlie stated he could imagine ways of accomplishing the goal though.
  - Tom asked for confirmation that the Microsoft implementation is already shipping and
    locked into its current ABI.
  - Charlie confirmed that is the case.
  - Tom stated that he would add a note to the ABI section stating that some implementations
    are already locked in to their current behavior.
  - Steve commented that there are escape hatches and that other extension means are possible
    should the need arise.
  - Charlie explained why implementing ABI resiliency would likely impose dynamic memory
    management costs including possible lifetime management challenges.
  - Jens reported finding it a bit concerning that the estimated width of a character would be
    honored in some cases but not in others, but recognized the trade offs involved.
  - Jens stated that boilerplate wording is needed within the format section in order for the
    proposed use of "U+007B LEFT CURLY BRACKET" and "U+007D RIGHT CURLY BRACKET" to be
    applicable to the literal encoding.
  - Tom stated that the proposed wording changes to table 64 need work; in
    "if that value is negative", it is not clear whether "value" refers to "*n*" or to
    "the width of the formatting argument".
  - Jens requested that "estimated" be inserted before "width" in
    "the width of the formatting argument".
  - Hubert stated that "formatting argument" doesn't sound like the right term in this context;
    it should probably be "formatted argument".
  - Tom reported that this term was used for consistency with wording elsewhere but that he
    would review and try to improve.
  - Jens requested that the note following table 64 be modified to replace "ignored" with
    "assumed to be 1".
  - Tom agreed.
- [L2/22-072R: Proposal for amendments to UAX#9 and UAX#31](https://www.unicode.org/L2/L2022/22072r-uax9-uax31-amd.pdf)
  - Tom provided a brief introduction.
  - Hubert asked if it is necessary to address the UAX31-R3 conformance concern for C++23.
  - Tom replied that he did not believe so since the annex is non-normative.
  - \[ Editor's note: Zoom crashed for Tom and it took him several minutes to get reconnected.
    Jens assured him that the time missed primarily concerned the flogging of a dead horse. \]
  - Jens asked what version of Unicode is expected to receive the proposed amendments.
  - Robin replied that Unicode 15 is expected to have these updates and that more significant
    normative changes are anticipated for Unicode 16.
  - Robin stated that Unicode 15 is expected to be released in September.
  - Jens observed that September would be just in time for adoption in C++23.
  - Steve suggested that the annex could be updated to claim non-conformance with UAX31-R3.
  - Hubert agreed and noted that we may not want to change our dated UAX31 reference at that
    late point in the C++23 release cycle.
  - Jens proposed that we proceed with an NB comment on the C++23 committee draft to request
    upgrading the bibliography reference for UAX31 to Unicode 15.
  - Jens explained that, since the new Unicode release won't be available before then, it won't
    be possible to act on a core issue and an NB comment would end up being required anyway.
  - Robin directed discussion to allowances for U+200E LEFT-TO-RIGHT MARK (LRM) and
    U+200F RIGHT-TO-LEFT MARK (RLM) to be used in combination with other whitespace.
  - Robin stated that example wording can be found in the Ada 2012 reference manual;
    [section 2.2 paragraph 7 1/3, "Lexical Elements, Separators, and Delimiters"](http://www.ada-auth.org/standards/rm12_w_tc1/html/RM-2-2.html#p7.1)
    states:
      > One or more other_format characters are allowed anywhere that a separator is;
      > any such characters have no effect on the meaning of an Ada program.
  - Jens noted that this would be a new kind of whitespace for C++ since sequences of these
    marks by themselves would not constitute whitespace.
  - Jens expressed curiosity regarding "implicit directional marks" as discussed in L2/22-072R.
  - Robin replied that "implicit directional marks" is discussed in
    [UAX #9 section 2.6, "Implicit Directional Marks"](https://unicode.org/reports/tr9/#Implicit_Directional_Marks).
  - Robin explained that, per
    [UAX #9 section 6.5, "Conversion to Plain Text"](https://unicode.org/reports/tr9/#Conversion_to_Plain_Text),
    such marks may be implicitly inserted during conversion to plain text for text subject to protocol
    [UAX9-HL4](https://unicode.org/reports/tr9/#HL4)
    and that Unicode 15 will recommend that protocol for source code text.
  - Hubert asked if it would make sense to prohibit sequences consisting of more than one of
    these marks.
  - Robin replied that he knew of no motivation for doing so; that the presence of multiple
    marks should not pose any negative consequences.
  - Jens expressed opposition to these marks constituting whitespace separation in isolation.
  - Tom agreed.
  - Jens noted that specification of LRM and RLM in whitespace will have to target C++26 as
    C++23 is now closed to new language changes.
  - Jens suggested that such a change could be adopted as a DR against C++23 to encourage
    recognition of these marks as a conforming extension in prior language modes.
  - Jens stated that a paper will be needed and that it should await the availability of
    Unicode 15.
  - Tom stated he would file a SG16 github issue to track the request for such a paper.
  - \[ Editor's note: Tom filed
    [SG16 issue 74: Extend whitespace to include NEL, LS, PS, LRM, RLM, and maybe ALM](https://github.com/sg16-unicode/sg16/issues/74). \]
  - Tom noted that this isn't a particularly urgent issue to address.
  - Jens countered that it would be helpful to prevent obfuscated display of source code
    and that the desire to avoid such confusion has gained prominence in recent times.
  - Jens directed discussion towards future conformance with UAX31-R3 and that there are
    questions about `Pattern_White_Space` that need to be answered.
  - Robin asked which `Pattern_White_Space` characters are not considered whitespace in
    C++.
  - Hubert listed them; they are all the ones outside the ASCII subset.
    - U+0085 NEXT LINE
    - U+200E LEFT-TO-RIGHT MARK
    - U+200F RIGHT-TO-LEFT MARK
    - U+2028 LINE SEPARATOR
    - U+2029 PARAGRAPH SEPARATOR
  - Hubert noted that the above characters can only appear in comments and character or
    string literals currently.
  - Jens asked if it is the intent of UAX31-R3 to require that all of the characters in
    `Pattern_White_Space` be supported as whitespace.
  - Robin replied that allowing a subset would render the requirement vacuous.
  - Jens suggested the possibility of updating UAX31-R3 to specify a minimal subset.
  - Robin responded that a sub-requirement like UAX31-R3a could be introduced; such
    sub-requirements can be found elsewhere in UAX #31.
  - Steve noted that the current normative text of UAX31-R3 allows deviation by specifying
    a profile.
  - Hubert asked what motivation exists for not accepting the other whitespace characters.
  - Steve noted existing practice and suggested this be addressed in the future paper.
  - Jens directed discussion to conformance with the `Pattern_Syntax` requirement of
    UAX31-R3.
  - Robin expressed a belief that C++ conforms to that.
  - Tom expressed curiosity with regard to the presence of `.` in `Pattern_Syntax` and
    its use within floating point literals.
  - \[ Editor's note: Tom's concern stems from the following note in the description of
    UAX31-R3. Is the use of `.` in floating point literals considered syntax or part of
    a literal?
      > **Note:** When meeting this requirement, all characters except those that have
      > the Pattern_White_Space or Pattern_Syntax properties are available for use as
      > identifiers or literals.

    \]
  - Hubert stated that this kind of confusion is why he is hesitant to declare conformance
    to UAX31-R3 prior to improved wording that will hopefully appear in Unicode 16.
  - Jens summarized the three tasks identified so far:
    - For C++23, file an NB comment after the July plenary to update
      [\[uaxid.pattern\]](http://eel.is/c++draft/uaxid.pattern)
      in annex E to state that conformance with UAX31-R3 is not claimed.
      At the same time, update the UAX references in the bibliography to refer to
      Unicode 15.
    - For C++26, author a paper to add LRM, RLM, and other `Pattern_White_Space` characters
      to the set of whitespace characters.
      If support for U+061C ARABIC LETTER MARK is also desired, that will require a profile
      to conform with UAX31-R3.
    - For C++26, update
      [\[uaxid.pattern\]](http://eel.is/c++draft/uaxid.pattern)
      in annex E to claim conformance with UAX31-R3.
      At the same time, update the UAX references in the bibliography to refer to
      Unicode 16 (or later).
  - Robin noted that Unicode 15 is planned for release on September 13th per
    https://www.unicode.org/versions/beta-15.0.0.html.
  - Tom recalled Hubert mentioning on the mailing list that
    U+000D CARRIAGE RETURN (CR)
    can now be added to the basic character set.
  - Hubert acknowledged and opined that we can do so as part of
    [P2348: Whitespaces Wording Revamp](https://wg21.link/p2348).
  - Tom stated that CR presumably should have already been present because of the existence
    of the `\r` escape sequence.
  - Jens explained that `\r` creates a requirement for literal encodings but not for the
    basic character set nor an allowance for its use in whitespace.
  - Tom noted that a paper will be needed that targets SG15 and discusses the concerns and
    options available to implementations with regard to UAX9-HL4 and presentation of source
    code that contains right-to-left characters.
  - \[ Editor's note: Tom filed
    [SG16 issue 75: SG15 proposal for implementations that present source code to conform with UAX9-HL4](https://github.com/sg16-unicode/sg16/issues/75)
    to track producing such a paper. \]
- Tom stated that the next meeting will be in two weeks, on 2022-06-08.


# May 11th, 2022

## Agenda
- [P2286R8: Formatting Ranges](https://wg21.link/p2286r8)
  - Review and approve final wording updates.
- [P2558R1: Add @, $, and \` to the basic character set](https://wg21.link/p2558r1)
  - Continue review pending the availability of an updated revision.

## Meeting summary
- Attendees:
  - Charles Barto
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [P2286R8: Formatting Ranges](https://wg21.link/p2286r8)
  - \[ Editor's note: D2286R8 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2286R8 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Victor summarized recent wording changes worked out on the SG16 mailing list.
  - Victor asked if "code point" should be preferred over "character" in the proposed wording
    for \[format.string.escaped\]p2.
  - Tom replied that he is unaware of any normative use of "code point" in the standard today.
  - Victor responded that it is used in the wording for format field width estimation.
  - Hubert stated that the usage there is in a Unicode specific context and that "character"
    is probably most appropriate here.
  - Hubert pointed out that, in \[format.string.escaped\]p2.3, it is odd that *c* is defined
    as a character, but then compared with UCS scalar values.
  - Jens agreed and proposed substituting "character" for "UCS scalar value" in paragraph
    2.3.1 and in the header of the associated table.
  - Jens suggested doing likewise in paragraph 2.3.3.
  - Hubert argued that a change is not needed in 2.3.3 due to the use of "corresponds".
  - Tom noted the use in that paragraph is also a Unicode specific context.
  - Tom asked Charles if he continues to have concerns regarding the lack of specification
    for determining the boundaries of ill-formed code unit sequences.
  - Charles replied that he does and that he would like to see it addressed via a reference
    to the [WHATWG Encoding Standard](https://encoding.spec.whatwg.org).
  - Tom responded with uncertainty whether such a normative reference is possible given the
    lack of versioning around that standard.
  - Charles suggested that the method specified in the WHATWG standard could be replicated
    in the C++ standard; we want the "maximal subpart" behavior described by policy option 2
    in [Unicode PR-121](http://unicode.org/review/pr-121.html).
  - Hubert asked if that policy is defined for all UTF encodings.
  - Charles replied that it is.
  - PBrett asked what the motivation is for rigorously specifying how the boundaries of
    ill-formed code unit sequences are determined.
  - Charles replied that the goal is to ensure consistent output, but then noticed that, in
    this case, the method used does not appear to be observable since each code unit of the
    sequence is written to the output anyway.
  - Tom agreed that it should not matter for self-synchronizing encodings.
  - Charles noted that this will be the first instance of Unicode UCD properties being
    normatively required by the C++ standard.
  - Charles suggested that, if we're ok with such normative use, we could revisit the wording
    for estimated format field widths to make the uses there normative as well.
  - \[ Editor's note: [\[format.string.std\]p11](http://eel.is/c++draft/format.string.std#11)
    specifies normative encouragement of behavior that depends on UCD properties in order to
    identify extended grapheme cluster boundaries. \]
  - \[ Editor's note: This would not be the first normative use of the UCD properties;
    [\[lex.name\]p1](http://eel.is/c++draft/lex.name#1) requires the `XID_Start` and
    `XID_Continue` properties to determine identifier boundaries and validity. \]
  - Jens requested that such changes not be handled via this paper.
  - Steve asked how much data is required for the new uses of the `General_Category` and
    `Grapheme_Extend` properties.
  - Victor replied that the necessary data fits in ~1K.
  - Charles agreed and shared a
    [link to code](https://github.com/microsoft/STL/blob/main/stl/inc/__msvc_format_ucd_tables.hpp)
    used to implement a grapheme break algorithm that uses the `Grapheme_Cluster_Break` and
    `Extended_Pictographic` properties.
  - Charles noted that some creative packing is necessary to get the size that small.
  - Tom expressed surprise that `Grapheme_Extend` is small.
  - Victor replied that it is composed of a number of compressable ranges.
  - \[ Editor's note: The set of all characters that satisfy the `Grapheme_Extend=yes` property
    can be viewed
    [here](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=%5B%3AGrapheme_Extend%3DYes%3A%5D&g=&i=);
    that set comprises 2090 code points in Unicode 14. \]
  - **Poll: Forward D2286R8 to LWG with 2.3.1 and associated table revised to substitute "character" for "UCS scalar value" as discussed for inclusion in C++23**
    - Attendance 8
    - No objection to unanimous consent.
- [P2558R1: Add @, $, and \` to the basic character set](https://wg21.link/p2558r1)
  - \[ Editor's note: D2558R1 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2558R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Steve introduced the changes made since the last review; just the addition of annex C wording.
  - **Poll: Forward D2558R1 to EWG for inclusion in C++26**
    - Attendance: 8 (1 abstention)

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   1 |   3 |   0 |   0 |

    - Consensus in favor.
  - Steve stated that he would follow up with SG22 with regard to issues found that
    were not discussed in WG14.
  - \[ Editor's note: Steve did so via a
    [post to the C liaison list](https://lists.isocpp.org/liaison/2022/05/1071.php). \]
- Tom stated that the next meeting is scheduled for May 25th.


# April 27th, 2022

## Agenda
- [P2286R7: Formatting Ranges](https://wg21.link/p2286r7)
  - Review recent updates and confirm direction.
- [P2558R1: Add @, $, and \` to the basic character set](https://wg21.link/p2558r1)
  - Review recent updates.

## Meeting summary
- Attendees:
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2286R7: Formatting Ranges](https://wg21.link/p2286r7)
  - \[ Editor's note: D2286R7 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2286R7 since the links to the draft paper were not shared
    publicly. The published document may differ from the reviewed draft revision. \]
  - PBrett provided an introduction.
  - Victor explained that LWG reviewed the wording and conditionally approved the paper subject
    to SG16 review.
  - PBrett recalled concerns raised in the past regarding the use of Unicode properties.
  - Victor replied that implementors were present during the LWG review and did not express
    any objections or concerns.
  - Victor noted that Hubert provided some wording tweaks during the LWG review.
  - PBrett presented wording updates Tom
    [proposed on the SG16 mailing list](https://lists.isocpp.org/sg16/2022/04/3111.php).
  - PBrett expressed a preference for Tom's wording relative to the current wording.
  - Victor stated that he is ok with Tom's wording so long as it is equivalent to the
    current wording in the paper for the Unicode case.
  - Victor stated that he would prefer not to defer to other format facilities for the
    description of how hexadecimal values are formatted.
  - Hubert expressed a desire to document spacing and non-printable characters by their
    encoded values as opposed to their character names or glyphs.
  - Hubert explained that doing so would free the library from having to be aware of the
    literal encoding selected at compile-time.
  - Tom acknowledged the concern; the set of spacing and non-printable characters, or
    their encoded values may differ for one literal encoding vs another.
  - Hubert noted that the concern applies to both EBCDIC and Windows code pages.
  - Hubert stated that the proposed wording could produce strange results in cases where
    unnecessary shift states are present.
  - PBrett observed that the current wording does not state which encoding is used in cases
    where printable characters overlap with control characters in a related encoding, but
    the proposed wording does.
  - Jens noticed that the proposed wording states that the literal encoding is used to
    construct *E*, but not to interpret *S*.
  - Tom acknowledged the omission and stated that it needs to be corrected.
  - PBrett returned to his example where a locale encoding overlays graphical characters
    over control characters and noted that the overlayed characters would be interpreted
    in the literal encoding.
  - Hubert reported that his implementations are not affected by overlay concerns and that
    locale support can be added later if motivated.
  - Zach asked if the method for determining whether *S* is in a Unicode encoding matches
    the method specified for `std::format()` in C++20.
  - Tom replied that he didn't recall how it was specified.
  - \[ Editor's note: It does not appear to be specified. The relevant wording simply states
    "For a string in a Unicode encoding, ...". See
    [\[format.string.std\]p11](http://eel.is/c++draft/format#string.std-11),
    [\[format.string.std\]p12](http://eel.is/c++draft/format#string.std-12), and
    [\[format.string.std\]p14](http://eel.is/c++draft/format#string.std-14).
    Improvements appear to be warranted. \]
  - Jens stated that, with the exception of the use of *CE* for string *S*, this is
    well-specified so long as it matches the desired behavior.
  - Tom noted that `std::format()` is intentionally locale independent.
  - Hubert reported that his implementations will likely assume a certain literal encoding
    rather than storing the literal encoding actually used at compile-time; that encoding is
    likely to be EBCDIC 1047 or, for ASCII contexts, ISO-8859-1.
  - Hubert expressed his understanding of the design intent to be that an escaped sequence
    can be interpreted to reproduce the original byte sequence.
  - Hubert suggested that it may be worth adding a note to that effect.
  - Tom acknowledged the intent and noted that his wording fails to reflect that intent for
    stateful encodings since state transitions in *S* should be reflected as escape sequences
    rather than interpreted when constructing *E*.
  - PBrett asked for other concerns.
  - Tom noted that there is the issue of handling boundaries of ill-formed code unit sequences
    and asked if anyone wanted to argue for addressing that now.
  - PBrett expressed a preference not to address it now.
  - Hubert suggested it could be unspecified or implementation-defined.
  - Tom replied that it is more-or-less implied at present.
  - PBrett agreed.
  - Tom summarized the discussion; we agree that we want revised wording for this case but that
    we don't quite have what we want yet.
  - Tom said he will inform LWG that we'll continue iterating on the wording with the intent
    to have something approved by our next meeting in two weeks.
  - Hubert agreed with the summary.
  - Victor gave a thumbs up.
- [P2558R1: Add @, $, and \` to the basic character set](https://wg21.link/p2558r1)
  - \[ Editor's note: D2558R1 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2558R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Steve reported that the prose was updated to record the results of prior discussions in
    order to better explain the intent; the wording has not been changed.
  - Steve presented the paper and noted that section 3 is new.
  - Tom suggested adding a comment in section 3.1 (Universal Character Name) to indicate the
    character corresponding to `\u0060`.
  - PBrett reported a typo in section 3.4, "sting literal" should be "string literal".
  - PBrett noted that, with respect to existing use of these characters, they are usually used
    for convenience where another mechanism could be used.
  - Steve agreed and noted that such use generally occurs in contexts that require some kind
    of magic and where they can generally be escaped in some way.
  - Tom stated that, with regard to raw string literals, a reason to exclude the new characters
    in the delimiter portion is because these characters might acquire meaning in the future
    that could become problematic.
  - Tom expressed a preference to exclude \` for now so that we can preserve it for use as a
    new type of string literal.
  - \[ Editor's note: Such exclusion is unnecessary; the raw string literal delimiter pattern
    is bounded by a double quote and a parenthesis. Allowing use of \` in between those poses
    no ambiguity for a hypothetical new string literal delimited by \`. \]
  - Tom suggested the paper explicitly note that the proposed changes enable these characters to
    portably be used in character literals by virtue of being encoded as a single code unit.
  - Steve agreed to update the paper.
  - PBrett reported another typo in section 3.3, "invarient" should be "invariant".
  - Jens expressed a continuing interest in the paper showing examples of behavioral changes.
  - Hubert noted that such examples should be added to annex C.
  - Steve reported two known compatibility issues:
    - Use of a UCN to name one of these characters in stringification.
    - Use of a UCN to name one of these characters as an argument to a function-like macro that
      does not use the corresponding parameter.
  - Steve stated that SG22 may want to review these updates.
  - Steve suggested it may suffice to forward an updated paper via an SG16 mailing list review.
  - Tom agreed.
- Tom stated that the next meeting will be May 11th and will hopefully include review of an
  updated revision of D2572R0 (std::format() fill character allowances).


# April 13th, 2022

## Agenda
- [P2558R0: Add @, $, and \` to the basic character set](https://wg21.link/p2558)
  - Initial review.
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/c84e3e4eef341795fb9ac44824525a3a89583fa7/presentations/2022-04-13-d2572r0.html)
  - Initial review.

## Meeting summary
- Attendees:
  - Charles Barto
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [P2558R0: Add @, $, and \` to the basic character set](https://wg21.link/p2558)
  - PBrett asked whether this proposal is an SG16 concern.
  - Tom replied that we are the encoding experts and best equipped within the committee to evaluate 
    whether these changes will have consequences for source character sets used in practice;
    our affirmation of the proposal will hopefully ease progress through other groups.
  - Charlie asked for confirmation that SG22 will review the paper as well.
  - Steve replied affirmatively and stated WG14 has already adopted the proposal for C.
  - Someone (apologies, the editor neglected to record who) noted the existence of
    [P2342: For a Few Punctuators More]([https://wg21.link/p2342)
    and that it argues that these characters could be used as new operators.
  - Tom responded that P2342 is an example of a paper that is not an SG16 concern; once the
    characters are available in the source character set, how they are used is an EWG concern.
  - Hubert observed that this introduces a requirement that these characters be encoded as a
    single code unit.
  - Jens acknowledged and noted that this is required by
    [\[lex.charset\]p6](http://eel.is/c++draft/lex.charset#6)
    for all characters in the basic literal character set.
  - Jens requested that the paper prose discuss this requirement.
  - Steve agreed to add such prose.
  - Jens stated that he does not know if this requirement would be problematic for any existing
    character sets.
  - Steve replied that there are infrequently used EBCDIC code pages that lack them.
  - Jens asked if those code pages also lack other characters.
  - Steve responded that they probably do.
  - Charlie asked if those problematic EBCDIC code pages have unused code points that could be
    used for these characters.
  - Tom suggested that digraphs could be introduced to support those code pages if needed.
  - Jens replied that digraphs can't be used inside character or string literals.
  - Steve suggested this concern can be addressed if these characters start getting used
    within the standard.
  - Jens reported that the addition of these characters to the basic character set makes them
    ineligible to be specified via a *universal-character-name* (UCN) outside of a character
    or string literal due to
    [\[lex.charset\]p3](http://eel.is/c++draft/lex.charset#3).
  - PBrett suggested that restriction could be lifted.
  - Charlie stated that existing uses of '$' are probably limited to identifiers and symbol
    renaming via attributes, pragma directives, or `asm` labels.
  - Hubert reported they may appear in preprocessor stringization.
  - PBrett reported they may appear in header names as well.
  - Jens noticed that use of a UCN to`#include` a source file named with one of these characters
    would become ill-formed.
  - PBrett reiterated support for lifting restrictions on use of UCNs to name characters from the
    basic character set with the rationale that we shouldn't ban things that are only bad ideas.
  - Charlie stated that, if such incompatibilities were to cause problems in practice, then
    lifting that restriction would be the obvious solution.
  - Steve suggested such concerns can be addressed after the paper is approved; we know programmers
    want to use these characters.
  - Tom asked Steve if he knows whether the UCN concern was discussed in WG14.
  - Steve replied that it was not.
  - Hubert asked when UCNs are translated in identifiers and other preprocessor tokens.
  - Jens replied, during translation phase 3 except in quoted contexts; so translation occurs as
    a *preprocessing-token* is formed.
  - PBrett observed that the new UCN restrictions would be limited to *h-char* and *q-char*
    sequences since these characters aren't otherwise usable outside quoted contexts.
  - Jens replied that they may also appear in a *preprocessing-token* used in stringization.
  - Hubert stated that a UCN specifying one of these characters would become ill-formed during
    stringization.
  - Hubert added that, likewise, use of a UCN to specify '$' in an identfier would become ill-formed.
  - Tom asked whether that matters since use of '$' in an identifier is already an extension.
  - Jens noted that these characters currently match the
    "each non-whitespace character that cannot be one of the above"
    case of
    [*preprocessing-token*](http://eel.is/c++draft/lex.pptoken#nt:preprocessing-token).
  - Jens requested that this discussion be included in the paper.
  - PBrett asked whether *h-char* and *q-char* sequences remain a backward compatibility concern.
  - Jens replied that they do, but that UCNs in such sequneces already have implementation-defined
    behavior; what UCNs mean in *h-char* and *q-char* sequences isn't really defined.
  - \[ Editor's note: Per
    [\[lex.phases\]p1.3](http://eel.is/c++draft/lex.phases#1.3),
    UCNs are not recognized and replaced in *h-char-sequence* and *q-char-sequence* sequences and, per
    [\[lex.header\]p1](http://eel.is/c++draft/lex.header#1),
    these sequences are mapped in an implementation-defined manner. \]
  - Tom suggested that it might be worth updating the paper to describe how existing implementations
    behave with respect to UCNs in preprocessor token concatenation, stringization and `#include`
    scenarios.
  - Jens asked if there are other ways in which these characters might plausibly be used today.
  - Tom replied that Objective-C uses '@'.
  - Jens mentioned the possibility of concerns being raised regarding the imposition of single code
    unit encoding for these characters on the execution character set.
  - Tom asked Hubert if he was aware of any EBCDIC related concerns.
  - Hubert replied that his colleagues in WG14 did not express such concerns and that he is confident
    that they would have if they had any.
  - Hubert noted that locales that don't support these characters would no longer be strictly
    conforming but could still be supported as extensions.
  - Tom summarized the discussion; there are requests to Steve to update the prose for several of
    the items discussed, but that there do not appear to be any objections to the paper direction.
- [D2572R0: std::format() fill character allowances](https://rawcdn.githack.com/sg16-unicode/sg16-meetings/c84e3e4eef341795fb9ac44824525a3a89583fa7/presentations/2022-04-13-d2572r0.html)
  - Tom provided an overview of the topic and prior discussions.
  - Tom asked for additional categories of characters that should be represented in the introductory
    table.
  - Tom stated that Zero-Width Joiner (ZWJ) and Zero-Width Non-Joiner (ZWNJ) cases were not added
    because he thought they were not interesting.
  - Tom noted that lone surrogates should not be possible.
  - PBrett suggested the bidirectional override characters.
  - \[ Editor's note: the bidirectional override characters are U+2066 through U+202E. \]
  - Tom agreed to add right-to-left and left-to-right examples.
  - Tom stated that extending fill character support to arbitrary extended grapheme clusters (EGCs)
    in the future would presumably impose an ABI break.
  - Mark agreed that it would; at least one implementation only stores a single code unit as the
    current wording appears to specify.
  - Charlie agreed and noted that another implementation stores the fill character as a code unit
    sequence with a maximum length of 4 code units for UTF-8.
  - Tom noted that, for the "Estimated display width restrictions" section, there is no good or
    right solution.
  - Tom asked if characters with an estimated width other than one were to be banned, how that would
    be accomplished without imposing undesirable overhead.
  - PBindels noted that the ZWSP case is interesting; if it were given an estimated-width of 0,
    then an infinite amount of padding would be required.
  - Charlie stated that the estimated width is not intended to be accurate; it is best effort.
  - Charlie stated that, in the "Existing practice" section, `std::format_error` is now thrown
    for the cases that previously produced the stack overflow for MSVC.
  - Charlie noted that the diagnostic is somewhat disappointing though since an invalid type is
    reported because the intended fill character does not match the *fill-and-align* grammar.
  - \[ Editor's note: The diagnostic produced by gcc with {fmt} is likewise disappointing. \]
  - PBrett suggested that a table that demonstrates the desired output inline with the proposal
    would be useful.
  - Victor stated that the paper direction makes sense and is consistent with previous guidance.
  - Victor pondered the consequences of diagnosing fill characters with an estimated width other
    than one; on one hand, it would be nice, but on the other hand, it adds overhead and
    potentially restricts valid use cases.
  - PBrett suggested that fill characters with an estimated width other than one could be
    conditionally supported.
  - PBrett stated that his preferred approach would be to diagnose at run-time (e.g., throw an
    exception) when alignment requirements could not be achieved due to the estimated width of
    the fill character.
  - PBindels reviewed the "Proposal" section and stated:
    - The first point to restrict to a single UCS scalar value seems sensible.
    - The third and fourth points appear to be consistent with what implementations currently do.
    - The second point is the questionable one.
  - PBrett suggested that the number of fill characters inserted could be unspecified when the
    fill character has an estimated width other than one.
  - PBindels replied that he considered that as well, but since the actual width is dependent on
    font selection, a consistent result may not be achieved anyway.
  - Charlie reminded the group that the estimated widths are not currently specified by any standard.
  - Charlie observed that diagnosing fill characters with an estimated width other than one will
    have the potential effect of rendering existing code invalid if estimated widths are changed
    in the future.
  - PBrett suggested another possibility that, if the fill character has an estimated width of two,
    then perform the alignment as if the fill character and all characters in the format argument
    have an estimated width of one; this would enable idiographic characters to be formatted properly.
  - Charlie responded that, if such a feature is desirable, then it would be preferable to add a
    flag to opt-in to it rather than inferring it based on the chosen fill character.
  - Tom agreed and noted that idiographic characters are just one special case.
  - Charlie stated that, for table style alignment, it is likely preferrable to emit a field
    separator character explicitly in the format string rather than to rely on the fill and align
    capabilities.
  - PBindels asserted that there is value to having well-defined portable behavior across
    implementations, so unspecified and implementation-defined behaviors should be avoided where
    possible.
  - Hubert asked if Victor has good examples of this facility being used with format arguments
    that have characters with estimated widths other than one regardless of fill character.
  - Victor replied affirmatively, but stated he did not recall specific examples; such cases
    involved terminal output.
  - Tom reported vague recollections of such examples being present in Victor's original papers.
  - PBrett stated that support for certain languages remains a concern for him and reported
    seeing Japanese characters reliably displayed in terminals in tabular formats.
  - Tom asked if he knew how the programmers were facilitating such output.
  - PBrett replied that he did not.
  - PBindels asked if it would be feasible to research what features would be useful for such
    languages.
  - PBrett replied that it isn't feasible for him to do so due to the number of possible
    solutions; he would like to allow implementations to be creative and see what the results bring.
  - PBindels again emphasized a desire for portable behavior.
  - Charlie agreed and stated that a creative solution in one implementation might produce an
    error in another.
  - Tom asked Peter Brett if it would suffice for an implementation to provide a flag to opt-in to
    an alternate behavior.
  - PBrett lamented the absence of attendees that are experts in non-Latin based languages.
  - Hubert questioned the frequency with which a programmer would want to use a fill character with
    an estimated width other than one; the programmer would presumably need to be able to specify a
    fill-remainder character or otherwise provide their own padding.
  - Victor agreed with the goal of specifying consistent behavior and suggested standardizing the
    demonstrated existing behavior in which a fill character is assumed to have an estimated width
    of one.
  - Charlie noted that a programmer can implement their own fancy formatter that produces a result
    that is then embedded using standard formatters.
  - Tom stated that it sounds like we have a few possible extension mechanisms that can be used
    for experimentation, work arounds, or future standard behavior.
  - Tom reported that he is leaning towards Victor's suggestion of specifying the currently
    demonstrated implementation experience.
  - PBindels indicated he would be content with any of the demonstrated outputs so long as behavior
    is consistent across implementations.
  - PBrett expressed concern about specifying particular behavior in the absence of more diverse
    expertise in SG16.
  - PBindels stated that he would reach out within his organization to try to find people with more
    diverse experience that would be interested in attending.
- Tom reported that the next meeting will be on 2022-04-27.


# March 9th, 2022

## Agenda
- ICU features to consider for C++26

## Meeting summary
- Attendees:
  - Charles Barto
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- Tom introduced the topic:
  - Tom was inspired by Jens' assertion during the previous telecon that
    "the elephant in the room is ICU and the functionality it provides".
  - Based on that, Tom created a
    [Google Doc](https://docs.google.com/document/d/1f-CLhYZIf_L0q1QBEqe2sVHyAofGx8Akt_xJKDGhcgA/edit?usp=sharing)
    containing a list of ICU feature categories annotated with Tom's opinions on whether
    such features are worthy of consideration for standardization in C++26 should suitable
    proposals materialize.
  - Tom would like to issue a Call for Papers covering the features we agree are worth
    consideration.
- Tom began reviewing the feature categories in the order they appear in the document.
- The categories enumerated below are those for which there were material comments.
- "Unicode character properties":
  - Tom pondered the benefits of exposing the set of raw UCD properties as opposed to just
    those that are needed for other features.
  - Charles responded that there are representation choices to be made based on usage.
  - Steve noted that support for segmentation requires many of the UCD properties.
  - Steve stated that it would be useful to expose all of the properties to enable experimentation.
  - Steve noted that, if there are design problems with how the data is exposed, that would be
    useful information.
  - PBrett observed that the UCD properties are needed to implement proper internationalization
    and localization support.
  - PBrett pondered whether exposing all UCD properties might create portability issues.
  - Tom asked if it might be reasonable to only expose properties with stability guarantees.
  - Steve replied that doing so probably would not be viable; some properties required for
    segmentation are not stable and there is a need to be able to fix things.
  - Tom noted the difference between data being stable as compared to property shapes being stable.
  - Steve acknowledged and noted that property shapes haven't changed in a while.
  - Steve added that the ICU maintainers would presumably push back hard if Unicode made significant
    changes to the shape of existing properties.
- "Sets of Unicode Code Points and Strings":
  - Tom commented that the items in this category appear to be simple utilities.
  - PBrett opined that may be a good reason to provide them.
  - Tom observed that they appear to be used to provide support for character classes.
- "Locales":
  - PBrett stated that one of the challenges with locale identifiers is that choice of locale is
    not fixed at compile-time.
  - PBrett added that locale IDs are subject to geopolitical changes.
  - Steve reported that there has been much work on client-side localization through
    [ECMA 402](https://www.ecma-international.org/publications-and-standards/standards/ecma-402/), and
    [ICU4X](https://github.com/unicode-org/icu4x).
  - Steve expressed caution over trying to standardize something like ECMA 401 and ICU4X given that
    they are recent developments.
  - Steve noted that client side support uses browser based facilities.
  - PBrett wondered if C++ code compiled to WASM should transparently proxy to the local environment.
  - Tom asked whether new locale support could be built on `std::locale`, perhaps via new facets.
  - Hubert objected to such support built on new `std::locale` facets due to `std::locale` being
    dependent on C locale names.
  - PBrett replied that it would be useful to be able to get an ISO locale name from a standard locale.
  - Hubert noted that encoding information would be lost in that case.
  - PBrett agreed and asserted that encoding ideally wouldn't be a locale concern anyway.
  - Hubert replied that a particular script could be implied by `std::locale`.
  - Steve observed that we seem to be in agreement that we don't know how to do this today.
  - Tom stated that the problem is that proper case mapping, case folding, and collation can't be
    provided without proper locale support.
  - PBrett agreed and asserted the need for a plan to improve locale support.
- "Resource Bundles":
  - Tom suggested that this feature could be built on top of features like `#embed` and support for
    dynamic libraries; perhaps a downstream feature then.
  - Charles noted that Microsoft style resource management can be provided on other platforms using
    linker scripts.
  - PBrett opined that resources are a requirement for a good locale system.
- "Calendars and Time Zones" and "Date and Time Formatting":
  - Tom stated that base facilities exist that could be expanded, but that there are locale
    dependenices.
  - PBrett acknowledged concerns raised by Corentin on the mailing list that noted that the existing
    facilities are not at parity with the ICU features.
- "Message Formatting":
  - Tom stated that this is awaiting further developments from the
    [Message Format Working Group (MFWG)](https://github.com/unicode-org/message-format-wg).
  - PBrett commented that, what programmers want and what they need are not always the same thing.
  - Charles expressed a desire for experience outside the standard before pursuing support in the
    standard; even more so for this feature than for other ones.
  - Charles added that, ideally, a production quality application would be built on top of such a
    facility; one that has users using it from multiple locales.
  - PBrett opined that `std::format()` may not provide a great base to build this on.
  - Charles replied that it is probably usable, but not sufficient as is.
  - Tom stated there would presumably be a need to pass a message ID in place of a format string.
  - Charles reported that could be done using `std::vformat()`.
- "Text Transformation":
  - Tom suggested that, if there is a specific transliteration that we have motivation to provide,
    then we can do so; range adapters provide general support for this otherwise.
  - Steve noted that JeanHeyd's
    [ztd.text](https://ztdtext.readthedocs.io/en/latest)
    library can do some of this.
  - Hubert asked if this feature category is referring to technical transliteration or linguistic
    transliteration.
  - Tom replied that he did not know.
- "Bidirectional Algorithm":
  - Tom asked for confirmation that this does not have locale dependencies and is effectively
    about state management for layout purposes.
  - Steve replied that the algorithm is complicated as it tries to support all possible scenarios.
- "Collation":
  - Jens described a design possibility involving locale independent base functionality that
    operates on a set of locale dependent collation rules.
  - Jens stated that the rules engine would have to be sufficient to perform all tasks required
    by all locales.
  - Jens noted that such a facility could be useful as a building block for locale support and as
    a standalone facility.
- "String Searching":
  - Tom noted the locale dependence.
  - PBrett noted collation dependence.
  - Jens stated that precise requirements are needed and that basic element searching is present.
  - Hubert suggested this might be provided by a regular expression facility.
- "Text Boundary Analysis":
  - Steve stated there are natural range interfaces for this and that the interface is probably clear.
  - Hubert asked when a C++ programmer would use this.
  - Steve replied that he performs such analysis for reflowing text in outgoing email.
  - PBrett added that such support was an integral part of a DSP language he worked on.
  - Steve stated that word wrapping comes up in many scenarios.
- "Regular Expressions":
  - Tom suggested we consider this category if a paper arrives.
  - Tom noted that a proposed design would be locale dependent and would presumably have to operate
    on various string types, potentially including segmented text data structures.
  - PBrett pondered the possibility of a run-time only library with a narrow interface that could
    later be overloaded for new extensions.
  - Steve stated that this is not an area of his experties but that he would be willing to help
    author a paper if a good design were to be proposed.
  - Steve noted that there are many SG16 and LEWG related issues to consider.
- "StringPrep":
  - Hubert stated that this feature is related to string normalization for interchange purposes
    such as key lookup.
  - Jens noted that the
    [stringprep RFC](https://datatracker.ietf.org/doc/html/rfc3454)
    specifies exclusion of certain characters and expressed a desire to better understand what this
    facility is used for.
  - Tom updated the Google Doc to change the consideration column value from "N/A" to "No", to
    add a reference to RFC 3454, and to note that this is a string normalization feature.
- "IDNA":
  - Tom expressed considerable ignorance of this topic.
  - \[ Editor's note: "IDNA" stands for "Internationalizing Domain Names for Applications" and is
    covered by [UTS #46](https://unicode.org/reports/tr46). \]
  - PBrett suggested such support might be needed for standard networking.
- "Universal Time Scale":
  - Tom suggested this is not an SG16 concern and could be tackled directly by LEWG if motivated.
  - Tom updated the Google Doc to change the consideration column value from "N/A" to "No; LEWG".
- "Paragraph Layout / Complex Text Layout":
  - Review of the ICU `playout.h` header revealed that this is an experimental facility.
  - Tom updated the Google Doc to change the consideration column value from "Not yet" to "No"
    and added a note about the facility being experimental.
- "ICU I/O":
  - Tom stated this is not an SG16 concern.
- Tom stated that the next telecon is scheduled for 3/23; the agenda is TBD.


# February 23rd, 2022

## Agenda
- Discuss objectives and priorities for C++26

## Meeting summary
- Attendees:
  - Charles Barto
  - Hubert Tong
  - Inbal Levi
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Tom reminded the group about the upcoming SSRG meeting on Monday, February 28th, and encouraged
  the contribution of suggested improvements for
  [P2528R0 (C++ Identifier Security using Unicode Standard Annex 39)](https://wg21.link/p2528)
  to the author.
- Discuss objectives and priorities for C++26:
  - Tom asked the group for suggestions on what we should focus on for C++26.
  - Tom suggested alias barriers as a remaining core language feature improvement.
  - \[ Editor's note: See [SG16 issue #67](https://github.com/sg16-unicode/sg16/issues/67). \]
  - PBrett suggested improvements for access to command line options and environment variables.
  - \[ Editor's note: See [SG16 issue #66](https://github.com/sg16-unicode/sg16/issues/66). \]
  - Jens noted the existing practice for the `_wmain()` entry point in Microsoft Visual C++.
  - PBrett noted the `envp` parameter that POSIX adds to `main()`.
  - Tom suggested `std::rope` for chained text segments.
  - Steve suggested transcoding and lamented JeanHeyd's absence.
  - PBrett suggested an owning string type that eschews null termination.
  - Charles expressed concern that a string type that doesn't ensure null termination may not
    improve security due to programmers attempting to pass such data to functions that require
    a null terminated string anyway.
  - PBrett suggested that implicit conversions could be prohibited.
  - Steve noted the usability challenges such prohibition creates.
  - Victor stated that programmers will misuse such types even if implicit conversions are not
    supported; they will assume that, for example, a `data()` member function will provide a
    null terminated string.
  - PBrett replied that such concerns apply to the existing `std::string_view` type as well.
  - PBrett asserted there is room for a `std::string_view` like type that owns the string data.
  - Charles noted that having to pass a string held in such a type to a function that requires
    null termination would require having to copy the string contents just to add a null
    terminator and lamented the cost of such copies.
  - Jens asked PBrett what other features he might like to see in a new string type.
  - PBrett responded that he would mostly like to not have to write yet more string types that
    avoid null termination concerns.
  - Jens suggested that a string type that helps to avoid allocation and deallocation costs
    could be beneficial.
  - Jens stated he would prefer not to spend time in SG16 on general data structures.
  - Jens asserted that the elephant in the room is ICU and the functionality it provides and
    expressed a desire for a roadmap towards providing similar functionality.
  - Steve suggested that PBrett publish a paper extolling the benefits of a string type
    without null termination.
  - PBrett responded that benefits appear when working with databases and graphics.
  - Tom stated that, if a new string type were to materialize, he would like to know for sure
    what encoding it is intended to be used with.
  - PBrett offered two categories of such encoding assurances: 1) a type intended for text
    with an assumed encoding, and 2) a type that enforces well-formed encoding.
  - Steve offered a third category: 3) a type that maintains invariants like normalization form.
  - Steve reported having to investigate problems due to assumption of UTF-8 leading to errors
    when data was passed to Python programs that enforced well-formedness.
  - Steve stated that Bloomberg is strongly in favor of a type that maintains such invariants.
  - Charles expressed desire for a way to pass a filename on the command line that is preserved.
  - Charles explained that this currently isn't possible on Windows due to transcoding that
    occurs when preparing a command line to pass to `main()`.
  - Tom asked if it is possible to enter such names on the command line from Windows shells in
    the first place, but acknowledged it can be done from `CreateProcess()`.
  - Charles replied that tab completion and similar shell features can produce such names.
  - Tom asked to confirm that this should be considered a language issue as opposed to a shell
    issue.
  - Charles explained that other languages provide such mechanisms and noted that Rust has an
    `OsString` type that stores WTF-8 on Windows.
  - PBrett added that Rust is a good example of a language that provides strings that don't
    guarantee null termination.
  - Tom returned to discussion about features to focus on and suggested Unicode algorithms.
  - Hubert asked if ICU provides message formatting features.
  - Tom confirmed that it does.
  - PBrett noted the work that the Message Format Working Group (MFWG) is doing.
  - \[ Editor's note: The MFWG tracks its work
    [here](https://github.com/unicode-org/message-format-wg). \]
  - Tom suggested improved support for regular expressions as another feature to work on.
  - Charles replied that such work depends on whether the committee is willing to standardize
    a `std::regex2` or similar.
  - Charles stated that a new regex design would presumably face the same challenges that
    `std::regex` did and may therefore produce a similarly poor result.
  - Charles noted that regular expression support is a feature for which interoperability
    across libraries is not often needed.
  - PBrett asserted that a standard regex facility is beneficial because general programmers
    aren't particularly good at writing their own.
  - Charles suggested that a class intended to be used as a base class for string buffer
    management could be beneficial for building parsers; particularly a type that provides
    interfaces to peek ahead and push back.
  - PBrett suggested a `std::lexy` with reference to Jonathan Müller's work.
  - \[ Editor's note: Jonathan's Lexy work is published
    [here](https://lexy.foonathan.net). \]
  - Tom asked if the work done on `std::format` provides a precedent for how to design a
    `std::regex` replacement that would be more isolated from ABI concerns.
  - Charles responded that `std::format` is fairly exposed to ABI concerns, but acknowledged
    the possibility of designing a more isolated type.
  - Victor stated that Hana Dusíková's CTRE provides a good example of how to write parsers.
  - \[ Editor's note: Hana's CTRE work is published
    [here](https://compile-time-regular-expressions.readthedocs.io/en/latest). \]
  - PBrett asked about ideas for how to be more explicit about associating an encoding with
    existing text; e.g., how to have text in UTF-8 and pass it to something that requires UTF-16.
  - Steve asked if anyone recalled a proposal that would allow specifically binding to a string
    literal.
  - Tom stated that he did not but noted that a user-defined literal (UDL) can provide similar
    functionality.
  - \[ Editor's note: Tom was thinking of something like this:

        #include <cstddef>
        class string_literal {
        private:
            const char *p;
            string_literal(const char *p) : p(p) {}
        public:
            const char* data() const { return p; }
            friend string_literal operator ""sl(const char *p, std::size_t);
        };
        string_literal operator ""sl(const char *p, std::size_t) {
            return string_literal(p);
        }
        void f(const char*);
        void g(string_literal sl) {
            f(sl.data());
        }
        void h() {
            g("hello"sl);
        }
    \]
  - Steve stated that a facility that allows associating a dynamic encoding
    would be useful for scenarios in which the text and its associated encoding
    are not known at compile time.
  - Victor noted that encodings are often properties of interfaces and suggested that an
    attribute based approach to specifying encoding expecations could be helpful; this would
    allow specifying expectations that are dependent on locale or Windows Active Code
    Page (ACP).
  - Charles expressed support for that approach.
  - PBrett asked what the advantage of an attribute would be.
  - Victor replied that it could be added to existing functions without ABI impact.
  - Charles observed that, if the `#embed` proposal is adopted, then text that is not
    in the literal encoding might be imported.
  - Hubert responded that the `#embed` author has been clear that the proposal is intended
    to provide binary resources.
  - Tom changed topics by asking for suggestions regarding how to solicit new SG16 attendees
    and reported that he and Peter had previously discussed inviting other WG21 members to
    share what the organizations they work with do in practice.
  - PBrett responded that backward compatibility and existing practice are motivation for
    not providing new facilities.
  - PBrett suggested that, if someone were to come forward with a proposal to adopt a suite
    of string types similar to those provided by Rust, that we might tell them no thank you.
  - PBrett stated that we should, of course, discuss any proposals that come before us.
  - Tom replied that seems to argue for the status quo plus what people actually do.
  - Jens expressed belief that there is good opportunity to make progress with small
    improvements and provided a UTF-8 decoding iterator as an example.
  - Tom replied that an existing proposal covers such iterators.
  - \[ Editor's note: See
    [P0244 (Text_view: A C++ concepts and range based character encoding and code point enumeration library)](https://wg21.link/p0244). \]
  - Charles responded that he has written a grapheme iterator.
  - Charles noted that such iterators are always going to be slower than bulk conversion routines.
  - PBrett suggested adding locale-independent replacements for character classification
    functions like `isdigit()`; e.g., `is_ascii_digit()`.
  - Charles expressed support for such locale invariant functions and noted via chat that glib
    provides such a variant named `g_ascii_isdigit()`.
  - Tom noted that there is a distinction; locale-independent variants would operate using an
    implementation-defined encoding where as ASCII variants would operate using ASCII even in
    an EBCDIC environment.
  - Hubert asked if anyone would object to having both variants; e.g., a locale-independent
    variant that always operates using the "C" locale and an ASCII variant.
  - No objections were raised.
  - PBrett stated that the highest priority item should be transcoding facilities.
  - Jens asked if he meant something like `iconv()`.
  - PBrett responded that he meant something more like JeanHeyd Meneide's `ztd::text`.
  - \[ Editor's note: JeanHeyd's `ztd::text` work is published
    [here](https://ztdtext.readthedocs.io/en/latest). \]
  - Charles stated that, with regard to providing an ICU interface in the standard, there are
    performance implications; support for generic iterators would warrant availability of
    definitions for inlining purposes.
  - PBrett asked if anyone could comment regarding the utility of `std::message`.
  - Steve responded that the main problem with message catalogs is that they don't tend to work
    well with real languages.
  - PBrett reported having good experience with GNU gettext, but that it required discipline to
    be used successfully.
  - PBrett stated that the other elephant in the room is locale, but noted that `std::format()`
    provides a foundation we can build on.
  - Tom suggested the possibility of enabling thread-specific locale facilities that avoid reliance
    on a global locale.
  - PBrett suggested a review of all locale dependent interfaces followed by a proposal that adds
    variants that accept a locale as an argument.
  - Jens replied that C already does that and that all C++ interfaces use `std::locale`.
  - Hubert stated that POSIX provides a thread aware locale interface that enables changing locale
    for a specific thread as well as interfaces that accept a locale argument.
  - PBrett provided an example; a `std::isalpha()` overload that accepts a `std::locale` argument.
  - Hubert responded that POSIX specifies a `isalpha_l()` interface that accepts a `locale_t` argument.
  - Tom asked if `std::locale` is fundamentally problematic or whether the problems we face with it
    are isolated to the facets.
  - PBrett responded that it has fundamental limitations due to reliance on inheritance.
  - Victor stated that the facet's assumption that characters fit in a code unit is the most
    significant problem.
  - Victor added that `std::locale` uses reference counting and therefore has a performance profile
    similar to a shared pointer.
  - Hubert stated that `std::locale` strongly ties C++ implementations to the suite of C locales
    since the interface depends on the names of C locales; it is therefore questionable how
    implementors might provide more generic locale support.
  - Steve stated that WG14 recently adopted a proposal that adds '@', '$', and '`' to the basic
    source character set.
  - Steve added that he intends to bring a matching paper to WG21 in the near future.
  - \[ Editor's note: The adopted WG14 proposal is
    [N2701](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2701.htm). \]
- Tom announced that the next meeting will be on March 9th and, unless a new paper materializes,
  will likely focus on diving deeper into one of the topics discussed today.


# February 9th, 2022

## Agenda
- [P2498R1: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r1)
  - Continue prior discussion and poll.
- [D2513R1: char8_t Compatibility and Portability Fixes](https://wg21.link/p2513r1)
  - Initial review.

## Meeting summary
- Attendees:
  - Charlie Barto
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- [P2498R1: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r1)
  - PBrett presented:
    - The R0 revision was reviewed by SG16 a few weeks ago.
    - The R1 revision rebases the wording on the latest P1885 revision.
    - The wording was reworked to decouple IANA IDs from the exposition only data members.
  - Victor noticed an unnecessary trailing semicolon following the closing brace of the
    `std` namespace declaration in the proposed updates to \[text.encoding\].
  - Hubert noted that Corentin's recently added response to P2498R1 in
    [P1885R10](https://wg21.link/p1885r10)
    noted unnecessary use of an enum for the proposed internal details of the `text_encoding`
    class and asked if it was necessary for it to be an enum.
  - PBrett responded that it is exposition only.
  - Jens pointed out an existing `using enum id` declaration in the `text_encoding` synopsis
    that should presumably have been changed to `using enum iana_id`.
  - Jens noted similar renaming updates needed in the postcondition for the
    `text_encoding(iana_id)` constructor where comparisons against `id::unknown` and
    `id::other` are currently present.
  - Jens observed that the `text_encoding(iana_id)` constructor does not state that
    its argument is stored.
  - PBrett explained that such storage is implied by the postcondition requirements on
    the result of calls to `iana_mib()`.
  - Jens suggested that there should be some wording that relates the exposition only `id`
    type to `iana_id`.
  - PBrett agreed that could be better specified.
  - PBrett indicated that some positive guidance is needed before spending further effort on
    this proposal.
  - Tom suggested polling support for the concerns the paper purports to address.
  - Discussion regarding polls ensued.
  - **Poll 1A: It should be more explicit in the identifiers used by the `text_encoding`
    interface that the facility is tied to the IANA character sets database.**
    - Attendance: 8

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   3 |   1 |   2 |   0 |

    - Weak consensus in favor.
  - **Poll 1B: The `text_encoding` class design should be modified to facilitate potential
    future association with additional encoding registries without retaining a bias towards
    the IANA registry.**
    - Attendance: 8 (one abstention)

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   3 |   2 |   0 |   1 |

    - No consensus.
    - SA: I think IANA is a reasonable default and others can be added; we shouldn't slow
      down progress.
  - **Poll 1C: The `text_encoding` class should be renamed to `iana_text_encoding`.**
    - Attendance: 8

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   2 |   2 |   3 |   0 |

    - No consensus.
  - **Poll 1D: Address feedback on wording in P2498R1 "Forward compatibility of text_encoding
    with additional encoding registries", and forward the paper as revised to LEWG as a bug
    fix for P1885 "Naming text encodings to demystify them" with a recommended ship vehicle
    of C++23.**
    - Attendance: 8 (one abstention)

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   4 |   0 |   2 |   0 |
    - Weak consensus in favor.
  - Jens requested that the changes regarding exposition only data members be removed if the
    intent is just to rename some identifiers as opposed to changing the original design intent.
- [D2513R1: char8_t Compatibility and Portability Fixes](https://wg21.link/p2513r1)
  - \[ Editor's note: D2513R1 was the active paper under discussion at the telecon. The agenda
    and links used here reference P2513R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - JeanHeyd presented:
    - The `char8_t` related changes in C++20 made it more difficult to write code that works
      in both C and C++.
    - The proposal is intended to improve compatibility with C.
    - The proposal provides an escape hatch in C++ to restore some uses of UTF-8 string literals
      with `char`, `signed char`, and `unsigned char`.
    - The proposal only relaxes array initialization; pointer behavior is not changed.
    - The changes are intended as a DR against C++20 so that common code can be written for
      C++17, C++20, C++23, and C.
  - Victor stated that relaxing initialization for arrays but not for pointers creates an
    inconsistency and that he prefers an error.
  - Victor added that `signed char` and `unsigned char` are commonly used for `int8_t` and
    `uint8_t` and the proposed changes would allow arrays of these types to now be initialized
    by UTF-8 string literals.
  - JeanHeyd acknowledged this would be the case and is consistent with C++11 through C++17.
  - Hubert presented a backward compatibilty concern involving overload resolution and
    initialization of parameters of aggregate type using list initialization syntax; the
    following example is well-formed in C++20, but would become ill-formed with the proposed
    change.

        struct A { char8_t s[5]; };
        struct B { char s[5]; };
        void f(A);
        void f(B);
        void foo() {
          f({u8"text"}); // Resolves to f(A) in C++20, ambiguous with the proposed changes.
        }

  - PBrett observed that the overload resolution issue currently exists with `signed char`
    and `unsigned char`.
  - Tom asked for confirmation that binding to a reference to an array would still be
    ill-formed.
  - JeanHeyd replied affirmatively.
  - Jens explained that there is an existing special case that permits initialization of
    arrays of `signed char` or `unsigned char` by an ordinary string literal.
  - PBrett summarized; the overload scenario already exists for `char`, `signed char`,
    and `unsigned char`.
  - Jens agreed and suggested adding an annex C entry with the above example to note the
    new ambiguity.
  - JeanHeyd reviewed the wording.
    - The value of the `__cpp_char8_t` feature test macro is updated.
    - The subsitution of "may" for "can" in \[dcl.init.string\] is a drive by fix done
      to maintain consistency with the other changes to the paragraph.
  - JeanHeyd noted that, with the changes, a program that passes a UTF-8 string literal
    as an argument for a function parameter of type `const char*` remains ill-formed.
  - JeanHeyd stated that the ability to initialize `char`-based arrays with a UTF-8
    string literal addresses constexpr concerns in a much simpler way than is presented
    in [P1423R3 (char8_t backward compatibility remediation)](https://wg21.link/p1423r3).
  - PBrett asked if any consideration was given for addressing these concerns with a
    core issue.
  - JeanHeyd replied that a core issue wouldn't be appropriate since the C++20 changes
    were deliberate.
  - Tom agreed and noted that this aspect of the C++20 changes was approved by EWG.
  - Jens agreed that a core issue is unlikely to be helpful, especially since a paper
    already exists.
  - Jens asserted that EWG should review and, as a DR, this can be considered after
    C++23 feature freeze.
  - Hubert observed that the backward compatibility impact to overload resolution can
    be avoided by limiting the allowance to variables of array type.
  - Jens agreed, but noted that would require more careful wordsmithing.
  - **Poll 2: Add an Annex C entry and discussion to D2513R1, and forward the published
    paper as revised to EWG as a defect report.**
    - Attendance: 8 (one abstention)

      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   5 |   0 |   1 |   0 |
    - Strong consensus in favor.
    - A: Concerned about the different handling for pointers vs arrays; concerns
      increased as discussion continued.
  - Tom asked if anyone felt concern about the possibility of unintended initialization
    by a UTF-8 string literal as opposed to an ordinary string literal.
  - Victor expressed minor concern, but that the risk is low.
  - JeanHeyd noted that such unintended possibilities are already the case in C.
- Tom announced that the next telecon will be February 23rd.


# January 26th, 2022

## Agenda
- [P2286R6: Formatting Ranges](https://wg21.link/p2286r6)
  - Review proposed wording for new SG16 concerns and consistency with prior guidance.

## Meeting summary
- Attendees:
  - Charlie Barto
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Tom informed the group of tentative plans for a SSRG and SG16 joint telecon to discuss the
  security aspects of
  [P2528R0 (C++ Identifier Security using Unicode Standard Annex 39)](https://wg21.link/p2528r0)
  and asked for feedback or concerns about such a meeting.
- [P2286R6: Formatting Ranges](https://wg21.link/p2286r6):
  - Tom informed the group that Barry was unable to be in attendance but that we are ok to
    discuss the wording and gather feedback for him.
  - Victor explained that he had assisted with the wording related to escape handling, but that
    Barry authored the rest.
  - Jens stated that it is generally not advised to discuss a paper without the author present.
  - Tom acknowledged the guidance and reported that he had communicated with Barry and that Barry
    was content with Victor being present to discuss any issues that are raised.
  - Jens asked for confirmation that LEWG has already approved the design.
  - Victor responded that the paper is present in the currently active electronic polling cycle.
  - Victor shared the paper and reviewed the revision history.
  - Victor began reviewing the wording.
  - PBrett asked if the `formattable` concept has semantic constraints that cannot be expressed
    in the concept definition.
  - Victor replied that it does not.
  - Jens noted that, in section 5.1 of the paper, \[format.formattable\] paragraph 2 states the
    semantic requirements.
  - Zach asked if the concept has been implemented as specified.
  - Victor expressed uncertainty regarding the concept definition, but assured the group that the
    rest of the design has been implemented.
  - Mark asked, with regard to section 5.2, why '?' appears as a type.
  - Victor explained a requirement for mutual exclusivity.
  - PBrett asked if there is intent to standardize the use of '?' to enable a debug representation
    generally; e.g., for non-standard types.
  - Victor replied that doing so is outside the scope of the standard, but expressed support for
    that direction.
  - PBrett noted that the paper introduces a `set_debug_format()` member function and asked if it
    would be desirable to add generic support for invoking it.
  - Jens replied that the parser for the formatted type would presumably have to be responsible for
    recognizing the '?' character and invoking the member function.
  - Jens noted that calls to `set_debug_format()` must activate the debug format regardless of
    whether a '?' is present in the format string.
  - Jens suggested that adding generic facilities to support the '?' specifier would be ok, but
    probably best addressed by a different paper.
  - Hubert noted that, in the proposed wording for \[format.string.escaped\], subparagraph 2.4.1,
    that the "Other" ("C") value of `General_Category` is an abbreviation for a set of categories
    and requested that the wording specify the individual categories.
  - \[ Editor's note: The values for `General_Category` are specified in
    [table 12 of section 5.7.1 of Unicode 14 UAX#44](https://www.unicode.org/reports/tr44/tr44-28.html#General_Category_Values). \]
  - \[ Editor's note: The wording also refers to the `General_Category` value of "Separator" ("Z")
    that is likewise an abbreviation for a set of categories and should presumably be expanded
    as well. \]
  - Hubert noted that format stability cannot be guaranteed and that output will change when
    newer Unicode standards are adopted.
  - Tom asked for confirmation that stability will only be lacking for currently unassigned characters.
  - Steve replied that this should be further researched and noted that the "Unassigned" ("Cn")
    property is not stable.
  - Hubert noted that the wording does not address non-Unicode text and asked if `isprint()` and
    `iswprint()` should be used to identify non-printable characters in those cases.
  - Jens replied that doing so warrants further discussion.
  - Hubert pondered whether it would be preferable to map non-Unicode characters to Unicode and then
    proceed with using the Unicode character properties.
  - Tom noted that, for implementations that support user defined encodings, the implementation may
    not know how to map to Unicode.
  - Hubert noted that such user defined definitions must define categories to be used for `isprint()`
    and other character classification functions, but acknowledged that a mapping to Unicode may not
    be present.
  - PBrett stated that \[format.string.escaped\] paragraph 2 does not state how to determine if the
    string to be escaped is in a Unicode encoding.
  - PBrett noted that he believes such wording to be present in the wording related to field width
    and suggested it may be desirable to generalize that and move it to a central location.
  - Steve asked if the determination might be locale dependent.
  - PBrett noted that previous guidance was that `std::format()` may be used for binary data and that
    any associated encoding is therefore tenuous.
  - Jens suggested that, in those cases, a programmer might be advised not to use the '?' formatting
    type.
  - Tom suggested it may be reasonable to, again, use the literal encoding as a proxy for the
    potentially locale dependent encoding.
  - Victor agreed.
  - Hubert stated that, for the non-Unicode case, determining printability would require either locale
    dependence or preservation of the compile-time literal encoding.
  - Charlie noted that, historically, the latter would have been difficult and that, for Microsoft,
    the active code page (ACP) was used in the past.
  - Hubert noted that, in a cross-compilation scenario, it is possible that the literal encoding is
    not a defined encoding for the target environment.
  - Tom suggested that, at some point, we will need to poll whether the non-Unicode behavior should
    be locale dependent or not.
  - Hubert expressed acceptance of non-locale dependent behavior for the non-Unicode case so long as
    there is no requirement to match the behavior for the Unicode case with regard to emitting hex
    vs UCN notation.  
  - Hubert noted that, if locale dependence is avoided, it will be necessary to assume an
    encoding for characters that are not consistently encoded for all locales; like '\\' in EBCDIC
    environments.
  - Hubert added that doing so might be ok if the choice is determined by the literal encoding.
  - PBrett suggested it may be useful to support opt-in to locale dependence via the 'L' modifier.
  - Victor stated that the 'L' modifier could be reserved for now.
  - Mark noted that the 'L' modifier is currently supported for character type.
  - Jens pointed out that the changes to \[format.formatter.spec\] paragraph 2 appear to indicate
    that a declaration of the `set_debug_format()` member function in any one of the specializations
    will affect all of them.
  - Victor agreed that this wording requires more work.
  - Mark asked when a formatter object for which `set_debug_format()` was called is reset or what
    happens when the '?' specifier is not applicable to the type.
  - Victor replied that it should be an error to specify mutually exclusive options or that the last
    option overrides prior ones but that further consideration is required.
  - Jens stated that the order of the interior bullets in \[format.string.escaped\] subparagraph
    2.2 need to be revised to address two issues:
    1) The algorithm must process the contents of string `S` in order.
    2) `S` consists of a sequence of code units, not UCS scalar values.
  - Jens suggested trying to factor out the code unit and UCS scalar value cases to avoid the
    exceptions.
  - Charlie stated that the handling of invalid code unit sequences needs to be specified since
    recovery may not always be possible; failure to recover could result in output containing a long
    sequence of values in hex notation.
  - Jens acknowledged the scenario and agreed that the specification must be made clear about that.
  - Jens asked what "universal character name escape sequence" is intended to mean in
    \[format.string.escaped\] subparagraph 2.4.2 and noted that a definition does not exist for
    "universal character name" though one does exist for *universal-character-name*.
  - Jens noted that this wording probably should not refer to *universal-character-name* since it
    describes a grammar nonterminal and suggested replacing "its universal character name escape sequence"
    with "a sequence of scalar values".
  - PBrett agreed.
  - Steve pointed out that similar uses of grammar nonterminals appear in the wording.
  - Jens agreed and suggested that the various "escape sequence" uses should be replaced with
    "a sequence of scalar values in the form ...".
  - Jens pointed out a grammar issue in the first line of \[format.string.escaped]\ paragraph 3;
    "... is equivalent to the escaped string representation a string of `C` ...".
  - Hubert requested that a note be added to \[format.string.escaped\] paragraph 4 to indicate that
    behavior is not locale dependent but that the encoding may be informed by the literal encoding.
  - Jens reported that the expected output noted in the comment for example `s3` in
    \[format.string.escaped\] paragraph 4 is incorrect; there should be two ranges and therefore two
    sets of brackets.
  - Tom observed that the examples that follow \[format.string.escaped\] paragraph 4 depict the
    expected Unicode behavior, but appear to be part of paragraph 4 which is specific to non-Unicode
    behavior.
  - Victor agreed there is a presentation issue that needs to be addressed there.
  - Jens advised moving paragraphs 2 through 6 of \[format.range\] after the `range_formatter` class
    definition.
  - Victor noted that "exposition only" should appear in italics.
  - Mark asked why, in the last row of the table associated with \[format.range\] paragraph 6, "?s"
    is required as opposed to just "?".
  - PBrett stated that requiring "?s" is inconsistent with the string case where "?" can be specified
    by itself.
  - Victor explained that "s" indicates that a range is intended to be formatted as a string; "?s" is
    therefore needed to format the range as a string in debug mode.
  - PBrett pointed out the "this is equivalent to invoking set_brackets({}, {})" note in \[format.range\]
    paragraph 5 and asked if a programmer is permitted to make such a call.
  - Victor replied that the wording is intended for implementors.
  - PBrett asked if, when implementing a range formatter, whether it is required to implement member
    functions like `set_brackets()`.
  - Victor replied that LEWG had discussed this and that the member functions are intended to help
    avoid ABI issues.
  - Mark asked if `set_separator()` and `set_brackets()` should be restricted to characters and how
    characters outside the basic character set need to be handled in various scenarios such as
    applicability to estimated field width determination.
  - Victor replied that the functions accept strings as input.
  - Tom reviewed the list of previously discussed design points that were noted in the
    [email announcing the agenda for the telecon](https://lists.isocpp.org/sg16/2022/01/2956.php).
  - Tom noted the need for wording to address recovery from encoding errors.
  - Charlie stated that recovery should follow the processes described in the
    [WHATWG Encoding Standard](https://encoding.spec.whatwg.org).
  - \[ Editor's note: See
    [section 4.1, "Encoders and decoders"](https://encoding.spec.whatwg.org/#encoders-and-decoders). \]
  - Tom noted the need to ensure that `std::filesystem::path` is rejected as a formattable range.
  - Victor replied that it is rejected by the constraints on the `formatter` partial specialization
    specified in the \[format.syn\] updates; those constraints reject recursive ranges.
  - Victor suggested it might be helpful to add a note that `std::filesystem::path` is rejected there.
- Tom announced that the next telecon will be February 9th.


# January 12th, 2022

## Agenda
- [P2491R0: Text encodings follow-up](https://wg21.link/p2491r0)
  - Initial review.
- [P2498R0: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r0)
  - Initial review.

## Meeting summary
- Attendees:
  - Hubert Tong
  - Jens Maurer
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: We did not have quorum due to low attendance; as a result, no polls were taken. \]
- \[ Editor's note: Changes made in a draft of
     [P1885R9](https://wg21.link/p1885r9)
     were material to review of the papers on the agenda, so we first reviewed it. \]
- [P1885R9: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r9)
  - Jens stated that there is a procedural question related to the changes made in this revision; the
    new draft changes the design after electronic polling.
  - Tom replied that the changes were at least partially inspired by comments received on the proposal
    by electronic polling participants and were intended to increase consensus.
  - PBrett noted that the polled revision did not have the wording to mandate `CHAR_BIT == 8` due to a
    procedural error and asked whether that warranted follow up with LEWG.
  - PBrett asked what it means in practice for the wording to mandate `CHAR_BIT == 8`.
  - Jens replied that it requires a call to a function specified with that wording to be ill-formed if
    the requirement is violated.
  - Jens explained that implementors can conform with this requirement by defining such functions as
    deleted, implementing them as a function template with an appropriate `static_assert`, or similar.
  - PBrett asked for more details regarding implementation as a function template and whether the
    functions could simply not be declared at all.
  - Tom replied that a function template is ok because taking the address of a standard library function
    is not allowed; the standard just requires a call expression to be well-formed.
  - Hubert explained that the name must be declared due to interaction with name lookup.
  - Jens stated an implementation preference to define the function as deleted.
  - PBrett: noticed that the revision history simply stated "Wording fixes" with no details.
  - Tom volunteered to review the R8 and R9 revisions and to summarize the differences in the meeting
    summary.
  - \[ Editor's note: Tom did so; the wording differences identified include:
      - An additional `using enum id` declaration was added to the definition of `text_encoding`.
      - The `wide_literal()`, `wide_environment()`, and `wide_environment_is()` declarations were
        removed and wording that referred to them adjusted accordingly.
      - "character encoding" was changed to "character encoding scheme" in the paragraph following
        the note regarding how the names of `text_encoding::id` enumerators were derived from the
        IANA registry.
      - A paragraph describing invariants maintained by `text_encoding` was added.
      - Wording that introduced and used `SUBSTITUTE_UTF_ENCODING()` for mapping the bigendian and
        littleendian UTF-16 and UTF-32 schemes to their respective encoding forms was removed;
        related wording was adjusted accordingly.
      - Wording to mandate `CHAR_BIT == 8` was added throughout.

    \]
- [P2491R0: Text encodings follow-up](https://wg21.link/p2491r0)
  - Jens summarized the paper.
  - Jens stated that the changes in P1885R9 improve consistency with the IANA intent and P1885 usage.
  - Jens added that there is opportunity for specification improvements, but that they can be
    addressed during LWG review.
  - Tom noted that the wording plan described in the paper indicated intent to remove the
    requirement that `CHAR_BIT == 8`.
  - Jens confirmed, but expressed a lack of concern; that restriction can be removed if motivation
    to do so arises.
  - PBrett expressed a preference for explicit specification for how IANA octets are mapped to
    C++ code units.
  - Jens agreed, stated that can be done during LWG review, and expressed a preference for a
    normative sentence that maps an IANA octet to a `char` code unit.
  - Jens expressed a belief that relying on IANA for anything other than octets would be a mistake.
  - PBrett asked if Jens had an alternative to suggest.
  - Jens replied that he did not, but that such concerns usually arose during discussion of UTF-16
    and UTF-32.
  - Hubert stated that mapping to IANA in those cases is feasible, but noted that there are
    multiple possible mappings that may be platform dependent; particularly when the size of
    `char` is not 8 bits.
  - PBrett agreed, but noted that a particular mapping could be required for a conforming
    implementation.
  - Tom added that a non-conforming implementation would map to "other" in that case.
- [P2498R0: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r0)
  - PBrett introduced the proposal:
    - Character encoding repositories other than IANA exist.
    - The mapping to IANA should be explicit such that a mapping to another registry could be
      gracefully introduced in the future if motivation arises.
  - PBrett summarized the proposed changes:
    - Rename "id" to "iana_id"
    - Rename "mib" to "iana_mib"
    - Add recommended practice to avoid implementations creating an over dependence on IANA.
  - PBrett asked for opinions on the proposed renames.
  - Victor asked if other viable candidate registries exist in practice and stated that, if not,
    the proposed renames seem premature.
  - PBrett replied that there are NB concerns about IANA being an unregulated, unaccountable,
    and unreliable organization.
  - PBrett added that examples of other registries can be found in
    the [WhatWG Encoding Standard](https://encoding.spec.whatwg.org),
    IBM's [Character Data Representation Architecture (CDRA)](https://www.ibm.com/downloads/cas/G01BQVRV),
    and [ISO/IEC 2022:1994](https://www.iso.org/standard/22747.html).
  - PBrett noted that the paper does not propose the addition of another registry; just the
    possibility to add more in the future in a seamless manner.
  - Jens suggested adding examples of other registries to the paper.
  - PBrett responded with concern that doing so might create disruption for the advancement of
    P1885 and result in considerable time spent debating whether the merits of each such
    repository warrant their being mentioned.
  - Steve asked for confirmation that, assuming an additional registry, that a single text
    encoding ID is still needed.
  - PBrett responded that the IANA ID is an enum class and that, in principle, multiple such
    classes are possible.
  - Steve stated that renaming `mib()` to `iana_mib()` results in the feature no longer being generic.
  - Jens agreed.
  - PBrett responded that code written for P1885 today that consults `mib()` is necessarily concerned
    with IANA specifically.
  - Steve asked what function a generic library should call then.
  - Jens replied that, if the IANA ID is desired, then call `mib()`.
  - Tom noted that, since multiple encodings may map to IANA's "other", reliance on `mib()` to uniquely
    identify an encoding is not possible.
  - Hubert opined that the proposed renames are fine, but that extension to other registries might
    require different terminology.
  - Jens offered examples such as "unique ID" and "UUID".
  - Jens opined that it doesn't hurt to add "iana" to make the terminology association explicit.
  - Hubert agreed.
  - Hubert stated that, for wide encodings, there are some registries that are somewhat suitable;
    in CDRA, wide encodings aren't explicitly represented as they constitute a composition of a
    character set and an encoding.
  - PBrett acknowledged and noted that the proposal is intended to clear design space for extension
    for such cases.
  - Tom provided some arguments in favor of support for multiple registries:
    - As previously noted, the IANA specification is goverened by an organization that some have
      concerns about.
    - The IANA registry is poor from a quality of specification perspective.
    - The IANA registry is missing entries that are found in other registries.
    - The same name is sometimes used by different registries to refer to differenc encodings.
    - Other registries are arguably more suitable for some environments; e.g., CDRA for IBM
      environments.
  - Tom suggested that the proposal replace the P1885 proposed exposition only data members with
    post conditions on the default constructor to require `iana_mib()` and `name()` to return
    `id::other` and an empty string respectively; this is to avoid encouraging implementations to
    simply store an IANA ID.
  - PBrett noted that much of the current wording is in terms of the `mib_` exposition only data
    member.
  - Tom replied that those can be changed to `mib()`.
  - Jens pointed out that the following text from the proposed wording creates the impression that
    the specified feature provides a remote API interface.
    - "\[text.encoding\] describes an interface for accessing the IANA Character Sets registry".
  - Jens stated that `text_encoding` currently containes a list of all encodings in the IANA
    registry and that this proposal makes the `text_encoding` class more of a first class entity
    for which mapping to other registries is ancillary functionality.
  - Jens opined that this direction suggests the need to create our own encoding registry since the
    functionality effectively defines one.
  - Jens stated that such a change constitutes a change in direction that is more significant than
    the proposed renames suggest.
  - PBrett acknowledged that the proposal makes the design more abstract in a manner similar to how
    Unicode specifies abstract characters.
  - PBrett added that he could imagine a C++ appendix that lists the encodings, but that would then
    necessitate defining them.
  - Jens stated that a registration service could be established, but did not advise doing so.
  - Jens observed that discussion has not yet reached the bottom of how encodings would be mapped
    between encodings registered with different registries.
  - Jens suggested the possibility of defining an `iana_text_encoding` class and later adding an
    `iso_text_encoding` class or similar for other registries if warranted.
  - Hubert observed that the P1885 design contains the same mapping problem since it presents a
    single domain, but doesn't adhere solely to that domain.
  - Hubert suggested the possibility of a `text_encoding` class template parameterized by a
    registry identifier.
  - Tom noted that, if one were to map the encodings present in the
    [ICU converter explorer](https://icu4c-demos.unicode.org/icu-bin/convexp),
    then parameterization by registry is necessary due to conflicting use of the same name for
    different encodings.
  - \[ Editor's note: For example, "korean" maps to "windows-949-2000" via the "Windows"
    provider, but to "ibm-1363_P11B-1998" via the "IANA" provider. \]
  - PBrett reiterated the intent of this proposal; to remove complete dependency on IANA.
  - Tom stated that the proposed change is consistent with the P1885 direction given that comparison
    is dependent on name when an encoding maps to IANA's "other".
  - Tom opined that there is no need to specify a mapping between repositories in the standard;
    the mapping can be implementation-defined.
  - Jens agreed that leaving the mapping implementation-defined is possible but felt an obligation
    to specify the mapping.
  - Hubert noted that, for implementors, the concern is what is in the interest of their users.
  - PBrett expressed a belief that creation of a character encoding registry service would be outside
    the scope of WG21 work, but that he would be willing to assist with such an effort outside of WG21.
  - Jens agreed and noted that such a service would essentially be attending to graves.
  - Hubert suggested that `text_encoding` may be more appropriate as a concept.
  - Tom stated that distinct classes or class template specializations for each registry would create
    friction at interface boundaries.
  - Hubert responded that a type erased interface could still be specified.
  - PBrett expressed being open to other suggestions.
  - Jens suggested renaming the current `text_encoding` class to `iana_text_encoding` and, if
    motivation arises for another registry, then a new class can be added.
  - General discussion ensued regarding the ramification of distinct classes.
  - Tom pondered what name would be returned by `name()` if multiple registries are supported.
  - PBrett responded that his proposal intended to avoid that question.
- Tom stated that the next telecon will be held on 2022-01-26 and that the agenda will include:
  - [P2286R5 (formatting ranges)](https://wg21.link/p2286r5),
  - the LWG issues concerning `std::format` fill characters, and/or
  - a new revision of
    [P2498 (Forward compatibility of text_encoding with additional encoding registries)](https://wg21.link/p2498).


# Meetings held in 2021

Meeting summaries for meetings held during 2021 are available at
- https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md
