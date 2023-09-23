# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, September 27th, 2023, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20230927T193000&p1=1440&p2=tz_pt&p3=tz_mt&p4=tz_ct&p5=tz_et&p6=tz_cest)).

Draft agenda:
- [P1729R2: Text Parsing](https://wg21.link/p1729r2):
  - Initial review.
- [P2728R6: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r6):
  - Continue review.


# Past SG16 meetings
- [September 13th, 2023](#september-13th-2023)
- [August 23rd, 2023](#august-23rd-2023)
- [July 26th, 2023](#july-26th-2023)
- [July 12th, 2023](#july-12th-2023)
- [June 7th, 2023](#june-7th-2023)
- [May 24th, 2023](#may-24th-2023)
- [May 10th, 2023](#may-10th-2023)
- [April 26th, 2023](#april-26th-2023)
- [April 12th, 2023](#april-12th-2023)
- [March 22nd, 2023](#march-22nd-2023)
- [March 8th, 2023](#march-8th-2023)
- [February 22nd, 2023](#february-22nd-2023)
- [February 1st, 2023](#february-1st-2023)
- [January 25th, 2023](#january-25th-2023)
- [January 11th, 2023](#january-11th-2023)
- [Meetings held in 2022](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# September 13th, 2023

## Agenda
- [P2845R3: Formatting of std::filesystem::path](https://wg21.link/p2845r3):
  - Continue review.
- [P2728R6: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r6):
  - Continue review.

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Nathan Owen
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2845R3: Formatting of std::filesystem::path](https://wg21.link/p2845r3):
  - \[ Editor's note: D2845R3 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2845R3 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Tom noted that SG16 previously reviewed P2845R0 and that the current revision addresses
    prior review feedback.
  - Victor provided an introduction:
    - The recent revisions correct some minor mistakes.
    - The proposed default format now produces a non-quoted non-escaped representation.
    - If the format specifier includes the `?` option, then a quoted escaped representation is produced.
    - The
      [{fmt} library](https://github.com/fmtlib/fmt)
      had previously implemented the behavior proposed in P2845R0 but was recently changed to implement
      the behavior introduced in P2845R2; this was a breaking change that impacted a few users.
  - Eddie pointed out an incorrect word choice in section 6, Proposal; "loose" is used where "lose" is
    intended.
  - Victor stated that the output shown for the first lone surrogate example in section 6, Proposal,
    might be incorrect and that he needs to check if a `\x` escape should be produced instead of the
    `\u` escape currently presented; the intent is for the behavior to match what is specified in
    [\[format.string.escaped\]](https://eel.is/c++draft/format.string.escaped).
  - **Poll 1: Forward P2845R2, Formatting of std::filesystem::path, to LEWG with a recommended target of C++26.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   5 |   2 |   1 |   0 |   0 |
    - Strong consensus.
- [P2728R6: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r6):
  - Tom reminded the group that our purpose as a study group is to assist paper authors in producing a
    proposal that has the best possible chance of passing review in other groups and, ultimately, an
    adoption poll in a plenary session.
  - Tom stressed that questions asked during discussion likely reflect some lack of clarity in the paper
    and should therefore inspire additional edits, not just immediate responses.
  - Tom listed the topics for discussion as presented in the
    [previously communicated agenda](https://lists.isocpp.org/sg16/2023/09/3955.php):
    - Continued review of error handling.
    - Opportunities for simplification; whether `std::uc::format` is still needed.
    - How the proposed features fit with the bigger picture and vision for future library proposals.
  - Zach summarized some other recent reviews:
    - SG9 has reviewed the paper three times and plans to review it at least one more time.
    - SG9 has provided some feedback that has not yet been incorporated in the paper.
  - Zach provided an overview of the proposed error handling:
    - The error handler receives an unspecified diagnostic message that programmers can use as
      they please.
    - The default error handler ignores the diagnostic message and returns a replacement character.
  - Zach stated that the error handling approach used in JeanHeyd's work doesn't fit into the
    iterator model.
  - Zach said he does not have strong opinions about the error handler and suggested it could be
    removed for now and added back later if needed.
  - Steve noted that transliteration is a use case for error handlers that allow multiple characters
    to be substituted for a non-translateable character.
  - Steve acknowledged that support for multi-character substitution would require a buffer that
    would make iterators larger and more complicated.
  - Corentin expressed confusion regarding the transliteration example since the proposed
    functionality is specific to UTF encodings.
  - Corentin suggested implementing transliteration as a layered view adapter.
  - Corentin stated that there are few good options beyond a single replacement character approach
    and that this approach is conforming, implementable, and useful.
  - Victor observed that the error handling interface treats all errors the same and that there is
    no distinction between different kinds of errors.
  - Zach responded that there are a fixed number of error possibilities and that a set of error
    codes would be isomorphic to the set of messages that are passed in the reference implementation.
  - Tom asked Zach if he has a strong preference.
  - Zach replied that his preference is to just substitute a replacement character and otherwise
    ignore any errors.
  - Tom expressed a belief that there are other reasonable error handling possibilities, but that
    a concrete proposal should be offered before trying to engage further on such discussion.
  - Jens noted that passing an error message creates an internationalization concern and expressed
    a preference against a message based interface.
  - Jens pondered the plausible options for reacting to an error:
    - The substitution approach is easily understood and Unicode provides a recommendation for how
      to perform them.
    - Throwing an exception is easily understood and works with ranges and iterators.
    - Since the error handler is not given access to the ill-formed code unit sequence, there is
      little context for doing anything else useful.
  - Zach indicated that he would be fine with replacing the `std::string_view` parameter with an
    enumeration.
  - Zach noted that substitution of a different replacement character would not be inline with
    Unicode recommendations.
  - Jens stated that there is no universal right answer for error handling for all programs;
    throwing an exception could be the right choice for one while aborting could be the right
    choice for another.
  - Zach suggested that `utf_iterator` could be used to single step through the input and noted
    that it provides access to the underlying sequence.
  - Zach stated that trying to provide a tool that handles every situation seems unnecessary.
  - Jens asked if the paper has an example that demonstrates single stepping through an input
    sequence with access to the underlying code unit sequence.
  - Tom commented that such an example would be a great addition to the paper.
  - Zach asked for a poll to remove the error handler.
  - Steve seconded Jens' preference to not use a stringly-typed error message.
  - Steve expressed tenuous consent for removal of the error handler based on the discussion.
  - Steve summarized the design requirements; there is one error handling mode that we want
    for sure, and a few others that we might want rarely.
  - Steve expressed a desire for more examples in the paper.
  - Corentin stated that views are not designed for error handling; they are designed for
    composition.
  - Corentin outlined a design approach for a different feature; a view that iterates over
    ill-formed code unit sequences.
  - Corentin pondered which replacement policy should be used.
  - Zach replied that Unicode specifies the recommended replacement policy.
  - Jens requested that the paper explicitly reference that policy.
  - Zach responded that it already does.
  - \[ Editor's note: section 5.4, "Add the transcoding iterator template", has a paragraph
    that states:
      > The number and position of the error handler invocations should use the
      > “substitution of maximal subparts” approach described in Chapter 3 of the
      > Unicode standard.
    \]
  - Hubert asked if formal wording is available.
  - Zach replied that there is some pseudo wording, but no real wording yet.
  - Eddie observed that removal of the error handling interface would require use of a for
    statement for even minimal error handling.
  - Eddie posited a use case that requires counting the number of errors encountered and
    noted that it could be implemented using the proposed design with the caveat that it
    would require global state since error handler objects are not persistent.
  - Zach acknowledged such use cases, but characterized them as examples of corner cases
    that are not frequently needed.
  - Hubert stated that he does not see a reason to prohibit the easy error handling cases
    and opined that removal of the error handler would be an over reaction.
  - Tom noted that the error handler is stateless; an object of the error handler is
    constructed on demand for each error and since the error handler is not passed details
    of the error encountered, error handling is severely constrained.
  - Jens charaterized the lack of persistence of an error handling object as a design
    defect; global state should not be required for Eddie's example.
  - Zach stated that the discussion has made it clear that we don't have a good grasp of
    the design that we want.
  - Corentin pondered how error handling in the middle of a lazy algorithm should be
    performed and suggested that may be a question for SG9.
  - Corentin stated that there are currently no standard views that throw.
  - Corentin suggested that views might not be the appropriate utility to use to sanitize
    input.
  - Corentin noted that a requirement to maintain state might make it difficult to
    match range complexity requirements.
  - Corentin advised using a view that operates on code units to analyze code units.
  - Zach agreed with Corentin's comments and stated that the proposal does not support
    custom error handling for views for exactly those reasons.
  - Tom suggested meeting with SG9 to discuss error handling in range pipelines.
  - Zach agreed to do so.
  - Eddie noted that exceptions are the only way to alter the control flow in range
    pipelines.
  - Tom agreed and stated that iterator operations don't provide an option other than
    throwing exceptions.
  - Eddie indicated that those limitations make him less inclined to support custom
    error handling.
  - Jens acknowledged that existing standard views might not throw exceptions directly,
    but noted that views that accept a callable, like `std::ranges::transform_view`
    allow an exception to be conditionally thrown based on the input in order to break
    the pipeline processing.
  - Jens concurred with having SG9 weigh in and perhaps poll error handling for ranges.
  - Jens requested an example of how error checking and handling could be performed
    using the proposed iterators in a for statement so that he could better determine
    how programmers could provide their own exception throwing view.
  - Zach provided an example in the chat.
    ```c++
    auto v = my_view();
    for (auto it = v.begin(); it != v.end(); ++it) {
      if (is_replacement_character(*it)) ...
    }
    ```
  - Jens pointed out that the example doesn't differentiate between a substitution
    character in the input vs a substitution made due to an ill-formed code unit
    sequence.
  - Zach replied that doing so would require inspecting and comparing code units.
  - Hubert opined that we don't have a great story here if we're going to be telling
    programmers to figure this out themselves.
  - Zach suggested that we don't have a good understanding of the needs right now, but
    stated improvements can be made later.
  - Tom expressed skepticism that error handling could be added later since the addition
    of a template parameter, even one with a default argument, would break passing
    these class templates as template template parameters.
  - Jens expressed a belief that the standard reserves the right to make such additions.
  - Zach agreed that such changes would constitute an ABI break.
  - Hubert agreed that it seems that we don't know exactly what we want.
  - Jens expressed skepticism that there aren't compelling use cases for custom error
    handling and suggested that a more complete design that addresses those use cases
    might subsume the use cases met with what is proposed.
  - Jens stated that his personal approach is to never accept bad data provided via a
    network since bad data can lead to security vulnerabilities.
  - Zach suggested that a good solution might be to wrap the for statement that single
    steps the character decoding in a convenient interface for users.
  - Tom advised that we not poll this topic for now and that we move on to other topics
    such as whether the `std::uc::format' enumeration is still needed.
  - Zach stated the enumeration is no longer needed and can be removed.
  - Zach backtracked slightly and stated that he needs to implement that removal to
    confirm that is the case.
  - Jens noted that the enumeration is isomorphic to the three UTF code unit types.
  - Tom directed the discussion towards another topic; how the proposed functionality
    fits in with other features we expect to provide in the future.
  - Corentin stated that the requirements are different with respect to JeanHeyd's work on
    [ztd.text](https://github.com/soasis/text) and
    [P1629 (Transcoding the 🌐 - Standard Text Encoding)](https://wg21.link/p1629).
  - Corentin noted that Zack's proposed features are suitable for freestanding and can
    therefore run on a toaster; that isn't the case for JeanHeyd's work.
  - Corentin expressed support for having multiple solutions, particularly since JeanHeyd's
    work cannot reasonably be implemented to work with the same constraints.
  - Jens recalled that JeanHeyd's work is targeting WG14 and C interfaces.
  - Tom replied that JeanHeyd has proposals targeting both WG14 and WG21 and that the WG14
    proposal provides low level functionality needed for his WG21 proposal.
  - \[ Editor's note: JeanHeyd's related proposal for WG14 is
    [N3095 (Restartable Functions for Efficient Character Conversion, r11)](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3095.htm).
    \]
  - Jens observed that Zach's proposal is limited to support for the well-defined UTF
    encodings and avoids the complications of table lookups and such that come with
    support for arbitrary encodings.
  - Tom asked Zach to confirm that there is no known reason that his proposal should not be
    implementable for freestanding implementations.
  - Zach confirmed.
  - Jens noted that there are no system calls involved.
  - Zach reported that he spent time looking at how ztd.text is implemented and how the
    features could be integrated and that, the more he discussed with Tim Song, the more it
    looked like integration just wasn't feasible.
  - Zach stated that his proposal implements lazy algorithms where as JeanHeyd's work
    implements eager transformations that can optimize based on knowledge of the destination.
  - Zach said he could not find a reasonable way to make these compatible or to implement one
    in terms of the other.
  - Tom claimed it is ok if these features are complementary without being integrated.
- Tom stated that the next meeting is scheduled for 2023-09-27 and that the anticipated agenda
  will include an initial review of
  [P1729R2 (Text Parsing)](https://wg21.link/p1729r2).
- Tom asked for opinions regarding what else should be discussed before we're ready to poll
  forwarding this paper.
- Corentin replied that we could work on improving the presentation in the paper for LEWG.
- Corentin noted that LEWG is likely to return the paper to SG16 for any Unicode questions
  not answered in the paper.
- Hubert suggested that LEWG review the design before substantial effort is expended on
  formal wording.


# August 23rd, 2023

## Agenda
- [P2909R0: Dude, where’s my char?](https://wg21.link/p2909r0).
- [P2728R6: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r6).

## Meeting summary
- Attendees:
  - Fraser Gordon
  - Hubert Tong
  - Mark de Wever
  - Peter Brett
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2909R0: Dude, where’s my char?](https://wg21.link/p2909r0):
  - Much appreciation was expressed for the clever paper title.
  - \[ Editor's note: in later revisions, the R0 title was demoted to a sub-title and a new title introduced;
    "Fix formatting of code units as integers". \]
  - Victor introduced the paper:
    - When `std::format()` was introduced, non-portable behavior due to the implementation-defined signedness
      of 'char' was not intended.
    - It is possible that some users expect the signedness to be reflected in the output, but most users that
      are formatting character types as integers are intending to expose bit patterns.
    - This is technically a breaking change.
    - This is more LEWG territory, but since it is text related, it seemed prudent to collect input from SG16.
  - PBrett requested that section 2, "Proposal", be expanded to illustrate the before/after effects for each
    of the type options.
  - Victor agreed to do so.
  - Victor explained that the change increases compatibility with `std::printf()` for the impacted type options
    other than "d"; the "%d" `std::printf()` conversion specifier always treats its argument as a signed type,
    but the proposed change for the "d" type option will always treat `char` as an unsigned type regardless of
    whether it is signed.
  - Zach expressed appreciation for symmetry and that the change improves support for portable roundtripping
    behavior.
  - Mark acknowledged that the change is a breaking change and asked if the intent is to handle this as a DR.
  - Victor replied that LEWG will decide that and that he would recommend handling this as a DR.
  - Mark observed the lack of a feature test macro.
  - Victor stated that he could add one.
  - Hubert requested that a more descriptive title be used for the paper.
  - Hubert noted that it is implementation-defined whether `wchar_t` is a signed type as well.
  - Victor replied that it would be reasonable to treat all `charT` types as being unsigned.
  - PBrett requested that the paper be updated to explicitly mention `wchar_t` as well.
  - Hubert expressed some concerns over the proposed change; `char` and `wchar_t` do have a signedness and it
    isn't good for programmers to ignore that.
  - Victor replied that, for `wchar_t` at least, the concern is not as strong since programmers don't tend to
    use `wchar_t` as an integer type as is done with `char`.
  - Hubert suggested it might make sense for the "d" type option to maintain signedness.
  - Victor stated a preference for the signedness handling being consistent across the type options.
  - Tom noted that `int8_t` could be implemented in terms of `char`.
  - Hubert noted that most of the changes increase consistency with `std::printf()` and stated the improved
    consistency should be extended to all of the integer types.
  - PBrett reminded the group that `char` is a distinct type from `signed char` and `unsigned char`.
  - Zach asserted that it is surprising to get a negative value for a `char` type and stated that negative
    `char` values are a wart in the language.
  - Hubert noted that
    [\[basic.fundamental\]p11](https://eel.is/c++draft/basic.fundamental#11) specifies that `char` is an
    integer type.
  - PBrett asked if an LWG issue should be raised regarding whether `int8_t` can use `char` as its
    designated type.
  - Fraser responded that cv-qualified types are also integer types and might therefore possibly be used
    as the designated type unless the `int8_t` wording excludes them.
  - Hubert noted that cv-qualified types being integer types was a recent CWG change.
  - PBrett reported that
    [\[cstdint.syn\]](https://eel.is/c++draft/cstdint.syn)
    specifies that `int8_t` must designate a signed integer type and that
    [\[basic.fundamental\]p1](https://eel.is/c++draft/basic.fundamental#1)
    doesn't include `char` in its definition of *signed integer types*.
  - PBrett stated that we will file a LWG issue to clarify this.
  - Tom asked for confirmation of the behavior for integer types other than `char` when used with the
    "o", "x", and "X" type options.
  - Victor replied that negative values may be produced.
  - Hubert stated that includes `wchar_t` when it is a signed type.
  - Tom noted that is consistent with the status quo wording.
  - Hubert noted that the wording is applicable to `charT`, but not to mixed character types.
  - **Poll 1: Modify P2909R0 "Dude, where's my char‽" to maintain semi-consistency with printf
    such that the 'b', 'B', 'o', 'x', and 'X' conversions convert all integer types as unsigned.**
    - Attendees: 8 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   2 |   0 |   2 |   2 |
    - No consensus.
    - SA: I'm not opposed to that direction in principle, but it is a deeper change and needs more
      research.
    - A: I'm concerned about the lack of implementation experience.
  - **Poll 2: Modify P2909R0 "Dude, where's my char‽" to remove the change to handling of the
    'd' specifier.**
    - Attendees: 8 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   1 |   2 |   1 |   1 |
    - No consensus.
    - SA: That would add a corner case to a corner case; this is more LEWG territory and will get
      discussed there.
  - **Poll 3: Forward P2909R0 "Dude, where's my char‽", amended with a descriptive title, an
    expanded before/after table, and fixed CharT wording, to LEWG with the recommendation to adopt
    it as a Defect Report.**
    - Attendees: 8 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   2 |   2 |   1 |   0 |
    - Weak consensus.
  - Tom asked if there are any concerns beyond the `std::printf()` inconsistencies that would
    motivate the N and A voters towards F/SF.
  - No other concerns were raised.
  - Hubert expressed unhappiness with the "d" type option direction since it won't provide help to
    those debugging issues related to `char` being a signed type.
- [P2728R6: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r6):
  - Zach introduced the changes made in recent revisions:
    - The type unpacking mechanism was reworked.
    - The `null_sentinel_t` type was moved to the `std` namespace.
    - A `std::ranges::project_view` was introduced bsaed on SG9 (Ranges) feedback though this view
      is likely to be replaced in a future revision with a conditionally borrowed `transform_view`.
    - The `utfN_view`s are now just aliases of a `utf_view` class template specialization.
  - PBrett asked if anyone has new SG16 concerns inspired by the changes since R3.
  - \[ Editor's note: SG16's last review of this paper was
    [P2728R3](https://wg21.link/p2728r3)
    during the
    [2023-05-10 SG16 meeting](https://github.com/sg16-unicode/sg16-meetings#may-10th-2023). \]
  - No new concerns were raised.
  - Tom asked for specific ideas on how to improve presentation in the motivation section of the
    paper to address any lingering concerns from reviews of previous revisions.
  - PBrett stated that the paper has improved significantly from previous revisions
  - PBrett volunteered to meet with Zach offline to more thoroughtly review that section.
  - Fraser asked whether support for the `approximately_sized_range` concept proposed by
    [P2846 (`size_hint`: Eagerly reserving memory for not-quite-sized lazy ranges)](https://wg21.link/p2846)
    has been considered.
  - Zach replied that he has to some extent and noted that there are range limits that could be imposed
    and that might work with that feature.
  - Fraser asked if the proposal could be retrofitted to support that feature as it progresses through
    the committee.
  - Zach replied affirmatively and explained that the `size_hint()` member could be conditionally
    enabled when size information is available.
  - Hubert requested clarification regarding the request for improvements to the motivation section.
  - Tom explained that he had received input from multiple people that they felt the motivation
    section was lacking.
  - PBrett explained that one of the perceived issues was the lack of rationale for the design decisions
    made and an analysis of alternatives considered; for example, during previous SG16 discussions, vague
    comments were sometimes made regarding the design being motivated by performance concerns, but the
    performance goals and concerns are not reflected in the paper.
  - PBrett repeated his earlier claim that recent revisions and the refined scope have improved the situation.
  - Hubert stated that it sounds like the motivation question might be resolved then.
  - Hubert suggested that a scope section could be added.
  - PBrett reported that, in a recent UK body discussion concerning the failure for some papers to attain
    consensus, observations were made that lack of a common understanding of the problem to be solved likely
    contributed to the failure.
  - PBrett opined that discussion of earlier revisions of the paper exhibited some confusion regarding which
    problems this paper is intended to address.
  - Zach stated that he has been working on prototypes that lead to this paper for about seven years now and
    that some of the design motivation is influenced by things he learned along the way, but that would
    require some reflection to recall.
  - Zach suggested that discussion move towards error handling as discussion of that topic was requested in
    the meeting agenda.
  - \[ Editor's note: Zach was referring to requests made on the SG16 mailing list. See
    https://lists.isocpp.org/sg16/2023/08/3930.php. \]
  - Robin added some background for the linked
    [PR-121 (Recommended Practice for Replacement Characters)](http://unicode.org/review/pr-121.html)
    policies. That policy paper was used to inform the recommendation made by the UTC during the
    [UTC 116 / L2 213 Joint Meeting held in Redmond, WA from August 11-15, 2008](https://www.unicode.org/L2/L2008/08253.htm)
    in which a
    [consensus to prefer policy 2](https://www.unicode.org/L2/L2008/08253.htm#116-C12)
    was established.
  - Zach reported having been unaware of PR-121 and that his design decisions were guided by what appears in
    the Unicode Standard.
  - Zach summarized the error handling options described by the Unicode Standard as:
    - terminate
    - report an error
    - substitute a replacement character.
  - \[ Editor's note: the Unicode 15 chapters that discuss handling of ill-formed code unit sequences are:
    - 3.9, Unicode Encoding Forms, U+FFFD Substitution of Maximal Subparts.
    - 5.22, U+FFFD Substitution in Conversion.
    \]
  - Zach stated that an option to just drop ill-formed code unit sequences seems misguided.
  - Robin agreed and stated that doing so can lead to security issues.
  - Zach stated that there are other options to identify encoding errors and that he does not want this
    feature to be made complicated.
  - PBrett asserted a need for a feature to just validate that a given string can be successfully decoded.
  - Zach responded that such a feature was in a previous revision of the paper, but that it was removed
    as part of reducing scope.
  - PBrett stated that he actually wants that feature more than he wants transcoding support so that
    input could be proactively rejected.
  - Tom expressed sympathy for Zach's perspective but stated a preference towards not providing an error
    handler at all over providing one that is unable to handle arbitrary complexity.
  - Zach replied that he really only cared to support terminate, throw, and substitute as recommended by
    the Unicode Standard.
  - Tom described the error handling approach that JeanHeyd developed for his work on
    [P1629 (Standard Text Encoding)](https://wg21.link/p1629); it allows for the current iterator to be
    moved to an error handler that manipulates it as necessary and then moves it back; this provides the
    error handler full autonomy.
  - Zach replied that such an approach doesn't work for a transcoding iterator since exactly one output
    code unit must be produced; or would otherwise require a buffer to be persisted and referenced for
    later outputs.
  - Tom expressed gratitude for that response and reported that he had not considered the limitations
    of lazily transcoding within iterator operations.
  - PBrett provided a brief introduction to the
    [ztd.text](https://github.com/soasis/text)
    error handlers.
  - \[ Editor's note: see the error handlers in the header files included by
    https://github.com/soasis/text/blob/main/include/ztd/text/error_handler.hpp. \]
  - Zach noted that each iterator dereference has to produce the next code unit value and that makes it
    expensive to support anything other than substitution of a single code point.
  - PBrett asked if more design space options are opened by considering views rather than iterators.
  - Zach replied that the iterators are stateful in either case.
  - Zach stated that he would be ok with dropping the error handler in favor of only doing substitution
    and noted that the error handler can only be specified when the iterators are used directly; the
    views don't support providing an error handler.
  - Tom asked Hubert if his previously expressed interest in exposing the type unpacking behavior has
    been satisfied.
  - Hubert did not recall his previous interest.
  - Tom explained his recollection; that Hubert wanted to be able to take advantage of the unpacking
    behavior when writing adapters to be used in range pipelines.
  - Zach stated that the concepts in the paper might need to be refined a bit but that he has a test
    that does that.
  - Tom requested that an example be added to the paper.
  - Hubert suggested that the motivation section be updated to explain that functionality as well.
- Tom reported that the next meeting will be 2023-09-13 and that likely agenda items include continued
  review of P2728R6 and initial review of
  [P1729R2 (Text Parsing)](https://wg21.link/p1729r2).


# July 26th, 2023

## Agenda
- [WG14 N3145: $ in Identifiers v2](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3145.pdf):
  - Determine whether a corresponding proposal for WG21 is desired.
- [P2811R7: Contract-Violation Handlers](https://wg21.link/p2811r7):
  - Discuss character encoding considerations for the `std::contracts::contract_violation::comment()`
    member function.
- [LWG 3944: Formatters converting sequences of char to sequences of wchar_t](https://wg21.link/lwg3944):
  - Continue review pending a proposed resolution or related paper.

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Eddie Nolan
  - Hubert Tong
  - Jens Maurer
  - Joshua Berne
  - Mark de Wever
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Ville Voutilainen
  - Zach Laine
- [WG14 N3145: $ in Identifiers v2](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3145.pdf):
  - Hubert introduced the topic.
    - C23 explicitly blessed `$` as an allowed character in identifiers as an implementation-defined extension.
    - C has traditionally allowed this extension and support for it is widely implemented.
    - [P2342 (For a Few Punctuators More)](https://wg21.link/p2342) contains additional analysis.
    - Up to and including C++20, this has been a conforming extension in C++ since `$` in an identifier would
      be ill-formed.
    - In C++20, `$` is a UCN and combines with adjacent identifier characters to produce an ill-formed identifier.
    - In C++23, `$` is no longer a UCN and adjacency with identifier characters now yields two pp-tokens, the
      second of which renders the program ill-formed.
    - In C++26, `$` is a member of the basic character set, adjacency with identifier characters continues to yield
      two pp-tokens, but the `$` token may be discarded such that it is never processed during translation phase 7.
  - PBrett asked for clarification of what constitutes a conforming extension.
  - Corentin observed that this extension requires the production of a single pp-token when `$` is adjacent to
    an identifier character.
  - Corentin stated that sanctioning this allowance in the standard would restrict evolution of the language
    since it would prevent use of `$` as an operator.
  - Steve noted that the status quo is that all implementations allow `$` in identifiers by default, `$` is
    widely used in identifiers, and `$` appears in mangled names.
  - Steve stated that compilers are free to issue a diagnostic and produce a working executable for source code
    that is ill-formed according to the standard.
  - Hubert replied that the concern is with preprocessing; if `$` is not explicitly allowed in an identifier by
    the preprocessor, then it is handled as a separate token and the difference is observable.
  - Hubert stated that issuing a diagnostic only during translation phase 7 would be difficult.
  - Hubert asserted that wording changes are in order to continue to permit existing practice with `$` in
    identifiers.
  - Hubert acknowledged concerns regarding how to word an allowance so that new uses of `$` are not restricted.
  - Hubert noted that new uses are only problematic if they are not surrounded by whitespace.
  - Jens suggested the possibility of reverting the adoption of
    [P258R2 (Add @, $, and ` to the basic character set)](https://wg21.link/p2558r2)
    for C++26.
  - PBrett expressed opposition to doing so since that would contradict the direction established in WG14
    and codified in C23.
  - PBrett stated that this discussion is a good start regarding how to move forward.
  - Jens opined that the WG14 rationale is not motivating and that he is therefore not motivated to follow
    the same direction in C++.
  - Tom noted that there are backward compatibility concerns for some platforms due to use of `$` in identifiers
    in system headers.
  - Corentin stated that the WG14 direction was to explicitly state that it is implementation-defined whether
    `$` is allowed in an identifier.
  - **Poll 1: Whether DOLLAR SIGN is accepted as an identifier start and/or identifier continuation character
    should be explictly implementation-defined.**
    - Attendees: 12 (4 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   2 |   1 |   2 |   2 |
    - No consensus.
    - SA: I don't think an identifier should be implementation-defined.
  - PBrett stated that the next step would be a proposal to EWG acknowledging the guidance here.
  - Tom asked for opinions regarding the default modes of current compilers being non-conforming.
  - Zach replied that all implementations offer an option to disable the extension.
  - PBrett stated that every implementation is non-conforming in their default modes in practice.
  - Corentin asserted that implementations should issue warnings for use of the extension.
- [P2811R7: Contract-Violation Handlers](https://wg21.link/p2811r7):
  - Joshua introduced the topic:
    - SG21 is working on a specification for a contract violation handler.
    - The proposed `comment()` member function of `std::contracts::contract_violation` is intended
      to return a string containing the source code of the violated contract predicate.
    - The proposed encoding for the returned string is the ordinary literal encoding.
  - Tom expressed support for use of the ordinary literal encoding.
  - Tom asked if anything should be specified regarding handling of characters that are not
    encodeable in the ordinary literal encoding.
  - Corentin agreed with use of the ordinary literal encoding on the basis that the text will be
    used at run-time.
  - Steve asked for confirmation that the feature effectively converts a source code snippet to text.
  - Joshua confirmed.
  - Steve suggested that a hand wavy approach similar to that taken for `static_assert` is likely
    necessary except that the string has to survive until run-time and we lack a mechanism to
    communicate the encoding.
  - Steve stated that the compiler should perform a best effort rendering in the target encoding
    with the understanding that, for example, an identifier might not be representable in Latin1.
  - Jens observed that is a different operation than stringizing.
  - Steve agreed.
  - Corentin asked what the anticipated use cases are for the `comment()` function.
  - Joshua replied that the primary use case is for logging; other use cases might involve using
    the result as a key for a map.
  - Joshua asserted that it is not intended to provide source code that a programmer might expect
    to parse.
  - Joshua stated that the output is only intended to be sufficient for a human to be able to
    correlate it with the original source code.
  - Zach ruminated on the interaction of source encoding and literal encoding and how preprocessor
    stringifying works.
  - Jens noted that the `assert` macro is similarly expected to embed source code in the output it
    produces.
  - Jens stated that the wording for `assert` does not capture the fact that producing the output
    involves multiple transcoding steps.
  - \[ Editor's note: the transcoding steps are the conversion from the encoding of the input file
    ([\[lex.phases\]p1](http://eel.is/c++draft/lex.phases#1.1))
    to the *translation character set*
    ([\[lex.charset\]p1](http://eel.is/c++draft/lex.charset#1))
    then to the *ordinary literal encoding*
    ([\[lex.charset\]p8](http://eel.is/c++draft/lex.charset#8))
    and then finally, if necessary, to the implementation-defined encoding used to write text to
    the standard error stream
    ([\[cassert.syn\]](http://eel.is/c++draft/cassert.syn) via reference to the C standard). \]
  - Jens observed that, for `comment()`, there is a possibility to differentiate these steps;
    the compiler performs the conversion to the ordinary literal encoding and the violation
    handler can then perform additional transcoding as necessary.
  - Jens asserted that these are not novel problems.
  - Jens observed that non-encodeable characters in string literals are ill-formed and that a
    preprocessor stringize operation that produces such a string would likewise be ill-formed.
  - Jens posited doing similarly for contracts.
  - Corentin stated that doing so makes sense and then described some additional encoding options:
    - UTF-8 in `char8_t`, though that doesn't improve usability.
    - implementation-defined.
    - ordinary literal encoding with an escaping mechanism for non-encodeable characters.
  - Corentin suggested it is likely best to just let implementors do what they think is best.
  - PBrett stated that SG21 had strong consensus for the text returned by `comment()` being
    implementation-defined.
  - PBrett noted that, since it is implementation-defined, there is no need to specify whether
    the content includes macro expanded text.
  - PBrett asserted that it is essential that the encoding be specified and expressed support
    for the current paper direction.
  - PBrett agreed that UTF-8 in `char8_t` is an option, but that the standard provides few
    facilities to consume it.
  - Hubert noted that, since C does not prohibit non-encodeable characters in string literals,
    the stringize operation suffices for `assert` in C.
  - Steve stated that it would be very suprising if a `char`-based string with an encoding
    other than the ordinary literal encoding was returned; a `char8_t`-based string should be
    used if a UTF-8 encoded string is always returned.
  - **Poll 2: The value of std::contract_violation::comment should be a null-terminated
    multi-byte string (NTMBS) in the string literal encoding.**
    - Attendees: 12 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   8 |   3 |   0 |   0 |   0 |
    - Unanimous consensus.
- [LWG 3944: Formatters converting sequences of char to sequences of wchar_t](https://wg21.link/lwg3944):
  - PBrett explained that the goal of discussing this issue is to determine if we agree with
    the proposed resolution.
  - Victor expressed support for it and stated that it is consistent with previous discussions.
  - Victor noted a minor markup issue in the proposed wording; the extent of the struck text should
    include the trailing `>` character.
  - **Poll 3: Recommend the proposed resolution to LWG3944 "Formatters converting sequences of char
    to sequences of wchar_t" to LWG, after fixing the typo.**
    - Attendees: 12
    - No objection to unanimous consent.
  - Mark asked what the next step is for this issue.
  - Tom advised sending the proposed resolution to the LWG chair and stated that he would work with the
    LWG chair to get a github issue filed to record the SG16 poll.
- Tom stated that the next meeting is scheduled for 2023-08-09.
- Zach indicated that he could have a revision of
  [P2728 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728)
  available by then.
- Victor reported that he has a a new revision of
  [P2845: Formatting of std::filesystem::path](https://wg21.link/p2845)
  available.


# July 12th, 2023

## Agenda
- [P1030R5: std::filesystem::path_view](https://wg21.link/p1030r5):
  - Discuss what to do in lieu of overloads with `std::locale` parameters.
- [P2845R0: Formatting of std::filesystem::path](https://wg21.link/p2845r0):
  - Continue review.
- [LWG 3944: Formatters converting sequences of char to sequences of wchar_t](https://wg21.link/lwg3944):
  - Initial review.

## Meeting summary
- Attendees:
  - Charlie Barto
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Nathan Owen
  - Niall Douglas
  - Peter Brett
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P1030R5: std::filesystem::path_view](https://wg21.link/p1030r5):
  - Niall stated that, during LEWG discussion in Varna, LEWG approved removal of `std::locale`
    function overloads that were added for compatibility with `std::filesystem::path`.
  - Niall noted that, for each overload set that has an overload with a `std::locale` parameter,
    there is an overload that does not.
  - PBrett asked for an explanation of the concerns with the overloads that work with
    `std::locale`.
  - Niall responded that locale support generally delegates conversion to the OS where they
    are handled efficiently, but conversions performed via `std::locale` impose considerable
    performance overhead; possibly including multiple conversions on some platforms.
  - \[ Editor's note: conversions controlled by `std::locale` require use of the `std::codecvt`
    facet which, per
    [\[fs.path.construct\]p6](http://eel.is/c++draft/filesystems#fs.path.construct-6),
    may require multiple conversions. \]
  - Niall stated that a replacement for `std::locale` would be welcome.
  - PBrett opined that, in his experience, treating paths as having an encoding leads to sadness.
  - PBrett stated that a lossy conversion to a definitive encoding can be used to display paths.
  - Niall noted that the proposed `path_view` supports a raw byte encoding and provides rendering
    operations.
  - PBrett asked if the facility provides features to produce a path suitable for display purposes.
  - Niall replied that such formatting falls more in the domain of
    [P2845 (Formatting of std::filesystem::path)](https://wg21.link/p2845)
    and that he has been in discussion with Victor.
  - PBrett asked if there is a plan to provide a formatter for `path_view`.
  - Niall suggested that such a formatter behave the same as for `std::filesystem::path`.
  - Victor summarized observations made during the LEWG discussion:
    - `std::locale` was present in `constexpr` overloads; that issue is easily solved by removing
      the `constexpr` specifier from those declarations.
    - the `std::locale` parameter is only present to support encoding conversions, but those
      conversions are better handled by an interface designed for such conversions.
  - Victor noted that `std::codecvt` is not an efficient method for transcoding.
  - Victor opined that the overloads with a `std::locale` parameter are not known to be needed and
    can be added back later, perhaps in a more restrictive form, if desired.
  - Niall asked Victor if he is suggesting that the existing `std::filesystem::path` overloads with
    a `std::locale` parameter should be deprecated.
  - Victor replied that he would be happy to write such a paper at some future point.
  - Tom asked why there is a `compare()` overload with a `std::locale` parameter.
  - Niall responded that comparisons are shallow by default and `compare()` is provided to allow
    for more comprehensive equivalence comparisons.
  - Niall explained that the `std::locale` parameter is used to convert each path to a common form
    that is then compared.
  - PBrett expressed an assumption that the `std::locale` parameter would be used for collation
    purposes using the `std::collate` facet.
  - Hubert asked why collation would be relevant for equality.
  - PBrett asked if, given a set of `path_view` objects, whether the `compare()` operation could
    be used to order them.
  - Zach responded that such collation might be better performed using features outside of the
    `std::filesystem` library.
  - Jens stated that the wording in the paper is suggestive that only the encoding is intended
    to be consumed from the locale object.
  - Jens observed that removal of the `std::locale` parameter results in a loss of transcoding
    facilities, but since what was provided was so thin, it isn't much of a loss.
  - Victor stated that the equivalent facility in `path_view` of the `std::locale` based
    `std::filesystem::path` construction is the locale dependent `render()` member function.
  - Niall explained that the reference implementation of the locale dependent `render()` member
    uses the `std::locale` object to convert a path to UTF-8 and then compares it.
  - Tom expressed confusion, stated that `std::locale` doesn't support conversion to UTF-8,
    and then realized the reference implementation is probably using the `char8_t` codecvt facets
    that don't actually convert between the locale encoding.
  - Niall responded that he is not aware of anyone that uses `std::locale` with the filesystem.
  - Victor pondered interaction with `std::format` and `std::print` and whether it would make
    sense for `path_view` to also rely on the literal encoding to detect UTF-8 encoding; that
    would enable construction with `char`-based data to be saved as `char8_t`.
  - Tom expressed some reservations; programmers might compile with a `/utf-8` or equivalent
    option, but file names produced or provided at run-time might be differently encoded.
  - Hubert expressed concerns regarding implementation experience obtained so far regarding
    preservation of the literal encoding for use by the standard library.
  - **Poll 1: Modify P1030R6 "std::filesystem::path_view" to restore function overloads with
    locale parameters.**
    - Attendees: 12 (4 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   0 |   2 |   4 |   2 |
    - Consensus against.
- [P2845R0: Formatting of std::filesystem::path](https://wg21.link/p2845r0):
  - Tom apologized for his delinquency in producing a meeting summary for the previous
    discussion on this paper that took place at the prior SG16 meeting.
  - Victor summarized his understanding of the direction from the prior meeting; to explore
    more options for quoting and escaping.
  - PBrett explained a desired ability to obtain a close approximation of a path validly encoded
    for display purposes and stated that the paper does not currently provide sufficient detail.
  - Victor asked for confirmation that Peter wants the path formatted without any transformation,
    no loss of information, no quoting, and perhaps just escaping for invalid code unit sequences.
  - PBrett explained that he wants three version:
    - one that provides the raw bytes; `path_view` provides that, but `std::filesystem::path`
      does not.
    - one that understands encoding and provides the path unmodified with the exception of
      substitution characters for invalid code unit sequences.
    - one with quotes and escape sequences for problematic characters.
  - Niall stated that, for both `std::filesystem::path` and `path_view`, it is possible to obtain
    the path as a string or to visit the components with a lambda.
  - Jens asked for confirmation that `std::format` includes a debug specifier that enables a
    string to be printed with escape sequences for problematic characters.
  - Victor confirmed that is the case and stated that it could be used for paths such that the
    default formatting provides the second option PBrett listed.
  - Jens asked what the output would be for the Belarusian example in the paper for arbitrary
    code pages used in practice.
  - Victor replied that, in either case, the same substitutions would be performed.
  - Jens expressed approval and noted that behavior would be consistent with choices previously
    made.
  - Mark observed that the options discussed so far, with an exception for the debug specifier,
    would retain newline characters.
  - PBrett acknowledged the behavior and noted that additional translations can be applied on
    the formatted result as needed; e.g., to substitute a space for the newline character.
  - Niall expressed frustration regarding rendering paths in quotes since quote characters are
    also valid path characters.
  - Tom acknowledged feeling similary frustrated by that.
  - PBrett stated that quotes would only be present when the debug specifier is used.
  - Niall pondered whether an additional format specifier to format the path with escape
    sequences but without quotes is warranted.
  - Tom responded that additional such options could be recognized by the `formatter`
    specialization.
  - Zach asked how control characters like RTL isolates should be handled; whether they should
    be ignored when formatting for display but preserved by the debug format.
  - PBrett replied that he doesn't have experience with those in path names but that he would
    expect them to be handled as a custom translation.
  - Zach suggested such characters should probably be passed through when formatting for display.
  - PBrett asked if the paper should be updated to address the `path_view` proposal.
  - Victor replied that `path_view` should be handled separately since there are additional
    complications for the byte case.
  - Tom stated that the consensus direction seems pretty clear for a paper revision.
- [LWG 3944: Formatters converting sequences of char to sequences of wchar_t](https://wg21.link/lwg3944):
  - Mark summarized the issue:
    - In C++20, it was an intentional design decision to not support formatting of `char`-based
      string arguments when formatting for `wchar_t`.
    - In C++23, such formatting was inadvertently added via support for range formatting since
      a range might have a `char` element type.
  - PBrett asked Mark what his preferred resolution is.
  - Mark replied with a preference to preserve formatting of individual characters of type
    `char` in general but to disable formatting of ranges with a `char` element type.
  - Mark noted that such range formatting probably wouldn't produce the intended result when
    the characters are, for example, individual UTF-8 code units.
  - PBrett expressed skepticism that the reported formatting was intentional.
  - Tom asked why a different conclusion is reached for formatting of an individual character
    vs an individual character in a range.
  - Hubert replied that a range of individual code units is more string-like.
  - Niall stated that, in principle, the range could be iterated to decode characters.
  - PBrett agreed but noted that doing so would require encoding information.
  - Niall acknowledged the requirement and noted it could be inferred for the `charN_t` types,
    but not for `char`.
  - Tom expressed a belief that support for the `charN_t` types is disabled.
  - Victor confirmed that is the case.
  - Hubert indicated that such conversions could be enabled, but that necessary facilities
    are not currently available at run-time; something like ICU or iconv would be needed.
  - PBrett suggested that an escape translation could be produced.
  - Hubert replied that stateful encodings would require representing state.
  - Tom asked what the downside is of disabling support for ranges that have a mismatched
    character type as the element type.
  - PBrett replied that, ideally, it should be possible to format everything.
  - Victor agreed with PBrett and stated that formatters for string-like types that have a
    mismatched character element type could be disabled and that a specifier to format a
    range as a string could be provided.
  - Hubert expressed support for a protocol to opt-in to support of string-like types.
  - Zach asked if `std::vector` would be considered a string-like type.
  - Zach expressed support for disabling formatting of ranges with a mismatched character
    element type.
  - Victor observed that disabling formatters for mismatched `std::string` and
    `std::string_view` would suffice to automatically disable types that derive from them.
  - Victor expressed support for distinguishing between string-like and non-string-like
    types.
  - Mark noted that support can always be added later for a disabled formatter and that
    disabling these formatters would be an improvement over the status quo.
  - PBrett agreed and asked Mark if he is willing to author a proposed resolution.
  - Mark agreed to do so.
  - \[ Editor's note: Mark offered a proposed resolution that is now reflected in the
    LWG issue. \]
- Tom announced that the next meeting will be 2023-07-26 and that the agenda will cover
  allowances for `$` in identifiers, encoding for the proposed
  `std::contracts::contract_violation::comment()` member function, and continued review of
  of Zach's UTF transcoding paper if a new revision becomes available.


# June 7th, 2023

## Agenda
- [P2779R1: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r1).
- [P2872R1: Remove wstring_convert From C++26](https://wg21.link/p2872r1).
- [P2845R0: Formatting of std::filesystem::path](https://wg21.link/p2845r0).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Charlie Barto
  - Corentin Jabot
  - Fraser Gordon
  - Giuseppe D'Angelo
  - Jens Maurer
  - Mark de Wever
  - Mark Zeren
  - Peter Brett
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2779R1: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r1).
  - \[ Editor's note: D2779R1 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2749R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Giuseppe summarized the paper and changes since the last revision:
    - The paper endeavors to identify a compromise position for the issues that have resulted in multiple
      changes to how the `std::basic_string_view` range constructor is specified.
    - Option 2 from the previous revision is still present though there was not much support for this
      option in the last discussion.
    - Option 1 follows existing precedent for type traits that enable some functionality; this option
      has been divided into two sub-options.
    - Option 1-A provides a type trait that enables conversion without regard to the `traits_type`
      member.
    - Option 1-B provides the type trait from option 1-A as well as an additional type trait that can be
      used to enable conversion that is sensitive to the `traits_type` member.
  - Tom asked if the intent is for the trait to be used only for conversion to `std::string_view` or for
    conversion to any string_view-like type.
  - Giuseppe responded that it is intended to be used for conversion to any string_view-like type.
  - Jens suggested in chat: "You can also define enable_string_view_conversion in a way so that the user
    specialization can compare char_traits, if so desired (or not)."
  - Jens' suggestion received several positive responses.
  - Alisdair, following up on Jens' suggestion in chat, asked if the traits in option 1-B could be
    merged.
  - Giuseppe confirmed that they could be.
  - Alisdair indicated that would be his preference.
  - Alisdair stated that the conversion could be enabled based on a class member similar to how transparent
    key comparison for associative containers is enabled via the `is_transparent` member of the compare class.
  - Giuseppe acknowledged that approach would work as well.
  - Tom noted that approach would require modifying the class.
  - Alisdair responded that the trait could still be specialized but could be defaulted based on the presence
    of a member.
  - Jens stated that the most convenient option would be to define a conversion operator with the trait
    available as a fallback.
  - Jens expressed a preference for a single trait with template parameters such that a specialization can
    be written to explicitly match `traits_type` or `std::char_traits` as desired.
  - Jens noted that `enable_string_view_conversion_with_traits` still requires comparison with
    `std::char_traits` or a `traits_type` member.
  - Jens suggested that third party string_view-like classes can provide their own trait to enable implicit
    conversions.
  - Giuseppe responded that the goal is to enable interconvertibility between different string types.
  - Giuseppe noted that the proposal doesn't require comparisons with specific type or member names.
  - Zach stated that he doesn't find the problem that the paper intends to address compelling and noted
    that `std::string_view` is available as a vocabulary type.
  - Zach noted that working around the lack of an implicit conversion just requires slightly more code;
    explicit construction of a `std::string_view` object.
  - Victor requested that the two traits in option 1-B be merged.
  - Victor agreed with Alisdair's suggestion to default the trait to enable based on the presence of a
    class member.
  - Victor asserted that only the author of a class should opt a class into the proposed behavior; not
    users of the class.
  - Victor repeated his opposition to enabling implicit third party interoperation.
  - Corentin stated that most of the proposed behavior should be being discussed in LEWG rather than in
    SG16 and that SG16 just needs to provide a recommendation whether use of `std::char_traits` is a
    good heuristic.
  - PBrett responded that there is an SG16 question concerning which types are sufficiently text-like.
  - PBrett asked for poll suggestions.
  - Tom noted that discussion revealed other options that should be explored.
  - Tom suggested polling the desire to enable interconvertibility across any/all string-like types in
    the ecosystem.
  - Poll wordsmithing ensued.
  - **Poll 1.1: Any opt-in to implicit range construction of `std::string_view` should be explicit on
    a per-type basis.**
    - Attendees: 12 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   8 |   0 |   1 |   0 |
    - Strong consensus.
    - A: If types have character traits, we should be making use of them to determine compatibility.
  - Jens responded to the against rationale by stating that use of character traits is not excluded;
    per-type enablement could be conditional on matching traits.
  - **Poll 1.2: The standard library should provide a general-purpose facility for enablement of
    implicit interconvertibility between string and string_view-like types (including UDTs).**
    - Attendance: 12 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   1 |   4 |   4 |   0 |
    - No consensus.
  - **Poll 1.3: A solution to the problem stated in P2779 needs to be included in the C++ standard library.**
    - Attendance: 12 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   1 |   5 |   4 |   0 |
    - No consensus.
  - Tom stated that he will record the poll results in the paper tracker and that it will be up to
    the LEWG chair to decide what to do next.
  - PBrett suggested that more examples of how this proposal could alleviate programming challenges
  - might help to increase motivation.
  - Tom agreed and noted that the large proportion of N votes presumably reflects insufficient
    motivation.
- [P2872R1: Remove wstring_convert From C++26](https://wg21.link/p2872r1).
  - \[ Editor's note: D2872R1 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2872R1 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Alisdair stated that, If feedback is light, that he will incorporate it and publish the paper as
    P2872R1; otherwise, he will publish P2872R1 as-is and incorporate the feedback in a newer revision.
  - Alisdair explained that `wbuffer_convert` and `wstring_convert` have been deprecated for three
    standard releases now.
  - Alisdair noted that removal permits implementors to continue to provide the functionality thanks
    to the additions to zombie names.
  - Alisdair indicated that wording updates might be needed, but that LWG will handle that.
  - Alisdair explained that the deprecation was motivated by underspecification and dependence on
    other deprecated features like `std::codecvt_utf8`.
  - Alisdair reported that there are currently four related open LWG issues and that reviving the
    feature would require more.
  - Corentin stated that, without `std::codecvt_utf8`, the standard no longer provides features needed
    to use these types.
  - Alisdair agreed and explained that programmers would have to provide their own `std::codecvt` facet.
  - Corentin acknowledged the requirement, but observed that programmers could more easily just
    implement the needed conversion.
  - Victor opined that these types provide little value since they are just light wrappers anyway.
  - Victor reported that a search of the projects he works on found a few uses, but that those uses
    should be replaced anyway.
  - PBrett asked if anyone had an objection to removing these features.
  - No objections were raised.
  - MarkZ reported that a Github search identified few uses.
- [P2845R0: Formatting of std::filesystem::path](https://wg21.link/p2845r0).
  - Victor introduced the paper:
    - [P1636 (Formatters for library types)](https://wg21.link/p1636) previously proposed formatting
      for `std::filesystem::path` but was specified to use the `native()` member function which might
      require transcoding and had no provisions for handling of non-printable characters.
    - This paper proposes a formatter that performs proper transcoding and substitutes escape
      sequences for non-printable characters and ill-formed code units.
  - Victor noticed a missing doublequote character in the first source code example in section
    2, "Problems".
  - Victor reported that some minor issues have been fixed in a draft R1 revision.
  - Corentin asked if backslash path delimiters on Windows would be formatted with escape sequences.
  - Victor confirmed that they would be, that such substitution might be surprising, but is
    consistent with `std::quoted()`.
  - Victor noted that an additional format specifier could be provided to choose an alternate behavior.
  - Corentin asked about use of the debug specifier, "{:?}".
  - Victor replied that the escaped format is proposed as the default behavior.
  - Charlie asserted that some lattitude is needed to choose an alternate escape character since
    backslash in paths has an important meaning on Windows.
  - Charlie noted that an alternate escape character could be surprising and would create an
    inconsistency across platforms.
  - PBrett asked about adding a specifier that enables specifying a different escape character.
  - Victor responded that such a specifier would be cumbersome and that there are other options
    such as performing a transformation.
  - Victor stated that there are use cases for both an escaped and a non-escaped variant.
  - Tom presented a few use cases including formatting for generic text, byte preserved for
    filesystem access, punycode for URLs, and quoted for shell scripts.
  - Tom suggested that most transformations should be done outside of formatting.
  - Corentin stated that the default behavior should just escape ill-formed code units and that
    the debug format specifier could be used to escape problematic characters.
  - Victor replied that quoting is useful but not always needed.
  - Tom suggested that a specifier could be added to opt in to quoting.
  - PBrett expressed two high level use cases:
    - The need to format the path precisely such that it can be used to open a file.
    - The need to format the path for textual display in a format friendly to humans.
  - PBrett opined that the paper does not clearly define the problem it intends to solve.
  - PBrett noted that, in
    [GLib](https://docs.gtk.org/glib),
    functions are provided to request a file name suitable for display as valid UTF-8 or as
    a byte array.
  - Victor replied that the goal of the paper is to address the issues discovered from prior
    review of
    [P1636 (Formatters for library types)](https://wg21.link/p1636).
  - Victor stated that additional use cases can be addressed as needed.
  - Zach reported that Python provides the functionality this paper is proposing and noted
    that its formatters will double Windows path separators.
  - Zach stated that Python allows printing unformatted paths by treating paths as a string
    and that C++ can do so as well.
  - Zach agreed that some kind of escaping and quoting is needed.
  - \[ Editor's note: Corentin later
    [posted a message to the SG16 mailing list](https://lists.isocpp.org/sg16/2023/06/3886.php)
    that demonstrates Python's behavior with a
    [Compiler Explorer link](https://godbolt.org/z/7sf5xPPsc).
    \]
  - Jens asserted that, due to various quirks with `std::filesystem::path`, that the paper
    should cover the motivation and design space and not solely focus on addressing the issues
    found from review of P1636.
  - Jens stated that the paper should discuss, for example, the implication of using backslashes
    in the syntax of character escapes in formatted paths.
  - PBrett agreed.
  - PBrett noted that we were out of time and that additional review will be needed to discuss
    encoding issues.
- Tom stated that the next meeting is scheduled for 2023-06-28, that there are several LWG issues
  awaiting review, and that Zach is working on a revision of
  [P2728 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728).
- \[ Editor's note: The following meeting was canceled due to summer vacations. \]
- Zach stated an expectation to have a new revision available in the next two weeks.


# May 24th, 2023

## Agenda
- [P2779R0: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r0).
- [P2863R0: Review Annex D for C++26](https://wg21.link/p2863r0).
- [P2871R0: Remove Deprecated Unicode Conversion Facets From C++26](https://wg21.link/p2871r0).
- [P2873R0: Remove Deprecated Locale Category Facets For Unicode from C++26](https://wg21.link/p2873r0).
- [P2872R0: Remove wstring_convert From C++26](https://wg21.link/p2872r0).


## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Charlie Barto
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Giuseppe D'Angelo
  - Jens Maurer
  - Mark de Wever
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2779R0: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r0):
  - Giuseppe presented an overview of the paper including relevant history:
    - [P1989R2 (Range constructor for std::string_view 2: Constrain Harder)](https://wg21.link/p1989)
      added an implicit `std::string_view` constructor that enables implicit conversion from any type 
      that satisfies a set of constraints, one of which includes having a member type alias named
      `traits_type` that matches the `std::string_view` member of the same name.
    - [P2499R0 (string_view range constructor should be explicit)](https://wg21.link/p2499)
      changed the new constructor to be declared `explicit` due to concerns involving ranges that do
      or do not contain an embedded null character; this broke the ability for string types to
      implicitly convert to `std::string_view`.
    - [LWG 3857](https://wg21.link/lwg3857)
      removed the constraint requiring a matching `traits_type` member type alias based on the rationale
      that such a safety precaution is no longer necessary since conversions are now explicit.
    - The proposed paper seeks to conditionally restore implicit conversions for string-like types
      without requiring modifications to those types to add conversion operators.
    - Two options are proposed:
      - Option 1 adds an opt-in trait and makes the constructor conditionally explicit based on the
        presence of a matching member `traits_type` type alias.
      - Option 2 makes the constructor conditionally explicit based on the presence of a matching member
        `traits_type` type alias without requiring an opt-in trait.
    - Qt has provided a `QStringView` class with an
      [implicit constructor that accepts a range](https://doc.qt.io/qt-6/qstringview.html#QStringView-7)
      that has worked well in practice for a decade.
  - PBrett asked what the essential nature of a string-like type is.
  - Giuseppe responded that it is a contiguous sequence of characters and associated character
    classification traits.
  - PBrett argued for substitution of "code units" for "characters".
  - Zach noted that the `traits_type` name might be used by types that are not string-like types, stated
    that he does not typically add a `traits_type` to his own string-like types, and asked what is
    commonly done in practice.
  - Giuseppe responded that the paper lists the results of a survey of various projects for occurrences
    of the `traits_type` name and found that it is strongly correlated with string-like types but that
    there are string-like types that don't have such a member.
  - Giuseppe acknowledged that the `traits_type` name is quite generic.
  - Victor expressed opposition to option 2 since it relies on what he considers to be a legacy feature
    and that `traits_type` is, in practice, always `std::char_traits`.
  - Victor asserted that implicit conversions and implicit interoperation with the standard library are
    not desired for Folly's `fbstring`.
  - Victor stated that he is ok-ish with option 1.
  - Tom asked Victor to further explain his concerns and the damage he fears the implicit conversions
    would cause.
  - Victor replied that use of `fbstring` is no longer encouraged and the proposed change would
    facilitate continued usage.
  - Victor noted that the proposed changes could also impact overload resolution in generic code and
    potentially introduce overload resolution failures due to ambiguity.
  - Corentin lamented the ability for programmers to specialize `std::char_traits` for their own
    user-defined types and stated he plans to propose deprecating or removing that allowance.
  - Corentin explained that the interface that `std::char_traits` provides is not a good match for how
    text processing works in practice.
  - Corentin asserted that increased use of `std::char_traits` should be discouraged.
  - Corentin opined that option 1 is fine but that option 2 is problematic in the long run.
  - Giuseppe acknowledged Corentin's position.
  - Corentin clarified that programmers should not be encouraged to use a different type than
    `std::char_traits` but rather that they should be encouraged not to use a char-traits-like type
    at all.
  - Tom summarized his understanding of the concerns; the proposed change could encourage programmers
    to add a `traits_type` member type alias of `std::char_traits` to classes that otherwise wouldn't
    define the type alias solely to enable implicit conversions to `std::string_view`.
  - Zach argued for not enabling such implicit conversions at all on the basis that `std::string_view`
    is intended to be implicitly convertible from other standard library types and that explicit
    conversions are appropriate elsewhere.
  - Alisdair opined that the right approach would be for types to opt themselves in to an implicit
    conversion.
  - Alisdair asserted that `std::char_traits` is not legacy and that it cannot be removed without
    significant ABI impact.
  - Alisdair stated that the matching `traits_type` constraint is a good heuristic and that the
    opt-in trait in option 1 is so specific that he would have a hard time supporting it.
  - Jens noted that the proposed wording for option 1 requires both the opt-in string-like-type
    trait and the matching `traits_type` constraint to enable implicit conversions.
  - Jens expressed a preference for an option that proposed only the string-like-type trait.
  - Jens stated that the wording needs to be rebased on the current working paper since the
    struck wording has already been removed.
  - Jens suggested `is_string_view_like` might not be the best choice of name for the opt-in
    trait and suggested `enable_view` as an example name for similar opt-in traits.
  - Giuseppe acknowledged the suggestion and stated that the name can be changed.
  - Jens noted that it doesn't matter how string-view-like the source type is as long as it
    provides contiguous storage and opts itself in.
  - Jens agreed with not wanting to encourage the addition of an otherwise unused `traits_type`
    member.
  - Jens observed that `is_string_view_like` is false by default.
  - Jens suggested that, if it is desirable to provide a safety check on a matching `traits_type`
    member, that the `is_string_view_like` trait can support a mechanism to enable that.
  - Jens expressed a preference for postponing a poll to forward the paper until it has been
    rebased on the current working paper.
  - Various poll options were discussed but it was decided that polling be postponed pending
    an updated paper revision with wording rebased on the current working paper and an additional
    option to enable implicit conversions based solely on the opt-in trait.
- [P2863R0: Review Annex D for C++26](https://wg21.link/p2863r0):
  - Alisdair introduced this and the following papers.
  - Tom explained his understanding of the ramifications for removal of standard library features;
    that an implementor may choose not to provide the removed features or may choose to provide
    them since the removed names are reserved as "zombie" names.
  - Alisdair acknowledged the intent, but noted that the standard currently lacks wording to
    support zombification of explicit template specializations.
  - Alisdair explained that there are four deprecated subclauses that are relevant to SG16;
    [D.26 (\[depr.locale.stdcvt\])](http://eel.is/c++draft/depr.locale.stdcvt),
    [D.27 (\[depr.conversions\])](http://eel.is/c++draft/depr.conversions),
    [D.28 (\[depr.locale.category\])](http://eel.is/c++draft/depr.locale.category), and
    [D.29 (\[depr.fs.path.factory\])](http://eel.is/c++draft/depr.fs.path.factory).
  - PBindels stated that
    [D.15 (\[depr.str.strstreams\])](http://eel.is/c++draft/depr.str.strstreams) and
    [D.25 (\[depr.string.capacity\])](http://eel.is/c++draft/depr.string.capacity)
    have to do with text facilities but that he reviewed them and concluded that the functionality
    is not strongly relevant for SG16.
  - Alisdair stated that, for `std::filesystem::u8path`, per
    [LWG 3840](https://wg21.link/lwg3840),
    there have been recent comments that removal would be problematic.
  - Tom stated that the LWG issue was recently discussed in LEWG but that the LWG issue
    does not appear to have been updated to reflect that discussion.
  - \[ Editor's note: LEWG discussed the LWG issue during its
    [2023-01-10 telecon](https://wiki.edg.com/bin/view/Wg21telecons2023/LWG3840). \]
  - Alisdair stated that deprecated features should either be undeprecated or removed and noted
    that this feature has been deprecated since C++20.
  - Jens expressed concern regarding Billy O'Neal's comment in the LWG issue that deprecation
    of `u8path` was one of the reasons that vcpkg discontinued use of `std::filesystem`.
  - Jens stated that SG16 should offer an opinion.
  - Corentin replied that there was a poll in LEWG in January and that there was no consensus
    to undeprecate `u8path`.
  - Corentin stated that a mechanism to access a sequence of `char` that holds UTF-8 code units
    as-if it were a sequence of `char8_t` is a feature that we should have; we're missing a way
    to pass such a sequence to the `std::filesystem::path()` constructor such that it is
    interpreted as UTF-8.
  - Tom noted that Corentin has a paper on that topic.
  - \[ Editor's note: See
    [P2626 (charN_t incremental adoption: Casting pointers of UTF character types)](https://wg21.link/p2626). \]
  - Alisdair noted that, if removed, `u8path` would be added to the list of zombie names, so
    implementors that wish to continue providing it may do so.
  - PBindels opined that `u8path` provides a solution to work around legacy issues but that
    Corentin's P2626 provides a proper solution.
  - PBindels suggested that we should neither undeprecate nor remove `u8path` until a proper
    solution is in place.
  - Alisdair stated that he can update the paper to reflect that guidance and to note further
    action as dependent on P2626.
  - Charlie agreed with not removing `u8path` without a proper alternative.
  - Charlie noted that, if `u8path` is zombified, that implementors can continue to provide
    it, but that portability is lost.
  - Charlie stated that he didn't see a reason to remove `u8path`; that it isn't harmful.
  - Alisdair acknowledged that a migration path is needed.
  - Tom explained that the original motivation for deprecation was to dissuade continuing to
    provide standard library functions that require UTF-8 data in `char`-based storage.
  - Tom noted that `u8path` and the deprecated `std::codecvt` facets were the only standard
    library features that did so.
- [P2871R0: Remove Deprecated Unicode Conversion Facets From C++26](https://wg21.link/p2871r0):
  - Alisdair presented the paper:
    - These facets were deprecated because they did not provide error handling capabilities
      and could not reasonably be extended.
    - There are some implementations that do not issue deprecation warnings.
  - Corentin noted the work in progress and general plan to provide replacements for C++26 and
    suggested waiting to remove them pending that work.
  - Jens agreed and stated that removal without replacements is ill-advised unless these are
    actively causing harm.
  - Tom noted that conversions are possible through the `mbrtoc*` and `c*rtomb` family of
    functions though those have their own issues.
  - Victor stated that the `codecvt` facets are so challenging to use that not having a
    replacement isn't really a problem.
  - Alisdair noted that implementors can continue to provide them thanks to zombification.
  - Alisdair reported that, per the paper, LEWG and SG16 previously recommended removal during
    the C++23 cycle, but that action wasn't completed.
  - Alisdair reminded the group that `codecvt_utf8` and `codecvt_utf16` convert to and from
    UCS-2 or UTF-32 depending on the size of the first template parameter.
  - PBrett asked for any objections to removal.
  - No objections were reported.
  - Alisdair stated he will take that feedback back to LEWG.
- [P2873R0: Remove Deprecated Locale Category Facets For Unicode from C++26](https://wg21.link/p2873r0):
  - Tom explained that these facets were deprecated because they convert to and from UTF-8
    in `char`-based storage rather than between the multibyte encoding like the non-deprecated
    facets do.
  - Tom reported that `char8_t`-based replacements were added as replacements, but those
    were a mistake because they won't be used by `char`-based streams anyway.
  - \[ Editor's note:
    [LWG 3767](https://wg21.link/lwg3767)
    tracks deprecating the `char8_t`-based facets. \]
  - PBrett asked for any objections to removal.
  - No objections were reported.
  - Corentin spoke in favor of removal.
- [P2872R0: Remove wstring_convert From C++26](https://wg21.link/p2872r0):
  - Giuseppe asked if the paper includes removal of `std::wbuffer_convert`.
  - Alisdair confirmed that it does.
  - Alisdair explained that these were deprecated because the example for `std::wstring_convert`
    used another deprecated feature, `std::codecvt_utf8` and, due to other underspecification
    concerns, noone was motivated to fix them.
  - Alisdair asked if SG16 is the right group to address this.
  - PBrett responded affirmatively and stated that SG16 is the group that misunderstands `wchar_t`
    the least.
  - Alisdair noticed some issues with the paper and concluded that updates are required before
    the paper is ready for any action to be taken on it.
- Tom stated that the next meeting is tentatively scheduled for 2023-06-07 and will likely
  continue review of 
  [P2779 (Make basic_string_view’s range construction conditionally explicit)](https://wg21.link/p2779) and 
  [P2872 (Remove wstring_convert From C++26)](https://wg21.link/p2872) if updated revisions
  are available followed by an initial review of
  [P2845 (Formatting of std::filesystem::path)](https://wg21.link/p2845).
- Zach reported that he expects to have a new revision of
  [P2728 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728)
  available soon after the Varna meeting.


# May 10th, 2023

## Agenda
- [P2728R3 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r3).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Nathan Owens
  - Jens Maurer
  - Peter Brett
  - Robert Leahy
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- A round of introductions was held in honor of a new attendee, Eddie Nolan.
- [P2728R3 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r3):
  - PBrett introduced the topics for today.
  - Zach provided an introduction to the latest revision:
    - Use case 4 in section 4.4 illustrates use with `std::print()` and `std::cerr`.
    - The `code_unit` concept still relies on `sizeof()` pending changes to infer encoding
      based on `charN_t` types; that change is still in progress awaiting fixes to existing tests.
  - Victor pointed out an error in section 4.4; the call to `std::print()` is missing the
    required format string.
  - Corentin asked how encoding is handled for the `operator<<` ostream inserter.
  - Zach responded that `as_utf8` produces a `utf_view` specialization for which specializations
    of `std::formatter` and overloads of `operator<<` are defined.
  - Zach noted that the current paper revision specifies `utf_view` but that prior revisions
    specified distinct templates for `utf8_view`, `utf16_view`, and `utf32_view`.
  - Zach explained that `utf_view` is able to produce UTF-8 from whatever encoding it adapts.
  - Corentin stated that some kind of string-like type is needed to enable formatting.
  - Zach noted the potential for additional views such as a `toupper_view` that performs case
    conversions.
  - Corentin responded that it should not be necessary to provide `operator<<` overloads for every
    view; a generic formatting mechanism is needed.
  - Zach explained that the goal is to provide interoperation with streaming and formatting and
    asserted that we need a conveient way to format these types.
  - Zach agreed that a `printable_view` or similar could be provided, but asserted it would be
    preferable to just be able to format them directly.
  - Victor stated that generic formatters can be provided assuming a mechanism to determine the
    proper source and destination encoding.
  - Victor observed that, when the changes to infer encoding based on `charN_t` types is complete,
    that there won't be any support for `char` and `wchar_t`.
  - Zach confirmed the observation and noted this reflects prior consensus in prior polls.
  - Robin posted the text of the relevant poll in the chat:

        Poll 2: UTF transcoding interfaces provided by the C++ standard library should operate on
        `charN_t` types, with support for other types provided by adapters, possibly with a special
        case for `char` and `wchar_t` when their associated literal encodings are UTF.

  - PBrett interpreted the poll as meaning that the author can choose to provide support for
    `char` and `wchar_t` as code units when the associated literal encoding is a UTF encoding.
  - Zach suggested those types could be supported with another adapter.
  - Tom stated that, with regard to another adapter, there is a question of whether such an
    adapter should be implicitly used or require explicit syntax.
  - Zach expressed disfavor twoards dependence on the literal encoding for portability reasons.
  - Tom acknowledged that existing use of the literal encoding to infer an encoding for
    `char-`based text is an imperfect heuristic.
  - PBrett expressed support for having a `std::formatter` specialization that supports
    these views, but expressed discomfort with ostream support for `operator<<` since there
    is no indication of what encoding to use.
  - PBrett asked what the proposed `operator<<` actually does.
  - Zach replied that it prints octets one at a time.
  - PBrett explained that `std::print()` doesn't necessarily just write octets.
  - Zach asked if `std::print()` is equivalent to streaming the result of a call to `std::format()`.
  - PBrett replied negatively.
  - \[ Editor's note: See the *Effects* description for `std::vprint_unicode()` in
    [\[print.fun\]p7](http://eel.is/c++draft/print.fun#7);
    the `std::print()` family of functions have specialized behavior when the target stream is
    a Unicode capable terminal. \]
  - Zach opined that stream support is very useful and suggested `operator<<` could be conditionally
    supported for non-ASCII based systems.
  - Zach stated that he is most concerned with ensuring that `std::format()` and `std::print()`
    work as intended.
  - Jens summarized the status quo; `std::print()` does not currently support `char8_t`-based text
    as either the format string or as a format argument.
  - Jens observed that handling of `char8_t` encoded data as proposed is novel since it effectively
    passes `char8_t`-encoded data as `char`-based input to `std::print()`.
  - Jens asserted that transcoding should be performed or the print attempt should be ill-formed.
  - Jens acknowledged the encoding questions will certainly be revisited at some point.
  - Corentin stated that the lack of support for `charN_t` in `std::format()` is a separate issue
    that awaits someone doing the work needed.
  - Zach explained that the new paper revision moves `null_sentinel_t` from the `std::uc` namespace
    to `std`.
  - Zach noted that `null_sentinel_t` equality is determined by comparison with a value constructed
    object of the other type.
  - Zach asserted that `null_sentinel_t` is important for support of string literals.
  - Corentin suggested that `null_sentinel_t` could be split off to a separate paper for SG9 and EWG
    to review since it doesn't need to be tied to Unicode.
  - PBrett observed that there is an implicit vs explicit tradeoff with regard to `null_sentinel_t`;
    some functions take sized ranges and support embedded null characters while others don't.
  - PBrett noted this presents the possibility of a string being inadvertently truncated.
  - Zach agreed that unintented truncation can occur with `utf_view`.
  - PBrett asked to confirm that such truncation can only occur when a single pointer is passed to
    the constructor.
  - Zach confirmed and directed attention to the `utf_range_like` concept.
  - Victor stated that `null_sentinel_t` makes sense as a generic facility but that the proposed
    `base()` member function seems specific to this use case.
  - Zach agreed that the member is specific to the ability to navigate a hierarchy of transformed
    ranges.
  - Steve agreed that something like `null_sentinel_t` is needed to have a good story for support
    of null terminated strings.
  - Steve stated that requiring explicit syntax just adds noise if practical use requires having
    to be explicit all the time.
  - Tom asked if ranges already has a concept for layered range transformations and navigation
    between them; if so, SG9 could comment on the usefulness of the proposed `base()` member
    function.
  - Zach noted that views often provide a `base()` member function; likewise with iterators such
    as `reverse_iterator`.
  - Tom asked if there is precedent for a range-or-iterator concept like `utf_range_like`.
  - Jens replied negatively.
  - Tom suggested taking the `base()` and range-or-iterator concept concerns to SG9 to see if they
    have comments or if there is existing practice that we should align with.
  - Jens stated that `null_sentinel_t` seems useful but that it should be moved to the
    `std::ranges` namespace.
  - Jens argued that there is no need to move `null_sentinel_t` to a separate paper now; that can
    be done later if it would be helpful.
  - Jens requested the removal of the `base()` member since there is no base to begin with and
    noted that there are other means to accomplish the purpose it is intended to serve.
  - Jens stated that any chaining will be on the range level rather than the iterator level.
  - Corentin agreed with Jens.
  - Corentin noted that sized range types like `std::string_view` are advantageous since the size
    is maintained; calls to `strlen()` are avoided.
  - Zach stated that Eric Niebler has demonstrated the effectiveness of sentinels.
  - Zach commented that Jens is probably right regarding removal of the `base()` member.
  - **Poll 1: Separate `std::null_sentinel_t` from P2728 into a separate paper for SG9 and LEWG;
    SG16 does not need to see it again.**
    - Attendees: 12 (3 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   1 |   4 |   2 |   1 |
    - No consensus; author's discretion for how to continue.
  - Zach began reviewing the proposed constants and utility functions in section 5.4.
  - Zach stated that `replacement_character` is useful to have.
  - Zach explained that the `starts_encoded()` and `ends_encoded()` functions are just for
    convenience.
  - Tom asked why `starts_encoded()` requires a range rather than supporting the range-or-iterator
    approach offered with `utf_range_like` and what the criteria is for determining when the
    range-or-iterator approach should be used.
  - Jens expressed a preference that these remain range-only.
  - Zach agreed with Jens and explained that these are low level functions that don't require a
    high level of ergonomics.
  - PBrett noticed that there is an `is_low_surrogate()` function, but that a corresponding
    `is_high_surrogate()` is absent and argued that neither or both should be provided.
  - Steve stated in chat:
    "If we don't provide `is_high_surrogate` we have to explain that forever, even if it's low value."
  - Zach reported a mistake in use case 3 in section 4.3; `is_lead_code_unit()` is used, but is
    no longer proposed with the other utility functions.
  - Corentin stated that the proposed utility functions provide a subset of Unicode character
    properties that programmers don't really want to know about.
  - Corentin suggested that, if support for use case 3 is desirable, it might be better to
    provide a type that maintains the required state internally instead of users having to use
    `is_lead_code_unit()` and such on their own.
  - Fraser suggested changing the names to `is_lead_surrogate()` and `is_trail_surrogate()`
    because it is difficult to remember what is meant by high and low.
  - Victor stated in chat:
    "I'd prefer to stick with established terminology and not invent new terms, even if they are marginally clearer."
  - Robert agreed with Victor in chat.
  - Jens offered a quote from Unicode 15 section 3.8:

        D71 *High-surrogate code point*: A Unicode code point in the range U+D800 to U+DBFF.
        ...
        D73 *Low-surrogate code point*: A Unicode code point in the range U+DC00 to U+DFFF.

  - Fraser countered with a quote from from later in the same section:

        D75 ...
        ...
        Sometimes high-surrogate code units are referred to as *leading surrogates*.
        Lowsurrogate code units are then referred to as *trailing surrogates*.
        This is analogous to usage in UTF-8, which has *leading bytes* and *trailing bytes*.

  - Jens opined that a clear scope for the utility functions is needed in order to avoid
    design-by-committee.
  - Jens suggested that `is_scalar_value()` and `is_code_point()` might be appropriate, but
    noted that `is_assigned_code_point()` would not be an elementary level building block.
  - Jens requested an analysis of what building blocks should be exposed.
  - Jens stated that the incremental read of a UTF-8 stream use case is interesting and can
    be in scope, but that more design and analysis is needed.
  - Jens asserted that the paper needs more rationale of what the scope is and what the
    criteria is for inclusions and exclusions.
  - Steve indicated that the proposed functions are facilities that he needs, but agreed
    with Jens that the streaming use cases probably deserve their own paper.
  - Steve offered to work with Zach to move these functions into a separate classification
    paper if Zach is interested.
  - Zach agreed that doing so sounds like the right approach.
  - PBrett stated that `find_invalid_encoding()` would be more useful if it returned the
    range of invalid code units rather than just an iterator to the first.
  - Zach agreed and noted that would be useful for replacement character handling.
  - Tom stated that there are multiple replacement strategies to be considered.
  - \[ Editor's note see
    [PR-121](https://www.unicode.org/review/pr-121.html)
    for a description of replacement character policies that conform to the Unicode
    standard. \]
  - Zach stated that he would probably remove all of the utilities except for
    `replacement_character`.
  - Tom responded that error policies need more discussion and suggested that
    `replacement_character` can likely be postponed as well.
  - Corentin noted that a replacement character policy is required since Unicode
    algorithms only operate on code points.
  - Zach explained that the transcoding iterators now adapt the iteratory category
    correctly.
  - Zach noted that the complete set of UTF transcoding iterators is still present.
  - PBrett asked what the `const char*` parameter of
    `use_replacement_character::operator()` is for.
  - Zach explained that an error message is passed to the function.
  - PBrett requested that the range of invalid code units be passed so that the entire
    sequence can be preserved in a thrown exception.
  - Jens acknowledged the need for the transforming iterators to implement the
    transcoding view, but stated a lack of motivation for exposing them.
  - Tom agreed and requested that, if there are strong use cases for the iterators, to
    please include the motivation for them in the paper.
  - Zach acknowledged that the iterators can be obtained from the view type.
  - Jens opined that the iterators seem like a step backwards given the effort to move
    towards range-based designs.
  - Corentin stated that the need to store three iterators within each transcoding
    iterator to track the beginning and end of the range as well as the current position is
    novel; iterators generally don't know where the beginning and end of a range are;
    ranges maintain that information.
  - \[ Editor's note: Further discussion regarding iterators that hold references to a
    view occurred on the SG16 mailing list. See the
    [2023-05-10 dated messages in the thread with subject "Re: [SG16] New revision of P2728"](https://lists.isocpp.org/sg16/2023/05/3850.php).
    \]
  - Tom reported a potential ambiguity with the range-or-iterator approach; string literals
    are arrays that satisfy range concepts but that also decay to a pointer that
    satisfies iterator concepts.
  - Tom indicated that an explicit deduction guide might be needed to ensure that `utf_view`
    works as intended with CTAD.
  - Tom and Zach agreed to take further discussion offline.
- PBrett stated that the next meeting will be on 2023-05-24 and that the agenda will include
  the following:
  - [P2779R0: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r0).
  - Review of proposed deprecations by Alisdair (awaiting paper).


# April 26th, 2023

## Agenda
- [L2/23-107: Proper Complex Script Support in Text Terminals](https://www.unicode.org/L2/L2023/23107-terminal-suppt.pdf):
  - Determine interest for participation in a potential new UTC project.
- [P2779R0: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r0):
  - Determine whether to commit SG16 time to discussing this paper.
- [P2741R1: user-generated static_assert messages](https://wg21.link/p2741r1).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Fraser Gordon
  - Jens Maurer
  - Mark de Wever
  - Nathan Owen
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [L2/23-107: Proper Complex Script Support in Text Terminals](https://www.unicode.org/L2/L2023/23107-terminal-suppt.pdf):
  - Tom provided an introduction:
    - The paper authors seek to specify a protocol for the display of complex scripts in
      traditional text-based terminals.
    - Such a protocol could improve text formatting behavior beyond what has been achieved
      with
      [P1868 (🦄 width: clarifying units of width and precision in std::format)](https://wg21.link/p1868)
      and
      [P2675 (LWG3780: The Paper (format's width estimation is too approximate and not forward compatible))](https://wg21.link/p2675).
    - The paper proposes the creation of a new project within the UTC.
    - Robin Leroy indicated that, should a new UTC project be approved, volunteers to
      participate in it would be welcome.
    - Anyone interested should reach out to Robin.
  - Fraser stated that the paper is an interesting read regardless of any interest in
    participation in a UTC project.
- [P2779R0: Make basic_string_view’s range construction conditionally explicit](https://wg21.link/p2779r0):
  - Tom stated that, in his opinion, the paper does not raise SG16 concerns; however,
    the paper lists SG16 as an audience and Victor requested that SG16 review it.
  - Tom explained that the discussion today is only intended to determine whether SG16
    should spend time on this paper prior to receiving a request from the LEWG chair.
  - Victor opined that SG16 should review because the paper proposes the use of
    `std::char_traits` to detect a string-like type.
  - Tom observed that the proposed wording doesn't actually reference `std::char_traits`.
  - Fraser asked for confirmation that the question in front of SG16 is whether to weight
    in on this use of `std::char_traits`.
  - Victor confirmed.
  - Tom commented that the proposed wording only appears to use a traits type to name
    specializations of `std::basic_string_view` in order to opt them into the proposed
    `is_string_view_like` trait.
  - Victor directed Tom to look at the wording for option 2.
  - Corentin stated that he has been considering writing a paper to prohibit user
    specializations of `std::char_traits`.
  - Zach commented that traits types can be awkward; especially with SFINAE.
  - Tom observed that the proposed wording only checks whether both types have a
    matching member type named `traits_type`; it doesn't check for `std::char_traits`
    specifically.
  - Corentin requested a poll to encourage LEWG not to rely on `std::char_traits`.
  - Tom asked if anyone was opposed to such a poll.
  - Jens noted that the proposal just performs a type tag comparison and doesn't inspect
    the type definition.
  - Jens emphasized that this is just a heuristic intended to identify types that are
    semantically similar to `std::string_view`.
  - Jens commented that if a better heuristic were to be found, that would be great, but
    otherwise the proposed heuristic seems conservatively correct.
  - Jens stated that he does not see an SG16 concern here.
  - Zach expressed a preference towards waiting for the paper author to present before
    any polls are taken.
  - Zach stated that the `traits_type` name is not great for enabling this heuristic, but
    is not as bad as examining `std::char_traits` directly.
  - Corentin suggested that option 2 might not be needed given the option 1 approach to
    explicitly opt in using a different name.
  - Jens noted that the proposed wording for option 1 subsumes option 2.
  - Victor noticed that the paper lists Folly's `fbstring` type and asserted that the
    implicit opt-in would not be wanted by its maintainers.
  - Victor expressed a desire to deprecate `std::char_traits`.
  - Tom agreed with Zach that the paper author should be granted an opportunity to present
    his perspective before SG16 takes further action.
  - Tom said he would reach out to the paper author to see if he would like to present.
- [P2741R1: user-generated static_assert messages](https://wg21.link/p2741r1):
  - Corentin introduced the paper:
    - The paper proposes an extension to `static_assert` to enable the optional message
      to be provided by a constant expression evaluated at compile-time.
    - Barry Revzin's
      [P2758R0 (Emitting messages at compile time)](https://wg21.link/p2758r0)
      proposes some additional `consteval` functions that do similarly.
    - The functionality these papers propose is not an SG16 concern, but the encoding
      used for the messages is.
    - The only encoding that is currently known at compile-time for strings in 
      `char`-based storage is the ordinary literal encoding.
    - There is a question of whether the proposed features should also support
      `wchar_t`, `char8_t`, `char16_t`, and/or `char32_t`.
  - Victor noticed that the paper contains an example that uses `std::format` in an
    expression that requires constant evaluation despite the current lack of `constexpr`
    support for it in the standard and no current proposal to add such support.
  - Corentin acknowledged that limitation but noted that the `format` implementation in
    [libfmt](https://github.com/fmtlib/fmt)
    has such support.
  - Corentin explained that the proposed addition to `static_assert` is that the message
    parameter accept string-like types that have appropriate `data()` and `size()` member
    functions.
  - Corentin noted that this suffices to enable any string produced during constant
    evaluation to be provided by wrapping it in a `std::string_view`-like type.
  - Corentin stated that there is an open question of whether string-like types with
    non-contiguous storage should be supported.
  - Corentin added that, as proposed, text in `char8_t`-based storage can also be used.
  - Zach asked why `std::format` doesn't support constant evaluation.
  - Corentin replied that the question should be directed to EWG, but noted some existing
    constant evaluation limitations; that floating-point types aren't supported for example.
  - Zach asked what an implementation would do when trying to present the message to a user.
  - Corentin responded that it would have to convert the message from the literal encoding
    to the encoding used to display text to a user.
  - Corentin noted that this would add a new conversion requirement to compilers.
  - \[ Editor's note: Implementations are currently required to convert from the source
    file encoding to the various literal encodings, but do not necessarily need to be able
    to convert from those literal encodings to any other encoding. \]
  - Zach commented that the proposed wording makes the design clear and that he has no
    concerns. 
  - Victor stated that `std::format` could support `constexpr` now given that is has been
    shown to be implementable.
  - Victor asserted that the ordinary literal encoding is the right choice for text in
    `char`-based storage.
  - Victor commented that the only question for SG16 is whether to add support just for
    `char` or for all of the character types.
  - Jens observed a parsing issue in the proposed wording that will require disambiguation;
    a string literal matches both *unevaluated-string* and *constant-expression*.
  - Jens suggested that, if text in `char8_t`-based storage is supported for the
    *constant-expression* case, then UTF-8 string literals should also be supported for the
    *unevaluated-string* case so that such literals don't fall into the former case.
  - Corentin suggested that EWG should decide whether pointers to null-terminated strings
    should be supported.
  - \[ Editor's note: Discussion ensued regarding unevaluated strings, UCNs, conversion to
    literal encodings, and whether two grammar productions are really required; the editor
    failed to record an accurate record of the discussion. \]
  - Jens requested that the wording be rebased on the current working draft.
  - Jens noted that the pointer+size interface is preferred for the constant evaluation case
    and that therefore creates motivation for treating string literals as a special case.
  - Jens noticed that the proposed wording suggests that the *constant-expression* argument
    is evaluated multiple times.
  - Jens identified an additional wording issue; "possibly const-qualified type is `char`\*
    or `char8_t`\*" should be something like "pointer to possibly const-qualified `char` or
    `char8_t`."
  - Mark asked Victor if the libfmt `format` implementation supports floating-point types
    in constant evaluation.
  - Victor confirmed that it does, but that it doesn't use `to_chars()` to do so.
  - Corentin spoke towards the motivation to support character types other than `char`:
    - Support for `u8""` and `char8_t` ensures the availability of an encoding that supports
      all characters.
    - Support for `L""` and `wchar_t` enables the use of existing `constexpr` string building
      functions used on Windows.
  - Tom asked if it is necessary to allow encoding prefixes for the *unevaluated-string*
    case and noted that
    [P2361 (Unevaluated strings)](https://wg21.link/p2361)
    argued that such allowances are not needed.
  - Corentin replied that the only motivation would be to prevent such expressions from
    falling into the *constant-expression* case.
  - Jens noted that falling into that case would render the program ill-formed since
    string literals don't have a type that satisfies the requirements for `data()` and
    `size()` members.
  - Tom responded that the *constant-expression* case could also support pointers to
    null-terminated strings.
  - Zach asked if the requirements could be specified in terms of `std::data()` and
    `std::size()`.
  - Corentin replied that such support would require including standard headers.
  - Jens observed that use of `std::data()` and `std::size()` with the arrays produced
    by string literals would create ambiguity regarding the presence or absence of a null
    terminator in the string data.
  - Zach lamented the absence of a trait to differentiate string literals from other kinds
    of expressions.
  - Jens replied that any such solution would require extensions into the type system.
  - Jens reported that the last line of the proposed wording refers to a *string-literal*
    that is not present in the *static_assert-declaration*.
  - Victor expressed a preference for avoiding null-terminated strings and sticking to the
    proposed pointer+size design.
  - Jens requested that the wording be aligned across other declarations with regard to
    the requirements to display messages at compile-time and advised discussing with the
    author of
    [P1301 (\[\[nodiscard("should have a reason")\]\])](https://wg21.link/p1301).
  - **Poll 1: Text produced during constant evaluation in char-based storage that is provided to the compiler shall be encoded in the literal encoding.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   4 |   0 |   0 |   0 |
    - Strong consensus in favor.
  - **Poll 2: static_assert(cond, constant-expression) should support expressions that produce a range of `char` result.**
    - Attendees: 6
    - No objection to unanimous consent.
  - **Poll 3: static_assert(cond, constant-expression) should support expressions that produce a range of `wchar_t` result.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   1 |   1 |   4 |   0 |
    - A: Would like to see more motivation.
    - Consensus against.
  - **Poll 4: static_assert(cond, constant-expression) should support expressions that produce a range of `char8_t` result.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   1 |   1 |   2 |   1 |
    - SA: We shouldn't complicate the feature; `char` should suffice.
    - No consensus.
  - **Poll 5: static_assert(cond, constant-expression) should support expressions that produce a range of `char16_t` or `char32_t` result.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   0 |   3 |   3 |   0 |
    - No consensus.
- Tom stated that the next meeting will be on 2023-05-10 and that an agenda is yet to be
  determined.


# April 12th, 2023

## Agenda
- [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0):
  - Continue discussion.

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Fraser Gordon
  - Jens Maurer
  - Nathan Owens
  - Peter Brett
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0):
  - Zach spoke to concerns raised in the previous discussion regarding the need for
    output iterators:
    - There is a need for programs that use UTF-8 internally to convert to and from UTF-16
      in `wchar_t` for Windows and `char16_t` for ICU.
    - The proposed "out" and "insert" transcoding iterators implement a push model; the
      others implement a pull model.
    - The "out" and "insert" transcoding iterators are useful to store the output of an
      eagerly evaluated pipeline.
  - PBrett stated that, for an eager algorithm, the size of the range is known.
  - Zach disagreed that the final size is necessarily known, but noted that it is often
    possible to predict an approximate size.
  - Tom asserted that output iterators don't work for transcoding since a failure to assign
    a complete code unit sequence results in silent data loss or UB or similar.
  - Zach suggested that the iterator destructors could perform some kind of flush operation.
  - Zach agreed that the output iterators could be removed from the proposal but that he
    had encountered situations where he couldn't both use a view and efficiently compute
    an output size.
  - Jens asserted that the existing `std::back_insert_iterator`, `std::front_insert_iterator`,
    and `std::insert_iterator` types should suffice for the proposed back insert, front insert,
    and insert iterators.
  - Jens observed that there has so far not been much demonstrated motivation for push-based
    iterators but stated that a general output iterator abstraction should be developed if
    compelling use cases are identified.
  - Jens recalled prior consensus for specifying Unicode algorithms that operate on code points
    rather than on code units.
  - Jens concluded that the output of any kind of eager algorithm should therefore be a
    sequence of code points that are then piped into encoding iterators.
  - Jens stated that he is strongly opposed to adding the full matrix of transcoding iterators.
  - Corentin requested stronger motivation for transcoding output iterators.
  - Corentin noted that the size of a range that has iterators that only model
    `std::input_iterator` is never known prior to iterating it.
  - Corentin observed that non-sized ranges exist in C++23 and programmers have so far been
    ok with that.
  - Corentin suggested that `std::ranges::to()` should suffice and should perform similarly
    to direct use of an output iterator.
  - Zach replied that output iterators are essentially never needed with ranges.
  - Corentin asked when an output iterator would be preferred over a range.
  - Zach replied that performance experiments demonstrated that output buffers performed
    better for eager algorithms.
  - Corentin expressed concern that output iterators add complexity but don't provide an
    order of magnitude performance improvement.
  - Zach stated that output iterators are somewhat odd, but that they aren't particularly
    complicated.
  - Corentin countered that their specification would still require spending additional
    time in wording review that would come at the expense of something else.
  - Zach reiterated his willingness to drop them for now and to revisit later if needed.
  - PBrett expressed support for deferring features that are not essential so as to narrow
    the proposal to the feature set that will provide the most value to the community.
  - Zach stated that it is an option to not include eager algorithms at all but that doing
    so leaves performance on the table.
  - Tom acknowledged that views are not well optimized today and suggested that might
    change in the future.
  - Jens indicated low expectations with regard to teaching optimizers the peculiarities
    of views and noted the lack of improvements for, for example, string concatenation.
  - Jens opined that implementors tend to be better off focussing on SPEC benchmarks.
  - Jens explained that the incremental processing of view pipelines requires intermediate
    state that is difficult to lower to a vectorizable loop.
  - Jens observed that vectorizing optimizers still lag the performance achieved by hand
    vectorized UTF-8 decoders.
  - Zach agreed with Jens in chat; "I am just as skeptical as Jens about the optimization
    prospects."
  - Jens stated that the paper would benefit from more rationale that motivates including
    the individual features in the C++ standard.
  - Jens observed that we appear to have consensus to at least provide views.
  - Jens expressed uncertainty whether it is reasonable to provide normalization as a view
    or whether an eager algorithm is required.
  - Corentin agreed that lack of support for eager algorithms does leave performance on the
    table and estimated the difference as between 2x to 5x.
  - Zach agreed, but argued the cost is closer to 2x.
  - Corentin noted that the performance difference matters more in some cases; several MB
    of text might be needed before the difference becomes noticeable.
  - Corentin asserted that quick and simple interfaces are needed in the standard to fill
    the existing functionality gap but that they don't need to be the fastest possible
    implementation.
  - PBrett reported that
    [P2300 (`std::execution`)](https://wg21.link/p2300)
    includes a simple set of algorithms with an expectation that implementations will
    pattern match and optimize accordingly.
  - PBrett asked whether implementors could provide, as a QoI concern, specialized
    implementations.
  - Zach responded that such improvements are possible and reported that ICU avoids
    decoding for some operations.
  - Zach stated that recognition of operations in pipelines will probably not be feasible.
  - Tom suggested a case that can be specialized; a transcode algorithm where the inputs
    and outputs operate on contiguous storage.
  - Zach agreed, but noted that dropping a chunk-by operation into a pipeline will prevent
    use of those kinds of specializations.
  - PBrett observed that `std::ranges::to()` is always eager and, at the end of a pipeline,
    it seems technically possible to optimize based on the input and output types.
  - Zach agreed and noted that library authors can handle that for simple cases.
  - Jens noted that the ranges library is often proscriptive about types used and that use
    of features like `decltype` can interfere with specialization.
  - Jens provided an example; the result of `std::ranges::views::take(R, n)` is
    a specialization of `std::span` if `R` is a `std::span`.
  - Corentin reported having used ranges to optimize based on type in his prototypes.
  - Corentin mentioned that text transformations tend not to produce sized ranges, but that
    their outputs usually have a size that is proportional to their input.
  - Robin explained that, with regard to normalization, there is an upper bound of 3x on the
    possible size of the output, but acknowledged that is still well above the size usually
    required in practice.
  - **Poll 1: SG16 would like to see a version of P2728 without eager algorithms.**
    - Attendees: 10 (3 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   2 |   0 |   1 |   0 |
    - Consensus in favor.
  - Zach explained that, with regard to the `as_utfN()` factory functions behaving differently
    from those for other views, it is because they are defined in terms of any UTF iterator
    and a sentinel; this is what allows any iterator that produces UTF code units to be used.
  - Jens expressed an expectation that an interface that requires a range of UTF-32 code points
    would use a concept that requires a range with corresponding constraints on its
    `value_type` and that programmers could provide their own views in that case.
  - Corentin agreed.
  - Tom stated that `as_utf8()` doesn't seem to actually do anything.
  - Zach replied that it selects a transcoding iterator to implement transcoding from the UTF
    input iterator to UTF-8 and noted that the input iterator might not produce UTF-8 code units.
  - Tom suggested a better name for such a function might be `to_utf8()`.
  - Zach explained part of the motivation for use of the `utf_iter` concept as in `as_utf8()`;
    since the algorithms work on code points, its use enables implicit conversions that would
    otherwise require an explicit call to `as_utf32()` or similar.
  - Jens acknowledged the utility of such conversions based on the `char8_t`, `char16_t`, and
    `char32_t`, but not for other types where the encoding is not clear.
  - Jens requested that a revision of the paper include a view that behaves similarly to existing
    views in the standard.
  - Jens also requested confirmation that normalization can be reasonably implemented as a view.
  - Zach replied that he did not implement normalization or collation as a view.
  - PBrett stated that collation can be performed by comparing two ranges.
  - Zach replied that it doesn't make sense to implement reduction as a view.
  - Zach stated that views didn't seem like a good match for normalization due to the state
    requirements.
  - Corentin reported success having implemented normalization as a view.
  - **Poll 2: UTF transcoding interfaces provided by the C++ standard library should operate
    on `charN_t` types, with support for other types provided by adapters, possibly with a
    special case for `char` and `wchar_t` when their associated literal encodings are UTF.**
    - Attendees: 9 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   5 |   1 |   0 |   0 |   1 |
    - Consensus in favor.
    - SA: There is a precondition that input is intended to be UTF-8 and that isn't avoided
      by adding a wrapper; this doesn't help programmers to find bugs.
  - **Poll 3: `char32_t` should be used as the Unicode code point type within the C++ standard
    library implementations of Unicode algorithms.**
    - Attendees: 9 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   6 |   0 |   1 |   0 |   0 |
    - Strong consensus in favor.
- Tom announced that the next meeting will take place 2023-04-26 and will include review of:
  - [P2741R1: user-generated static_assert messages](https://wg21.link/p2741r1).
  - [P2758R0: Emitting messages at compile time](https://wg21.link/p2758r0).


# March 22nd, 2023

## Agenda
- [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0).

## Meeting summary
- Attendees:
  - Charles Barto
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Mark de Wever
  - Nathan Owens
  - Peter Bindels
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0):
  - Zach provided an introduction:
    - The proposal provides interfaces to facilitate conversion between the UTF encodings.
    - The intent is to provide support for ranges and iterators equally well.
    - The proposed interfaces allow for use of SIMD operations with contiguous iterators.
    - Transcoding algorithms are also proposed.
    - Special accommodations are privided for easy use of null-terminated strings.
    - The ubquity of string literals and pointers to `char` motivates specialized interfaces.
    - The proposed interfaces constrain code unit types based on size, not particular
      character type.
    - Code unit types could also be constrained to particular character types but
      algorithms are generally not so constrained; this design is more general.
    - Most programmers are expected to use higher level interfaces, but these lower level
      interfaces enable specialized behavior; e.g., for text chunking.
    - A `null_sentinel_t` type and a corresponding `null_sentinel` variable enable
      generalized support for null terminated strings.
    - Additional utilities like `is_encoded` and `find_invalid_encoding` provide
      nice-to-have functionality.
    - The `transcode_to_utf8` and similar functions could be expanded to perform UTF
      validation without transcoding.
    - Transcoding iterators are provided for converting between UTF encodings.
    - Error handling is configurable, but only one error handling policy is currently
      specified; `use_replacement_character`.
    - Insert, front-insert, back-insert, and output transcoding iterators are specified
      with associated factory functions.
    - It is expected that the transcoding views would be most frequently used.
    - The `as_utf` family of functions return a type that, given a sequence of code units
      in one UTF encoding, provides a view of code units for another UTF encoding.
    - Formatter specializations are provided for the views.
    - The transcoding iterators wrap a range, not just a single iterator, because advancing
      the iterator might advance the underlying iterator multiple times thus requiring a
      sentinel to recognize the end of the underlying range.
    - Wrapping a transcoding iterator in another transcoding iterator yields a transcoding
      iterator from the base UTF encoding to the final one; this avoids accumulating multiple
      levels of wrapped iterators without requiring type erasure.
  - Fraser reported in chat that there is a stray single quotation mark in the `requires`
    expression in one of the `operator==` declarations for `utf_8_to_16_iterator` in section
    4.6.1, "First, the basic ones".
  - Jens stated that the proposed factory functions are probably not needed if support for
    class template argument deduction (CTAD) can be provided.
  - Zach replied that he added them to follow existing precedent in the standard but agreed
    they could be omitted.
  - Tom expressed surprise regarding the proposed behavior of `as_utf8()`; he expected a
    function with that name to provide a view that decodes UTF-8 from underlying data in
    order to produce code points.
  - Zach replied that the proposed `as_utf8()` design provides a view of UTF-8 code units
    (not code points) by transcoding from whatever encoding the underlying data is encoded
    in.
  - Jens stated that the proposed transcoding views (e.g., `utf8_view`) don't appear to
    function like other view adapters.
  - Hubert agreed and noted that, unlike other view or iterator adapters, it appears that
    these views place additional semantic requirements on the iterator template parameters.
  - Zach explained that, if `as_utf8()` is passed a pair of pointers to `char` that the
    iterator/sentinel pair is returned as is.
  - Hubert noted that, for `utf8_view`, that makes `utf8_iter` an odd choice of name.
  - Jens explained that requiring transcoding work to be performed by the provided
    `utf8_iter` is very surprising.
  - Zach replied that the design is similar to `std::ranges::filter_view`; that view uses a
    filter iterator.
  - Jens explained that there is a difference; `filter_view` defines a member type that
    functions as an iterator adapter and performs the work; in the proposed design, the user
    provided iterator does the work.
  - Hubert noted that, if the provided iterator does all the work, then the view doesn't
    adapt anything.
  - Corentin asserted that `utf8_view` does effectively the same thing that
    `std::ranges::subrange` does.
  - Zach replied that there is a difference in that the transcoding views add a constraint
    that the provided iterator satisfy `utf_iter`.
  - Fraser asked if it is intended that `as_utf8()` should be usable with, for example, a
    code page iterator that transcodes to UTF-8.
  - Zach replied affirmatively.
  - Corentin asserted that this design is a departure from prior ranges work.
  - Hubert observed that the transcoding algorithms, unlike the transcoding iterators, do
    not allow for an error handler to be provided and asked Zach to confirm that they are
    intended to be less customizable and that programmers can use iterators in a loop to
    satisfy custom requirements.
  - Zach confirmed and explained that the transcoding algorithms are intended to provide
    the functionality that is most often wanted, replacement character substitution, at
    high speed.
  - Hubert stated that support for segmented data that is not necessarily aligned on a code
    unit sequence boundary requires a way to store a partial code unit sequence so that it
    can be completed by the following segment rather than substituting a replacement character
    for the partial sequence.
  - Zach replied that a programmer could handle that requirement by checking that the segment
    ends with a complete code unit sequence by assigning an iterator to the end of the segment
    and decoding backwards.
  - Jens suggested another approach would be to signal the end of the sequence early and then
    check if the base iterator has reached its end.
  - Zach repled that adding additional semantics would complicate the usage experience.
  - Hubert noted that, with regard to performance considerations, the work that JeanHeyd has
    been doing in WG14 offers more flexibility for error handling.
  - Hubert asked if the transcoding iterator hierarchy unpacking is exposed such that a
    programmer could take advantage of it.
  - Zach replied that he had not considered exposing it, but that doing so is a possibility
    that could be looked into.
  - Zach agreed that it would be useful to have generalized support for such unpacking.
  - Tom directed discussion towards the notion of using `char32_t` as a general Unicode code
    point type.
  - Zach mentioned that his proposal uses `uint32_t`.
  - Robin noted that ICU's `UCHAR` type is an alias of `int32_t`.
  - Zach explained that the `value_type` of the UTF-32 iterators need only be a sufficiently
    sized integral type; not always a specific type like `char32_t`.
  - Zach argued that the design should allow adaptation to the types the programmer is using.
  - Jens asserted that the `value_type` of the UTF-32 converting iterators should be `char32_t`
    and that programmers can provide range wrappers for other types.
  - Steve expressed support for always using `char32_t` because doing so enables overloading
    without ambiguity.
  - Steve conveyed agreement with use of an adapter for other types.
  - Fraser also expressed support for use of the `charN_t` types with the rationale that
    programmers should not be punished for using the right types.
  - Fraser acknowledged that the design should not encourage casts.
  - PBindels stated in chat, "I value new code getting warnings / errors on bad conversions,
    over legacy code getting support without casts."
  - JeanHeyd reported that his implementation supports a configuration option that allows for
    use of a Unicode code point type other than `char32_t` and that every time he tries to
    exercise it that things break.
  - JeanHeyd provided a link in chat to the documentation for the configuration option;
    https://ztdtext.readthedocs.io/en/latest/config.html#config-ztd-text-unicode-code-point-distinct-type.
  - JeanHeyd added that, for older code bases, casts end up getting used regardless.
  - JeanHeyd suggested that, if a choice has to be made, `char32_t` be preferred but with a
    possible opt-in option for use of another type by a minority of users.
  - Zach stated that a template parameter could be added to types like `utf_8_to_32_iterator`
    to allow for a custom `value_type`.
  - Zach asserted that the `charN_t` types are fine in some cases, but that the community
    currently uses `char` and `wchar_t` for UTF-8 and UTF-16 respectively and that it would be a
    shame to force the `charN_t` types on such users.
  - Corentin stated that the choice of types accepted for input vs output are orthogonal.
  - Corentin asserted that it makes sense to specify a single type for the Unicode code point
    type for many uses, such as for working with EGCs and argued that `char32_t` is the right
    type.
  - Corentin noted that support for historical uses could hurt composability and stated that
    imposing questions of what type to use on programmers should be avoided.
  - Corentin admitted that few people use `char8_t` and `char16_t` and stated that we can accept
    use of `char` and `wchar_t` with the caveat that programmers don't understand what the
    associated encodings are.
  - Corentin expressed appreciation for the `charN_t` types having well-defined associated
    encodings.
  - Jens argued that the library is too large as currently proposed and that it needs to be
    pruned and made more orthogonal.
  - Jens insisted that we should be courageous; we are the standardization committee and we
    define what the future should look like.
  - Jens noted that the standard containers were forward looking and the legacy container-like
    libraries are all gone now.
  - Jens encouraged designing for composability by specifying elementary builing blocks that
    can be combined.
  - Jens asserted that it is ok if programmers are required to write a few wrappers for use
    with their existing projects.
  - Zach asked what Jens would suggest cutting.
  - Jens suggested removing the front, back, and insert iterators, perhaps in favor of a generic
    adapter that facilitates use with the existing front, back, and insert iterators.
  - Jens added that the full matrix of UTF converters should be avoided in favor of conversion
    from one UTF encoding to a code point sequence and then to another UTF encoding.
  - Jens expressed a desire for diagnostics on bad conversion as Peter Bindels mentioned in chat.
  - Zach asked if that would imply issuing diagnostics for input provided in other integer types.
  - Jens replied that a transform view can be used to explicitly support those cases.
  - Jens stated that he wants a view that works more like other views; not like `as_utf8` in
    this proposal.
  - Jens requested that range object adapters be proposed instead of functions.
  - Jens explained that functions are problematic because of argument dependent lookup (ADL) and
    that range object adapters avoid that problem.
  - Zach replied that his implementation uses customization point objects (CPOs), that the paper
    doesn't reflect that, but that it should.
  - Victor stated that the project he works on contains a massive amount of code that assumes
    data held in `char`-based storage is UTF-8; that and similar projects require first class
    support for use of UTF-8 with `char`.
  - Victor reported that his project has banned use of `char8_t` due to conflicts introduced when
    programmers tried to use it.
  - Victor stated that, based on his basic understanding of Zach's proposal, the proposed design
    accommodates such usage.
  - Tom asked Victor if such first class support could be conditionally provided based on the
    literal encoding being UTF-8.
  - Victor replied that doing so could make sense.
  - Victor indicated that, without good support for use of UTF-8 with `char`, his project would
    probably recommend against use of the facility.
  - Corentin reported having considered implicit first class support for UTF-8 and `char` when
    the literal encoding is UTF-8, noted that such code is not portable, but expressed hope that
    such code would fail compilation rather than produce mojibake.
  - Corentin suggested decreasing the size of the library by first focusing on a view and then
    adding eager converters and inserters later.
  - Corentin expressed appreciation for the focus on UTF encodings vs support for all encodings.
  - Tom stated that his and JeanHeyd's prior work on a `text_view` type that uses codecs
    satisfied a number of the composability concerns that Jens raised.
  - JeanHeyd agreed that codecs provide more flexibility.
  - JeanHeyd noted that bulk speed is attainable with his, Tom's and Zach's designs.
  - JeanHeyd stated that codecs impose performance overhead relative to iterators due to state
    management but that good QoI can mitigate those costs.
  - JeanHeyd observed that `short`, `int`, `wchar_t`, and other types have historically been used
    for text because the `charN_t` types weren't available.
  - JeanHeyd asserted that whether and how programmers migrate to `charN_t` types depends on how
    difficult we make such a transition.
  - JeanHeyd suggested that `charN_t` types be used by default due to their overloading abilities
    and strong encoding associations.
  - JeanHeyd declared that, for `char` and `wchar_t`, one has to assume an encoding and, most of
    the time, that works out ok, but when it doesn't, it is a problem.
  - JeanHeyd commented that the codec approach works well for handling `char` and `wchar_t`, but
    less well with iterators.
  - JeanHeyd insisted that the missing library support for `charN_t` is an impediment.
  - JeanHeyd reported that the work he is doing is more encompassing.
  - Fraser asked whether anyone has written a paper regarding the pain points with using the
    `charN_t` types.
  - Corentin replied that standard library support is missing.
  - Jens provided specific examples of missing support; `printf()`, `std::format()`, and
    `std::iostreams`.
  - JeanHeyd agreed that the most significant problem is the inability to conveniently print data
    held in those types.
  - Corentin agreed that the lack of support for `charN_t` types in `std::format()` is a big issue.
  - Steve replied that we would have to figure out what it means to print `char32_t`.
  - Tom suggested we might be able to specify it for `std::print()`.
  - Steve tentatively agreed but noted a need to consider locale impact.
  - Victor agreed that locale issues need to be addressed.
  - Steve noted that these are the reasons that Python 3 moved to the `C.UTF-8` locale by default.
  - \[ Editor's note: The Python 3 migration to the `C.UTF-8` locale was proposed in
    [PEP 538 (Coercing the legacy C locale to a UTF-8 based locale)](https://peps.python.org/pep-0538). \]
  - JeanHeyd noted that there is still a lot of code in the wild that assumes ASCII.
- Tom announced that the next meeting will be on April 12th and that we'll continue discussion of
  this paper.
- Tom suggested we should review the prior work on `text_view` given how long it has been since
  we've discussed it.


# March 8th, 2023

## Agenda
- [P2773R0: Considerations for Unicode algorithms](https://wg21.link/p2773r0).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Nathan Owen
  - Peter Brett
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
- [P2773R0: Considerations for Unicode algorithms](https://wg21.link/p2773r0):
  - PBrett introduced the agenda.
  - Robin provided an overview of tailoring:
    - \[ Editor's note: Robin shared his notes following the meeting; they can be found
      [here](https://docs.google.com/document/d/12fKu7-p35oH-sP06Hq4SzdZUbOzdtk9hHyCP4Abtl5g/edit).
      \]
    - Points 3 and 5 of the "TL;DR" portion of the paper are related to tailoring.
    - Normalization is noted as a priority in the paper and that is a good thing as there are
      examples of languages and products that do not handle normalization well.
    - The Unicode standard provides examples of tailoring, but those examples are not prescriptive.
    - Tailoring does not mean "language dependent"; it permits many kinds of transformations.
    - Case folding has exactly one case of language specific behavior; Turkic case folding.
      - "I" -> "ı" (U+0049 LATIN CAPITAL LETTER I -> U+0131 LATIN SMALL LETTER DOTLESS I)<br/>
        "İ" -> "i" (U+0130 LATIN CAPITAL LETTER I WITH DOT ABOVE -> U+0069 LATIN SMALL LETTER I)
      - ICU supports this behavior via a boolean flag on case folding interfaces.
      - Case folding was intended to support identifier equivalence.
    - NFKC case folding does not include language specific tailoring.
    - UAX #29 provides examples of language-dependent grapheme cluster tailoring, but at present,
      that isn't done in practice.
      - The CLDR technical committee is experimenting with a language-independent tailoring of
        grapheme clusters with a different behavior for Indic scripts. That work has not
        been forwarded to the UTC yet, but is intended to eventually be used as the new default
        default behavior.
      - Changes to
        [UAX #29 (Unicode Text Segmentation)](https://unicode.org/reports/tr29)
        are likely to be proposed.
    - ICU supports tailoring for line breaking beyond what is stated in the Unicode Standard:
      - Support for dictionary based layout for Thai.
      - Machine learning based layout for Burmese, Chinese, Japanese, and Thai.
      - Different line breaking rules for numbers.
    - Line breaking behavior can be script based as opposed to language based.
    - Case mapping includes language specific tailoring.
    - Collation is used for sorting, but is also used for case insensitive search:
      - The French word "ŒUF" is primary-equal to "oeuf" for collation, but case-folding would
        not produce a match.
      - The German word "fuer" matches "für" in German, but not in French.
  - Fraser shared in chat: "my favourite tailoring (for collation) is that in traditional name
    collation in Scotland, surnames starting "Mc" (e.g. McAdam) sort as if they begin "Mac"
    (so McAdam and MacAdam sort equivalently)."
  - PBrett noted that, in some Scandinavian dictionaries, words beginning with
    Å (U+00C5 LATIN CAPITAL LETTER A WITH RING ABOVE)
    get ordered differently when they correspond to a place name, but not otherwise.
  - PBrett added that, in Japanese, kanji have different meaning if they form part of a
    person's name as opposed to part of another word.
  - Corentin asked for examples of production systems that handle these cases correctly.
  - Robin replied that collation tailoring doesn't generally perform natural language processing,
    but noted that locale specifiers may include extensions for phone book order, dictionary
    order, or other ordering forms.
  - PBrett stated that it is common for programmers to want to sort in many different ways
    and shared examples of ordering by surname vs address.
  - Robin replied that the CLDR provides data for some of those applications and provided an
    example of ordering contacts for display on a phone.
  - Robin noted that the non-tailored collation algorithm will produce incorrect results for
    many languages but will still be more accurate than sorting by, for example, code point values.
  - Corentin asserted that collation support is necessary, but that it should not be considered
    high priority for now.
  - Corentin noted that support for collation is responsible for a significant proportion of the
    data included with ICU.
  - Robin stated that Swift supports non-tailored EGCs and both default and language dependent
    collation and case mapping.
  - Robin noted that Swift encountered some challenges with their EGC segmentation and regional
    indicators but have not, in general, had issues with instability and
    [UAX #29 (Unicode Text Segmentation)](https://unicode.org/reports/tr29).
  - Robin reported that, with highly unstable data, programmers will generally want to opt-in to
    updates independently of compiler upgrades.
  - Tom observed that might be an argument for providing Unicode versioned interfaces in some cases.
  - Robin agreed, but advised doing so only for highly unstable data.
  - Corentin asked about governance of the CLDR:
    - Is there a specification?
    - Is there a stability policy?
    - Could the CLDR be referenced from the C++ standard?
  - Robin replied that he does not think the CLDR has a stability policy.
  - Robin stated that the CLDR is released every six months, that it moves fast, and that it is
    maintained by its own committee within the Unicode Consortium.
  - Robin noted that the syntax used for the CLDR data is standardized via
    [UTS #35 (Unicode Locale Data Markup Language (LDML))](https://unicode.org/reports/tr35).
  - Tom asked if UTS #35 could be used as a specification to implement an interface to the CLDR as
    a data source.
  - Robin replied that it could be in principle but that compatibility problems might arise if the
    CLDR version is not aligned with the implemented version of UTS #35.
  - Corentin asked Robin if he agreed that it would be useful to add support for non-tailored case
    transformations in the near term.
  - Robin replied that doing so would be a considerable improvement over the status quo.
  - Robin noted that programmers that use the locale independent interfaces where they should not
    will attract appropriate attention from the internationalization proponents within their
    organization.
  - PBrett observed that there is a segment of programmers that might not care about collation
    being correct for various locales.
  - Corentin agreed and noted that ICU must be used today for locale specific support and then
    observed that having locale independent interfaces might prompt programmers to do the
    right thing.
  - Robin asserted that providing non-tailored interfaces would be benefitial and that the standard
    should note their appropriate use.
  - PBrett asked for comments regarding how tailored interfaces should be provided.
  - Corentin replied that tailoring has different requirements and requires different types.
  - Corentin suggested that such types can perhaps be hidden from programmers; for example, views
    that adjust the types used based on provision of a locale object.
  - PBrett asked if tailoring should be expressed via locale facets or if it is sufficiently disjoint
    from locale that it should have its own facility.
  - Corentin opined that we should not further build on `std::locale`, but that an interface that
    accepts some kind of locale object to opt-in to tailoring without other customization is possible.
  - Corentin noted that ICU4X allows customization via "providers" in addition to locale-based
    tailoring.
  - Corentin expressed uncertainty whether customization beyond locale-based tailoring should be
    provided.
  - Robin replied that tailoring is unbounded and thus too vast a concept to be used in an unqualified
    manner.
  - Robin stated that support for
    [UTS #35 (Unicode Locale Data Markup Language (LDML))](https://unicode.org/reports/tr35)
    would likely be required to do more, but that probably isn't feasible for the near future.
  - Corentin stated that `std::locale` facets support customization but that the design can't possibly
    account for all tailoring possibilities.
  - Corentin expressed a preference for an implementation-defined locale-based design.
  - Jens stated that tailoring appears to mean a lot of things, that it isn't clear why or how we would
    provide an interface, and that we are unlikely to specify use of an AI for line breaking.
  - Jens opined that tailoring appears to go beyond the existing facilities that do things like
    replacing "." with "," when formatting numbers.
  - Jens asserted that programmers can insert their own transformations and that the standard does not
    have to provide support other than via interoperability.
  - Jens opined that there is not a need to invest time in that direction now.
  - Jens agreed that there are likely cases that can be plausibly and meaningfully provided based on
    locale.
  - Jens expressed skepticism that we'll pursue a replacement for `std::locale` in the near term.
  - Jens expressed support for specifying some tailored algorithms when the tailoring can be specified
    with few parameters.
  - Hubert shared a perspective that `std::locale` facets are extensions of what C provides.
  - Hubert stated that it might have been a mistake to make `std::locale` extensible, but such
    extensions remain an option subject to the limitation that these objects are tied to the
    C locale ID.
  - Tom asked if there is reason to believe that it is not sufficient for programmers to be able to
    insert their own tailored transformations in pipelines that they construct.
  - PBrett pondered whether the standard library should include non-DUCET data.
  - \[ Editor's note: The Default Unicode Collation Element Table (DUCET) is decribed in
    [UTS #10 (Unicode Collation Algorithm)](https://unicode.org/reports/tr10). \]
  - Jens asked why we would provide data if we don't provide algorithms that use it.
  - PBrett replied that the availability of the data could enable programmers to use it to provide
    their own tailoring.
  - Corentin responded that, given an expectation that programmers provide their own algorithms,
    there is nothing to provide.
  - Corentin noted that the more we provide, the greater the risk that we'll have to break it later.
  - Corentin asserted that the CLDR data cannot be consumed in a similar manner to timezone data.
  - Tom suggested that such consumption should be possible with an implementation of the LDML.
  - Corentin responded that providing such an implementation is equivalent to implementing ICU.
  - Corentin shared an understanding that ICU's complexity is primarily due to integration with
    the CLDR.
  - Corentin expressed our task as determining how implementors can provide CLDR-based tailoring
    using ICU or ICU4X.
  - Corentin noted the implication with regard to portability and suggested ICU4X might provide
    a better building block.
  - Robin noted his own association with ICU4X and expressed its goal to improve portability based
    on a more flexible and modular design.
  - Robin stated that ICU4X does not offer strong stability guarantees.
  - Robin agreed with the perspective that implementing support for LDML is tantamount to
    implementing half of ICU.
  - Hubert noted that the existing C++ collation support is not customizable and that it simply
    exposes what is provided by the C library.
  - Jens suggested it might be feasible to provide the DUCET data in a pre-compiled form.
  - \[ Editor's note: doing so would potentially side step the LDML implementation concerns. \]
  - Jens noted that, for collation, we all have an intuitive understanding that languages work
    differently, but that such understanding is less clear for other algorithms.
  - **Poll 1: Papers proposing standard library Unicode algorithms should include a section
    discussing future extensions to support Unicode locale-based tailoring.**
    - Attendees: 10 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   5 |   0 |   0 |   0 |
    - Unanimous consensus in favor.
  - **Poll 2: It is a design goal that non-tailored standard library Unicode algorithms be efficiently
    implementable using ICU.**
    - Attendees: 10 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   2 |   1 |   3 |   1 |
    - No consensus.
  - Tom pondered concerns regarding ABI, ODR, and support for constant evaluation.
  - Corentin noted that we haven't discussed whether we want to support constant evaluation or not.
  - Corentin stated that the relevant ODR concerns are similar to those for `std::source_location`
    and that we strongly don't care about such violations.
  - Hubert expressed a desire to, from an implementation perspective, place much of the associated
    data in shared libraries and not have them exposed via header files.
  - Corentin suggested discussion is needed regarding freestanding support and how that impacts
    support for header-only implementations.
- Tom announced that the next meeting will take place on 2023-03-22 and that we'll start reviewing
  Zach's
  [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0).
  - PBrett noted that Zach's paper will provide additional fodder for discussing use of `char32_t`
    as a Unicode code point type and exposure of Unicode algorithms as views.


# February 22nd, 2023

## Agenda
- [P2773R0: Considerations for Unicode algorithms](https://wg21.link/p2773r0).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Nathan Owens
  - Peter Brett
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- [P2773R0: Considerations for Unicode algorithms](https://wg21.link/p2773r0):
  - PBrett suggested that Corentin provide a brief introductory overview by speaking to each of
    the points in the "TL;DR" section.
  - Corentin presented an overview:
    - The paper is guided by experience obtained through prototyping.
    - The paper is informed by expectations of performance requirements.
    - Views are a good fit for Unicode algorithms.
    - It is not clear what invariants would be desirable for a new text container.
    - Unicode does not impose constraints on what code points may follow other ones;
      new code points can be inserted effectively anywhere.
    - The paper assumes the availability of transcoding interfaces.
    - Normalization should be an early focus.
    - The existing interfaces for uppercase and lowercase operations in the C++ standard
      do not suffice to address the needs of all languages.
    - The existing interfaces for case insensitive operations in the C++ standard are
      likewise insufficient.
    - Text operations need to be easy for programmers to use with UTF-8 encoded text.
    - Interfaces for text operations should not be replicated for every encoding of
      Unicode code points.
    - It should be possible to, for example, perform casing and normalization operations
      without having to materialize a code point sequence in between the operations.
    - The standard lacks localization facilities sufficient to support tailoring.
    - Interfaces that support tailoring should be implemented using ICU4X.
    - Interfaces for the non-tailored algorithms may be provided as `constexpr` since
      they are locale invariant.
    - Providing views implemented with ICU would be challenging and would limit performance
      opportunities and iterator categories.
    - Interfaces that support tailored algorithms with an interface similar to that used
      for non-tailored interfaces can be added later.
    - Non-tailored interfaces are useful despite their being insufficient for user
      presentation purposes in general.
    - There are no known use cases for performing normalization for non-Unicode encodings
      like EBCDIC or Shift-JIS.
    - Code unit sequences should be validated by default on consumption; for safety reasons.
    - Standardized interfaces should not be constrained by what ICU is capable of providing.
    - Implementation via ICU should be supported when doing so doesn't limit potentially
      better solutions.
    - Implementation via ICU prohibits `constexpr` and `noexcept`.
    - Standardized interfaces should take advantage of ranges and views.
    - Size hints are useful for reserving memory in order to avoid reallocations.
    - It is important and reasonable to optimize table lookups for most character properties.
    - In place mutation of text does not perform well.
    - UTF decoding and encoding is inexpensive even when not optimized; it might not be
      necessary to design every interface to support maximum optimization possibilities.
  - Zach stated that normalization is a relatively expensive operation and is therefore best
    suited to eager transformations.
  - Victor commented in the chat that lazy operations often limit optimizations like SIMD.
  - Jens also commented in the chat that range filters are probably at odds with SIMD, noted
    that table lookups aren't SIMD-friendly, and pondered how much the Unicode algorithms
    benefit from SIMD.
  - Zach noted that maintaining multiple levels of enclosed iterators can be painful.
  - Zach reflected on prior discussions regarding requirements to be able to implement
    Unicode functionality using ICU and asked how important such implementability is.
  - \[ Editor's note:
    [P1238R1 (SG16: Unicode Direction)](https://wg21.link/p1238)
    lists as a constraint that implementors cannot afford to rewrite ICU. \]
  - Tom responded that his prior statements were partially motivated by politics; a desire
    to assure implementors that SG16's efforts would not culminate in a requirement for them
    to implement all Unicode functionality on their own.
  - PBrett indicated that he is not worried regarding implementability via ICU.
  - Tom noted that the pipeline approach presented in the paper allows combining
    transformations in ways that may be order dependent.
  - Tom asked Robin to confirm that case folding and normalization operations are order
    dependent.
  - Robin noted that case folding does not depend on tailoring and confirmed that there
    are order dependencies; `toCasefold(toNFKC(S))` does not produce the same result as
    `toNFKC_Casefold(S)`.
  - \[ Editor's note: In later correspondence, Robin noted that Turkic case folding
    (I -> ı, İ -> i) is usually not performed for non-Turkic languages as noted in
    [CaseFolding.txt](https://www.unicode.org/Public/UCD/latest/ucd/CaseFolding.txt). \]
  - Robin stated that, for canonical normalization, it is common to normalize at program
    boundaries, but that compatibility normalization might need to be done locally.
  - Tom noted the implication; programmers can't expect to combine transformations
    arbitrarily and get the "right" result.
  - Jens replied that this means special algorithms are needed for some transformations.
  - Jens stated that the range pipeline approach is idiomatic and seems amenable to these
    transformations.
  - Jens noted that ranges was tranformational in its ability to avoid the need for
    intermediate storage.
  - Jens cautioned that this ability comes with the cost that the transformations be
    interruptible.
  - Jens expressed appreciation for the syntax that views enable but that he would like to
    understand the performance trade off with respect to eager transformations.
  - Jens asserted it would be useful to have some performance data in a paper.
  - Jens acknowledged that normalization as a view adapter would require some local memory,
    but noted that might be cache advantageous.
  - Steve expressed concern over including normalization as a pipeline stage; if
    normalization iterators have to bounce between various buffers, performance may suffer.
  - Jens noted that views can be materialized when it is advantageous to do so.
  - PBrett reported that he has applications for normalization views.
  - Corentin stated that it is probably advantageous to materialize a view if it will be
    iterated more than once.
  - Corentin reported having implemented a normalization view and that he did not find the
    implementation to be too difficult.
  - Corentin noted that normalization can benefit from limits like those specified in the
    stream-safe text format.
  - \[ Editor's note: The stream-safe text format is described in
    [UAX #15 (Unicode Normalization Forms)](https://unicode.org/reports/tr15). \]
  - Corentin commented that normalization can be expensive, but only when transformations
    are actually necessary; characters corresponding to some of the `General_Category`
    classes can be recognized and copied without further lookup.
  - Victor stated that, with regard to implementability with ICU and the benefits of range
    based interfaces, good performance is more important.
  - Victor advised creating a reference implementation so that performance can be evaluated
    relative to ICU.
  - Victor noted that we do not want another experience like `std::regex` where the
    implementations available exhibit poor performance.
  - Zach reported having compared performance between his
    [Boost.Text](https://tzlaine.github.io/text/doc/html/index.html)
    implementation and ICU and found his implementation initially lagged ICU performance
    by 50 times.
  - Zach explained that he was able to improve performance after studying the implementation
    in ICU, but that his implementation was still 10 times as expensive as ICU.
  - Zach asserted that we should not expect implementors to match ICU performance.
  - Zach declared that we don't want to specify a facility that will pose a decade long
    implementation challenge as happened with `std::from_chars()` and `std::to_chars()`.
  - Zach noted that the lazy range approach can be implemented using ICU.
  - Zach suggested that we can specify both eager and view based implementations.
  - PBrett provided a use case for lazy normalization; Unicode regular expression matching
    can perform better with NFKD normalized text and it can be advantageous to only normalize
    until a match is found.
  - Corentin replied to Victor's request for a reference implementation that he would make
    his prototype work available, but that better implementations are possible.
  - Corentin expressed skepticism that there isn't room to improve on ICU performance.
  - Tom asked Robin if the CLDR follows BCP-47.
  - Robin replied that they are maintained in sync and that the CLDR uses some extensions
    defined in BCP-47.
  - Robin stated that, with regard to standardizing localization support, localization is
    fundamentally not stable since it tracks evolving human behavior.
  - Robin noted that, since the C++ standard is updated every 3 years, it will always trail
    localization changes.
  - \[ Editor's note: Robin noted in later offline discussion that CLDR releases occur at
    least every six months. \]
  - Tom asked if some of the locale properties specified in BCP-47 are stable.
  - Robin replied that BCP-47 specifies a syntax and that it has some stability assurances.
  - \[ Editor's note: Robin provided additional detail in offline correspondence following
    the telecon; The relation between Unicode language and locale identifiers and BCP-47 is
    documented in the "BCP 47 Conformance" section of
    [UTS #35 (Unicode Locale Data Markup Language (LDML))](https://unicode.org/reports/tr35)
    and stability is discussed in the "Stability of IANA Registry Entries" section of BCP-47
    in [RFC 5646](https://www.rfc-editor.org/rfc/rfc5646.html).
    The
    [ISO 3166](https://www.iso.org/iso-3166-country-codes.html)
    standard responsible for assigning country codes also implements a transition policy
    for changes to country codes as described at
    https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Transitional_reservations. \]
  - Corentin recalled discussion of Zach's papers in Issaquah and noted that the level of
    stability guarantees is not sufficient for ABI purposes.
  - Robin reported that the line breaking algorithm changes frequently but that other
    algorithmes, like grapheme breaking, change less frequently.
  - Robin advised focusing on use cases when considering the Unicode algorithms as different
    use cases may have different concerns.
  - Robin noted that case folding has stability concerns and that it is stable for NFKC
    normalized text.
  - Zach pondered whether it is reasonable to standardize something like a case-insensitive
    search.
- Tom reported that the next meeting will be 2023-03-08 and that we will continue discussion
  of this paper.


# February 1st, 2023

## Agenda
- [P2749R0: Down with ”character”](https://wg21.link/p2749r0).

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - Mark de Wever
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- Tom announced that this telecon is SG16's 100th!
- Corentin noted that LEWG is considering hosting an evening session in Issaquah to
  discuss Zach's 
  [P2728R0: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r0)
  and
  [P2729R0: Unicode in the Library, Part 2: Normalization](https://wg21.link/p2729r0)
  papers.
- Steve expressed support for early LEWG review so as to avoid a situation in which SG16
  forwards a paper with interfaces that LEWG does not approve of; such cases have occurred
  with other study groups.
- PBrett noted that there are sometimes competing perspectives between what domain experts
  value and what LEWG values.
- PBrett acknowledged the possibility that LEWG will approve of Zach's design, that SG16
  proceeds with making changes during its review, and that LEWG finds that it does not
  approve of the changed direction.
- [P2749R0: Down with ”character”](https://wg21.link/p2749r0):
  - \[ Editor's note: D2749R0 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2749R0 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Tom provided a summary of the last telecon.
  - Tom raised two concerns to be addressed.
    - Comments that Jens raised in a
      [post to the SG16 mailing list](https://lists.isocpp.org/sg16/2023/01/3693.php).
    - Whether the paper should take a dependency on
      [P2348 (Whitespaces Wording Revamp)](https://wg21.link/p2348).
  - Corentin explained that, with regard to Jens' concern about inconsistent use of the
    "Unicode code point" and "character" terms, that the changes made to mechanically replace
    "character" in 10-20 pages of wording were quite extensive.
  - Corentin stated that, in cases where the wording refers to a specific character, such as
    U+0020 SPACE, that the term "character" is appropriate.
  - Corentin acknowledged Jens' concerns, but noted that the updated wording does reduce
    ambiguity.
  - Corentin claimed that the proposal includes a minimal change and that additional changes
    could be done editorially at a later time.
  - Tom reported having spent time reviewing the changes and that he found the various uses
    of "Unicode scalar value", "Unicode code point", and "character" rather confusing.
  - Tom expressed concern that the differences are subtle and that it might be unfair to place
    the project editor in the position of having to deal with those differences; at least not
    without clearly specified guidelines.
  - PBrett responded that the project editor shouldn't make such changes since they can have
    normative impact.
  - Corentin reiterated that his goal with the paper is to remove the
    "translation character set" terminology in C++23 to avoid its appearance in new teaching
    materials.
  - Tom suggested modifying the paper title to append "in lexing" since that better matches
    the scope of the proposed changes.
  - Tom suggested reviewing the wording to ensure consistent terminology use.
  - The group started reviewing the changes to \[lex.phases\].
  - PBrett noted that people complain about the Unicode terms, but that their use is well
    justified in an international standard.
  - PBrett noted the use of "character" in association with new-line and asked whether new-line
    could consist of multiple code points.
  - Tom responded that, since the translation input is now specified in terms of Unicode code
    points, that we can define exactly what a new-line character is.
  - Hubert agreed and stated that would provide a better basis for defining whitespace.
  - Steve noted that `\n` can have platform impact in some contexts but that it doesn't in lexing.
  - Corentin replied that more significant changes would be required to substitute
    U+000A LINE FEED for "new-line character" and that there would still be remaining uses of
    "character".
  - PBrett stated it could be a conscious choice to leave those cases to a later paper like P2348.
  - Hubert responded that the motivation for asking for additional work is to avoid increasing
    internal friction within the standard wording as the paper does now.
  - Corentin expressed concern regarding incorporating work from P2348 due to concerns CWG had
    with that paper.
  - Steve noted that, in lexing context, specifying new-line is not observable.
  - Fraser asked if new-line characters are observable in raw string literals.
  - Hubert replied negatively and explained that, in a raw string literal, new-line is mapped to
    `\n` in the execution character set.
  - Steve stated issues with that were fixed.
  - Tom stated that there are related CWG issues.
  - \[ Editor's note: See
    [CWG issue 1655 (Line endings in raw string literals )](https://wg21.link/cwg1655)
    and
    [CWG issue 1709 (Stringizing raw string literals containing newline)](https://wg21.link/cwg1709). \]
  - Corentin pondered whether it is necessary to consider both papers at the same time.
  - Hubert recommended sending a message to the CWG mailing list to ask about that.
  - Corentin noted the substitution of a Unicode code point reference in place of
    "backslash character".
  - Corentin mentioned that the changes are intended to allow "code point" to be used
    for non-Unicode character sets; hence "Unicode code point" is used in contexts specific
    to Unicode.
  - Tom expressed uncertainty about the addition of "abstract" in \[lex.phases\]p1.
  - Corentin responded that abstract characters are used to explain mapping between
    character sets.
  - Tom agreed, but stated that wording is missing to tie the input to a sequence of
    abstract characters.
  - Fraser suggested adding a statement to specify that the lexer processes a sequence
    of Unicode code points.
  - Hubert noted that the current wording limits the effort required to document how input
    is mapped to a sequence of characters.
  - Corentin acknowledged that wording could be added to state that the implementation-defined
    mapping produces a sequence of Unicode scalar values.
  - Corentin pointed out how "space character" and "whitespace character" is used differently
    in \[lex.phases\]p3.
  - Mark observed that the changes to \[lex.phases\]p3 substituted "multi-Unicode code point"
    for "multi-character".
  - Hubert suggested substituting "token comprising multiple Unicode code points" instead.
  - Tom expressed support for substituting "U+0020 SPACE character" for "space character".
  - Corentin observed that "character" can be omitted in the substitution.
  - Hubert agreed.
  - Tom suggested that, in \[lex.charset\], "code points" could be substituted for "characters"
    in "The basic character set is a subset ... consisting of 96 characters".
  - Hubert replied that such a substitution would introduce a category error; the basic
    character set is intended to be a set of abstract characters and is used as such in
    some places.
  - Tom suggested "The basic character set is a subset of the abstract characters included in the
    Unicode character set".
  - Hubert suggested a simpler change; "the basic character set consists of the 96 characters
    specified in \[lex.charset.basic\]".
  - Tom stated that the changes to the note in \[lex.charset\]p6 should state "Unicode code point"
    instead of just "code point" for consistency.
  - PBrett opined that, with only 15 minutes remaining, that he did not think we'll be ready to
    forward the paper.
  - Tom agreed and stated that he doesn't feel that we have sufficiently reviewed the paper to be
    confident in polling it.
  - Tom noted that our goal is not to make a perfect standard, but rather to make improvements;
    we can poll forwarding it knowing that more work will be needed.
  - PBrett suggested polling to continue work and then poll a recommended resolution for the related
    NB comment in C++23.
  - Steve asked what the motivation is for getting this change in C++23.
  - Corentin responded that he is motivated to remove "translation character set" before it appears
    in training materials.
  - **Poll 1.1: P2749R0 "Down with 'character'" should be included in the IS only if the updates
    to whitespace specification described in P2348 "Whitespaces Wording Revamp" are also included.**
    - Attendees: 7 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   4 |   1 |   0 |   1 |
    - Weak consensus.
  - **Poll 1.2: Forward P2749R0 "Down with 'character'", revised as discussed, to CWG for C++23 as
    the recommended resolution of ballot comment FR-020-014.**
    - Attendees: 7
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   1 |   3 |   2 |   0 |
    - No consensus.
  - **Poll 1.3: Recommend rejection of ballot comment FR-020-014 as no consensus for change.**
    - Attendees: 7 (1 abstention)
      | F   | N   | A   |
      | --: | --: | --: |
      |   4 |   1 |   1 |
    - Consensus.
- Discussion ensued regarding how to prioritize papers for review following the Issaquah meeting
  and ended with the following tentative prioritization schedule:
  - [P2741R1 (user-generated static_assert messages)](https://wg21.link/p2741r1).
  - [P2758R0 (Emitting messages at compile time)](https://wg21.link/p2758r0).
  - [P2773R0 (Considerations for Unicode algorithms)](https://wg21.link/p2773r0).
  - [P2728R0 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728r0).
  - [P2729R0 (Unicode in the Library, Part 2: Normalization)](https://wg21.link/p2729r0).
  - [P2348R3 (Whitespaces Wording Revamp)](https://wg21.link/p2348r3).
  - [P2749R0 (Down with ”character”)](https://wg21.link/p2749r0).
- Tom announced that the next meeting will take place on 2023-02-22.


# January 25th, 2023

## Agenda
- Planning for NOT Issaquah.
- [P2736R0: Referencing the Unicode Standard](https://wg21.link/p2736r0).
- [P2749R0: Down with ”character”](https://wg21.link/p2749r0).

## Meeting summary
- Attendees:
  - Charlie Barto
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Nathan Owen
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- A round of introductions was conducted for Nathan; though he had attended previous
  meetings, we had never formally introduced ourselves.
- Planning for NOT Issaquah.
  - Tom explained that, due to competing priorities and a shortage of conference rooms,
    the only time slot available was for an evening session and, per previous discussion,
    an evening session time slot would be challenging for remote attendees; as a result,
    SG16 will not host an in-person meeting, but Tom is open to hosting another telecon
    next week before Issaquah to continue paper review.
  - Zach agreed with meeting next week, but argued that an in-person meeting in Issaquah
    should still be held.
  - PBrett opined that there would be few attendees.
  - Corentin stated that a number of people that will have opinions on his papers will
    be present in Issaquah.
  - Corentin asserted we should plan to meet in Varna.
  - PBrett stated that Zach's 
    [P2728R0: Unicode in the Library, Part 1: UTF Transcoding](https://wg21.link/p2728r0)
    and
    [P2729R0: Unicode in the Library, Part 2: Normalization](https://wg21.link/p2729r0)
    require SG16 review from an interface perspective.
  - Tom agreed with Peter.
  - Steve suggested that it would be useful to get early feedback from LEWG for Zach's
    papers.
  - Steve noted that we don't want to spend months in review and then have LEWG question
    the design later.
  - Corentin stated that we should ensure people are aware that these papers target
    C++26 and that time slots will be available in Varna and later meetings.
  - Steve agreed that we should not host an official SG16 meeting in Issaquah.
  - Tom stated that we will proceed with a telecon next week and no meeting in Issaquah.
- [P2736R0: Referencing the Unicode Standard](https://wg21.link/p2736r0):
  - Corentin explained the changes made, as suggested by Jens, to provide a definition
    for UCS-2 as needed for `std::codecvt_utf8` and `std::codecvt_utf16`.
  - Corentin stated that the UCS-2 definition is specified in terms of scalar values so
    as to exclude lone surrogates.
  - Corentin noted that the previous wording did not address how lone surrogates were
    to be handled.
  - Hubert suggested moving where "only" appears in the UCS-2 wording.
  - Corentin reported that various grammar and spelling issues pointed out by Jens were
    corrected.
  - Corentin stated that the prior discussion of the `__STDC_ISO_10646__` predefined
    macro was inconclusive.
  - Hubert recalled a suggestion to treat this macro the same as `__STDC_VERSION__`.
  - Fraser asked if `__STDC_ISO_10646__` could be removed from the C++ standard and
    noted that implementations could still define it since it is a reserved identifier.
  - Corentin expressed reluctance to doing so as part of this paper since this paper is
    not intended to make design changes.
  - Corentin stated that he plans to work with SG22 and WG14 regarding the intended use
    of the macro.
  - Corentin asserted that a minimal change suffices for now to remove the reliance on
    ISO/IEC 10646.
  - Hubert replied that the proposed change isn't the minimal solution since it diverges
    from the C standard.
  - Hubert clarified that the suggestion wasn't to reference the C standard, but rather
    to leave the definition rather meaningless so that implementors lean on C for meaning.
  - Corentin asked if the suggestion was to just make the macro implemenation-defined.
  - Tom replied that he thought that was what Fraser had suggested.
  - Fraser confirmed.
  - Jens asserted that the wording should preserve the condition that the macro, if
    defined, has a value with a particular syntactical form.
  - **Poll 1.1: Whether `__STDC_ISO_10646__` is predefined and if so, what its value is,
    are implementation-defined, retaining the mandated `yyyymmL` form.**
    - Attendees: 11 (3 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   6 |   2 |   0 |   0 |   0 |
    - Unanimous consent.
  - Hubert noted some existing occurrences of "Unicode encoding" in the wording for
    \[lex.string.escaped\].
  - Corentin reported that he did not see a reason to update that wording.
  - Hubert stated that the relevant encodings should be restricted to UTF-8, UTF-16,
    and UTF-23 because the formal definition of "Unicode encoding" is too inclusive.
  - Discussion ensued regarding encoding form vs encoding scheme and the observation
    that, for `std::format` with a wide format string, `wchar_t` elements correspond
    to an encoding form.
  - PBrett asked if the wording can just state "UTF-8, UTF-16, or UTF-32".
  - Corentin agreed to make that change.
  - Jens lamented the loss of wording in \[lex.name\] regarding what `XID_Start` and
    `XID_Continue` are and where to find their definitions.
  - Jens asserted a note should be retained to direct readers to their definitions.
  - Corentin opined that a note isn't needed since the terms are in a normative
    reference.
  - Jens replied that such a note is present for other properties such as
    `Grapheme_Extend`.
  - Corentin stated that he is fine with retaining a note.
  - PBrett asked about following the existing pattern in \[format.string.escaped\]
    for the `General_Category` and `Grapheme_Extend` properties where it is stated
    "as described by table 12 of UAX #44".
  - Zack expressed concern about the stability of text files.
  - Tom suggested more generic wording like "as described in the Unicode character database".
  - Jens agreed with that approach.
  - Fraser noted that internet searches for `XID_Start` yield good results.
  - Corentin edited the paper to update the wording.
  - **Poll 1.2: Forward P2736R1, amended as discussed, to CWG and LWG as the recommended
    resolution of NB comments FR-010-133 and FR-021-013.**
    - Attendees: 10 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   7 |   2 |   0 |   0 |   0 |
    - Unanimous consent.
- [P2749R0: Down with ”character”](https://wg21.link/p2749r0):
  - \[ Editor's note: D2749R0 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2749R0 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin provided an introduction:
    - The wording substitutes "Unicode scalar value" for "character" in many places, but
      retains the latter in some contexts.
    - This removes the "translation character set" indirection.
    - The changes were mechanically applied.
  - PBrett expressed support for the improved specificity.
  - Corentin began reviewing the wording changes.
  - Tom noted that Jens had previously requested an overview of the final state we are
    driving towards with these kinds of changes.
  - Corentin replied that the motivation section addresses some of those concerns.
  - Jens stated that he finds the proposed wording confusing since "character" ends up
    getting mixed in with Unicode terminology.
  - Corentin explained that he has concerns about introducing a lot of churn that doesn't
    help to improve clarity.
  - Fraser stated that additional specificity is probably needed to clarify which characters
    constitute new-line and whitespace.
  - Jens noted that, with the exception of new-line, that characters are specified using
    Unicode code points.
  - Jens noted that
    [P2348 (Whitespaces Wording Revamp)](https://wg21.link/p2348)
    is relevant.
  - Corentin explained that he intentionally did not modify the specification of whitespace
    in this paper.
  - Corentin expressed a desire for agreement on the replacement of
    "elements of the translation character set".
  - PBrett noticed an editorial issue in \[lex.charset\] for *n-char*; the updated wording
    retains "set" from the intended substitution of "Unicode code point" for
    "member of the translation character set".
  - Jens observed that a change in \[lex.phases\] to substitute "Unicode scalar value"
    for ".. elements of the translation character set" retains a reference to
    \[lex.charset\] that no longer makes sense.
  - Jens opined that the note in \[lex.charset\] that describes the difference between
    "code points" and "scalar values" should be retained.
  - Hubert stated that the location of that note is a little odd since it doesn't encapsulate
    the notion of "abstract character".
  - Hubert observed that the updates to \[lex.phases\]p3 only updated one of the two uses of
    "space character".
  - Corentin asked for opinions regarding a footnote in \[lex.name\] that discusses
    representation of characters outside the basic character set in external identifiers.
  - Hubert stated that the footnote could use some updates.
  - Tom opined that the footnote should just be removed.
  - Jens noted that
    [\[implimits\]p(2.6)](http://eel.is/c++draft/implimits#2.6)
    does specify a minimum limit for the number of significant characters in an external
    identifier.
  - PBrett stated that the the uses of "character" in that annex need to be addressed.
  - Corentin asked if CWG would be content with the removal of that footnote.
  - Jens replied that he does not know but that he personally does not see value in
    retaining it; the note probably serviced its value 20 some years ago.
  - Jens observed that "characters" would have to be interpreted as code points for the
    purposes of the external identifier limit.
  - Tom noted the implication that, if UTF-8 was used for the encoding of external identifiers,
    a worst case limit must be assumed such that a limit of 1024 code points implies a limit of
    4096 code units.
- Tom reported that SG16 will meet in one week, on 2023-02-01 in order to squeeze in one more
  review of P2749R0 before the WG21 meeting in Issaquah.


# January 11th, 2023

## Agenda
- Planning for Issaquah.
- [P2736R0: Referencing the Unicode Standard](https://wg21.link/p2736r0)
- [D2749R0: Down with ”character”](https://isocpp.org/files/papers/D2749R0.pdf)

## Meeting summary
- Attendees:
  - Corentin Jabot
  - Fraser Gordon
  - Hubert Tong
  - Jens Maurer
  - Mark de Wever
  - Mark Zeren
  - Nathan Owen
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- A round of introductions was held to welcome Fraser as a new attendee.
- Planning for Issaquah:
  - Tom expressed interest in holding a meeting in Issaquah despite neither he nor Peter
    Brett planning to attend in person.
  - Tom reported that Steve agreed to facilitate the in-person aspects of the meeting in
    Issaquah.
  - Tom suggested aiming for a half day on Thursday.
  - Tom asked who planned to attend in person; three people expressed such intent.
  - MarkZ reported that he would have a conflict at 3pm every day.
  - Discussion ensued regarding the merits of reserving a room vs planning for in-person
    attendees to join via Zoom.
  - Steve noted that Zach's recent and upcoming papers may attract more interest.
  - Zach noted that SG16 tends to attract a few additional attendees beyond the regulars.
  - Tom stated he would request a room.
- [P2736R0: Referencing the Unicode Standard](https://wg21.link/p2736r0):
  - Tom summarized the discussion from the
    [2022-12-14 SG16 telecon](https://github.com/sg16-unicode/sg16-meetings#december-14th-2022)
    concerning the `__STDC_ISO_10646__` predefined macro.
  - Corentin provided an introduction.
  - Corentin reported having reviewed the terminology from the Unicode Standard to identify
    wording changes to be made.
  - Corentin explained that ISO/IEC 10646 uses "character" in its wording, but that the
    proposed wording uses "abstract character" when appropriate.
  - Corentin noted that "character" is retained for uses such as "character type".
  - Hubert stated that the "abstract character" definition from the Unicode Standard can be
    broadly applied and thus should only be used when a broad interpretation is actually
    intended.
  - Corentin replied that "abstract character" is relevant when mapping between different
    character sets.
  - Corentin indicated that "abstract character" only ended up being used in one place.
  - Jens asserted there is a need for a term to express equivalence between characters.
  - Tom agreed and noted that "abstract character" is useful when there is more than one
    possible encoding for the same character; as in Unicode normalization forms.
  - Hubert acknowledged that "abstract character" would be appropriate for the mapping of
    source code characters to the translation character set.
  - Jens suggested that is a QoI concern since translation phase 1 behavior is
    implementation-defined.
  - Hubert agreed use of the term could be avoided there if desired.
  - Corentin explained that the C++ standard currently contains two normative references
    to ISO/IEC 10646, one of which is to an obsolecent version for a definition of UCS-2;
    the proposed wording replaces references to UCS-2 with a restricted form of UTF-16.
  - Corentin stated that references to the Unicode Standard are inclusive of the
    annexes; normative references to the annexes are therefore removed.
  - Corentin reported that many of the changes are mechanical; "UCS" was replaced with
    "Unicode".
  - Corentin noted that the control code alias names table was removed following discussion
    on the SG16 mailing list.
  - Steve pondered whether notes should be added to the C++ standard that explain where
    to find information in the Unicode Standard.
  - Corentin replied that doing so can be useful; for example for `NameAliases.txt`.
  - Hubert stated that "UCS Encoding Form" is more restrictive than "Unicode Encoding Form";
    the latter isn't limited to the common UTF encodings..
  - Mark asked if that terminology should not then be changed.
  - Hubert replied that it might be necessary to add constraints or to find another way to
    identify the relevant encodings.
  - Mark suggested that the first heading in Table 1 in \[lex.charset\] could be changed to
    "abstract character".
  - Jens objected and explained that the first column lists code points and the second
    column lists names; these are concrete character references.
  - Corentin replied that he had not felt a need to change the use of "character" in that
    table heading.
  - Jens stated that the change to remove the control code alias table changes the
    specification with regard to allowances for the "BELL" and "ALERT" names.
  - Corentin replied that wording was added to restrict alias names to those that are
    specified as "control", "correction", and "alternate".
  - Jens noted that the code page chart appears to list "BELL" as a control name, but
    in a confusing way that is inconsistent with the names in `NameAliases.txt`.
  - \[ Editor's note: The discussion of "BELL" and "ALERT" centers around how the Unicode
    Standard presents the alias names for U+0007. The
    [C0 Controls and Basic Latin PDF](https://www.unicode.org/charts/PDF/U0000.pdf)
    displays as follows.

        0007  <control>
                = BELL

    [`NameAliases.txt`](https://www.unicode.org/Public/UCD/latest/ucd/NameAliases.txt)
    is more clear in its intent:

        # Note that no formal name alias for the ISO 6429 "BELL" is
        # provided for U+0007, because of the existing name collision
        # with U+1F514 BELL.
        
        0007;ALERT;control
        0007;BEL;abbreviation

    \]
  - Tom summarized the concern; implementors might look at the code page charts and
    become confused or implement something other than what is intended.
  - Corentiin replied with doubts that implementors would base their implementations
    on the code page charts.
  - Zach asked if the intent can be made more explicit by reintroducing a note to
    direct readers to `NameAliases.txt`.
  - Jens replied that a note would be helpful and that be believes the existing table
    was originally built from content in `NameAliases.txt`.
  - Steve suggested amending the proposed "control, correction, or alternate" wording
    to add "as specified in `NameAliases.txt`".
  - Jens expressed concern about duplicating content from the Unicode Standard.
  - Zach suggested retaining the prior "These names are derived from the Unicode
    Character Database's `NameAliases.txt`" wording but with "derived" removed.
  - Corentin agreed to make a change.
  - Jens stated that references to the Unicode Standard should have "the" capitalized.
  - Tom expressed a preference in favor of "Unicode code point" over
    "Unicode scalar value" with the latter reserved for use in expressing requirements.
  - Zach expressed indifference and noted that UCD properties won't be present for
    surrogate code points.
  - Hubert stated that use of "Unicode scalar value" has the advantage of avoiding the
    question of whether non-scalar values need to be considered in the given context.
  - Steve noted that "Unicode scalar value" implies a precondition that, if violated,
    could lead to undefined behavior.
  - Jens suggested that references to chapters of the Unicode Standard should use both
    numbers and names for resiliency against changes.
  - Corentin explained that references to UCS-2 were replaced with references to UTF-16
    with additional restrictions to limit encoded characters to those in the BMP.
  - Fraser replied that there is a semantic difference since UCS-2 allowed encoding
    surrogate code points.
  - Corentin responded that the previous wording was not clear how such code points were
    to be handled.
  - Hubert pointed out that, in the proposed wording for the `codecvt` facets, the
    first bullet describes the artifacts produced by an encoding where as the second
    bullet names an encoding.
  - Hubert stated that both bullets should be written such that they can be easily read
    as specifying encodings.
  - Jens suggested retaining UCS-2 teminology by adding a definition of it that specifies
    it as a restricted form of UTF-16.
  - Zach expressed a preference for the currently proposed wording with the category error
    corrected.
  - Hubert suggested that the wording state that the facet only maps from that code point
    range and nothing else.
  - Tom observed that, if the UTF-8 text has characters that map outside the BMP, the
    wording doesn't say what happens.
  - Hubert stated that we need to make it clear that just converting to UTF-16 isn't
    acceptible.
  - Corentin explained that he did not remove the UAX #31 reference since Steve is working
    on related changes.
  - Corentin expressed uncertainty whether a separate UAX #31 reference is needed.
  - Corentin observed that some unintended `tcode` LaTeX markup appears in one of the
    bibliography entries proposed for removal.
  - Zach returned discussion to the `__STDC_ISO_10646__` predefined macro, noted that it
    is inherited from C, and opined that there is nothing to be done for it.
  - Jens replied that the wording essentially states that `wchar_t` must be at least 21
    bits for the macro to be defined.
  - Hubert observed that the proposed change loses the requirement that storing a wide
    character stores a value that matches that character's Unicode scalar value.
  - Hubert explained that this behavior is the design flaw that makes it not possible for
    a compiler to predefine this macro; the value held in an object of type `wchar_t` has
    a locale dependent interpretation.
  - Zach suggested that restricting the implication to the encoding of wide character
    literals might be an improvement.
  - Hubert suggested this might be a matter worth discussing in SG22.
  - Zach asked if the wording could just defer to the C standard.
  - Jens replied that we can do so for library wording, but not for core wording.
  - Jens stated that we could match the wording in the C standard.
  - Steve noted a misspelling of 10646 in the first paragraph of the Motivation section:
    "10446".
- [D2749R0: Down with ”character”](https://isocpp.org/files/papers/D2749R0.pdf):
  - Discussion was postponed due to lack of time.
- Tom reported that the meeting will be on 2023-01-25 and will prioritize further review
  of P2736R0 and then D2749R0.


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
