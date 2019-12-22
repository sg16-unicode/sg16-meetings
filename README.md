# SG16 Meeting Summaries

SG16 meetings are typically held on Wednesdays from 3:30pm-5:00pm EST5EDT4 on the 2nd
and 4th weeks of each month, but scheduling conflicts or other time pressures sometimes
force alternative scheduling.  Meeting invitations are sent to the mailing list and
prior attendees.

The next SG16 meeting is scheduled for Wednesday, January 8th 2020, from 3:30-5:00pm EST.

- [December 11th, 2019](#december-11th-2019)
- [November 20th, 2019](#november-20th-2019)
- [October 23rd, 2019](#october-23rd-2019)
- [October 9th, 2019](#october-9th-2019)
- [September 25th, 2019](#september-25th-2019)
- [September 4th, 2019](#september-4th-2019)
- [August 21st, 2019](#august-21st-2019)
- [July 31st, 2019](#july-31st-2019)
- [June 26th, 2019](#june-26th-2019)
- [June 12th, 2019](#june-12th-2019)
- [May 22nd, 2019](#may-22nd-2019)
- [May 15th, 2019](#may-15th-2019)
- [April 24th, 2019](#april-24th-2019)
- [April 10th, 2019](#april-10th-2019)
- [March 27th, 2019](#march-27th-2019)
- [March 13th, 2019](#march-13th-2019)
- [February 13th, 2019](#february-13th-2019)
- [January 23rd, 2019](#january-23rd-2019)
- [January 9th, 2019](#january-9th-2019)
- [December 19th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#december-19th-2018)
- [December 5th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#december-5th-2018)
- [October 17th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#october-17th-2018)
- [October 3rd, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#october-3rd-2018)
- [August 29th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#august-29th-2018)
- [July 25th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#july-25th-2018)
- [July 11th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#july-11th-2018)
- [June 20th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#june-20th-2018)
- [May 30th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#may-30th-2018)
- [May 16th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#may-16th-2018)
- [April 25th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#april-25th-2018)
- [April 11th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#april-11th-2018)
- [March 28th, 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md#march-28th-2018)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# December 11th, 2019

## Draft agenda:
- Vocabulary type(s) for extended grapheme clusters?
  - Per Michael McLaughlin's questions posted to the (old) mailing list on 11/01.
- P1097: Named character escapes
  - Review research on minimizing the name lookup DB and code size.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - David Wendt
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- [1097: Named character escapes:](https://wg21.link/p1097)
  - Tom introduced the topic:
    - Since our last meeting, Corentin did some outstanding investigative and evaluation work and blogged
      about his results:
      - https://cor3ntin.github.io/posts/cp_to_name
    - Corentin's implementation of his size reduction techniques is available at:
      - https://github.com/cor3ntin/ext-unicode-db/tree/name_to_cp
    - The goal for today is to review his results and determine next steps.
  - Corentin opined that the data is still kind of large at approximately 260K.
  - Zach noted that Corentin did a good job of estimating a theoretical lower bound for reducing the data
    at around 180K, so achieving a result of 260K is great.
  - Steve commented that the code shows the challenges C++ has with variable length data.  The natural
    representation would use variants, but that can't be represented as well.
  - Corentin agreed noting that good performance demands working at the byte level.
  - Zach expressed a similar experience working on [Boost.text](https://github.com/tzlaine/text); flat arrays
    of bytes had to be used to achieve scaling goals.
  - Tom stated that we need to draft a revision of this paper and that he is happy to do so, but would welcome
    any other volunteers.
  - Corentin asked if we know how to get in touch with Martinho.
  - Tom responded that he tried, but did not get a response.
  - Tom noted that, if we can't get in touch with Martinho, then we'll need to submit a new paper rather than
    a new revision.
  - Corentin asked if a new paper was really necessary.
  - Steve responded that, as a matter of procedure, we need a new paper to get it on the schedule.
  - PeterBi added that we need a place to record the new information.
  - Tom stated he would attempt to contact Martinho again.
  - \[Editor's note: Tom did reach out again via email, but again did not get a response. \]
  - Tom asked Corentin if he wanted to take this and run with it given the considerable investment he has already
    made.
  - Corentin responded that he is unfortunately time constrained.
  - Corentin mentioned that the new paper should state the need for matching name aliases and case insensitivity.
  - Tom agreed and noted that we have polls on those topics from presentation to EWGI in San Diego that record
    a trail of intent for those cases.
  - Zach asked Corentin if dashes are handled properly in his experiment.
  - Corentin replied affirmatively that spaces, dashes, and underscores can be omitted or swapped as recommended
    by Unicode in [UAX44](https://unicode.org/reports/tr44/#Matching_Names).
  - Corentin added that the current 260K size includes support for name aliases.
  - Steve observed motivation for allowing spaces, dashes, and underscores to be swappable; that behavior falls
    out of a good implementation.
  - Corentin stated that, should a desire arise to be able to map code points to names, then a different
    implementation would provide a more optimized data set that handles mapping both directions.
  - Tom asked Corentin for an estimated size for a perfect hash approach.
  - Corentin responded with 300K to 400K.
  - Corentin pointed out a potential challenge; that it may be desirable to support code point to name mapping
    in the standard library, but probably not in the compiler.  This implies a potential need for the Unicode
    character name data to be available to both.
  - Steve stated that it seems unfortunate to not expose the compiler data to the library.
  - Corentin suggested the data would probably need to be present in both the compiler and the library.
  - Tom provided a possible way to avoid that; by making it available in the library, but accessible from the
    core language.  At least one EWG member strongly advocated for such an approach; a string interpolation like
    facility.
- Vocabulary types for extended grapheme clusters:
  - Tom introduced the topic:
    - Michael McLaughlin had posted some questions to the (old) mailing list on 2019-11-01:
      - http://www.open-std.org/pipermail/unicode/2019-November/000868.html
    - These questions are related to representation of extended grapheme clusters (EGCs), specifically, how a
      collection or sequence of them might be stored.
    - Should the standard library provide vocabulary types for EGCs?
  - Zach explained the choices he made for [Boost.text](https://github.com/tzlaine/text).  There are two vocabulary
    types; [grapheme](https://github.com/tzlaine/text/blob/master/include/boost/text/grapheme.hpp#L25-L115) provides
    value semantics and stores a small vector optimized sequence of code units with a maximum size limited according
    to the
    [Unicode stream-safe text format described in UAX #15](https://unicode.org/reports/tr15/#Stream_Safe_Text_Format),
    and
    [grapheme_ref](https://github.com/tzlaine/text/blob/master/include/boost/text/grapheme.hpp#L120-L163)
    provides read-only reference/view semantics over a code point range denoted by an iterator pair.
  - Zach added that he is unsure if anyone is using the value type.
  - Corentin acknowledged the uncertainty regarding use cases for a value type.
  - Corentin asked why the reference/view version is not an alias of a span.
  - Zach responded that he wanted to support subranges and non-contiguous storage.  The implementation uses the
    `view_interface` CRTP base from C++20 ranges.
  - Steve asked who the anticipated consumers are for use of EGCs.
  - PeterBr expressed similar curiosity and provided some background experience; he previously worked on a product
    that was text based and everything was done on graphemes.  Support was available for individual grapheme
    replacement, but a value type was never needed because reference/view semantics were always desired.  All text
    processing was performed in terms of ranges of graphemes.
  - Zach offered a couple of examples.  Text rendering depends on knowledge of EGC boundaries.  Additionally, an
    EGC reference is the value type of an (EGC-based) iterator on a text range.
  - Zach observed that breaking algorithms don't always break on EGC boundaries, though split EGCs still remain
    EGCs on either side of the boundary.
  - Steve stated that having a named type is very useful.  An EGC view is essentially a subrange, but naming it is
    useful.
  - PeterBr clarified that an EGC is effectively a range of code points.
  - Tom asked if there is a good distinction between an EGC type that represents a range of code units or code points
    that constitute exactly one grapheme vs a type that represents a range of EGCs in terms of a range of code units
    or code points.
  - Zach replied yes, [Boost.text](https://github.com/tzlaine/text) has a type that represents the latter case as well;
    [grapheme_view](https://github.com/tzlaine/text/blob/master/include/boost/text/grapheme_view.hpp#L23-L89) is a
    view that provides an EGC iterator.  So, yes, there are three potentially useful types: an owning EGC, a
    reference EGC, and an EGC view.
  - Steve asked how breaking algorithms that split EGCs interact with these types.
  - Zach replied that all Unicode algorithms are specified in terms of code points, not EGCs.  So, a split EGC just
    becomes two EGCs.  The sentence breaking algorithm may cause this to happen.
  - Tom recalled prior conversations where we discovered that the EGC sum of the parts of a text may be greater than
    the EGC sum of the whole text.
  - Steve asked for confirmation that you can still view the split code point ranges as EGCs.
  - Zach confirmed, yes.
  - Corentin asked if all of these types aren't effectively subranges.
  - Steve replied yes, but different types is useful to avoid subranges of subranges.
  - Corentin countered that, if you have a `text_view` and you split it, you get a `text_view`.
  - Zach stated that the idea that the Unicode algorithms produce sequences of code points but programmers want
    EGCs is a key idea.
  - PeterBr observed that rendering text requires more than just EGCs.
  - Steve returned converation to the motivation for EGC types and mentioned the DB field example; there is a known
    limit of how many bytes can be stored, EGCs indicate where text should be truncated to.
  - Tom asked if there is a need to distinguish between an EGC view and a subrange of EGC view other than an EGC
    reference; as Corentin mentioned, a subrange of a `text_view` is a `text_view`, so is a subrange of an EGC view
    an EGC view?
  - Zach stated he didn't see a need for such a distinction.  Most interfaces should operate on EGC views, but for
    Unicode algorithms, it is necessary to drop down a level to a code point view.
  - Steve summarized; an EGC reference is a view over code points with a contract that its range represents exactly
    one EGC.
  - PeterBr imagined a scenario in which a range of code points is sliced to produce multiple EGCs, but when
    recombined with additional text, might yield different EGCs.
  - \[Editor's note: Some discussion was missed here. \]
  - Tom stated a need for consistent terminology.  Tom originally proposed `text_view` as a sequence of code points,
    but we now think it should be EGC based.
  - PeterBr expressed concern; most people think they want code points.  LEWG might object to an EGC based design.
  - Zach stated that a concern we have is that we're the Unicode experts and everyone with strong opinions is pretty
    much on this call; we need to be aware of echo chamber issues.
  - Tom added that echo chamber issues are the thing that keeps me up at night; how do we ensure we deliver what is
    truly useful?
  - Steve added that he frequently is asked why some simple thing isn't implemented.  The answer is, because it isn't
    actually simple.
  - Corentin stated that he gets quite concerned whenever we discuss going in a direction that doesn't align with
    Unicode recomendations; the UTC (Unicode Technical Committeee) doesn't get things wrong very often.
  - Steve noted that, fortunately, we're kind of late to the game, we can learn from the experience of other languages,
    and we don't have to discover all the problems ourselves.
  - Tom returned discussion to the subrange of subrange concern; there may be a need to put subranges back together.
  - Corentin replied that there is an ongoing effort to support that, but it is complicated.  JeanHeyd is working on
    [P1664](https://wg21.link/p1664) and it should be discussed more in Prague.
  - Steve described one of the challenges; for efficiency, when we have an EGC view and want to get down to the code
    unit range for efficient IO, reassembly can get difficult.
  - Zach replied that, if you have an EGC view over a code point view over a sequence of code units, that is easy.
  - Tom countered that doing so requires that you know that the underlying storage is contiguous if you want to
    operate on it at the code unit level.
  - Steve added that there can't be a missing range in the middle.
  - Corentin expressed a belief that this will be solved; maybe not for C++20, but for C++23.
- Tom stated that our normal meeting cadence would have us meeting again on December 25th 🎅, but expected meeting that
  day would be unpopular, so we'll plan to meet next on January 8th.


# November 20th, 2019

## Draft agenda:
- Belfast follow up and review.
- Volunteers to draft a library design guidelines paper.

## Meeting summary:
- Attendees:
  - JeanHeyd Meneide
  - Mark Zeren
  - Steve Downey
  - Tom Honermann
  - Yehezkel Bernat
  - Zach Laine
- [P1868 - 🦄 width: clarifying units of width and precision in std::format](https://wg21.link/p1868):
  - Tom introduced the topic:
    - Concerns were raised in Belfast with regard to the stability of the proposed code point ranges to be
      used for display width estimation.  The currently proposed ranges map all extended grapheme clusters
      (EGCs) to a display width of one or two despite there being a number of known cases of EGCs that consume
      no display width (e.g., `U+200B {ZERO WIDTH SPACE}`) or more than two display width units
      (e.g., `U+FDFD {ARABIC LIGATURE BISMALLAH AR-RAHMAN AR-RAHEEM}`).
    - Additionally, the EGC breaking algorithm is dependent on Unicode version and the proposed wording does
      not specify which version of Unicode to implement.  Concerns were raised regarding having a floating
      reference to the Unicode standard and the potential for differences in behavior across implementations
      if the Unicode version is implementation defined and subject to change across compiler versions.
    - How should we address these concerns?
  - Zach commented that the wording review went through LWG ok and that he had posted a message to the LWG
    mailting list responding to one concern that was raised.
  - Zach reported that Jonathan Wakely stated that floating references to other standards are not permitted
    but that implementors can, as QoI, offer support for other versions.
  - Tom expressed surprise regarding that restriction given that we have a floating reference to ISO 10646
    in the working paper today.
  - Zach responded that LWG stated a requirement for a normative reference and is therefore planning to add
    a normative reference to Unicode 12 with the intent that we update the normative reference with each
    standard release.
  - Tom asked that, if we reference a particular version, can implementations use a later version and remain
    conforming.
  - Zach responded that doing so seems to be acceptable to implementors.
  - Steve remarked that CWG expressed a preference for a floating reference.
  - JeanHeyd confirmed and added that is how the working paper ended up with the floating reference to ISO 10646.
  - Zach said he will follow up about this discrepancy.
  - Mark asked if we have a preference for floating vs fixed.
  - Zach responded that implementations will do what they need to do for their users.
  - Tom turned the discussion back to concerns raised by Billy regarding changes to the width estimate algorithm
    being a breaking change; e.g., changing the width estimate for a given EGC.  This is a related but distinct
    concern from the EGC algorithm changing due to a change in Unicode version.
  - Zach stated that `U+FDFD` is an example of something we need to fix that can also be a breaking change.
  - Steve repeated that the concern is basically any change in behavior potentially resulting in a surprising or
    undesirable change.
  - Mark asserted that we're going to continue having difficulties with dependencies on Unicode data and that the
    situation is analagous with respect to the timezone database.  Implementors can enable stable behavior by
    allowing choice of Unicode version.
  - Steve noted that the rate of change of the Unicode standard has skewed towards stability.
  - Mark opined that we should not solve this problem in the standard.
  - Tom agreed and added that we can specify a minimum version, but leave the atual version implementation defined.
  - Mark asked which version of the Unicode standard the proposed code point ranges were pulled from.
  - Tom responded that the Unicode standard doesn't contain character display width data and that these were
    extracted from an implementation of `wcswidth()`.
  - Steve stated that he maintained a list of double wide characters for years and that it was not a significant
    burden.
  - Tom stated that his desire for a floating reference to the Unicode standard with an implementation defined
    choice of version is intended to allow implementors to keep up with new Unicode versions.  Unicode releases
    happen every year while C++ standards are only released every three years.  Implementors probably can't lag
    Unicode by three years.
  - Zach acknowledged the goal and stated that will result in some implementation divergence as some implementors
    will keep up and some won't, but that the differences are likely to be minor.
  - Tom asked if ISO 10646 annex U constitutes a reference to [UAX#31](http://www.unicode.org/reports/tr31).
  - Steve suggested this is probably a beuracratic issue and added that having a normative reference is helpful.
  - Zach responded that it could be harmful if we get cconflicting floating and non-floating references for
    ISO 10646 vs Unicode, but this should fall to LWG and CWG to decide.
  - Tom asked how we should go about fixing the currently proposed width estimates since the proposed ranges are
    clearly missing support for cases of zero width or width greater than two.
  - Zach opined that he wasn't sure there is a problem to be fixed since what is specified matches existing practice.
  - Tom asked if we know where this implementation of `wcswidth()` came from and how widely deployed it is.
  - Zach suggested asking Victor.
  - \[Editor's note: According to [P1868R0](https://wg21.link/p1868r0), the implementation of `wcswidth()` is the
    one at https://www.cl.cam.ac.uk/~mgk25/ucs/wcwidth.c. \]
  - Tom asked for opinions regarding writing a short paper that explains the Unicode stability guarantees and argues
    for floating references and implementations.
  - Zach suggested waiting for a more motivating reason to do so.
- [P1949 - C++ Identifier Syntax using Unicode Standard Annex 31](https://wg21.link/p1949):
  - Tom introduced the topic:
    - EWG rejected the SG16 guidance offered in response to NB comment
      [NL029](https://github.com/cplusplus/nbballot/issues/28) to deprecate identifiers that do not conform to
      [UAX#31](http://www.unicode.org/reports/tr31) with noted exceptions for the `_` character.
    - A suggestion was made that a CWG issue be filed to consider the lack of updates to the allowed identifiers
      since C++11 as a defect.
    - Tom agreed to file a core issue and started to do some research.
    - According to [N3146](https://wg21.link/n3146), the original identifier allowances appear to have been
      aggregated from various sources including
      [UAX#31](http://www.unicode.org/reports/tr31) and
      [XML 2008](http://www.w3.org/TR/2008/REC-xml-20081126/#sec-common-syn), and following guidance in
      annex A of a draft of
      [ISO/IEC TR 10176:2003](http://www.open-std.org/JTC1/sc22/WG20/docs/n970-tr10176-2002.pdf).
    - Thank you to Corentin for quickly providing a way to query the code point ranges that have the `XID_Start`
      or `XID_Continue` property set.  https://godbolt.org/z/h7ThEh.  These ranges differ substantially from
      what is in the current standard.
    - What should the proposed resolution for the core issue be?
  - Steve stated that [UAX#31](http://www.unicode.org/reports/tr31) permits extensions, and what was adopted for
    C++11 effectively whitelisted a large set of code points.
  - Zach asked what EWG's concern was.
  - Steve replied that they were nervous about such a late change and want more time to think it through.
  - Zach opined that this seems like something better addressed in C++23.
  - Steve noted that what is done can be back ported to prior standards though, that Clang and gcc support
    Unicode encoded source code \[Editor's note: so does MSVC \], and that the longer we wait to address this,
    the more code we potentially break.
  - Tom stated that, from the DR perspective, we could either figure out what we want for C++23 and recommend
    that as the proposed resolution, or we can do a more targetted fix for C++20 for specific problematic
    cases knowing that we'll likely do differently for C++23.
  - Steve stated that the only difference C++ needs from [UAX#31](http://www.unicode.org/reports/tr31) is support
    for `_`, and such an extension is conforming.  It would also be ok to restrict identifiers to a common script
    to avoid homoglyph attacks.
  - Steve added that there is also the issue of normalization forms and that gcc will currently warn if
    identifiers are not in NFC form.
  - Mark asked if we should make it ill-formed for identifiers to not be in NFC form.
  - Steve responded that doing so could break existing code.
  - Tom suggested normalizing when comparing identifiers is another approach.
  - Steve noted that doing so requires the Unicode normalization algorithms.
  - JeanHeyd mentioned that we'll also have the problem of reflecting identifiers in the future and that
    normalization will be relevant there.  Corentin brought this up in SG7.  Requiring NFC would be helpful there.
  - Mark expressed support for the idea of requiring NFC.
  - Steve suggested that there is always the `universal-character-name` escape hatch.
  - Mark opined that EWG probably won't like requiring conversion to NFC in name lookup.
  - Tom responded that gcc is at least detecting non-normalized identifiers today, that doing so must require
    some level of Unicode database support, and that performance costs are presumably reasonable.
  - Steve stated that gcc looks for some range of combining code points and may not be 100% accurate.
  - Mark asked if non-NFC normalization can be detected without having to fully normalize?
  - Zach responded that he didn't think so.
  - Mark asked if normalization was brought up in EWG.
  - Steve responded that it wasn't, that we didn't get that far in the discussion.
  - Tom suggested that we have a good amount to think about here and that he is looking forward to the next
    revision of Steve's paper.
  - Steve took the bait and agreed that the paper will have to provide good arguments for why this is important.
  - Zach suggested that this should be easy for implementors if they don't have to deal with normalization and
    that we should just require NFC for performance reasons.
  - Mark asked if we could make use of non-NFC ill-formed NDR so that implementations are not required to diagnose
    violations.
- [P1097 - Named character escapes](https://wg21.link/p1097):
  - Tom introduced the topic:
    - EWG narrowly rejected the paper, but expressed good support for the direction.
    - Most concerns had to do with implementation impact and, in particular, the potential increase in compiler
      binaries.  Some distributed build systems distribute compilers as part of the build process and the
      additional latency imposed by incresing the size of compiler binaries adds cost.  Numbers haven't been
      obtained, but guesses were around 2MB, but could probably be reduced to under 600K.
    - One prominent EWG member was strongly opposed to the design because he would prefer a solution that avoids
      baking Unicode into the core language.  Something like a string interpolation solution that could call
      out to `constexpr` library functions to do character name lookup.
    - Martinho was working on an implementation in Clang at Kona, but Tom doesn't know the state of it or where
      to find it.  Tom reached out to Martinho via email, but didn't hear back.
    - Anyone have time and interest to experiment and produce some estimates to address the implementation
      impact concerns?
  - Steve stated that he could probably do some work on it and that the name DB should compress really well with
    use of a trie.
  - JeanHeyd suggested that the [UAX44-LM2](https://www.unicode.org/reports/tr44/#UAX44-LM2) compression scheme
    could help to reduce size.
  - Tom expressed uncertaintly that it would help much over a trie, but we could experiment and put the results
    in a paper.
  - Zach suggested splitting names that contain "with" in them since the suffixes that tend to follow "with" are
    highly repeated.
  - Tom noted that the algorithmically generated names could be specially handled as well.
  - Steve added that a tokenization approach could help too.
  - Tom asked if anyone might know of a link to Martinho's implementation.
  - Zach replied that a link was provided at some point, possibly in Slack.
  - \[Editor's note: Tom searched Slack, but failed to find a reference. \]
- [P1880 - uNstring Arguments Shall Be UTF-N Encoded](https://wg21.link/p1880):
  - Tom introduced the topic:
    - LEWG rejected the SG16 guidance offered in response to NB comment
      [FR164](https://github.com/cplusplus/nbballot/issues/162) to adopt P1880 for C++20.
    - What should we do next?
  - Zach expressed frustration that he was available when the NB comment and paper were discussed in LEWG, but
    that no one notified him that the discussion was happening.
  - Zach stated that, after the SG16 meeting, he went through all references to `std::basic_string` and added
    missing references to PMR strings and `std::basic_string_view`.  This research also identified a number of
    references that are deserving of more scrutiny.
  - Zach opined that this isn't very important for C++20 and that he will work on a revision for C++23, though
    not for the Prague meeting.
  - Zach stated he was surprised at how many references to these types he found in function templates.
- Tom asked for volunteers to draft a library design guidelines paper.
  - Tom introduced the topic:
    - During the
      [SG16 meeting on July 31st](https://github.com/sg16-unicode/sg16-meetings/blob/master/README.md#july-31st-2019),
      we discussed guidelines for when to add function overloads for each of `char`, `wchar_t`, `char8_t`,
      `char16_t`, and `char32_t` and he would like to have a library guideline paper that records our guidance.
    - Would anyone be interested and willing to work on this?
  - Zach expressed interest in doing so.
- Mark brought up a wording update email Zach sent to LWG with regard to [P1868](https://wg21.link/p1868):
  - Mark noted that the wording introduces a new term of art: "estimated display width units".
  - Zach responded that the new term was intentional; we're leaving the width estimation effectively unspecified
    for non-Unicode encodings.  Implementors expressed a preference for not having to document their choices and
    we didn't want to force embedded compilers to have to be Unicode aware.  So, we needed a non-Unicode term.
  - Tom noted that the wording appears to require embedded compilers to use the proposed Unicode algorithm if
    their execution character set is Unicode.
  - Zach acknowledged that would be the case.
  - Mark siggested that is probably what we want if they are actually doing Unicode.
  - Tom agreed and suggested such implementors could otherwise state that their execution character set is ASCII.
- Tom communicated that the next meeting will be on December 11th.


# October 23rd, 2019

## Draft agenda:
- P1844R0: Enhancement of regex
  - https://wg21.link/P1844R0
- P1892R0 - Extended locale-specific presentation specifiers for std::format
  - https://wg21.link/P1892R0
- P1859R0 - Standard terminology for execution character set encodings
  - https://wg21.link/P1859R0
  
## Meeting summary:
- Attendees:
  - David Wendt
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Yehezkel Bernat
  - Zach Laine
- Tom initiated a round of introductions for new attendees.
- P1844R0: Enhancement of regex
  - https://wg21.link/P1844R0
  - Tom introduced the paper on behalf of the author:
    - The proposal is an expansion of `std::basic_regex` specializations.
    - We've discussed issues with `std::basic_regex` before.  The author has put significant effort into this
      proposal.  It includes wording.  We owe it to the author to set aside any biases and consider the benefits of
      this paper.
    - An implementation is available though it only implements the proposed `char8_t`, `char16_t`, and `char32_t`
      specializations, not the existing `char` or `wchar_t` specializations.
    - The paper does not propose an alternative to `std::basic_regex`, but rather attempts to address shortcomings
      of it for UTF encodings via specializations.  \[Editor's note: this implies that the proposal doesn't address
      issues with support of UTF encodings with the `char` and `wchar_t` specializations.\]
    - The paper proposes a new regex syntax option, `ECMAScript2019`, to be used to select a regular expression
      engine that implements the ECMAScript 2019 specification.  This option would be available for use with all
      `std::basic_regex` specializations.
    - The paper proposes a new `dotall` syntax option that allows the `.` character to match any Unicode code point,
      including new line characters, when using the `ECMAScript2019` option.
    - The new `ECMAScript2019` syntax option would be the only syntax option supported for the `char8_t`, `char16_t`,
      and `char32_t` specializations.
    - The `ECMAScript2019` regular expression engine would *NOT* exactly match the ECMAScript 2019 specification:
      - The `\xHH` expression is redefined to match code points rather than code units.  However,
      - The author would be fine with removing support for the `\xHH` expression since support for code points is
        provided by the `\uHHHH` and `\u{H...}` expressions.
    - The proposal removes locale dependency for the `char8_t`, `char16_t`, and `char32_t` specializations and
      therefore does not propose any new specializations of `std::regex_traits`.
    - The paper proposes new overloads of `std::regex_match` and `std::regex_search` to allow specifying look
      behind limits on ranges.
    - The proposed changes to `std::regex_iterator` are ABI breaking.
  - PeterBr observed that the proposal doesn't deal with language specific aspects like case folding.
  - PeterBr stated he liked the motivation for this paper and the notion that `std::regex` can be made to work.
  - Zach asked about support for collation and whether anyone was familiar with the existing `collate` syntax option.
  - PeterBr responded that the paper states that the `collate` option is ignored for these specializations.
  - Zach stated that the default collation is not useful and that tailoring is required.
  - Tom summarized, so the paper needs to address collation.
  - Zach refuted that need since it could profoundly impact performance.
  - PeterBr suggested that, perhaps, regex for Unicode should operate on `std::text`.
  - Tom expanded that suggestion to any sequence of code points and observed that the proposal kind of does that
    already via the changes to `regex_iterator`.
  - Zach agreed it would be useful to use as an adapter for code points.
  - Tom asked if a new regex feature for non-compile-time regex support would be preferred over specializing
    `std::basic_regex` as proposed.
  - Zach responded that he doesn't think `std::regex` is DOA, but if we're going to support Unicode regex with
    dynamic patterns, then, we should pursue some of the design of CTRE.
  - Zach added that solving the problem is important and that he wants to see Unicode regex support but would
    prefer to take a wait-and-see approach on this paper while watching how CTRE and `std::format` evolve.
  - PeterBr acknowledged the benefits of CTRE, but stated that we do need a solution for dynamic regex.
  - Zach reported that be believes that Hana is planning to make CTRE capable of supporting dynamic pattern
    strings and If that were to happen, then we wouldn't need `std::regex` any longer.
  - Mark lamented the lack of a proposal like this one when C++11 was being designed since the approach looks
    good relative to other papers from the past.
  - Mark added that it is an embarassment that we don't have a solution for this today, but that he feels kind
    of neutral on it as well due to concerns about allocating time for this relative to other things we could
    do.
  - Mark asked what implementors would think and if they get requests for Unicode `std::regex` support.
  - Mark asserted that the implicit use of the `ECMAScript2019` engine when a different syntax option is
    specified has to be changed.
  - Zach reiterated that this proposal is definitely an ABI break, that an ABI break is a serious problem, and
    that the need for such a break suggests we need a different family of types.
  - Mark added that the paper should make it clear that it does break ABI, not that it might.
  - Tom asked if this proposal solves the `std::basic_regex` issues with support for variable length encodings.
  - Zach responded that `std::regex` doesn't handle incomplete or ill-formed code unit sequences and suggested
    that perhaps those should match against `\uFFFD`.
  - Zach reported that `std::regex` can also match code unit ranges that stride code unit sequences since
    `std::regex` effectively matches bytes.
  - Tom asked what guidance we should offer to LEWG.
  - Zach suggested:
    - We should solve this problem.
    - This approach is premature given other things in flight now, but if this had been proposed three years
      ago he might have felt differently about it.
  - PeterBr suggested it should be prioritized behind CTRE.
  - Tom asked whether support for tailoring is important.
  - Zach suggested placing tailoring at the lowest priority and mentioned that he doesn't think ICU supports it
    as people don't often want to do collation aware searching.
  - Tom reiterated that we should offer guidance that it be ill-formed to specify a syntax option other than
    `ECMAScript2019` for the proposed specializations.
- P1892R0 - Extended locale-specific presentation specifiers for std::format
  - PeterBr introduced the paper:
    - Looking through the `std::format` specification he found that there are useful floating point formats that
      can not be produced in locale specific formats.
    - Locale specific formats are important in scientific fields.
    - The `'n'` specifier has a different meaning for integers than it does for floating point.
    - An NB comment was filed to make the `'n'` specifier indicate a locale specific format rather than a type
      modifier.
    - The proposed change should not affect existing well-formed `std::format` calls except for `bool` which
      would now be formatted as locale variants of "true" or "false" instead of 1 or 0.
    - This would make `std::format` unambiguously the best choice for localized formatting since locales can
      be easily specified and `std::format` already solves short falls of iostreams and printf such as ordering.
    - Without this change, there is still a need to use `printf` for locale sensitive formatting.
  - Mark noted that this change will break existing users of [{fmt}](https://github.com/fmtlib/fmt).
  - PeterBr responded that it will for existing uses of `bool` but that he isn't concerned about existing users
    of [{fmt}](https://github.com/fmtlib/fmt).
  - Tom observed that use of `'l'` as the specifier as suggested in the paper avoids the break and aligns with
    Victor's [P1868R0](http://wg21.link/p1868r0) paper to enable locale specific handling of character encodings.
  - Mark stated that the core issue is that there remains some uses of `printf` that can't be directly replicated
    with `std::format` and asked how a programmer would print, for example, the locale specific decimal character
    but without the locale specific thousands separator.
  - PeterBr responded that the programmer can create a custom locale.
  - Zach stated that we can't defer this until C++23 because changing the meaning of `'n'` would break compatibility
    and asked why we can't just introduce an `'l'` specifier in C++23?
  - PeterBr responded that doing so makes things more complicated and asked whether we would deprecate `'n'` if
    `'l'` were to be adopted.  We can postpone addressing this, but we get a cleaner solution in the long term by
    addressing it now.
  - Zach agreed with the motivation being to avoid a wart that we'll need to teach but that some opposition will be
    raised due to perceived risk at this late stage.
  - Zach stated that he likes the change, but that it needs good motivation.
  - PeterBr suggested that `'n'` could be removed now and then restored with desired changes in C++23.
  - Zach suggested that if Victor supports the paper, it will probably pass, but if he disagrees with it, then it is
    probably DOA.
  - Mark stated that the choices need to be clearly presented for LEWG.
  - Zach observed that there are a few options and suggested presenting a cost/benefit of each so that LEWG is given
    clear choices.
  - Mark suggested socializing the issue on the LEWG mailing list now to flush out any objections.
  - PeterBr stated that any help improving the paper would be appreciated.
  - Mark suggested presenting either slides or a different paper that presents the options and analysis.
  - PeterBr stated he would create a doc that could be collaboratively edited.
- P1859R0 - Standard terminology for execution character set encodings
  - Steve introduced the paper:
    - The goal is to not affect implementations, but rather to fix wording so that we can use modern terminology
      and understand each other better.
    - We often use terms like "execution encoding" that are not defined in the standard and are opportunities for
      confusion.
    - We need to admit that `wchar_t` is not, in practice, able to hold all code points of the wide execution
      character set.
  - Zach asked what "literal encoding" is for.
  - Steve responded that it reflects the encoding for non-UTF literals.
  - Zach asked what difference is intended by "character set" and "character repertoire".
  - Steve responded that the goal is to tighten up the meanings of existing terminology so as to avoid massive
    changes to the standard.
  - Mark observed that there seems to be a missing word in the definition of "Basic execution character set"; that
    there seems to be a missing "that".
  - PeterBr stated that this should be high priority in C++23 so we can get everyone on board with terminology.
  - Steve agreed and asserted we'll need to socialize these new terms.
  - Tom asked if there are any terms being dropped; it looks like the paper adds "literal encoding" and
    "dynamic encoding".
  - Steve responded that none are dropped and stated there will be an additional associated encoding added for
    character types as well.
  - Mark noticed that the paper discusses `literal_encoding` and `wide_literal_encoding` but doesn't define a term
    for "Wide literal encoding".
  - Tom asked if "source encoding" should be added.
  - Tom asked if we should add a statement that the dynamic encoding must be able to represent all of the characters
    of the execution character set.
  - Steve responded that we could add that.
  - PeterBr observed a potential problem with doing so on Windows where the dynamic encoding might be UCS-2, but the
    execution character set is UTF-16.
  - Tom suggested refining the requirement such that characters used in literals must have a representation in the
    dynamic encoding.
  - Mark suggested it would be helpful to have a cheat sheet with mathematical notation of which terms denote a
    subset of other terms.
  - Steve agreed.
  - Tom suggested that we also need "wide dynamic encoding".
  - Zach asked about the difference between the "encoding" and "character set" terms.
  - Steve responded that the former states how characters are represented while the latter states what characters
    must be representeable.
  - Zach stated it would be useful to have text explaining the difference.
  - Tom asked how ODR violations would be avoided for `literal_encoding` since literal encoding can vary by TU.
  - Steve responded that the same technique used for `std::source_location` can be used; a value is provided.
- Tom confirmed that the next meeting will be November 20th.


# October 9th, 2019

## Draft agenda:
- P1880R0 - u8string, u16string, and u32string Don't Guarantee UTF Endcoding
  - https://github.com/tzlaine/small_wg1_papers/blob/master/P1880_uNstring_shall_be_utf_n_encoded.md
- P1879R0 - The u8 string literal prefix does not do what you think it does
  - https://github.com/tzlaine/small_wg1_papers/blob/master/P1879_please_dont_rewrite_my_string_literals.md
- P1844R0: Enhancement of regex
  - https://wg21.link/p1844

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - David Wendt
  - Henri Sivonen
  - JeanHeyd Meneide
  - Peter Bindels
  - Peter Brett
  - Tom Honermann
  - Zach Laine
- P1880R0 - u8string, u16string, and u32string Don't Guarantee UTF Endcoding
  - https://github.com/tzlaine/small_wg1_papers/blob/master/P1880_uNstring_shall_be_utf_n_encoded.md
  - Zach introduced:
    - The idea is that interfaces taking these string types expect that contents of these strings are
      well-formed UTF-8, UTF-16, UTF-32 respectively; this requirement needs to be reflected in the standard.
    - We should state a blanket requirement for these expectations.
    - The paper proposes a 4th bullet to [[res.on.arguments]](http://eel.is/c++draft/res.on.arguments).
  - PeterBr asked if the requirement should be for well-formed data.
  - Zach replied that it should be.  LWG should confirm that.
  - Henri asked what happens if an ill-formed code unit sequence is passed.  Is it undefined behavior or as-if
    the Unicode replacement character was present?
  - Zach replied that the current wording makes it undefined behavior.
  - PeterBr provided an example of why the behavior is undefined.  Consider a string that ends with an incomplete
    code unit sequence; the implementation could run off the end of the buffer.
  - Zach responded that, for `std::basic_string` types, the buffer overrun can be avoided, but in that case, the
    interface specification should state that behavior.  The proposed blanket wording is for the weakest interface
    requirements and can be strengthened by individual interfaces.
  - Henri asked if that is useful as it seems like undefined behavior is a huge foot cannon; replacement character
    semantics would provide a safer interface.
  - Zach responded that, if this is a foot gun, then so is `std::vector operator[]`.  You must meet preconditions.
    Implementations can always constrain their handling if they want.  The intent here is to enable the fast path.
  - PeterBr added that it would add complexity to implement replacement character behavior; interfaces would not
    be able to use SIMD instructions if ill-formed strings must be handled.
  - Zach repeated that the proposal just specifies the default behavior unless otherwise specified for an interface.
  - Corentin opined that this seems almost editorial.
  - Henri stated that, for `char8_t`, there are values that are never valid in well-formed UTF-8 text and asked what
    an individual `char8_t` means; it must be restricted to ASCII.
  - Tom noted that matches UTF-8 character literals; they can only specify ASCII values.
  - Zach read the existing content in [[res.on.arguments]](http://eel.is/c++draft/res.on.arguments) in order to
    demonstrate similarity in existing requirements.
  - Henri asked if this represents a requirement that is more difficult to satisfy than the existing requirements.
    For example, in UTF-16, almost all code bases will allow unpaired surrogates.  Does this requirement make the
    standard library useless for their code bases?
  - Zach stated that interfaces can specify their handling of unpaired surrogates.
  - Henri asked again if this is a practical requirement.
  - Tom responded that this is needed for our mantra of not leaving performance on the floor; we can't both check
    for ill-formed text and maximize performance.
  - Zach added that ICU already does this for performance.  Within Boost.Text, Zach added interfaces for both
    unchecked and checked text.
  - PeterBr opined that this paper is great and sorely needed.
  - Tom and Corentin agreed.
  - Henri asked Zach to expound on his statement that ICU already exhibits undefined behavior.
  - Zach responded that, in ICU normalization code, assumptions are made when decoding UTF-8.  For example, unsafe
    unpacking of UTF-8 is performed.
  - Henri asked if ICU does likewise for UTF-16 for unpaired surrogates.
  - Zach responded that he thought so, but is not completely sure.
  - Corentin expressed support for an NB comment to include this in C++20.
  - Tom opined that it doesn't much matter if this makes C++20 as implementors will already do the right thing.
  - Henri asked if this might introduce a backward compatibility issue in C++23 if added after C++20.
  - Tom responded that the undefined behavior is effectively already there; this is fixing an underspecification.
  - Henri stated it would be a huge task to scrub existing code bases to avoid this undefined behavior.
  - Zach predicted that we'll end up with separate interfaces for assuming an encoding vs checking the encoding.
    This isn't hurting anybody, it is just enabling fast path implementations.
  - Henri expressed concern about digging deeper into making default interfaces unsafe; like `std::optional::operator*`
    is.  He would prefer unsafe interfaces be clearly marked as unsafe.  This undefined behavior has the potential
    to introduce security issues.
  - Zach responded that most standard interfaces are unsafe in some way, for example every function that accepts
    arguments of pointer type.
  - Henri countered that the undefined behavior can be avoided in this case; just like we could for
    `std::optional::operator*`.
  - Zach suggested that C++ is often used for its performance advantages; we want the default to be fast.  But this
    proposal isn't really about that; it is about documenting our default behavior.
  - PeterBr stated that `std::u8string` is `std::basic_string` with `char8_t`.  `std::basic_string` provides many
    interfaces that allow mutating the string in a way that would break otherwise well-formed UTF-8.  Rust doesn't
    do that.  We could specify a UTF-8 string type that maintains invariants, but it wouldn't be a `std::basic_string`
    any more.  Thus, it is up to the programmer to not violate UTF-8 requirements.
  - Corentin agreed that we don't want to change `std::u8string`; it is just a container of code units.  String
    mutation should be managed via some overlying type like `std::text`.  This paper just reflects existing behavior.
  - Henri asked if we really want to enable so much performance that we risk our users.  In Firefox, lots of string
    checking is done to avoid security issues even though ill-formed UTF-8 is very rare.  The performance isn't bad.
  - PeterBr responded that an implementation can choose to define its behavior.
  - Henri countered that, if it isn't required everywhere, then it can't be relied on.
  - Corentin suggested that, if you want safety, then `std::basic_string` is not the type you're looking for.  We're
    going to need other types on top and, eventually, we'll have more trusted types.
  - Zach added that no interfaces are being specified in this paper, so there are no ergonomic concerns.  Again, this
    is just proposing blanket wording that can be strengthened in individal interfaces.
- Tom initiated a discussion about polling during telecons.
  - Tom introduced:
    - He prefers to avoid polling during telecons in favor of polling during face to face meetings.  This is due
      to 1) larger numbers of attendees at face to face meetings, 2) more opportunity for input from those that do
      not regularly attend telecons, and 3) more opportunity for background thinking after a discussion before having
      to respond to a poll.
    - He also sees the telecons as useful for priming discussion and identifying non-obvious concerns.
  - Tom asked if anyone wanted to argue for a change in practice.
  - The group expressed general agreement to continue doing what we've been doing.
- P1879R0 - The u8 string literal prefix does not do what you think it does
  - https://github.com/tzlaine/small_wg1_papers/blob/master/P1879_please_dont_rewrite_my_string_literals.md
  - Zach introduced:
    - This started from an experience from a while back that we have previously discussed.
    - Tests involving UTF-8 formatted source files failed when compiled with the Microsoft compiler, but not with
      other compilers.
    - The source files did not have a UTF-8 BOM and Microsoft's `/source-charset:utf-8` option wasn't being used,
      so the source files were decoded as Windows-1252.
    - String literals therefore did not contain what was expected because code units were not interpreted as expected.
    - The paper proposes prohibiting use of `u8`, `u`, and `U` literals unless the source file encoding is a Unicode
      encoding.
  - Corentin suggested relaxing the prohibition to allow use of these literals so long as the source contents of the
    literal only use characters from the basic source character set.  \[Editor's note: presumably this would still
    allow characters outside the basic source character set if specified with `universal-character-name` escape
    sequences.\]
  - Corentin also stated that the current behavior makes sense according to the standard, but most programmers aren't
    aware of source file encoding vs execution encoding concerns.
  - Henri stated that the behavior makes sense if you think of C++ source code as text rather than bytes and agreed
    that this isn't what programmers expect.
  - PeterBr expressed support for the paper because it ensures you get the same abstract characters written in the
    source file and added that it would be nice if this paper used the same terminology as propsoed in Steve's recent
    terminology paper ([P1859R0](https://wg21.link/p1859r0)).  \[Editor's note: this paper will be in the Belfast
    pre-meeting mailing.\]
  - Zach agreed regarding use of terminology.
  - Tom expressed concerns regarding breaking backward compatibility, particularly for z/OS where source files are
    EBCDIC and `u8` literals are used to produce ASCII strings.
  - Zach asked if it would help to only allow characters from ASCII.
  - PeterBr stated that, if the compiler is not explicitly told what the source encoding is, you are in trouble since
    the compiler can't always detect an encoding expectation mismatch.
  - Henri noted that the translation model matches what is done on the web where HTML source is transcoded to some
    internal (Unicode) encoding.  A compiler could preserve meta data about the encoding a literal came from and,
    if the transcoded code point is above 0x80, issue a diagnostic.
  - Zach asked for more information regarding concerns for z/OS and EBCDIC.
  - Tom explained the source translation model according to [translation phase 1](http://eel.is/c++draft/lex.phases#1.1).
    Source files are first transcoded from an implementation defined encoding to an implementation defined internal
    encoding.  The internal encoding has to be effectively Unicode (or isomorphic to it) due to possible use of
    `universal-character-name` sequences in the source code.  The internal encoding is then transcoded to the various
    execution encodings where needed.
  - Tom went on to explain that there are multiple EBCDIC code pages and that many of the characters available in
    them are not defined in ASCII.  Restricting UTF literals to just ASCII would prevent use of those characters.
  - Tom restated PeterBr's point from earlier.  This problem is always due to mojibake; the source file being
    encoded in something other than what the compiler expects.
  - PeterBr agreed that the root cause is the encoding mismatch and opined that this is a problem worth solving.
    The question is how best to solve it.  The first place to look is at the translation from source encoding to
    internal encoding.
  - Henri expressed belief that it makes sense to address the problem where Zach suggests.
  - Zach stated that the right place to detect this is during parsing; when parsing a UTF literal, it is critical
    to know what the source encoding is.
  - Tom countered that it is necessary to know the encoding as soon as you hit a code unit that doesn't represent a
    member of the basic source character set.
  - Henri stated that diagnosing any such code unit is a harder sell than just diagnosing one in a UTF literal.
  - Tom agreed.
  - PeterBr noted that it is implementation defined how (or if) characters outside the basic source character set
    are represented.  The goal of the paper is effectively to tighten that up.  That means implementations can
    have extensions to relax diagnostics.
  - Henri responded that such arguments apply to any change to the standard.
  - Zach agreed, but noted this is restricted to source files that have UTF literals with transcoded code points
    outside of ASCII.
  - Henri stated that there is more potential for failures for some character sets than others.  For example,
    some character sets don't roundtrip through Unicode.  This failure mode already exists, but there is little value
    in trying to diagnose this outside of UTF literals.
  - PeterBr stated that a source file with code units representing characters outside of the basic source character
    set is ill-formed subject to implementation defined behavior.  When a programmer writes a UTF literal, that is a
    request for a specific encoding, but it is perfectly valid for the source file to be written in Shift-JIS.
  - Henri acknowledged that perspective as logically valid, but doesn't address the problems caused by the Microsoft
    compiler's default behavior not matching user expectations.  Programmers are using UTF-8 editors these days.
  - PeterBr asserted that is a quality of implementation concern and not an issue with the standard.
  - Tom agreed.
  - Zach stated that the proposed restrictions can be worked around by using `universal-character-name` escapes
    and stated a preference for implementing a solution that results in a diagnosis for the problem he encountered,
    but that this isn't a critical issue.
  - Corentin brought up static reflection and that, at some point, reflection will require defining or reflecting
    the source file encoding.
  - Tom stated that dovetails nicely with Steve's P1859R0 draft that provides a callable for conversion of string
    literal encoding.
  - Corentin noted that Vcpkg compiles all of its packages with the Microsoft compiler's `/utf-8` option and that
    Microsoft may be open to defaulting source encoding to UTF-8 when compiling as C++20.
  - Zach added that the Visual Studio editor, by default, adds a UTF-8 BOM to new source files it creates, though
    it doesn't implicitly add a UTF-8 BOM when existing files are added to a project.
  - Corentin observed that, because source encoding is not portable, most programmers just don't use characters
    outside of ASCII except in comments; which is why such characters are ignored.
  - PeterBr suggested that an evening session in Belfast to discuss this or other ideas might be an option and that
    it would be good to talk directly with implementors.
- Tom confirmed that the next meeting will be on October 23rd and will be the last meeting before Belfast.


# September 25th, 2019

## Draft agenda:
- Discuss LWG#3290 - Are std::format field widths code units, code points, or something else?
  - https://cplusplus.github.io/LWG/issue3290
  - Victor plans to have a draft paper for discussion.
- Discuss P1844R0: Enhancement of regex
  - https://wg21.link/p1844


## Meeting summary:
- Attendees:
  - Corentin Jabot
  - JeanHeyd Meneide
  - Lyberta
  - Mark Zeren
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Discuss D1868R0 - 🦄 width: clarifying units of width and precision in std::format
  - http://wiki.edg.com/pub/Wg21belfast/SG16/D1868R0.html
  - Addresses https://cplusplus.github.io/LWG/issue3290
  - Victor introduces:
    - Any solution to this problem must deal with conflicting constraints.  The programmer's intention is
      to align text output assuming a monospace font and some understanding of how the text will be rendered
      (e.g., how many terminal columns will be consumed by each "character").  Implementors desire a clear
      and precise specification; preferably one that does not have great complexity that may lead to
      reliability issues or bug reports.
    - Field precision is more consequential than field width because it truncates text potentially resulting
      in ill-formed output if truncation doesn't occur at a suitable boundary.
    - Experimentation with an approach that estimates field width based on Unicode's extended grapheme clusters
      and script blocks produced good results; better results than estimation based on code point counts.
    - Experimentation on macOS, Linux, and Windows revealed that Windows currently has the most significant
      limitations with regard to support for Unicode characters currently not represented in Microsoft's
      supported ANSI code pages.  Experiments have not been performed using the new Windows terminal which
      may be expected to produce better results.
    - Testing of Unicode family emoji demonstrated the most variability of results since family emoji may be
      rendered as a single glyph or as a series of glyphs each representing a family member.
    - Field width is an estimate.  Unless apriori knowledge of how the text will actually be rendered is
      available, the width of any given text can only be approximated.
    - The experimental implementation uses [Boost.text](https://github.com/tzlaine/text) to identify extended
      grapheme cluster boundaries and computed width based on Unicode block ranges culled from an
      implementation of `wcswidth`.
  - Corentin mentioned that the issue with family emoji extends to other sequences of combining emoji.  For
    example, ninja cat (`U+1F431 {CAT FACE}`, `U+200D {ZERO WIDTH JOINER}`, `U+1F464 {BUST IN SILHOUETTE}`) is
    rendered with a single glyph on Windows, but currently with two glyphs on Linux.  Width fundamentally
    depends on rendering.
  - Corentin added that, for non-Unicode encodings, width estimation must look at code units and do things
    differently for double-byte characters vs single-byte characters.
  - Victor stated that he is content with handling of non-Unicode encodings being implementation defined.
  - Zach agreed and asserted that we want a 90% solution.  Support of non-Unicode encodings would require
    information that we can't currently specify in the `std::format` interface assuming `std::format`
    remains locale independent; it is ok for implementations to assume an encoding.
  - Tom thanked Victor for doing this research and stated he found it sufficiently compelling to take the code
    unit solution he previously advocated for resolving [LWG 3290](https://wg21.link/lwg3290) off the table.  In
    particular, the demonstration of prior art in the form of POSIX
    [`wcswidth`](https://pubs.opengroup.org/onlinepubs/9699919799/functions/wcswidth.html) lent confidence to
    this approach.
  - Tom asked if width calculation for `wchar_t` could be delegated to `wcswidth`.
  - Victor replied that `wcswidth` is locale dependent and that goes against the `std::format` design.
  - Tom asked if width calculation for `char` and `wchar_t` couldn't be implementation defined such that an
    implementation could query locale only when width or precision is explicitly specified and the arguments
    are characters or strings.  Width or precision specifiers would effectively constitute an opt-in for locale
    dependence.
  - Zach objected on the basis that dependence on locale could cause output to differ on one platform vs another
    for the same character or string data.
  - Victor clarified that, if encoding doesn't match, the worst case result is mis-alignment.
  - Corentin stated that, as currently specified, `std::format` formats bytes since it doesn't know the precise
    encoding of inputs.  Correct text manipulation requires knowing the encoding.
  - Corentin expressed agreement that display width is what programmer's expect.  Perhaps in C++23, the ability
    to pass an encoding argument could be added.
  - Tom mentioned that `std::format` can take a `std::locale` option from which the encoding could be queried
    thus making it possible for programmers to opt-in to locale awareness simply by passing a locale object.
  - Zach again objected based on the desire to have portable output.
  - Corentin expressed a strong preference for a good solution in C++20 and asked if we could specify that width
    and precision units are display width and, for characters outside the basic source character set, behavior is
    implementation defined.
  - Victor stated that is a minimum viable solution.  The paper proposes that encoding is an implementation
    defined fixed encoding, not a run-time selected one.
  - Corentin confirmed satisfaction with a minimal solution for C++20 that we can iterate on for C++23 and that
    retains some flexibilty.
  - Zach observed that, if we make it implementation defined today, then we'll be stuck with implementation
    choices.  If the standard doesn't specify behavior, then implementors will choose one and we'll get stuck
    either way.  This is similar to breaking ABI; it can be an over-my-dead-body issue.
  - Corentin again expressed a desire for some way to preserve the ability to make changes later.
  - Zach stated that it is important to remember what Victor said previously; width is an estimate.
  - Mark observed that what we're discussing is mostly an edge case since most fields are aligned for numeric output.
  - Tom countered that alignment is useful for things like names.
  - Tom asked if `std::format` is constexpr.
  - Victor replied that parsing of the format string is constexpr, but actual formatting is not.
  - Corentin stated it would be useful to have constexpr formatting at some point, but querying locale would prevent
    that.
  - Tom disagreed and stated that an implementation could use an internal locale if formatting at compile-time.
  - Tom summarized his perceptions of our positions so far:
    - We appear to have agreement for display widths in some form.
    - We have disagreements over adding a locale dependency as part of encoding assumption.
  - Corentin asked Zach if he thought a best attempt at display width is sufficient.
  - Zach replied that he wants the algorithm in the paper so that the same behavior is exhibited on all platforms
    and is unconcerned about rendering dependent cases like for family emoji.
  - Victor reiterated that width calculation is best effort and that he is ok with consistent results only being
    ensured for the basic source character set.  This assurance only requires a fixed system dependent encoding.
  - JeanHeyd asked for clarification that we would only be guaranteeing alignment for the basic source character
    set in C++20 while leaving further specification until C++23.
  - Victor replied, yes, basically.
  - JeanHeyd asked if that implied an implementation defined fixed encoding.
  - Victor responded, not implementation defined, but rather platform dependent so that all implementations targeting
    a given platform would exhibit the same behavior.
  - Tom observed that, if the system defined fixed encoding differs by platform, then we won't get consistent results.
  - Zach disagreed based on a premise that, for the purposes of width computation, consistent results are achieved by
    interpreting the input as Unicode.
  - Corentin stated that he thinks we need to defer to (wide) execution encoding when computing width.
  - Tom agreed stating that we should make width calculation as right as we can make it.
  - JeanHeyd reformulated the trade off.  The most right answer depends on locale.  The always consistent result
    generates garbage consistently but avoids the locale dependency.
  - Victor stated that rendering can always change; we just need to decide if we are ok depending on something at
    run-time.
  - Zach re-iterated that, with the current specification, width calculation only works for single byte characters
    that render as a single glyph and we don't have a way to customize the width formatting unless we defer to
    something at run-time, but doing so conflicts with design goals of `std::format`.
  - Corentin observed that the same issue exists with `printf` as it will fail if the execution encoding doesn't
    match the run-time locale encoding; C and C++ fundamentally depend on encoding compatibility.
  - Victor reminded everyone that the paper does support use of the locale encoding via an opt-in specifier.
  - Steve reminded everyone that there is no system call to get the actual display width, so we're always guessing
    anyway.
  - JeanHeyd stated that he thought opt-in for locale dependent width was acceptable.
  - Zach expressed a desire to get the right default for the long-term.  If we make the default behavior locale
    sensitive, then we'll be stuck with that forever.
  - Tom responded that, in the long term, encoding will hopefully become separated from locale thereby eliminating the
    wrong default concern.
  - Corentin suggested that, for C++20, we could require the `'l'` in the specifier and not have a non-locale option
    until we figure this out.
  - Steve observed that the locale dependency creates a buffer overflow situation in the case where the locale changes
    in between width calculation and actual formatting to a buffer.
  - Corentin stated a preference to just require `'l'` in the width specification for C++20 to give us time to address
    this properly.
  - Tom suggested adding a reference to [LWG 3290](https://wg21.link/lwg3290) in the paper.
- Tom announced that the next meeting will be on October 9th.


# September 4th, 2019

## Draft agenda:
- Discuss Corentin's draft D1854R0 - Conversion to execution encoding should not lead to loss of meaning
  - https://cor3ntin.github.io/posts/encoding/D1854.pdf
- Discuss a few follow up items from
  [P1689, "Format for describing dependencies of source files"](https://wg21.link/p1689) following discussion in SG15.
  - Bikeshed "data". What do we call the code unit equivalent in path names?
  - Are we ok stating that JSON readers/writers are not allowed to apply Unicode normalization?
  - Are we ok with allowing a BOM (JSON doesn't permit one)?
- Is "execution character set" the right term for the run-time locale dependent encoding used by the character
  classification and conversion functions?

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - David Wendt
  - JeanHeyd Meneide
  - Nathan Myers
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- The meeting started off with a round of introductions for the benefit of new attendees.
- Discuss Corentin's draft D1854R0 - Conversion to execution encoding should not lead to loss of meaning
  - https://cor3ntin.github.io/posts/encoding/D1854.pdf
  - Corentin introduced the paper:
    - The basic idea is to avoid the meaning of the program silently changing in unintended ways due to lack of
      representation in the execution character set for a character in a character or string literal.
  - Zach asked if he hadn't previously signed up to write this paper.
  - Corentin explained that Zach signed up to write a paper about `u8string`.
  - Tom then proceeded to explain the wrong paper but succeeded at only further confusing himself.
  - Zach clarified that the paper he did sign up to write was to permit `uX"xxx"` string literals only when
    the execution encoding is a Unicode encoding.
  - Tom returned discussion to the paper at hand and noted that the paper only adds restrictions on ordinary
    and wide literals because restrictions are already in place for `u8`, `u`, and `U` literals.
  - Corentin demonstrated via godbolt.org that gcc rejects non-representable characters and that MSVC
    substitutes a `?`.
    - https://godbolt.org/z/kDwR1l
    - \[Editor's note: demonstration of MSVC's substitution of a `?` character requires adding the
      `/source-charset:utf-8` option to the MSVC command line in the above link.  Without that option, the
       UTF-8 encoded source is interpreted by the MSVC compiler as Windows-1252.\]
  - Corentin summarized that the goal is to standardize gcc's behavior.
  - Corentin stated that he was unsure if Microsoft would be willing to implement this outside of `/permissive-`
    mode since this might break existing code even though such code is already fragile and subject to breakage
    just by being compiled on a different system (with a different default execution character set).
  - Tom noted that by making this standard, if an implementor remains non-conforming, then users can complain if
    they want to.
  - Tom asked if there are any possible advantages to status quo.
  - Zach replied no, this just hurts portability.
  - Corentin observed that code can always be updated to use an escape sequence instead of an unrepresentable
    character.
  - Peter expressed concern about wide encoding because, on Windows, it is (or used to be) UCS-2, so emoji can't be
    represented.
  - Tom restated Peter's point; there may be cases where graceful degradation is ok.  E.g., losing emojis.
  - Peter reported testing gcc and found that, in wide encodings, characters outside the BMP were lost when printing
    to the console.
    - ```
      int main() {
          std::wstring s = L"\U0001f4a9";
          std::wcout << s;
      }
      ```
  - Tom suggested that this is due to a libstdc++ iostreams issue; wide characters are simply truncated when
    `std::wcout` writes them to stdout.
  - Corentin demonstrated that gcc rejects wide string literals with characters not representable in the wide
    execution character set as well.
  - Tom requested a quick walk through of the wording.
  - Tom suggested to update the paper to use stable names for the sections to be updated since numbers change.
  - Peter noted that, in section 5.13.3.8, the red text is missing strike through.
  - Corentin commented that, until writing this paper, he was not aware of multi-character literals.
  - Peter responded regarding a recent use case for them for a table driven switch handling approach:
    - ```
      uint32_t tableId = (table->Signature[0] << 24) |
                         (table->Signature[1] << 16) |
                         (table->Signature[2] << 8) |
                         (table->Signature[3] << 0);
      switch(tableId) {
          case 'APIC':
          ...
      }
      ```
  - Tom expressed some initial surprise to see the proposed wording changes for octal and hex escapes, but
    concluded that they make sense.
  - \[Editor's note: it would be helpful to add examples to the paper of code that would become ill-formed.\]
- Discuss a few follow up items from
  [P1689, "Format for describing dependencies of source files"](https://wg21.link/p1689) following discussion in SG15.
  - Bikeshed "data". What do we call the code unit equivalent in path names?
    - Tom introduced the naming concern.  [P1689R0](https://wg21.link/p1689r0) used the name "data" to refer to the
      sequence of individual elements of a path.  [P1689R1](https://wg21.link/p1689r1) changed the name to "code-units"
      following feedback in Cologne.  Do we want to suggest a different name given our stance on file names not having
      an associated encoding and, arguably therefore, no "code units"?
    - Corentin argued to not invest time in this discussion unless/until SG15 progresses the paper further.
    - Corentin also observed that user's won't see this name, so it doesn't really matter.
  - Are we ok stating that JSON readers/writers are not allowed to apply Unicode normalization?
    - Tom explained that this is no longer a concern.  in [P1689R1](https://wg21.link/p1689r1), code units are always
      explicitly specified.
  - Are we ok with allowing a BOM (JSON doesn't permit one)?
    - Corentin argued that we should follow the JSON specification.
    - Tom explained his understanding that allowing one doesn't violate RFC 8259 since the BOM limitations there only
      apply to network-transmitted text, and ECMA 404 doesn't specify encoding at all; there is no mention of "BOM",
      "byte order", or "UTF-8" in that specification.
      - https://tools.ietf.org/html/rfc8259#section-8.1
      - https://www.ecma-international.org/publications/standards/Ecma-404.htm
    - Zach asked what motivation exists for allowing a BOM.
    - Tom replied that it would be useful for non-ASCII based platforms like z/OS.
    - Peter added that it is useful for Windows as well since text files are likely to be interpreted as Windows-1252.
    - Corentin noted that Unicode recommends against use of a BOM.
    - Corentin stated that, if the specifications don't require UTF-8 encoded JSON, then we should specify that.
- Is "execution character set" the right term for the run-time locale dependent encoding used by the character
  classification and conversion functions?
  - Zach suggested asking core about this since it seems like we've just been using the wrong terms.
  - Steve noted that the existing wording is all old langauge pertaining to character sets, not necessarily encoding.
  - Tom stated that there was an email thread about this on the core and SG16 mailing lists and that the conclusion
    was that Steve and Tom should write a paper.  Steve has since done some work, but Tom hasn't.
  - Zach stated that we need someone to go through the existing wording and refine our understanding of it.
  - Tom agreed, and added that that is the paper to be written.  We use terms like "execution encoding" now that
    aren't defined in the standard.
  - Steve stated he would love to expose encoding details somehow.
  - Corentin asked if we want to change the names as they've been around a long time.
  - Steve stated he thinks it is worth tightening the specification without changing the intent.  Other than that
    we should state that the wide character encoding can be a variable length encoding.
  - Zach commented that clarifying terms in the standard is a good use of our time.
  - Corentin stated we should have different names for compile-time and run-time encodings and that wording should
    state requirements regarding their compatibility.
  - Steve asserted that some archaeology is necessary here as much of this wording was created when locales were
    being developed around the expectation that code worked with the "C" locale.
  - Peter observed that variable length encodings go back to at least GB2313 from the 1980s.
  - Steve noted that shift encodings go back to then too.
- Zach mentioned that he has a repository where he is working on several small papers.
  - https://github.com/tzlaine/small_wg1_papers
- Peter requested feedback on his slides for CppCon.
- Tom stated that the next meeting will be September 25th.


# August 21st, 2019

## Draft agenda:
- Discuss P1108, "web_view".  Our focus will be, unsurprisingly, character encodings and the use of iostreams with (presumably) UTF-8 data.
- Goals for WG14 in Ithaca (October 21st-25th).
- Goals for Belfast (November 4th-9th).
- Discuss a few follow up items from P1689, "Format for describing dependencies of source files", following discussion in SG15.
  - Bikeshed "data".  What do we call the code unit equivalent in path names?
  - Are we ok stating that JSON readers/writers are not allowed to apply Unicode normalization?
  - Are we ok with allowing a BOM (JSON doesn't permit one)?
- Is "execution character set" the right term for the run-time locale dependent encoding used by the character classification and conversion functions?

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hal Finkel
  - Hubert Tong
  - JeanHeyd Meneide
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Discussion of a draft of P1108R3 - web_view:
  - https://wg21.link/p1108r3 (link not yet active).
  - Hal introduces.
    - A protoype is available using wxWidgets:
      - https://github.com/hfinkel/web_view
    - There are a variety of ways we can provide graphical interaction within the standard.
    - This approach comes out of discussions with folks at Apple and Nvidia.
    - This approach outsources functionality to well used outside standards.
    - The basic idea is that system services already exist with different APIs that can be wrapped in a standard
      interface.
    - For security reasons, interactions should run out-of-process and the interface must therefore not be too fine
      grained.
    - There is a common subset of functionality among the various system services that provides a push/pull interface.
    - Constructing a `web_view` presents a window in which web content can be displayed and (Javascript) scripts can
      be run.
    - URI scheme extensions are supported by registering a (single) callback handler (per scheme).
    - Close handlers are supported by registering a (single) callback handler.
    - Interfaces are provided to request window close and to wait for window close.
    - An example of a dynamic page is available in the paper.
  - Hal provided a (successful!) live demonstration of the example from the paper.
  - Hal then provided an additional (successful!) live demo of an additional example.
  - Zach asked how C++ code can be invoked to update the displayed page.
  - Hal responded that interaction is enabled by registering a URI scheme handler callback via the
    `set_uri_scheme_handler` interface.
  - Tom asked if the interface is effectively append only.
  - Hal responded that it is based on a push model, so yes, requests update state.  The design supports both push
    (via `run_script`) and pull (via callbacks registered with `set_uri_scheme_handler`).
  - Zach stated that users will want the ability to route schemes to direct requests.
  - Tom suggested that routing can be implemented via the callback registered with `set_uri_scheme_handler`.
  - Corentin suggested using Web Sockets as well.
  - Hal responded that there are many examples where utility libraries would come in helpful.  For example, we
    probably don't want to do URI encoding and decoding, nor build interfaces using `std::format`.  We probably
    want JSON support libraries.  Such utility libraries should be proposed separately though.
  - Tom asked to clarify if `run_script` is for Javascript only and whether it would make sense for other languages
    to be supported.
  - Hal responded that it may be useful to specify the scripting language, like for Web Assembly.
  - Zach suggested that such support could always be wrapped in Javascript.
  - Zach acknowledged the elephant in the room by asking about the use of `std::string` in the interface.
  - Corentin stated that we should give the same advice as for 2D graphics; use Unicode everywhere and,
    specifically, UTF-8.  Supporting both UTF-8 and UTF-16 would complicate the interface.
  - Zach noted that the W3C recommends UTF-8 only.
  - Zach observed that for support of [RFC 39865](https://tools.ietf.org/html/rfc3986), encoding of URIs could
    be handled within the library thereby allowing all URIs to be provided in UTF-8.  The remaining interfaces
    could all take UTF-8 only as well, except, perhaps, for the window title.
  - Tom stated that, for the title, even if UTF-16 is eventually required, conversion from UTF-8 is loss-less.
  - Corentin suggested that URI escaping is complicated and that an interface for it should not be part of this
    proposal.
  - Tom asked if existing web view providers provide URI encoding services or if the implementation would be
    obligated to provide it.
  - Hal responded that some web view implementors just reject invalid URIs and that some others may not validate
    much for file handling.  It isn't clear how existing web view providers interpret input; they probably just
    assume UTF-8.
  - Hal asked that, if UTF-8 were required, would it be sufficient to indicate that by just using `std::u8string`
    in the interface.
  - Zach responded yes, though `std::u8string` doesn't enforce well-formed UTF-8, so it may still be necessary
    to explicitly specify a requirement for well-formed UTF-8 data.
  - Corentin asked if use of `char8_t` based types doesn't already ensure that.
  - Hubert responded no, we can't enforce well-formedness since programmers can always create `char8_t` arrays
    with non-UTF-8 data.
  - Zach suggested that we add blanket wording somewhere in the standard library specification stating that,
    for interfaces that use `std::u8string` in library functions, that behavior is undefined if data is not
    well-formed UTF-8.
  - Hubert stated that approach makes sense.
  - Hal, changing topics, asked for feedback regarding use of `std::ostream` in the URI scheme callbacks.
  - Zach asked if we have `char8_t` based streams yet.
  - Tom responded no.
  - Zach stated that we would want that to help ensure the data is UTF-8.
  - Hubert suggested that `codecvt` facets could be used to perform conversions.
  - Zach acknowledged and added that, if the programmer imbues a locale, it is up to them to make sure it makes
    sense.
  - Corentin asked if Hal had considered use of strings instead of streams?
  - Hal responded that a string based approach might make sense.  The benefit of the stream approach is that it
    allows partial writes and some of the lower level interfaces support that.
  - Tom, clarifying, stated that, within a callback handler, data written to the stream may start being processed
    by the web view before the handler returns.
  - Corentin suggested that we're going to have to provide `char8_t` based streams in C++23 anyway.
  - Tom agreed.
  - Hubert returned discssion to the earlier comments on blanket UTF-8 wording for `std::u8string`.  The place to
    add such wording is in [[res.on.arguments]](http://eel.is/c++draft/res.on.arguments); "each of the following
    applies to all functions ... unless explicitly stated otherwise".
  - Zach volunteered to draft that blanket wording.
  - Hal stated that we kind of broke UTF-8 hello world in C++20, but iostreams are weird for non-text data anyway.
  - Tom replied that it was already broken, but we certainly didn't make it any easier.
  - Hubert noted that localizations on iostreams currently require characters not in ASCII.  For example, monetary
    symbols like the Euro sign (€).
  - Hal noted that the URI scheme handler takes a constrained parameter, so overloads could be provided to handle
    strings and streams.
  - Hal stated that the next revision of the paper will include discussion about the URI scheme handler composing
    a string and returning it vs support for partial writes via iostreams or some other concept.
  - Tom suggested that there may be something in the Networking TS worth looking at.
  - Hubert suggested that something lower level in iostreams, like `std::streambuf`, might be worth looking at too.
  - Hal observed that `std::streambuf` has an associated locale.
  - Tom acknowedlged; that is where `std::codecvt` facets do their work.
  - Tom pondered whether we should ban `std::codecvt` facets on future `char8_t`, `char16_t`, and `char32_t`
    iostreams by making attempts to imbue such streams with such a facet an error.
  - Tom mentioned that we've talked about string builders in the past and this is a clear example where such
    builders could be useful; though `std::format` might just be that tool these days.
  - Zach observed that Beast and the like traffic in large ranges.  Perhaps some of those types would be useful here.
  - Corentin suggested that Web Sockets are a better solution.
  - Tom asked if it might make sense for the URI scheme handler to just use Web Sockets.
  - Hal responded with concerns about complexity; the underlying APIs aren't the same.
  - Hal stated that we will need to figure out the string vs stream interface as we want to avoid having to do
    unnecessary copies.  We don't want to motivate the interface based on not knowing how to print UTF-8 to streams.
    Responses are probably small, so strings are usually ok.  But encoded images might get pushed through these
    interfaces as well.
  - Zach asked how many URL scheme handlers can be active at a time; if we were reviewing for SG13, I would want to
    know how much data can get pushed.
  - Hal responded that the interface currently feels quick from a human perspective, but measurements of throughput
    haven't been done yet.
  - Hal followed up with some details of the prototype; wxWidgets has an unfortunate feature where all of the URI
    callbacks are called on the UI thread.  That isn't desired since a slow handler blocks the UI.  All of the
    underlying implementations support running handlers on non-UI threads.  The prototype needs to be changed to
    further explore that.
  - Hubert noted that an implementation could presumably host this as a single processs where the C++ code is the
    plugin, so we can't necessarily assume a thread model.
  - Hal responded that, on most systems, the straight forward implementation method has the UI driven by a thread
    in the same process, but the web content renderer code runs in a separate process driven by RPCs.  This will
    determine performance characteristics.
- Discussion of goals for WG14 in Ithaca (October 21st-25th):
  - JeanHeyd stated that he is planning to attend and to bring papers for:
    - \[nodiscard\]
    - Additional conversion functions for `char` and `wchar_t`.
    - Support for `C.UTF-8` as the default C locale.
  - Steve stated that the only thing that knows the encoding of `wchar_t` is the standard library and asked if any
    encodings other than UTF-16 or UTF-32 are used in practice.
  - JeanHeyd responded yes, AIX for Chinese locales uses Big-5.
  - Tom added that z/OS uses a wide EBCDIC.
  - Corentin asked what the motivation is for SG16 to add more conversion functions to C.
  - JeanHeyd responded that it allows C++ implmenentors to use features provided by C.
  - Tom suggested that it might be worth asking implementors what they would want and whether they would actually
    use C interfaces.
  - JeanHeyd acknowledged and stated he would ask.
  - Zach stated that such interfaces might be nice to have for C, but C interfaces can't achieve the performance
    that Bob Steagall demonstrated with his UTF-8 work.
  - JeanHeyd noted that, since these interfaces are based on NTBSs, they will need to check for null characters
    or know the string length ahead of time.
  - Zach suggested that, for performance, it may be worth only looking ahead 16 bytes at a time.
  - Tom stated that he is hoping to attend Ithaca and to bring papers for:
    - char8_t.
    - Make char16_t/char32_t string literals be UTF-16/32.
    - Named character escapes.
- Discussion of goals for Belfast (November 4th-9th).
  - Steve stated he would like to put together an initial pass at cleaning up terminology for encoding and
    character sets.
  - Hubert stated that he would be happy with SG16 bringing such a paper, but timing is bad for CWG given where
    C++20 is at.
  - Tom stated he would like to bring a paper to enable a portable method of specifying that source files are
    UTF-8 encoded.
  - JeanHeyd stated he is working towards getting funding to work nearly full time on the
    [P1629](https://wg21.link/p1629) standard text encoding paper.
  - Tom asked JeanHeyd what we can do to help prove the design works well in practice and suggested porting some
    project to it to demonstrate that:
    - the interface works and fits existing use cases.
    - that code is better.
    - that performance is retained or improved.
  - JeanHeyd responded that there are opportunities for a few checkpoints along the way.  For example, CppCon
    where a presentation is currently planned.
  - Tom asked for candidate projects that would be good for exercising the interface.
  - JeanHeyd responded that he had previously tried with a chat server and that a text editor would be a good
    choice.
- Tom confirmed that the next meeting will be on September 4th.


# July 31st, 2019

## Draft agenda:
- Cologne post-meeting discussion.
- Goals for WG14 in Ithaca (October 21st-25th).
- Goals for Belfast (November 4th-9th).

## Meeting summary:
- Attendees:
  - JeanHeyd Meneide
  - Mark Zeren
  - Peter Bindels
  - Tom Honermann
  - Zach Laine
- Discuss drafting guidance explaining our consensus regarding providing char/wchar_t, char16_t, and char8_t
  overloads in Cologne.
  - Tom introduced the need to discuss guidance by presenting poll results taken for three papers:
    - [P1030R2](http://wg21.link/p1030r2): std::filesystem::path_view:
      - `char` and `wchar_t` oriented interfaces should be provided that behave according to the
        `std::filesystem::path` specification in terms of encoding.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   3 |   2 |   0 |   4 |   2 |

      - `char32_t` oriented interfaces should be provided that behave according to the
        `std::filesystem::path` specification in terms of encoding.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   2 |   2 |   4 |   2 |   2 |

    - [P0267R9](http://wg21.link/P0267R9): A Proposal to Add 2D Graphics Rendering and Display to C++
      - Provide overloads for `char` (execution encoding) and `wchar_t`.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   4 |   3 |   3 |

      - Provide overloads for `char16_t`.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   5 |   2 |   3 |

      - Provide overloads for `char32_t`.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   3 |   3 |   4 |

    - [P1750R0](http://wg21.link/P1750R0): A Proposal to Add Process Management to the C++ Standard Library
      - Provide `std::process` `char` (execution encoding) and `wchar_t` interfaces.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   7 |   2 |   0 |   0 |   0 |

      - Provide `std::process` `char8_t` interfaces.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   3 |   0 |   5 |   0 |   0 |

      - Provide `std::process` `char16_t` interfaces.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   8 |   1 |   0 |

      - Provide `std::process` `char32_t` interfaces.

        |  SF |   F |   N |   A |  SA |
        | --: | --: | --: | --: | --: |
        |   0 |   0 |   3 |   5 |   0 |

  - Tom explained that, to an outside observer, our guidance looks inconsistent:
    - For polls about providing `char` and `wchar_t` based interfaces:
      - For P1030R2, we were evenly split with strong positions on both sides.
      - For P0267R9, we were fairly opposed to providing them.
      - For P1750R0, we were strongly in favor of providing them.
    - For polls about providing `char16_t` based interfaces:
      - For P1030R2, we didn't even ask the question (we know of UTF-16 based file systems).
      - For P0267R9, we were opposed to providing them.
      - For P1750R0, we barely could have cared less about the question.
    - For polls about providing `char32_t` based interfaces:
      - For P1030R2, we were evenly split with strong positions on both sides.
      - For P0267R9 and P1750R0, we were opposed (though more strongly so for P0267R9).
  - Zach addressed `char32_t` as the easy case first.  The `char32_t` overloads exist for completeness, but no one
    actually uses them.  They are inefficient.  `char32_t` is more useful for interfaces that accept non-contiguous
    data.
  - Mark stated that `char32_t` is useful when examining Unicode scalar values or elements of a grapheme cluster.
  - Zach replied that, If we have a grapheme cluster span like type some day, then we'll want a contiguous
    `char32_t` interface.  We can always add `char32_t` overloads as needed later.
  - Mark agreed that we can wait for use cases to materialize.
  - Tom asked if we should consider deprecating any existing `char32_t` interfaces.
  - Peter, despite not having been present for these polls and related discussion in Cologne, quickly recognized
    some patterns in the polls and offered some insightful rationale:
    - For P1750, we are replacing existing functionality, so need to support existing non-standard `char` and
      `wchar_t` based interfaces.  `char8_t` is our intended future direction, so we want that interface.  We don't
      want to emphasize `char16_t` and `char32_t` going forward.
    - For P0267, we are not replacing existing functionality, so we don't need `char`, `wchar_t`, `char16_t`, or
      `char32_t` based interfaces; we can restrict to `char8_t` for now.
    - For P1030, it seems like we don't know what we want.
  - Mark added an additional rationale for P0267; fonts are Unicode based, so it makes sense to just start with
    Unicode input.
  - Tom noted that, in the time since Cologne, Niall has decided to add `char` and `wchar_t` based interfaces to
    P1030.
  - Zach expressed support for Peter's observations; `char` and `wchar_t` based interfaces are important for migration
    purposes.
  - Mark agreed and noted that we don't want to construct road blocks for proposals for new interfaces.
  - Peter acknowledged that we don't want to make migration difficult and then raised the point that Apple's HFS+ and
    APFS filesystems are problematic for `path_view` because their behavior is non-portable.
  - Zach noted that similar problems exist for Windows with NTFS allowing UCS2 file names that are not valid UTF-16.
  - Peter provided an additional example regarding FAT derived filesystems storing locale case translation tables and
    noted that this is problematic when files are written with one locale and read using a different one (probably on
    a different system).
  - Tom returned to Peter's rationale in the context of P1030.  What is being proposed is a more performant alternative
    for some uses of `std::filesystem::path`.
  - Peter stated that the rationale for not providing `char` and `wchar_t` based interfaces is that the filesystem only
    offers bytes when names are enumerated.  If we give those bytes back, the filesystem will accept them.  We can get
    a displayable string, as from the `u8string()` member function of `std::filesystem::path`, but we can't necessarily
    pass that path back to the filesystem.
  - Tom stated that that rationale contradicts guidance regarding not wanting to construct impediments to migration.
    The vast majority of file names use only the basic source character set.  By not providing `char` interfaces, we're
    making very common use cases difficult.
  - Zach observed that support for all valid file names requires use of `char` on Linux and `wchar_t` on Windows today.
    The goal of the `std::byte` oriented interface is to provide something portable.
  - Tom objected to those interfaces providing a portable abstraction since:
      1. The underlying operating system interfaces used to implement those interfaces may themselves perform
         translations.  For example, the normalization performed by HFS+ and APFS, and
      2. Some OS interfaces don't support arbitrary byte sequences as file names.  For example, on Window's, a byte
         oriented interface would either use `CreateFileA` which would perform locale conversions, or `CreateFileW` which
         requires a sequence of 16-bit values (e.g., an odd number of bytes isn't supported).
  - \[Editor's note: at this point, Tom became completely engrossed in the conversation and utterly and completely
    failed to record individual commentary.  The following reflects his recollection of the discussion.
      - Zach lol'd at the contortions that Tom's face apparently exhibited as Tom struggled to comprehend why anyone
        thought the `std::byte` based interface was a good idea.
      - Tom was awakened to the possibility that the `std::byte` interface wasn't necessarily conceived of as a means to
        specify an actual sequence of bytes to be stored directly in the filesystem, but rather as a pointer to a sequence
        of bytes that represent an opaque structure that was (probably) provided by the OS in the first place.

    \]
  - Zach stated that `path_view` is intended for performance and doesn't support mutation.
  - JeanHeyd asserted that the `std::byte` oriented interface is intended to allow passing back to the OS a path name
    that was originally provided by the OS.
  - Zach agreed and added that the byte oriented interface is more like a handle to a file name, specifically a reference
    to something matching the representation stored in `std::filesystem::path`.
  - JeanHeyd added that the byte oriented interface exists for performance, but the `char` and `wchar_t` interfaces should
    be provided for simple portable uses.
  - Zach expressed a preference for making use of the `path_view` `char` based interface ill-formed on Windows and use of
    the `wchar_t` interface ill-formed everywhere else, but added he was now convinced that the `char` and `wchar_t` based
    interfaces should be provided.
  - Mark observed that providing those means we need to worry about life-time management and when conversions occur.
  - JeanHeyd responded that working implementations of `path_view` have already shipped and have demonstrated reduced
    overhead due to avoidance of allocation.
  - Tom expressed a preference for introducing a `raw_path` type to represent a canonical path rather than using
    `std::byte`.
  - JeanHeyd suggested using `std::filesystem::path::value_type` but noted that casts would still be needed.
  - Zach ponded the idea of a `raw_path` type that is only constructible from `wchar_t` on non-Windows systems and only
    constructed from `char` elsewhere.
- Tom confirmed the date for our next telecon; August 21st with the intent being to discuss [P1108R2](http://wg21.link/p1108r2) - `web_view`.


# June 26th, 2019

## Draft agenda:
- Discuss papers from the Cologne pre-meeting mailing.  At least:
  - P1629R0 - Standard Text Encoding
  - P0267R9 - A Proposal to Add 2D Graphics Rendering and Display to C++
    - just the new interfaces for text rendering.

## Meeting summary:
- Attendees:
  - Elias Kosunen
  - Hubert Tong
  - JeanHeyd Meneide
  - JF Bastien
  - Mark Zeren
  - Michael Spencer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Tom started the meeting with some administrative details:
  - Our regular meeting cadence would have us meet July 10th and July 24th, but the Cologne meeting is the 15th through
    the 20th.  Tentative plan is to skip the next two regular meetings, meet July 31st, and then back to our regular
    meetings during the 2nd and 4th weeks of the month in August.
  - Hubert asked when the post-meeting mailing deadline is.
  - Mark responded, August 5th.
  - Tom communicated that issue #8 (https://github.com/sg16-unicode/sg16/issues/8) has been closed as resolved by the
    adoption of [P1139R2](https://wg21.link/P1139R2) in Kona.
  - Tom also communicated that the revision of [P1423R2](https://wg21.link/p1423r2) in the Cologne pre-meeting mailing
    adds deleted `operator<<` overloads for wide streams for `char8_t`, `char16_t`, and `char32_t` following LWG
    feedback during their [May 21st paper review telecon](http://wiki.edg.com/bin/view/Wg21cologne2019/LWGTelecom21May).
    These changes will require LEWG review in Cologne.
- [P1629R0 - Standard Text Encoding](https://wg21.link/p1629r0):
  - JeanHeyd presented and provided a link to a draft revision (with only clerical errors fixed).
    - https://thephd.github.io/vendor/future_cxx/papers/d1629.html
    - The proposal includes low level and high level interfaces.
    - Normalization support will come later.
  - Peter (via chat): There is a typo in section 3.3.2, "GB1032" should be "GB2312" or "GB18030".
  - Elias (via chat): In 3.2.3.2, on the last line of the first snippet, the `basic_utf8` instead of `basic_utf16`
    is probably a typo?
  - Zach expressed surprise at the lack of low level transcoding algorithms and lack of iterator based interfaces.
  - JeanHeyd replied that those algorithms are implemented within the encoding object and that the interface is
    range based rather than iterator based.  Objects are used instead of free functions in order to maintain state.
  - Zach asked where code point conversion is happening; there isn't much state needed.  
  - JeanHeyd explained that roundtripping through the encoding handles code points internally.  State is needed for
    non-Unicode encodings and for error handling.
  - Zach stated that, in Boost.text, the error handler is a template parameter.
  - Zach asked if this design precludes doing performance optimizations like Bob Steagall has demonstrated.
  - JeanHeyd replied that such optimizations are excluded in the encoder interface, but are intended to be supported
    by specializing the high level interfaces; the specified free functions are customization points that can enable
    optimizations.
  - Tom asked why the `encode` and `decode` functions on the encoding object preclude optimizations.
  - JeanHeyd replied that they only process one code point at a time.
  - Zach asked what the motivation is for the slower interfaces over faster ones.
  - JeanHeyd replied that the `encode` and `decode` customization points are eager and convert as much as possible.
    The encoding object enables an iterative approach in which writing just the encoding object suffices to enable
    the high level interfaces to work correctly, but at a less-than-optimal speed.  
  - Steve said that it sounds like the code point at a time encoding object is the extension point for custom encoding.
    It is unlikely that anyone will bother with a high performance implementation for many legacy encodings as
    vectorizing support takes a lot of work.
  - Zach expressed support for a convenience approach and a fast path, but also sees value in an iterator approach as
    well.  Encoding details should be in either the algorithm (eager/fast) or in the iterator (lazy/slow).  Having
    building blocks for constructing iterators isn't key.
  - Zach expanded by contrasting with Python where the encode and decode functions always confused him because encoding
    and decoding are basically different names for the same algorithm with direction reversed.  This design seems over
    generalized.
  - Tom stated that the design is range based, so iterators can be wrapped in a range, does that not suffice for
    iterator use cases?
  - Zach replied that standard alorithms don't take an output range, they take output iterators.
  - Zach stated, when I'm doing a transcode, sometimes I want to loop and break, sometimes I just want to convert
    everything.
  - Peter stated he was confused by Zach's comments.
  - JeanHeyd attempted to paraphrase.  What Zach is saying, is rather than specify building blocks, we should specify
    lazy transcoding iterators.  The concern with that approach is that writing an iterator is a lot harder to do.
  - Tom agreed noting that he discovered how hard they are to write when working on text_view.  For example, decoding
    iterators need to eagerly consume code units.  
  - Mark noted that we don't need to make it easy for implementors to write iterators, but it is good to make things
    easy for other programmers.
  - Zach stated that someone still needs to write the lazy iterator.  There is an impedence mismatch between input
    and output.  A general template based iterator doesn't work.
  - Tom stated it did for text_view.
  - JeanHeyd stated that the ideas came from text_view and libogonek.  The encoding object avoids having to write
    iterators and ranges.
  - Zach stated he would like to understand how that works.
  - Tom explained how input text iterators and output text iterators can be used together; e.g., via `std::copy`.
  - JeanHeyd expounded; Libogonek proved this out and Peter's S2 library did something similar.
  - Peter (via chat): +1, doing exactly that in http://github.com/dascandy/s2.  I have the rope concept that
    combines different code-point iterators as a single range so you can copy from that to a target (and the
    assignment operator for target encodings is optimized to first calculate size & then do the copy).  
    `s2::basic_string<s2::encoding::utf8> u8s = u16s.view();`
  - Peter (via chat): 90% sure this is my hook for encoding conversion fast path -
    https://github.com/dascandy/s2/blob/master/include/s2/detail/rope_detail.h#L41
  - Zach said he would like to see the code in libogonek to better understand it.  It is well understood how encoders
    produce code units and decoders produce code points, but hard to see how transcoding can be done without missing
    optimization opportunities.
  - JeanHeyd explained that the fast path customization points enable that optimization by skipping the separate
    decode and encode steps.
  - Zach asked if iterator facade ever got standardized?  It makes writing iterators easy.
  - \[Editor's note: no they haven't.  The iterator facade proposal is [P0186](https://wg21.link/p0186).  It was
    discussed in Oulu in 2016.  Meeting minutes are [here](http://wiki.edg.com/bin/view/Wg21oulu/P0186).\]
  - Zach expressed skepticism regarding encoding builders; we just need to worry about common encodings.
  - Tom stated that there are use cases for code point at a time enumeration.
  - Zach agreed but stated that should be provided via lazy iterators; this design is taking generic programming too far.
  - Zach expressed a desire to be able to write a transcoding iterator that avoids construction of the intermediate
    code point value during conversion.
  - JeanHeyd noted that there are three extension points for customizing performance: the encoding object, transcoding
    iterators, and customization points.
  - Steve provided an example in which fast transcoding is trivial: transcoding ASCII to ISO-8859-1.
  - Mark observed that programmers want fast functions and transcoding iterators, not encoding objects. 
  - Steve stated that, within iconv's implementation, all transcoding conversions go through Unicode code points for
    all encodings.  This is presumably fast enough for most use cases.  Converting from Shift-JIS to Big-5 doesn't
    require extreme performance.
  - JeanHeyd stated that additional work is needed to enable that middle path with fast transcoding iterators.
  - Tom agreed; we need the lowest level for fall back to enable transcoding iterators between all encodings, but
    can optimize specific cases.
  - Zach stated that we really just need to list the specific transcoding iterators that are required.
- [P0267R9 - A Proposal to Add 2D Graphics Rendering and Display to C++](https://wg21.link/p0267r9):
  - Tom, unsurprisingly, stated that the interface should use `std:u8string` since it requires UTF-8 encoded text.
  - Michael agreed and expressed dislike for the asumption of UTF-8 in a `std::string` object.
  - Zach stated that the interfaces should be `std::string_view` and execution encoding.
  - Steve pondered whether all current graphical display systems are Unicode.
  - Tom stated that the X window system is locale based.
  - Zach suggested it would be least surprising to programmers to use execution encoding.  That way they can just
    pass regular strings.
  - Peter stated that, On UNIX systems, UTF-8 tends to be the default, so things will work as is, but Windows
    would be problematic.
  - Zach observed that, without standard library support, converting text from execution encoding to UTF-8 is hard.
  - Peter suggested leaving it to the UI libraries to figure it out.
  - Zach responded that this is a UI library, so we need to figure it out.
  - Michael pondered whether we should add overloads for `char`, `wchar_t`, `char8_t`, `char16_t`, and `char32_t`.
  - Zach suggested that we only need `char` and `char8_t`.
  - Hubert observed that the standard library is designed around locales.
  - Tom asked Hubert to clarify, are you thinking these interfaces should take a locale object?
  - Hubert responded that, if you have strings that you don't know the encoding for, then yes.
  - JeanHeyd expressed a preference for just using `std::u8string` to avoid locale dependencies.
  - Mark agreed that, perhaps, just `char8_t` is enough.
  - Tom stated that, by the time 2D graphics is standardized, we should be able to get good conversion routines in
    the standard library or we will have failed miserably!
  - Hubert observed that the paper is missing bidirectional language support.
  - Tom noticed that the paper doesn't say what happens with ill-formed encoded input.
  - Mark suggested discussing font names; these should probably be bag-of-byte names.  The paper defers to the HTML
    CSS specification.
  - Zach noticed that the paper doesn't discuss normalization.  It would be nice if it called it out specifically.
  - Tom asked if normalization matters.
  - Zach responded that it does in some cases.
  - JF suggested that we should make it possible to defer to the CSS specification if we can't right now.  We don't
    want to do what we previously did in forking the Unicode identifier specification from
    [UAX#13](https://unicode.org/reports/tr31)
  - Mark noticed that some of the interfaces pass and return `std::string` by value where they probably shouldn't.
  - JF pondered about overlap with SG13 and avoiding conflicts in scheduling when meeting in Cologne.
  - \[Editor's note: SG13 and SG16 are meeting on separate days.\]
- [P1750R0 - A Proposal to Add Process Management to the C++ Standard Library](https://wg21.link/p1750r0):
  - Elias described the overlap with [P1275](https://wg21.link/p1275) and stated he is aware of previous SG16
    review and is working with Isabella Muerte.
  - Elias described the pipe interface.
  - Tom asked if any operating system supports wide pipes.
  - Elias stated he is unsure if Windows does.  The interface is templated on char type.
  - Tom stated that Windows doesn't; `ReadFile` and `WriteFile` are used with pipes and they are byte oriented.
  - Hubert asked about the interaction with streams.
  - Elias responded that pipes can be wrapped in iostreams.
  - Tom summarized the feedback so far: wide pipes may not be needed and prior SG16 concerns regarding environment
    variables still stand.
  - Tom stated that command lines probably need to be considered to be in execution encoding.
  - Hubert stated that, for command lines, `exec` interfaces will likely be used and they use arrays, not strings.
    A formatting approach makes sense.
  - Elias stated that `process_launcher` takes a `std::filesystem::path`, not a string.
- Meeting in Cologne.
  - Tom communicated the tentative schedule for when SG16 would meet.
  - Zach stated he will miss Monday.


# June 12th, 2019

## Draft agenda:
- Discuss and provide feedback for any draft papers targeting the 6/17 pre-Cologne mailing.

## Meeting summary:
- Attendees:
  - Nathan Myers
  - JeanHeyd Meneide
  - Mark Zeren
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Planning for Cologne:
  - Tom communicated that SG16 has requested a half day session in Cologne.
  - Tom communicated that SG16 will host an evening session.  Potential topics (subject to author's desire) include:
    - UTF-8 and current ecosystems.
    - JeanHeyd's work on transcoding interfaces.
    - Corentin's work on character properties.
    - Hana's work on Unicode support in CTRE.
  - JeanHeyd confirmed that his transcoding interfaces paper will appear in the pre-meeting mailing.
- Discussion of the file name constraints added to the draft D1238R1 posted to the SG16 mailing list:
  - http://www.open-std.org/pipermail/unicode/2019-June/000386.html
  - Steve expressed approval for the new section.
  - Zach agreed noting uncertainty that anyone cares about the details of normalization-insensitivity.
  - Tom concurred and indicated he was unsure how important that is.
  - Zach stated that it is important since extremely subtle bugs can happen from changing normalization.
  - Tom acknowledged the possibility and noted reported problems for Apple's migration from HFS+ to APFS.
  - Zach observed that there is no good way to tell what filesystem you are working on and what its
    idiosyncracies are.
  - Nathan asserted that programmers have to deal with presentation of file names and allow user selection.
  - Steve noted that different file names can present the same (due to Unicode confusables or normalization
    differences).
  - Zach recalled an email from Marshall Clow some time ago regarding file systems using completely different
    normalization schemes.  Different filesystems do things differently.
  - Nathan stated that uploading a file to a web site also has presentation issues.
  - Mark stated that jumping from one filesystem to another is inherently lossy, but treated as a transfer issue.
    The only way to store a file accurately in text is to write it in something like base64.  Writing a file name
    to a text file may break the encoding of the file.
  - Zach claimed that we can't fix these issues except by declaring "things must work" and letting implementors
    figure it out, which they probably can't do.
  - Steve noted that we keep getting asked about handling of file names and this is intended to document constraints.
  - Mark recalled an example; from the stack trace proposal, we specified file names be handled as a sequence
    of bytes.
  - Tom mentioned he was thinking about sending an email to the Unicode Consortium's mailing list asking about
    current thinking regarding file names in text files.
  - Mark argued that we should just try and stay out of this space.
  - Tom asserted it is a big question for `std::text`.  How do we allow file names in `std::text`, particularly
    if we require well-formed content?
  - Mark suggested relying on an error policy.
  - Zach claimed that we need to emphasize that, if a file name is retrieved from the file system, programmers must
    maintain it as is.  Don't mutate it at all, don't compare it to text.
  - Tom asked how one puts file names in text and have it be well-formed text?
  - Zach replied simply, you don't.
  - Mark provided an example of Apache using base64 encoding of names in URLs.
  - Zach asserted that applications must provide a file selector interface.
  - Tom asked how one would write `ls`?
  - Zach responded that the file name be written in a presentation format that isn't necessarily suitable for
    referencing the file.
  - Steve observed that this already happens all the time that file names appear in output, but can't be parsed out
    or referenced as is.
  - Tom acknowledged and observed this is why GNU `find` has a `-print0` option.
  - Nathan suggested that we may need to publish a document on how to deal with file names.
  - Steve mentioned that we have `std::filesystem` and it has facilities for getting names out of paths.
  - Zach claimed that problems happen if, for example, you have a UCS-2 file name on Windows that is ill-formed
    UTF-16.
  - Tom confirmed that recent Windows 10 releases still allow creation of file names that are not valid UTF-16.
  - Zach asserted that we don't want interfaces that do transcoding or normalization to touch filenames.
  - JeanHeyd suggested adding a new non-directive to the paper stating that we won't attempt to impose restrictions
    on file names.
  - Tom agreed to do so.
  - \[Editor's note: Tom did so in [P1238R1](https://wg21.link/p1238r1) for the Cologne pre-meeting mailing\]
- Discussion of planned transcoding papers:
  - Zach stated he wasn't going to be able to produce a paper on transcoding for the Cologne pre-meeting
    mailing.
  - Tom let Zach know that was ok, especially since JeanHeyd was who had volunteered to write that paper and is
    currently working on a draft.
  - Zach noted a performance concern to address in the paper; generic transcoder interfaces don't perform well
    with smart iterators.  For maximum performance, vector operations must be used as Bob Steagall demonstrated.
  - Tom acknowledged that specializations for contiguous storage are needed.
  - JeanHeyd said he came to the same conclusion and that the paper would discuss it.  He also indicated intent
    to share the draft on the SG16 mailing list.
  - \[Editor's note: JeanHeyd later shared that draft on the SG16 Slack channel.  The draft can be found at
    [https://thephd.github.io/vendor/future_cxx/papers/d1629.html](https://thephd.github.io/vendor/future_cxx/papers/d1629.html)
    and will be in the pre-meeting mailing as [P1629R0](https://wg21.link/p1629r0).\]
- Discussion of z/OS compiler updates:
  - Tom communicated recent news within the z/OS ecosystem.  IBM recently released versions of Clang for z/OS with
    their latest updates for their xlC compiler.  Additionally, a third party provider also maintains a z/OS
    C++14+ compiler based on LLVM.  Tom stated the details would appear in a revision of P1238.
  - \[Editor's note: Tom did add those details to [P1238R1](https://wg21.link/p1238r1) for the Cologne pre-meeting
    mailing\]
- Discussion of Boost review for JeanHeyd's [`out_ptr`](https://github.com/ThePhD/out_ptr).
  - Zach communicated that Boost formal review for JeanHeyd's
    [`out_ptr`](https://github.com/ThePhD/out_ptr) library would begin on Monday June 17th and encouraged everyone
    to participate via the Boost mailing list.
- Discussion of C standard string transcoding functions:
  - JeanHeyd asked for feedback regarding a set of transcoding functions he is considering proposing to the C
    committee at their October meeting in Ithaca.  The functions match the existing C `mbstowcs`/`wcstombs` and
    `mbsrtowcs`/`wcsrtombs` functions but transcode between UTF-8 (`char8_t`), UTF-16 (`char16_t`), and UTF-32
    (`char32_t`).  The full cartesian product for all of the encodings results in approximately 40 functions.
    He is wondering if the full set is needed or if a reduced set would suffice.  These functions are not used
    often and aren't very performant.
  - Tom stated that `mbstowcs` should be able to perform ok.
  - JeanHeyd stated that dropping the restartable ones would reduce the number, but those are useful in some cases.
    Another approach is to just propose the `c8`, `c16`, and `c32` variants that convert between the execution
    encoding.
  - Tom agreed that just providing conversion between the execution encoding and UTF variants was probably sufficient.
- Discussion of updates to [P1072](https://wg21.link/p1072):
  - Mark provided an update regarding plans for [P1072](https://wg21.link/p1072).  There are two options:
    - Propose a lambda based interface.
    - Propose an independent class coupled to `std::string`.
  - Mark clarified that neither proposal would appear in the pre-meeting mailing.
  - Zach expressed a desire for the functionality and for additional progress to be made.
- Discussion of planned C committee proposals:
  - Tom asked for any volunteers interested in writing and presenting papers to the C committee in October that
    propose functionality we've added or plan to add for C++.  Such features include:
    - `char8_t` ([P0482](https://wg21.link/p0482))
    - Make char16_t/char32_t string literals be UTF-16/32 ([P1041](https://wg21.link/p1041))
    - Named character escapes: ([P1097](https://wg21.link/p1097))
  - JeanHeyd asked if we had ever followed up with the C committee regarding any known implementations that use
    an encoding other thatn UTF-16/UTF-32 for `char16_t`/`char32_t` literals or that don't define
    `__STDC_UTF_16__` and/or `__STDC_UTF_32__`.
  - Tom responded that Philipp Krause had confirmed that there are no known implementations.
  - \[Editor's note: though not mentioned in the meeting, there are implementations that use UTF-16 and UTF-32,
    but neglect to define the `__STDC_UTF_16__` and/or `__STDC_UTF_32__` macros.\]


# May 22nd, 2019

## Draft agenda:
- Axel Andrejs from Microsoft will present and discuss Microsoft's ongoing efforts to improve UTF-8 support in Windows.

## Meeting summary:
- Attendees:
  - Axel Andrejs
  - Henri Sivonen
  - Hubert Tong
  - JeanHeyd Meneide
  - Mark Zeren
  - Steve Downey
  - Tom Honermann
- Microsoft's on-going efforts to improve UTF-8 support in Windows.
  - Axel lead with some Windows history and current efforts:
    - Windows was initially developed using locale dependent code pages, but switched to UTF-16 long ago.
    - Today, the industry is moving to UTF-8, especially on the web.
    - So, what to do about UTF-8?  Initial efforts were to improve resource managers, but Windows remains UTF-16 based.
    - Now, what about the rest of the OS?  Windows 10 added support for UTF-8 as an (algorithmic) active code page (ACP).
    - All of Windows' "ANSI" interfaces use `MultiByteToWideChar()` to convert `char` based input to UTF-16 using the
      active code page.  This suffices to make UTF-8 mostly magically work, though Microsoft platforms remain UTF-16 based.
    - Within the industry, most Windows developers don't test support for many code pages; usually just a few for
      critical markets.  This leaves a large testing gap.
    - UTF-8 poses some problems as a code page.  Testing UTF-8 support has revealed cases of code that fails due to a
      number of issues:
      - It is variable length and may require more than two code units per code point.  Code that (incorrectly) assumes 
        wide strings are always larger (in terms of bytes) than the corresponding narrow encoding can cause buffer
        overflows.
      - The native C and C++ character type is `char` which is good in terms of flexibility, but bad in terms of type and
        encoding safety.  `char` can be used for UTF-8, but failure to perform conversions where needed leads to mojibake.
      - Some code just plain fails with any non-ASCII characters.
      - Many programs assume an encoding (ASCII or Windows-1252) and fail with UTF-8.
    - Because of known cases of existing code failing when the active code page is changed to UTF-8, Microsoft has no
      plans to ever change an existing machine's active code page.  There is too much potential for breakage.
    - Current efforts include improving UTF-8 support for individual Windows components, resource managers, resource
      loaders, etc...  UTF-8 strings tend to be approximately 1/3 the size of wide strings on average.  Focus on where
      that savings is beneficial.
    - UTF-8 as active code page is still a beta option because there are major applications that don't work correctly
      when it is enabled.  Most applications work ok in the US, but have problems elsewhere.
    - Outside Windows desktop where compatibility with legacy applications is less important, Windows platforms are
      moving more towards UTF-8.  These include Xbox, Hololens, smart devices, etc...
    - Bifurcation will continue.  We may evangelize UTF-8 in some markets, but are unlikely to ever be able to move the
      entire Windows ecosystem to UTF-8.
    - The latest Windows 10 release allows executables to opt-in to UTF-8 as active code page via a fusion manifest.
    - May add support for executables to opt-out of UTF-8 support for compatibility, either via a manifest setting or
      application compatibility shim.
    - Windows subsystems will continue to migrate to UTF-8.
    - Would like to discontinue the ANSI/Wide interface split.  Likely to introduce more interfaces that are UTF-8/Wide
      or just UTF-8.
    - There are no plans for a native Windows UTF-8 kernel.
    - We'll continue to reach out to major applicaions that are found not to work correctly when the active code page is
      set to UTF-8.
    - Within Microsoft, a number of developers have UTF-8 enabled as the active code page on their workstations.
    - We will continue to do more ecosystem outreach as our confidence in UTF-8 as active code page increases.
    - But, Windows will always need to retain compatibility.
  - Henri asked if there are plans to augment existing ANSI/Wide interfaces with U8 variants that only work with UTF-8.
  - Axel responded that they would like to do so where it makes sense.  Decisions to do so are up to component owners.
    Feedback and requests for specific interfaces are appreciated.  There are no plans for mass conversion.
  - Henri asked what would happen if an executable that was marked to run with UTF-8 was run on an older platform.
  - Axel replied uncertainly that the fusion manifest entries would probably just be ignored.  This is what happens with
    Universal Windows Programs (UWP) support.  Unsure if there is a way to mark the executable to fail in such cases,
    but the executable could be marked to require a particular level of OS support.
  - Mark asked how an executable that opts-in to UTF-8 as ACP would interoperate at the command line.  Is any transcoding
    performed for stdin/stdout?
  - Axel responded that, at present, all the opt-in does is override the ACP, so no, no transcoding of the command line
    or standard streams is performed.
  - Mark observed that this can then lead to failures.
  - Axel affirmed adding that thought has been put into implicit transcoding, but it is a hard problem.
  - Tom agreed noting that file names pose a significant problem since they may not be representable in a particular
    encoding.
  - Axel acknowledged, but stated that most file names are UTF-16.
  - Henri asked about the new terminal coming to Windows 10.  How will it know how to interpret the output of a particular
    program?
  - Axel stated that there are active discussions about this and decisions are not yet settled, but people are working
    on it.
  - Tom asked about recommendations for current developers.  How do we move into this new world?
  - Axel responded that `char*` is kind of nice for it's genericity but isn't safe.  Stronger types add safety, but
    increase the interface surface area.  `char8_t` is a big topic.  ICU supports both `char16_t` and `wchar_t`, but
    adds surface area.  As a global model, that doesn't work too well.  If targeting Windows only, best to stick to wide
    strings.  For cross platform, we're all on this journey.  Would like more feedback.  There are always workarounds
    because developers can do conversions themselves.  If there is demand, we'll add additional interfaces if the value is
    there.  Would like more support for command line handling.  Really want the industry to move to UTF-8 as ACP.  Library
    writers have to worry about all code pages anyway, including now UTF-8.
  - Mark asked how new types like `char8_t` fit in.
  - Axel expressed similar curiosity.
  - Tom provided some thoughts on `char8_t`.  Unsure what kind of adoption will occur.  Expecting to see uses in niches or
    as an internal encoding type.  Type safety can be used to guard components that are UTF-8 only from components that are
    locale dependent.
  - Henri asked if type based alias analysis is planned for the Microsoft compiler.
  - Axel responded that he was unsure of the compiler team's plans.  Windows interfaces have pretty basic types, so there
    is a lot of targeting lowest common denominator.  Always looking to take advantage of new features.
  - Mark offered the idea of a compiler option that would allow use of `char8_t`, but would mangle it the same as `char`
    for compatibility with prior compiler versions.  This would require errors for ambiguous overloads, but might still
    be useful.
  - Tom expressed interest noting that Microsoft already does something similar to duplicate symbols for `char16_t` and
    `wchar_t`.
  - Axel confirmed noting that they sometimes put code in headers and compile it twice (e.g., for ANSI and UNICODE
    expansions of `TCHAR`).
  - Henri asked why `char16_t` was not made the same type as `wchar_t` on Windows.
  - Hubert responded that C++ requires different types for overloading purposes.  Also because the encoding can differ.
  - Henri pondered whether, in retrospect, it would have been better if `char16_t` was specified as the same type as
    `wchar_t` on Windows and `char32_t` the same type as `wchar_t` on POSIX systems.
  - Steve stated that anyone attempting to write portable code is unhappy with `wchar_t`; it just isn't portable.
  - Mark added that the type separation is useful.  For `char8_t`, the non-aliasing properties are a good motivator for
    a separate type.
  - Steve concurred noting that injecting Unicode into the type system will be useful.  Additionally, `std::byte` will
    help us move further away from `char` for everything.
  - Axel mentioned that, on Windows, there are few APIs that take `char*` and that expect an encoding other than the ACP.
    The only indication is in documentation; the type system can't help enforce encoding expectations today.
  - Mark asked what code page is used for Windows Subsystem for Linux (WSL).
  - Axel responded that he would have to check, but once code reaches the kernel, everything is UTF-16.
  - Tom observed that different encoding expectations in Windows vs the WSL makes piping data problematic.
  - Mark surmised that the WSL uses UTF-8 like most Linux distributions.
  - Axel added that the International Platform team didn't do anything special for WSL.
  - Mark speculated that, if we decided to be very aggressive, we could require C++ code on Windows to run with the UTF-8
    manifest option.
  - Axel confirmed, but noted that requires new OS versions.
  - Tom asked Axel if his team had reached out to other language maintainers like for Python, Ruby, and Go.
  - Axel responded yes for .NET languages obviously, but not for other languages.  Need to reach critical mass internally
    first, and then will expand outreach to other languages.
  - Henri asked about enabling app development with UTF-8 on older OS versions.  Are there any plans for the standard
    library to provide UTF-8 interfaces that convert to internal UTF-16 ones?
  - Axel responded that work is progressing to improve support for UTF-8 in the CRT, but not sure of the time line.
  - Mark asked about any work on interfaces that operate at the grapheme cluster level.
  - Axel responded no, at present, they are more focused on basic APIs like `CreateProcess`.
  - Tom asked how SG16 can help with the effort to improve UTF-8 support.
  - Axel explained that the big challenge is how to handle the lowest common denominator.  New language features are used
    internally, but public APIs are very old school and limited to basic types.
  - Tom clarified, so keeping interfaces indpeendent of fancy new language features is helpful?
  - Axel responded yes, but always interested in new types that make sense within the Windows type system.
  - Tom summarized all of the different encodings that the C++ standard has to interact with; source encoding, internal
    compiler encoding, presumed (compile-time) execution and wide execution encodings, (run-time) execution and wide
    execution encodings, UTF-8, UTF-16, and UTF-32.  How do all of these encodings affect you?
  - Axel responded that they sometimes have to guess about encodings; may rely on BOMs or recognition of UTF-8.
  - Tom asked if Microsoft had ever considered allowing filesystems to support tagging files as having a particular
    encoding.  Some other OSs like z/OS have such support.
  - Axel responded no, not aware of any such efforts.
  - Mark asked if Windows makes use of the Unicode Private Use Area (PUA).
  - Axel responded yes, because, given the size of the development team at Microsoft, the answer to "do we use ..." is
    always yes somewhere.
  - Henri commented that Microsoft's eudcedit.exe editor generates a magic font for the PUA.
  - Tom asked if Axel had any thoughts about changing the default "C" locale to be UTF-8.
  - Axel responded that it might work out ok.  Old CRTs still get used though.  But this would make it easy for
    programmers to start using UTF-8.
  - Mark noted that Microsoft maintains backward compatibility, but that there may be some desire or intent for an ABI
    break at some point.  Perhaps that would be the right time to change the default locale encoding.
  - Henri asked if layering new versions of C++ on top of older C and C++ run-times is supported or whether new C++
    language standards require the latest C and C++ run-time libraries.  Would it be possible to have the compiler set
    the per-binary UTF-8 flag depending on target language level?
  - Axel responded that the UTF-8 flag affects the process, so can't depend on DLL options or settings.
  - Mark brought up a new issue; at some point, we will require various Unicode data sets.  Windows now distributes a
    version of ICU.  Concerns about the size of the chrono library were raised when it was added to the standard and it
    is much smaller than the Unicode data set.  We'll likely require at least data for normalization and collation.
  - Axel provided some additional background.  Windows has NLS interfaces.  ICU was added to Windows 10 two years ago,
    but application developers still want to target Windows 7 where it isn't available.  Windows 10 now supports about
    3-4 times more locales than Windows 7 due to the inclusion of the CLDR.  Carrying ICU with an application is
    becoming a significant servicing issue.  Time zone data bases were integrated into Windows to address similar
    servicing issues, but have to be updated often and quickly for geopolitical reasons.  CLDR data is unlikely to
    be updated as frequently.
  - Henri asked for more details.  How is ICU updated in Windows 10?  Will older Windows 10 releases get updates?
  - Axel responded that the latest available ICU is distributed in each 6 month release cycle, but that locale data and
    Unicode versions are not otherwise patched.  Exceptions could be made, but would require significant motivation like
    the geopolitical reasons that motivate time zone updates.
  - Henri surmised that older Windows 10 releases won't get support for new Unicode characters, data tables, etc...
  - Axel confirmed.
  - Hubert stated that he had heard that the ICU distributed in Windows 10 does not exactly match any official ICU
    release.
  - Axel confirmed adding that patches are made for geopolticial reasons.
  - JeanHeyd stated that the road to UTF-8 support is going to be a long one.  He plans to take papers to the C and
    POSIX committees proposing to change the default locale to UTF-8 in order to facilitate a similar change for C++.
    The goal is to allow applications to at least be able to communicate without mangling text.  It sounds like
    Microsoft is heading in a good direction, but the C committee may be reluctant to make such a change.
  - Axel agreed that this will be a long journey and encouraged everyone to play with the new UTF-8 functionality,
    report problems, and poke application providers to improve support.  The problems are not massive, but cost/benefit
    analysis must line up as always.  Application providers will be required to support UTF-8 as ACP for some Microsoft
    platforms like the Xbox and Hololens.
  - JeanHeyd commented that our biggest concern has been how to migrate to a UTF-8 world.  At least it sounds like there
    is a path to follow.


# May 15th, 2019

## Draft agenda:
- Continue discussion of UTF-8 as execution encoding.  Our focus last time was on impediments to use of UTF-8 as
  execution encoding.  Focus this time will be on anticipated benefits of mandating UTF-8 and impact to existing
  ecosystems.

## Meeting summary:
- Attendees:
  - Cameron Gunnin
  - Henri Sivonen
  - Hubert Tong
  - JeanHeyd Meneide
  - JF Bastien
  - Michael Spencer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Discussion of potential benefits/costs of mandating UTF-8 as execution encoding:
  - Tom introduced the topic with a brief summary from the last meeting.
  - Zach stated he was all for moving to UTF-8.
  - Tom asked how code would be written differently compared to today.
  - Zach presented some problematic examples he has encountered in the past.  The first was surprises with UTF-8
    encoded literals in source code not retaining UTF-8 encoding at run-time.  The second was difficulties writing
    text and having it display in terminals as expected.  Today's compilers don't have options to state that the
    output of a program will have any particular encoding.  Writing non-ASCII output is expert territory.  We can't
    write portable code that dumps text and expect it to just work.
  - Tom noted some subtleties with those examples; there are actually four encodings involved.  Source encoding,
    presumed execution encoding, run-time execution encoding, and terminal/console encoding.  This raises the question
    of what is meant by mandating UTF-8.  Mandating it for all of these encodings?
  - Steve stated that these issues affect all platforms.  Use of characters outside the basic source character set
    doesn't work unless `std::setlocale()` is called to set a locale other than `"C"`.  Changing the default locale
    to `"C.UTF-8"` would be an improvement as it would suffice to make the multibyte conversion functions work as
    expected without changing behavior for character classification functions.  This matches what Python is doing
    as described in [PEP-538](https://www.python.org/dev/peps/pep-0538) and
    [PEP-540](https://www.python.org/dev/peps/pep-0540).  This still allows the locale to be run-time selectable,
    but provides a better default for character encoding.
  - Tom commented that this would preserve existing behavior since, today, unless `std::setlocale()` is called to change
    the current locale, characters outside the basic source character set elicit undefined behavior for the multibyte
    conversion functions.
  - Zach asked how this would be proposed.  By defining a "C.UTF-8" locale?  Or by specifying that the default "C"
    locale operate as if `LC_CTYPE` were set to UTF-8?
  - Steve responded that the implementation behave as though an implicit call to `std::setlocale(LC_CTYPE, "C.UTF-8")`
    occurred during process startup.
  - Henri observed that the behavior of `nl_langinfo` would be affected by doing so; `nl_langinfo(CODESET)` would now
    return a string reflecing UTF-8 rather than the encoding used to implement the "C" locale.
  - Zach noted that such a change needs discussion with WG14 and POSIX members.  It would not be good if behavior
    differed based on whether C or C++ headers were included.
  - JeanHeyd indicated that he is already working on such a discussion and plans to submit a paper to WG14 proposing
    that "C.UTF-8" be made a standardized locale.
  - Steve noted that POSIX exposes more encoding aware facilities than C does; more character classification functions
    for example.
  - Zach asserted that, if we made UTF-8 the default, life would be easier for everyone.
  - Tom summarized discussion so far; we've been discussing changing the default locale, but not mandating UTF-8.
  - Hubert noted that mandating UTF-8 will affect presumed encoding.
  - Henri suggested that mandating a particular encoding might solicit reluctance from implementors.  If implementors
    don't go along, then the standard doesn't match reality.
  - JeanHeyd agreed with the concern and noted that changing the default leaves open an escape hatch for preserving
    existing behavior.  While mandating a particular encoding would make some things easier, it would also leave some
    platforms and/or implementations behind.
  - Tom asked Hubert for his perceptions regarding changing the default; how would the platforms he supports be impacted?
  - Hubert replied that, on z/OS, it would be kind of odd due to the possibility of multiple processes sharing the same
    language environment.
  - Tom asked what happens today if a single process changes its locale.
  - Hubert responded with some uncertainty.  Switching between EBCDIC code pages is much less impactful than switching
    from an EBCDIC code page to something ASCII based would be.
  - Hubert returned to questions of implementation; how would the implicit call to `std::setlocale()` be implemented?
    This isn't a typical language level thing.
  - Tom responded that such a question is what he would have posed to Hubert.
  - Hubert elaborated on potential complexities.  How would this work when separately compiled components potentially
    compiled for different standard versions are linked together?  Is this a linker option?
  - Tom stated that is outside the scope of the standard.
  - Hubert agreed, but noted that concerns like this don't come up very often.
  - Zach reiterated the intent; that the C++ startup code perform as if an implicit call to `std::setlocale()` took
    place.
  - Hubert acknowledged the intent, but noted the potential unintended effects that Henri eluded to earlier.  For example,
    on AIX, Hubert tried a program that displays the current locale encoding.  When invoked with `LANG=C`, it indicated
    ISO-8859-1.  An implicit call to `std::setlocale()` would change this behavior.
  - Tom said he would like to see a concrete example of that behavior.
  - \[Editor's note: Tom later experimented on a Linux system and observed the same behavior:

        $ cat t.cpp 
        #include <langinfo.h>
        #include <locale>
        #include <cstdio>
        
        int main() {
          std::printf("%s\n", nl_langinfo(CODESET));
          std::setlocale(LC_CTYPE, "");
          std::printf("%s\n", nl_langinfo(CODESET));
        }
        
        $ g++ t.cpp -o t
        
        $ LANG=C.UTF-8 ./t
        ANSI_X3.4-1968
        UTF-8

    \]
  - Zach suggested that the multibyte conversion functions don't really work now,
    so changes can be made.
  - Hubert disagreed and stated they work exactly as intended.
  - Steve stated that functions like `std::wctomb` will silently drop or replace characters for the "C" locale.
  - Tom asked Zach if this is an example of what he meant when he said they were broken.
  - Zach replied, yes.
  - Henri noted that silently dropping/replacing characters can be a security issue.  By specifying behavior, we
    may reduce security problems.
  - Hubert agreed that, if you don't do proper error checking, that can lead to problems.
  - Tom asked if these functions have appropriate error handling interfaces.
  - JeanHeyd stated that they do, they return -1 on error.
  - Tom clarified, yes, they return -1 if an ill-formed code unit sequence is encountered, but do they also return in
    error if a character lacks representation in the current locale and a replacement character is substituted?  Tom
    thought at least some implementations substituted replacement characters without errors.
  - Tom summarized the ramifications of an implicit `std::setlocale()` call; doing so is a breaking change given
    Henri and Hubert's observations about querying the current locale encoding.
  - Hubert agreed, noting that non-exotic platforms are impacted.
  - Steve suggested that the observeable impact should be limited to querying locale properties.
  - Hubert stated that may be true, but that we haven't discussed presumed execution ncoding yet.  The standard only
    discusses one execution encoding, but there are two.
  - Tom acknowledged and added that we know this to be problematic as it imposes a lowest common denominator approach
    for encoding literals.  If the presumed execution encoding were UTF-8, that would clearly be problematic on z/OS,
    but even on ASCII based platforms, if the locale can be changed at run-time, that limits use of UTF-8 in literals.
  - Hubert commented that the fallout for z/OS for changing presumed execution encoding may not so bad because
    extensions are already available to specify execution encoding and to opt into an ASCII based encoding.  Additional
    support might be needed for locale encodings.
  - Tom asked to clarify what was meant by additional support.
  - Hubert responded that he was thinking about message catalogs used with translation.  Generally, messages can be
    written in a common subset of characters available in all locales.  If we mandated an encoding that doesn't share
    a common subset (e.g., UTF-8 on a predominantly EBCDIC based platform), then strings would have to be maintained
    in resource files outside of translation units, or written in escape sequences.
  - Tom asked if Unicode escape sequences are used much on z/OS.
  - Hubert responded that, in newer code, yes, but generally only in Unicode literals, not in ordinary or wide literals.
  - Tom returned to the question of benefits of mandating a single execution encoding.  If we did so, then we could make
    text processing decisions at compile-time.
  - JeanHeyd suggested that we can do that anyway.
  - Tom responded that, no, evaluation of functions that are locale dependent must be deferred until run-time since the
    encoding is not known.
  - Tom asked about the feasibility of changing the default locale given existing ecosystems.  We would have to work with
    POSIX, WG14, implementors, other languages?
  - Zach reiterated that he wants to see the portability problems writing to terminals be fixed.
  - Tom asked, but isn't that a problem not specific to C++?  All languages face this issue.
  - Zach noted, for all processes, data comes out as bytes, but terminals can't handle them.
  - JeanHeyd noted that codecvt facets may interfere, but the primary difficulty programmers face on Windows is that the
    default terminal settings and execution encoding are locale dependent.
  - Zach observed that, if everything was UTF-8, then the terminal could just do the right thing.  But we can't mandate
    behavior for all languages.
  - Henri asked if Microsoft's new terminal might help.
  - Tom stated that it should, but will require some form of opt-in.  Historically, Microsoft's default console encoding
    has been constrained by backward compatibility.  The encoding of the console differs from the locale encoding in
    order to support those old applications that depend on line drawing character sets.  Unclear how new applications will
    opt-in to UTF-8 behavior.
  - Zach suggested that just having a way to determine if the current locale supported UTF-8 would be useful.
  - Henri asserted that the experience with Python demonstrated that such approaches don't work in practice.  Asking the
    C environment what the execution encoding is rather than just assuming it may actually cause more problems.  What
    would you do if the current encoding wasn't compatible?
  - Zach replied that, if the encoding is known, then the program can convert.
  - Tom stated that is how the multibyte conversion functions are already specified to work; if they are used, then the
    output will match locale encoding.
  - JeanHeyd expressed having unsatisfactory experience with the multibyte conversion functions.  For example, Microsoft's
    implementation of `mbrtoc32` unconditionally converts between UTF-8 and UTF-32 in violation of the standard.  The
    conversion functions are also unable to detect some kinds of mojibake; for many single byte encodings, all possible
    code unit sequences are valid.
  - Hubert concurred that the multibyte conversion functions are not a good alternative to ICU.  Discussions about
    `source_location()` are touching on a bigger problem; C++ is just one language residing in a large ecosystem in which
    implementors are beholden to the platforms they support.
  - Henri asked about wide characters being compatible across locales.  What encoding does z/OS use for them?
  - Hubert deferred to documentation and noted that, on AIX, the wide character set does vary for some Chinese locales.
  - Tom stated that the wide character set on z/OS is a wide form of EBCDIC with support for ISO-2022 escape sequences.
  - Hubert followed up regarding the wide character sets used on AIX.  Depending on the size of `wchar_t`, either
    UTF-16 or UTF-32 is used except for the Taiwanese locale which uses Big-5.
  - Tom asked JF what benefits Apple might see from changing the default locale encoding to UTF-8.
  - JF responded that there would be some simplicity.
  - Tom pondered if the biggest benefit to Apple would come from dropping locale dependent encoding completely.
  - Hubert asserted that isn't feasible; IBM customers are known to create their own custom locales.
  - Steve noted that one way in which applications are meeting the requirement for GB18030 by the PRC is via locales.
  - Henri expressed a belief that the PRC doesn't actually require GB18030 support; rather that the mandatory character
    subset from it be supported.
  - Steve stated that he was required to add support for GB18030 and did so via conversions at program boundaries.
  - JeanHeyd suggested that no one is really looking to deprecate locale support.  We just want to make text processing
    easier and better locale facilities would help.
  - Henri stated that he would like to deprecate broken character classification functions like `isalpha()` since they
    can't properly handle Unicode inputs.
  - JeanHeyd suggested that, if we had new and improved locale primitives, then we could deprecate the old ones.
- Discussion then moved on to an issue that JF raised on the mailing list concerning Unicode characters in identifiers.
  - http://www.open-std.org/pipermail/unicode/2019-May/000367.html
  - https://github.com/sg16-unicode/sg16/issues/48
  - Tom briefly introduced the topic.  The C++ standard specifies a subset of Unicode characters that may be used in
    identifiers.  That specification is via a series of code point ranges in
    [[lex.name]p1](http://eel.is/c++draft/lex.name#1), but the standard doesn't offer a rationale for the specified
    ranges.  It seems likely that the ranges aren't being maintained as Unicode evolves.
  - JF stated that the current ranges lack justification, but that isn't much of a problem in practice.  Clang accepts
    identifiers using the specified code points, but gcc does not, so such identifiers are not portable in practice.
    Perhaps the standard should just adopt and defer to [UAX#31](https://unicode.org/reports/tr31).
  - Henri asked what the motivation is to address this if it isn't a problem in practice.
  - JF responded that it is a problem in principle.  It is unclear why gcc allows the code points in identifiers if
    specified via `\u` escapes, but not when the actual characters are present in the source encoding.  If the standard
    was more precise, perhaps implementations would be more consistent.  Also, such characters should be allowed in
    module names and we should use the same identifier scheme there.
  - Henri asked how much of the concern is separating identifiers from operators.
  - JF responded little since there are no plans to, for example, adopt Unicode math symbols as operators.
  - Hubert provided a little history.  The existing code point ranges were provided by Clark Nelson in WG14's
    [N1518](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1518.htm) and were based on the version of
    [UAX#31](https://unicode.org/reports/tr31) current at that time.
  - Hubert stated that it would be annoying to have the standard defer to a Unicode TR as doing so makes it that much
    more difficult to determine what the actual rules are for a given standard.
  - Tom suggested that deferring to a Unicode TR would at least have the benefit of the ranges matching whatever version
    of the Unicode standard the implementation adheres to.  This would presumably help maintain the ranges as characters
    are added over time.


# April 24th, 2019

## Draft agenda:
- Discuss execution encoding, locale dependency, impediments to supporting UTF-8, and the feasibility of mandating UTF-8.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Henri Sivonen
  - JeanHeyd Meneide
  - Mark Zeren
  - Nathan Myers
  - Steve Downey
  - Tom Honermann
- Discuss execution encoding, current locale dependency, and the feasibility of mandating UTF-8.
  - Tom initiated discussion by asking for a list of issues in the standard that don't work as expected when the
    execution encoding is UTF-8.
  - Steve led with the observation that locale settings default to the "C" locale.  A call to `std::setlocale` is
    required to enable characters outside the basic source character set.  Failure to set the locale results in
    functions like `mbrtoc16`, `c16tombr`, and `mbrlen` failing when such characters are present.
  - Steve added that iostreams requires I/O to match the current locale in order to meet expectations of attached
    `std::codecvt` facets.
  - Tom asked Nathan if he knew the history of where `std::codecvt` originated.
  - Nathan responded that it was in the original design.  The intent was for it to perform conversions for external
    I/O for the benefit of other parsing functions like for parsing numbers.  The design was intended less for
    `std::cin` and `std::cout`, but more for bespoke streams.
  - Steve mentioned that JeanHeyd had recently discussed another issue.
  - JeanHeyd explained the problem with requirements that `std::basic_filebuf` place on `std::codecvt` facets in
    [[locale.codecvt.virtuals]p3](http://eel.is/c++draft/locale.codecvt#virtuals-3); that the mapping of characters
    is 1 internal character (code unit) to N external characters (code units).  This requirement prohibits support
    for variable length encodings when the internal character type is not large enough to hold a decoded code point,
    as is the case with any `std::codecvt<char, char, ...>` specialization that would be used to convert between,
    for example, UTF-8 and ISO-8859-1.
  - Tom asked if this requirement causes any problems when the `std::codecvt` facet is a `noconv` one.
  - JeanHeyd clarified that the requirement prohibits arbitrary chunking of input/output because there is no
    provisions for decoding/encoding a partial code unit sequence.
  - Henri asked if `std::basic_filebuf` is broken for every multibyte encoding.
  - JeanHeyd responded yes, according to standard implementors he has discussed this with, broken and unfixable.
  - Tom wondered why this limitation exists as it sems to imply a buffer of size 1.
  - Nathan commented that, since it is already broken, we can't break it further.
  - Tom disagreed noting that it works for single byte encodings.
  - Tom surmised that lifting the restriction might require an ABI break and wondered how much use of
    `std::codecvt` exists in the wild and would be affected.
  - Nathan asked if this issue only affects files.
  - Tom responded that the limitation is present only for `std::basic_filebuf` and not for `std::basic_streambuf`,
    so presumably yes, only affects files.
  - Nathan provided some historical context; when iostreams was introduced, wide characters were expected to be
    1x1 mappings from code unit to code point, so variable length encodings would be unnecessary.  Most UNIX
    systems adopted a 32-bit `wchar_t`.
  - Nathan suggested that, given the issues with it, we don't need to worry about improving `std::codecvt`.
  - Steve responded that its presence gets in the way of implementing something else.
  - Henri asked if it would be feasible for C++ startup to implicitly initialize the locale to UTF-8.
  - Steve noted that doing so would break existing code.
  - Nathan stated that we don't need to actually change the C or POSIX locale, we can define our own.
  - Tom asserted that would be surprising to programmers expecting facilities to continue working as they do today.
  - Steve added that programmers expect `printf` and `std::cout` to work together.
  - Nathan responded that writes via `printf` go into a buffer and that writes to `std::cout` go to the same buffer.
  - Steve countered that `std::codecvt` facets only hook iostreams.
  - \[Editor's note: A few minutes of discussion were missed here \]
  - JeanHeyd mentioned that the "C" locale doesn't have to match the system encoding.
  - Tom stated that it has to be compatible though.
  - Steve added that it must also be a single byte encoding.
  - \[Editor's note: Another few minutes of discussion were missed here \]
  - Tom stated that there needs to be a protocol for agreeing on encoding at both ends of a stream.  That protocol
    is currently the current locale setting.  Writing something other than what a terminal expects is mojibake.
  - Steve noted that much existing code works because streams are typically just bytes that are passed through.
  - Tom added that most programs only deal with ASCII and break with non-ASCII characters.
  - Corentin expressed two view points regarding status quo:
    - 1) The current locale setting is a guess.
    - 2) There is a conversion loss if the current locale cannot represent all characters from the internal encoding.
  - Tom disagreed that current locale is a guess; implementations are required to know locale settings.
  - Nathan claimed that the standard can lead implementations; that we can provide a target for implementors to aim for.
  - JeanHeyd disagreed with that notion; if we make execution encoding UTF-8, implementors can aim for it over time.
    However, it would be better to abandon execution encoding and focus on bytes.  Changing execution encoding breaks
    existing machinery, changes the encoding of literals, causes `codecvt` facets to observe different data, etc...
    Making execution encoding UTF-8 is not a practical reality; it is too big a breaking change.
  - Henri offered another perspective.  glibc still offers traditional locales, but back around 2002, RedHat decided
    that GTK would use UTF-8 internally.  To support existing file names, GTK provided `G_FILENAME_ENCODING` and
    `G_BROKEN_FILENAMES` environment variables that influenced interpretation of file names.  Debian followed suit
    in 2007.  The Linux ecosystem has moved to UTF-8.  Now that Microsoft has support for UTF-8 on terminals and is
    UTF-16 internally, Microsoft should be able to migrate.
  - Tom acknowledged that that matches his understanding of what Microsoft is working towards.
  - Steve observed that most programmers don't want locale to affect their streamed data, they just want to write bytes.
  - Henri asked about the feasibility of the implementation transcoding implicitly.
  - JeanHeyd responded that `codecvt` gets in the way.
  - Tom added that filenames are a problem as, in general, they can't be transcoded without harming them.
  - Henri provided some background on how Rust handles file names.  A separate type is used for file names.  On
    non-Windows platforms, file names are sequences of bytes and are decoded as text for presentation, but may not
    roundtrip.  On Windows, WTF-8 is used.
  - Steve noted that `std::filesystem` could operate similarly.
  - Henri added some additional Firefox history.  At some point, a bug was introduced that resulted in it only
    supporting UTF-8 file names.  When the problem was discovered, a decision was made to only support UTF-8 file
    names and that remains the current policy.
  - Nathan stated that he is not worried about breaking things because implementors will retain support for prior
    behavior.
  - JeanHeyd countered that some implementors may take an over-my-dead-body stance on mandating UTF-8.  We don't want
    to introduce yet another language dialect.


# April 10th, 2019

## Draft agenda:
- Continue discussion of JeanHeyd's D1629R0: Standard text encoding
- Discuss any further work-in-progress from Corentin and Martinho on code point properties, and normalization.
- Discuss execution encoding, current locale dependency, and the feasibility of mandating UTF-8.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hana Dusíková
  - JeanHeyd Meneide
  - Mark Zeren
  - Steve Downey
  - Tom Honermann
- Continue discussion of JeanHeyd's D1629R0: Standard text encoding
  - JeanHeyd walked us through the code he has been developing to prototype interfaces to be proposed.
    - https://github.com/ThePhD/phd/tree/master/include/phd/text
    - Encoding types have `encode()` and `decode()` member functions that accept an input range, an
      output range, a state, and an error handler and return an `encoding_result` type that forwards
      the possibly mutated input range, output range, and state.  These functions operate on a single
      code point at a time.
    - `text_transcode` and `text_transcode_into` interfaces are provided for conversion of multiple
      code points at a time.  Generic implementations are provided, but the design is intended to
      support optimizing for contiguous ranges or characteristics of specific encodings.
  - Tom asked if input and output iterators/ranges are supported or if forward iterators/ranges are
    required.
  - JeanHeyd replied that input and output iterators are supported, but an error handler won't be able
    to observe the code units that provoked invocation of the error handler.
  - Tom suggested that a
    [caching iterator](https://github.com/tahonermann/text_view/blob/master/include/text_view_detail/caching_iterator.hpp)
    can be used to solve that problem.  This is the approach used by
    [text_view](https://github.com/tahonermann/text_view).
  - Steve added that the state type can also be used to cache such code units.
  - JeanHeyd explained more about the error handling.  `encoding_result` can store an error status
    and any additional useful information.  The implementation uses the facilities provided by the
    `<system_error>` header.
  - Tom asked for clarification; ranges are always moved into and back out of error handlers?
  - JeanHeyd answered, yes, via `encoding_result`.
  - Tom asked about the possibility to encode only a state change without encoding a character.
  - Steve asked for clarification; as in for a ISO-2022 style shift sequence?
  - Tom confirmed.
  - JeanHeyd replied that the state type can be used for whatever purposes.
  - Tom expressed skepticism about that working from an interface perspective since both input and
    state are provided.  Sometimes, you just want to encode a state transition.
  - Steve noted that state is strongly tied to encoding and asked if state needs to be exposed in the
    interface.  The ability to resume a conversion is still necessary, but wouldn't have to be handled
    via state.
  - JeanHeyd stated that having the state be separate is useful for flexibility in resumption.
  - Steve added that state often becomes a house keeping burden.  Users generally don't know how to
    work with it and do things like passing an initial default constructed state when a resumption
    state is needed.
  - Tom asked how much JeanHeyd had reviewed
    [text_view](https://github.com/tahonermann/text_view) as some of what is being discussed appears
    to be reinventing solutions implemented there.
  - JeanHeyd responded that the interfaces were influenced by reviews of
    [Boost.text](https://github.com/tzlaine/text),
    [text_view](https://github.com/tahonermann/text_view), and
    [Ogonek](https://github.com/rmartinho/ogonek).
  - Corentin asked if the transcoding interfaces can provide lazy ranges.
  - JeanHeyd responded no, not yet.
  - Steve stated that lazy ranges don't necessarily play well with optimized transcoding operations.
  - JeanHeyd stated that the interface is intended to allow optimization.  Implementors can use
    `if constexpr` internally.
  - Tom expressed concern about reliance on `if constexpr` within an encoding agnostic generic
    function and suggested specialization as a more extensible solution.
  - JeanHeyd explained that overloading can be used to provide more optimized implementations
    without lots of specializations.
  - Tom observed that the trade off is a bunch of overloads vs a bunch of specializations.
  - JeanHeyd acknowledged the trade off, but noted that often fewer overloads are required because
    conversions can be relied on.
  - Tom suggested that, perhaps, there should be a `std::transcode` customization point.
  - JeanHeyd acknowledged and said he is still playing around with such ideas and wants to enable
    users to provide custom overloads.
  - Tom expressed hope that users won't be writing these often at all; that such interfaces should
    mostly be written by library providers.
  - Steve agreed and added, or small infrastructure teams.
  - Steve asked about type erasure and support for dynamic encodings.
  - JeanHeyd expressed uncertainty about the need to provide that within the standard and illustrated
    how a custom encoding that handles dynamic encodings could be written.
  - Steve added that POSIX provides iconv which allows requesting a codec for a named encoding and
    such functionality should be provided.
  - Tom suggested it might suffice to be able to write an `iconv_encoding` type that wraps iconv.
  - Tom asked how transcoding between encodings with different associated character sets are handled.
  - JeanHeyd responded that no support is present yet, but that attempting to transcode between such
    encodings would fail compilation it the code point types were not compatible.
  - Tom observed that failing compilation requires a strong type, not `char32_t`, to enforce safety
    via the type system.
  - Corentin asserted that `basic_text_view` should not have a template parameter for normalization
    since normalization is not relevant for all encodings.
  - Tom agreed that, if present at all, normalization should be incorporated into the encoding type.


# March 27th, 2019

## Draft agenda:
- Discussion with JF Bastien regarding JavaScript support for Unicode regular expressions.
  Based on outcome, JF can arrange for JavaScript maintainers to attend a future meeting.
- Discuss any work-in-progress from JeanHeyd, Corentin, and Martinho on transcoding, code point
  properties, and normalization.
- Discuss the recent LEWG mailing list emails regarding iostreams and char8_t support.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hana Dusíková
  - Hubert Tong
  - JeanHeyd Meneide
  - JF Bastien
  - Mark Zeren
  - Michael Spencer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Discussion with JF Bastien regarding coordinating Unicode regular expression support with ECMA TC39
  and the ECMAScript standard.
  - JF introduces:
    - In contrast to what was stated in Kona, ECMAScript does specify Unicode support for regular expressions.
    - It would be beneficial to align C++ and ECMAScript support for Unicode regular expressions.
    - ECMA TC39 is currently working on adding support for Unicode sequence properties.
    - ECMA TC39 is coordinating their work with the Unicode Consortium.
    - SG16 should get involved and collaborate with ECMA TC39.
    - JF provided the following links for reference purposes:
      - https://github.com/tc39/proposal-regexp-unicode-sequence-properties
      - https://unicode.org/L2/L2018/18337-broaden-properties.pdf
      - https://www.unicode.org/L2/L2019/19056-prop-cmts.pdf
      - http://unicode.org/reports/tr18/
  - JF volunteered to connect interested SG16 participants with ECMA TC39 participants and asked for
    volunteers.
    - Zach expressed interest with the specifc desire for C++ to be aligned with the defacto standard (ECMAScript).
    - Hana opted in with explicit concerns regarding whether the C++ standard can defer to ECMAScript for
      wording specification.
    - Tom expressed interest in following along, but has no significant ECMAScript or Unicode regular expression
      experience to contribute; mostly intersted in staying informed for SG16 administrative purposes.
    - Corentin said, sure, why not.
  - Tom, responding to Hana's concern, stated that, by working with TC39 we can help ensure that the ECMAScript
    standard can be referenced normatively by the C++ standard.
  - Hana noted that, in Kona, we stated a goal of supporting [UTS#18](http://unicode.org/reports/tr18) level 1,
    but ECMAScript doesn't meet that.
  - Tom stated that is a good reason to work with them to find out why it isn't implemented.
  - Hana provided a link discussing why level 1 is not met:
    - https://github.com/tc39/proposal-regexp-unicode-property-escapes
  - Zach suggested that, if ECMAScript doesn't support it, we probably don't need to either.  Small differences
    in what is supported in different languages is annoying because programmers tend to think it is ok to copy
    and paste between languages, but then get different behavior.
  - Zach suggested researching what level of UTS#18 support ICU provides.
  - JF noted most implementations defer to ICU and only inline simple expressions for performance.
  - Corentin observed that full UTS#18 support is madness and subsetting is necessary.
  - JF stated it would be beneficial to identify an appropriate subset of UTS#18 for both standards.
  - Hana noted that, in the link she provided, TC39 states what is required and discourages implementors from
    offering extensions in order to preserve portability and compatibility.
- D1628R0: Unicode character properties
  - Draft document available in the SG16 mailing list archives:
    - http://www.open-std.org/pipermail/unicode/2019-March/000266.html
  - Corentin presents:
    - Goal: Provide useful properties from [UAX#44](http://www.unicode.org/reports/tr44).
    - Goal: Enable querying properties for any code point for a subset of the UAX#44 properties that are deemed
      generally useful.
    - A reference implementation is available, but is considered early work:
      - https://github.com/cor3ntin/ext-unicode-db.
    - Hana has been using the reference implementation in CTRE to provide Unicode regular expression support
      in constexpr form.
    - The interface is specified as a set of predicate functions and enumerations.
    - How to handle Unicode versions is an open question.  Some properties tend to be stable (e.g., general
      category), others are less so (e.g., script, directional, joining).
    - Corentin compared the last 5 Unicode standards for differences in property values and found little change.
    - Multiple version support is needed in order to provide a stable and portable interface while allowing for
      implementors to provide newer versions.
  - Michael asked about providing different versions of the algorithms as doing so could require table duplication.
  - Zach reported discovering that requirement as well.  Multiple versions of the algorithms can't be provided
    without duplicating some tabular data.  This could double the necessary storage foot print.
  - Zach observed that multiple versions of code point properties isn't useful if version specific algorithms are
    not provided.
  - Zach stated he didn't see a reason to expose the "age" property.
  - Corentin offered two use cases for properties:
    - For use in implementing the Unicode algorithms.
    - For use by general programmers for non-algorithm purposes.
  - Tom stated that it seems problematic to potentially have user code using a version other than what the
    standard library is using.
  - Zach noted that providing multiple versions goes against our existing guidance allowing implementors to
    float the Unicode version.
  - Steve observed that the specified interfaces are constexpr, but ICU doesn't provide data in constexpr form.
  - Tom responded that the interfaces could be implemented using intrinsics that defer to ICU or a custom database.
  - Corentin added that most tables are small with the name table being a notable exception.  The constexpr
    design allows linking only what is needed.
  - Tom asked, won't you still need the tables for run-time calls?
  - Corentin responded that the tables could be linked in only if referenced.
  - Zach stated that isn't dependable; implementors might have to link them in anyway.
  - Zach listed a few specific concerns with the paper:
    - `codepoint` is marked as exposition only but can't be because it is named in specified interfaces.
    - `codepoint` needs to support `char` and `wchar_t`.
    - Interfaces taking code points should accept any integral type, encoding is not relevant here.
  - Corentin explained that the `codepoint` type was introduced specifically to not allow `char` and
    `wchar_t` in order to avoid calls with character literals that might not be ASCII based.
  - Zach stated a preference for integer values anyway.
  - Tom noted that using a `codepoint` type allows using the type system to catch mistakes.
  - Zach stated that type safety is illusory because `char` and `wchar_t` are code units not code points.
  - Tom countered that accepting `char` and `wchar_t` is useful for character literals, but only for
    character literals.
  - Corentin mentioned that he wants the interface to be noexcept all the way through and that wide
    contracts be used to avoid UB.
  - Michael stated that these should be Unicode scalar values instead of code points then since any
    value is valid.
  - Corentin agreed, the interface is defined for any integer; the predicates just return false if the
    value isn't a valid code point.
  - Steve suggested we may want code point and scalar value types with contracts, but that probably
    depends on alignment with `text_view` and ranges.  Maybe that is only useful at a higher level than
    is needed for code point properties.
  - Zach predicted that LEWG will object to the "cp_" prefix on these interfaces.
  - Zach expressed a desire for more motivation in the paper; to demonstrate a need or justification
    for each exposed property.  Examples of why a regular programmer would care about each of these.
    Maintaining large interfaces or lots of properties complicates teaching.
  - Corentin explained wanting to provide replacements for some broken things in the standard, like
    `std::isalnum`.  Having these available will help programmers use Unicode properly.  As an example,
    they are needed to implement Unicode regular expression support.
  - Zach acknowledged, just want to see that motivation expressed in the paper.
  - Tom agreed with adding explicit motivation like the `std::isalnum` example.  Not necessarily code
    examples, but scenarios.
  - Zach observed that some properties can be used incorrectly because they typically aren't used in
    isolation.  Some properties should only be used via the Unicode algorithms.
  - Hana stated a preference for exposing the Unicode standard as it is specified.  Considerable work
    and expertise has gone into it.  It is a standard that people can learn.
  - Zach disagreed on a philosophical basis; want to keep things simple.
  - Steve observed that some of this is ergonomics of naming.  Programmer should reach for a function
    first, then raw properties only if necessary.
  - Zach cautioned about exposing an expert-only interface.
  - Corentin mentioned, by defering to Unicode, we avoid making mistakes.  Properties that are only
    used for derived properties are already excluded.
  - Tom stated that we can always expose additional properties later as we identify use cases.
  - Michael stated that some properties are implementation detail within the Unicode standard; they exist
    for the algorithms to refer to them.  We should focus first on high level interfaces and those
    probably won't be defined in terms of low level property interfaces.
  - Zach stated that properties that are only needed to implement an algorithm need not be exposed
    individually.
  - Tom asked about tailoring and properties for the private use area (PUA).
  - Corentin replied that tailoring should be provided by a separate interface.  The PUA shouldn't be
    used in open interchange.
  - Tom agreed, but stated that, within an application, a programmer might want all libraries to see the
    same customized properties for the PUA.
  - Steve noticed that the Unicode version numbers in the `version` enumerator values jump from `0x09`
    to `0x10` rather than to `0x0A`.
  - Corentin replied, oops.
  - Corentin added, if we don't support multiple Unicode versions, there is a question of enumeration
    value stability across implementations and differing Unicode versions.
  - Tom suggested that we'd like to see a revision of the paper and asked for objections.
  - No objections were raised.
- D1629R0: Standard text encoding
  - JeanHeyd screen shared an early draft that has not yet been published, so no link is available.
  - JeanHeyd presents:
    - The proposed design follows review of a number of prior papers and projects:
      - [P0244 - Text_view: A C++ concepts and range based character encoding and code point enumeration library](http://wg21.link/p0244)
      - [text_view](https://github.com/tahonermann/text_view)
      - [libogonek](https://github.com/libogonek/ogonek)
      - [Boost.Text](https://github.com/tzlaine/text)
    - Enabling optimizations is a goal.
    - Want a range based approach.  Want to enable lazy encoding/decoding.
    - Wrapping iterators can be large, iterator/sentinel pairs are helpful to reduce iterator sizes.
    - Can't depend on locale or `codecvt` because of performance costs; `wstring_convert` exhibited these costs
      in [Sol2](https://github.com/ThePhD/sol2).
    - Exposing state enables chunked streaming.
    - An empty state can indicate a self-synchronizing encoding.
    - State could be potentially omitted in interfaces for stateless encodings.
    - The default error handler will substitute replacement characters.
    - Error handling can be elided by specifying an assume_valid handler.
    - Sized output ranges can be used for memory safety.


# March 13th, 2019

## Draft agenda:
- Post Kona review and follow up.
- RFP: Transcoding interfaces.
- RFP: Code point and EGC iterators.

## Meeting summary:
- Attendees:
  - Bob Steagall
  - Corentin Jabot
  - JeanHeyd Meneide
  - Martinho Fernandes
  - Michael Spencer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
- Post Kona review and follow up.
  - Tom started discussion with a proposal to initiate a draft working paper for SG16 proposals.  The intent
    being to start drafting wording for features we'd like to get into C++23.
  - Corentin expressed concerns that a large paper could prompt calls for a TS approach and that small focused
    papers would be preferred.
  - Steve noted that a consolidated paper has an advantage in demonstrating how the features work together.
  - Peter observed that we will have co-dependent parts.
  - Michael expressed distaste for large papers with loosely connected features; everything shouldn't go in
    one paper.
  - Tom suggested brainstorming a list of features we'd like in C++23.  The following were suggested:
    - `std::text` and `std::text_view`.
    - Unicode support for regular expressions.
    - Unicode code point properties.
    - Transcoding and transliteration interfaces (both compile-time and run-time).
    - A trie container.
    - A rope container.
    - Unicode algorithms.
    - Normalization.
    - A code point type.
    - A (Unicode) scalar type.
  - JeanHeyd suggested separate papers could address code point properties, a code point type, and a scalar type.
  - Martinho stated that risks getting a result that isn't useful depending on what features do/don't make it in.
  - Tom mentioned that the Design Group has stated a preference for complete and cohesive proposals.
  - JeanHeyd stated that a collection of papers can demonstrate a cohesive design.
  - Steve observed that large papers are hard to review and provided the Ranges and Networking proposals as examples.
  - JeanHeyd suggested starting with determining what we need for the 5 standard mandated encodings without support
    for extensions.
  - Steve noted that support for extensions may demand different interfaces for lossless vs lossy conversions and
    different error handling.
  - JeanHeyd countered that the ordinary and wide encodings already may be lossy, so such support is already needed.
  - JeanHeyd suggested that strong typing can be used to provide interfaces that SFINAE based on requirements; e.g.,
    that can require non-lossy code point conversions.
  - Tom brought discussion back to the working paper idea and noted that such a paper can help drive a consensus
    based process.
  - Steve expressed another concern with small papers; we can end up with features being copied or re-implemented
    in different papers.  For example, `source_location` in both the Library Fundamentals TS and in Contracts.
  - Corentin asked what the dependencies are between each of the brainstormed features.
  - Martinho stated that there is a core set that needs to be done first.  Discussion identified the following:
    - Decoding and Encoding of UTF, both compile-time and run-time.
    - Unicode properties with tailoring for the private use area.
    - Normalization.
  - Corentin asked if we could postpone tailoring and dependencies on localization.
  - Martinho expressed a preference for Swift's model; default interfaces use the default locale, tailored
    interfaces support providing a locale.
  - Peter stated that, if tailoring is postponed, there is some risk of defining interfaces that won't work with
    tailoring.
  - Corentin suggested that, if we need locale support, we need to start from scratch.
  - JeanHeyd countered that, what Unicode demands from the locale is different than what is provided by
    `std::locale`.
  - Tom asked, for locale support, do we rely on OS settings?  Or require the program to establish a locale?
  - Steve noted that, today, by default, we get the "C" locale unless `std::setlocale` is called.
  - Tom drew discussion back to the working paper idea and asked for volunteers to work on core features.
    - JeanHeyd volunteered to work on transcoding and transliteration features.
    - Corentin volunteered to work on code point properties.
    - Martinho volunteered to work on normalization.
- Discussion of D1515R0 - Code points, scalar values, UTF-8, and WTF-8
  - https://rmartinho.github.io/cxx-papers/d1515r0.html
  - Martinho presents.
    - There is a trade off.  If we favor code points, then interfaces can work with WTF-8, Windows file names,
      and other bad data.  If we favor scalar values, then we don't have to check for the presence of surrogate
      code points.
  - Steve asserted that we need to be able to work with ill-formed UTF text, but only at program boundaries.
  - Tom suggested there are reasons to support both code point types and scalar value types.
  - JeanHeyd agreed that both are needed, but that scalar values should be preferred.
  - Bob asked if data can be appropriately round-tripped if conversions are done at program boundaries.
  - Tom replied that a higher level protocol is needed for that.
  - Steve provided the example of CDATA in XML.
  - Martinho reported seeing use of the private use area to preserve invalid values.
  - JeanHeyd asserted that handling of invalid values should require some form of opt-in.
  - Peter responded that the opt-in is the choice of encoding and transcoding or transliteration operations.
  - Corentin asked about the motivation for both a code point type and a scalar type.  Why not just rely on
    UB which is what contracts would provide anyway?
  - JeanHeyd asked rhetorically where the contract would be written if there wasn't a type.
  - Tom elaborated, if the scalar type is a class type, then the contract goes on constructors and assignment
    operators.
  - JeanHeyd asked about how to handle WTF-8 via an encoding.
  - Peter responded that you define a transcoder from WTF-8 to UTF-8.
  - Peter also suggested that, instead of using the private use area to preserve invalid values, you map them to
    something else, some kind of substitution character or marker.  This doesn't necessarily preserve roundtripping,
    but allows handling.
  - Steve noted that, if transcoding/transliteration interfaces are extensible, then we don't have to solve this
    problem.
- https://github.com/cplusplus/draft/pull/2768
  - Tom introduced the issue; this PR to the C++ standard was marked as requiring SG16 review.  The issue was
    created by Richard following his editorial review of the wording changes in [P1139R2](http://wg21.link/p1139r2).
  - Tom asked that everyone take a look and offer any feedback.
- Tom announced plans for our next meeting.  It will be on 3/27 and JF has volunteered to arrange for us to talk
  with the JavaScript team about their support for Unicode regular expressions.  At this meeting, we'll discuss
  what we might want to ask/learn from them.  If warranted, JF will then seek to arrange a future meeting.


# February 13th, 2019

## Draft agenda:
- Preparation for Kona.
- Discuss P1228R1 - A proposal to add an efficient string concatenation routine to the Standard Library (Revision 1)
  - https://wg21.link/p1228r1
- Discuss P1439R0 - Charset Transcoding, Transformation, and Transliteration 
  - https://wg21.link/p1439r0

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Hubert Tong
  - JeanHeyd Meneide
  - Jorg Brown
  - Mark Zeren
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Preparation for Kona.
  - Tom mentioned that we meet after EWGI and LEWGI have wrapped up for the week.
  - Steve observed that we can become a roadblock for proposals if we meet late in the week.  That probably 
    isn't a concern for this meeting, but could be for future meetings.
  - Peter noted that the `char8_t` remediation paper needs scheduling in LEWG.
  - Tom stated he will reach out to Titus.
    \[Editor's note: Tom checked the LEWG schedule and [P1423R0](http://wg21.link/p1423r0) is on the P1 priority
    list to be slotted in ad-hoc.  Titus expects to get through all P1 priority papers\]
  - Corentin asked about scheduling for [P1097R2](http://wg21.link/p1097r2), Martinho's named character escapes proposal.
  - Tom responded that he doesn't think of it as targeting C++20 due to lack of implementation experience.
  - Zach stated it shouldn't be hard to implement.
  - Tom asked if escape sequences impact the preprocessor.  Would preprocessors require updates?
  - Hubert responded that they shouldn't, though `_Pragma` is potentially impacted due to sometimes needing
    to reverse translation of the literal.
  - Corentin observed that the paper is already on EWG's schedule for Saturday.
- [P1228R1: A proposal to add an efficient string concatenation routine to the Standard Library (Revision 1)](http://wg21.link/p1228r1)
  - Jorg introduced the paper:
    - The proposed design has been in use at Google for 12 years and is available in Abseil as `StrCat`.
    - The design is motivated by performance and desire for a simple API.  Only two overloads are proposed.
    - The design has been discussed on the LEWG mailing list.
      - http://lists.isocpp.org/lib-ext/2019/01/9692.php
      - http://lists.isocpp.org/lib-ext/2019/01/10020.php
    - The design does not have Unicode dependencies.
  - Corentin observed that there is overlap with `std::format`.  Can internals be shared?  Are customization
    points duplicated?
  - Zach stated that seems like more of a discussion for LEWG to have.
  - Corentin stated that the interface should prevent mixing types with potentially different encodings.
    E.g., `std::string` and `std::u8string`.
  - Victor agreed that it should not be possible to mix differently encoded strings.
  - Zach suggested that it is reasonable to only support `char` initially.  Once you step outside of `char`,
    other locale considerations kick in.
  - Tom disagreed with locales only being a concern outside of `char` and professed agreement with the proposal
    that locales be a separate concern.
  - Hubert agreed with the proposal scope; avoid conversion aspects for both encoding and formatting, don't invite
    the complexities exhibited by stream inserters.
  - Jorg stated that having to consider locale would kill performance.
  - Tom asked if anyone wanted to argue for locale awareness and got no responses.
  - Corentin asked about dropping support for integral and float types such that only string types would be supported.
  - Hubert agreed with that direction on the basis that, with numeric types, you often want locale support.
  - Zach agreed observing that the proposed functionality seems to be conflating concatenation and formatting in a
    single API.
  - Hubert observed that it is useful to be able to request how much space would be needed for a numeric conversion.
  - Jorg stated that basic (non-locale aware) integer formatting is cheap (4 instructions on Intel), but not for
    floating point.
  - Hubert mentioned that it is also useful to be able to query a maximum buffer size for a type.
  - Jorg suggested that `std::numeric_limits` supports that.
  - Hubert disagreed; It says how many digits roundtrip, not how many might be printed.
  - Corentin observed that concatentation of differently normalized strings can change the number of perceived
    characters.
  - Peter asked why that is a problem.
  - Zach responded that combining NFC can result in fewer extended grapheme clusters than the two strings by
    themselves contained.
  - Tom expressed distaste for section III.A and treating `char` as an integral type instead of a character type.
  - Peter agreed, characters should be characters.
  - Jorg explained the direction was taken to handle `int8_t` and friends that are often defined in terms of `char`.
  - Zach suggested letting deduction work, `'0'+1` deduces as `int`.
  - Peter asked about section III.A and whether it is always customary for a minus sign to precede a negative number.
    In financial contexts, it sometimes follows the number.
  - Zach noted that the minus sign may appear at the end in RTL languages.
  - Tom asked for additional argumentation regarding treating `char` as an integral type vs a character type.
  - Zach suggested following the precedent set by `std:string::operator+()`; accept the kinds of arguments that it
    does and handle them the same way.
  - Jorg stated that, without numeric conversions, users would have to call `to_string` which is more expensive.
  - Hubert suggested the use of a proxy type when conversion is intended.
  - Peter posted a link to example code he had previously written that used a rope to build a string.
    - https://github.com/dascandy/s2/blob/master/tests/string/test_simple.cpp
  - Tom summarized, the dea is to use `operator+` to construct a rope that is evaluated and collapsed upon
    assignment to a `std::string` or other concrete type.
  - Hubert noted that such approaches have difficulty with `auto`.
  - Peter acknowledged that the result is `rope` if no conversion is specified.
  - Zach asserted this is not a problem in practice and that `auto` can be beneficial to postpone materialization.
  - Hubert stated that runs into problems with lifetime.
  - Tom asked Mark about applicability to P1072.
  - Mark responded, yes, [P1072](http://wg21.link/p1072) explicitly mentions Abseil's `StrCat` and is instrumental
    to achieving desired performance.
  - Jorg asked for more feedback on whether `wconcat`, `u8concat`, etc... should be provided.
  - Corentin replied, yes please.
  - Tom responded yes, I'd like to hear reasons not to provide them.  As long as the feature remains locale
    independent, there are no encoding related concerns.
  - Peter reiterated, for any locale stuff, let some wrapper type deal with it.
  - Jorg added, or, if you want locale sensitive stuff, use `std::format`.
  - Peter mentioned it would be good to update the paper with benchmarks comparing `concat` and `std::format`.
  - Peter asked if `concat` needs to be concerned with `char_traits` and `allocator`?
  - Zach stated that "allocators are why we can't have nice things"; ignore them.
  - Tom stated that the alternative is to pass an allocator as an argument.
  - Hubert suggested relying on independent type deduction for each argument, no conversions.
  - Zach asked for clarification; calling `concat(1,0)` produces `"10"`?
  - Jorg responded, yes.
  - Peter asekd about allowing the result type to be an explicitly specified template parameter?  This would allow
    supporting multiple string types without requiring deduction of the value type.
  - Jorg expressed a preference for the option of passing an empty string as the first argument.
  - Zach stated that LEWG will ask about constraints on the function.  Where does SFINAE happen?
  - Jorg commented that he came into this meeting only intending to support `std::string` and things easily
    convertible to `std::string_view`.  Support for other types will require constraining the value type across
    all arguments.
  - Tom asked for poll requests.
  - Corentin suggested, do we want to support unadorned numeric conversions as arguments?
  - Poll: Do we want to restrict arguments to strings, characters, and types convertible to strings.

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   3 |   4 |   1 |   0 |   1 |

  - Jorg explained his against vote; It is really convenient to be able to simply convert integers and there is
    lots of usage experience in Google and Abseil.
  - Corentin asked if a better `to_string` would change his vote.
  - Jorg responded, pobably not as it wouldn't be as convenient.
  - Peter stated that wrappers let us add features incrementally.
  - Jorg mentioned that Abseil's `StrCat` provides some converters (e.g., for hex), but they are rarely used.
  - Victor stated he would like to see `concat` merged with an improved `to_string`.
  - JeanHeyd stated that Sol2 provides a number of adorning types but that users don't like them.


# January 23rd, 2019

## Draft agenda:
- Peter Bindels will present his work on a simple 2D graphics library.
- Discuss Steve's latest draft of the SG16 rubric.
- Discuss Tom's latest draft of the char8_t remediation paper.

## Meeting summary:
- Attendees:
  - Bryce Adelstein Lelblach
  - Corentin Jabot
  - JeanHeyd Meneide
  - Michael Spencer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Peter Bindels presented his work on a simple 2D graphics library.
  - https://github.com/dascandy/pixel
  - Peter summarrized applicability to SG16:
    - In a graphics API, what is the first thing you want to put on the screen?  Text of course!
    - Putting text on the screen requires Unicode support for the library to be generally usable.
    - A text type handling Unicode is therefore needed.
  - Michael stated that how to display text is not part of text processing and therefore not part
    of SG16 scope, but rather fits into SG13 scope.  SG16 won't standardize
    [harfbuzz](https://www.freedesktop.org/wiki/Software/HarfBuzz).  The question for SG16 is,
    how to accept text.  
  - Zach suggested the perspective that, give me a sequence of code points and I will render them.
    The Unicode line break algorithms handle layout pretty well.
  - Peter noted that the bidirectional algorithm is needed as well.
  - Zach added that normalization probably isn't required though.
  - Tom asked if Peter wanted to support italic, bold, or underlined text.  A long and contentious
    debate had been on-going on the Unicode Consortium mailing list regarding whether Unicode should
    enable encoding stress indicators like these.  See the threads at
    https://unicode.org/pipermail/unicode/2019-January/007313.html and
    https://unicode.org/pipermail/unicode/2019-January/007434.html.
  - Peter responded, no, plain text is sufficient.
  - Zach stated that stress indicators are handled by fonts and controlled by markup.
  - Tom elaborated, the question was intended to discover if Peter's needs are limited to plain text
    or whether a higher level of markup is needed.  Would there be a desire to standardize some kind
    of markup?
  - Steve suggested that inline markup could be supported.  Or not supported as desired.
  - Zach added that text display is relatively simple once decoding, line breaks, and bidirectional
    support are enabled; fonts take care of the rest.
  - Steve stated that our immediate goals are low level; provide code point and EGC decoding support.
  - Peter summarized, so we're on the right track working to get new types into the standard.
  - Tom agreed, new types and new algorithms.
  - Steve added, and views.
  - Peter, changing topics, Christopher DiBella has been asking for SG20 how to educate people about
    Unicode.
- [P1253R0: Guidelines for when a WG21 proposal should be reviewed by SG16, the text and Unicode study group](http://wg21.link/p1253r0)
  - Tom asked, do we want to present this to the various WGs or just the WG chairs?
  - Zach stated he was most concerned about EWGI and LEWGI.
  - Corentin suggested presenting to LEWGI, WG chairs, and mentioning it at plenary.
  - Bryce suggested that we could present it at an evening session and could arrange presentation at
    EWGI and LEWGI at Kona.
  - Tom stated he would follow up with WG chairs
    \[Editor's note: Tom did later reach out to the EWG, LEWG, CWG, LWG, EWGI, and LEWGI chairs to ensure that
    1) the chairs agree with the guidelines, and
    2) are willing to direct proposal authors to SG16 when discussion touches on the topics discussed in the paper.

    Several chairs have indicated their agreement so far.  Tom  also requested presenting the paper to EWGI and
    LEWGI in Kona.\]
  - Peter mentioned that there may be examples where a filename may be mutated on open (for normalization purposes)
    such that attempts to reopen the file by the mutated name fail.  We should 1) verify that this can happen and,
    if so, 2) update the paper to mention it.
  - Tom advised that, while we're all participating in WG discussions, that we continue to look for additional
    guidelines to be added.
- Kona pre-planning:
  - Tom mentioned that he was not intending for SG16 to meet in Kona, but it looks like we'll have a quorum after
    all, and papers to discuss, so we will plan to meet.
  - Steve mentioned he has a paper discussing transliteration: [P1439R0: Charset Transcoding, Transformation, and
    Transliteration](http://wg21.link/p1439r0).
  - Tom mentioned that Martinho and Hana have papers for us as well.
    - [P1139R1: Address wording issues related to ISO 10646](http://wg21.link/p1139r1)
    - [P1433R0: Compile Time Regular Expressions](http://wg21.link/p1433r0)
  - Peter asked why Hana's paper is targeting SG16.
  - Zach responded that the Unicode standard specifies algorithms for regular expressions.
  - Bryce suggested SG16 may want to review Hana's paper before LEWGI does.
- `char8_t` remediation:
  - Peter asked if anyone had searched for uses of `u8R`.
  - Tom replied, no, I didn't think to search for `u8` raw literals.
  - Peter mentioned having found one in the wild.
  - Victor searched Facebook and found 3 uses.
  - Tom remembered that Victor previously mentioned approximately 1000 `u8` literals in Facebook code.
  - Victor confirmed, mostly in Facebook code, mostly in tests.
  - Zach commented that he mostly uses `u8` literals in tests as well.
  - Steve stated that Chromium has a number of uses of `u8R` literals.
  - Peter added that a December 2017 snapshot of the code base he works on had 27 uses of `u8` literals, all of
    which were in tests.  Probably has some more now, but not a lot.
  - Tom wondered why hits tend to be in tests.  Perhaps library authors test things that users just don't use?
  - Zach responded that real world uses of libraries tend to use data in strings, not string literals.
  - JeanHeyd echoed Zach, data tends to come from databases or files.
  - Steve stated that most `u8` literals in the code bases he works on are in SQL queries or test code.  They're
    still working to get off of C++03 code and have only mostly been using Unicode internally in the last 10 years.
  - Zach, stated that any changes from the `char8_t` proposal that would result in silent behavioral changes must
    be made ill-formed and that the remediation paper covers that.  We need to be careful when discussing the
    remediation paper that we don't blow up concerns that aren't real.  For example, with concerns that some code
    bases might be badly impacted.
  - Tom asked Zach how he was feeling about code like `std::string(u8"text")` now as he had previously expressed
    concern.
  - Zach responded that he was previously concerned about the amount of breakage, but based on anticipated impact
    and the fact that existing uses will now be ill-formed, no longer concerned.
- Zach asked for clarity regarding guidance SG16 gave proposal authors in San Diego regarding encoding aware
  interfaces.
  - Zach explained, in our [response](http://wiki.edg.com/bin/view/Wg21sandiego2018/D0881R3) to
    [P0881R3: A Proposal to add stacktrace library](http://wg21.link/p0881r3), we said that file names should be
    treated as just a bag of bytes.  But in our [response](http://wiki.edg.com/bin/view/Wg21sandiego2018/P1275R0)
    to [P1275R0: Desert Sessions: Improving hostile environment interactions](http://wg21.link/p1275r0), we
    argued for an interface matching `std::filesystem::path` that exposes content in multiple encodings.
  - Corentin argued that the responses are consistent.  In both cases, the content is stored as a bag of bytes,
    but in the latter case, interfaces are available to offer it in an encoding suitable for display.
  - JeanHeyd expressed a preference for just exposing bytes and leaving display issues up to the consumer.
  - Zach stated that the display forms encourage errors; programmers try to round-trip the names and that doesn't
    necessarily work.
  - Tom stated that it is good for the standard to provide encoding aware interfaces, otherwise programmers will
    re-invent them inconsistently.
  - Corentin observed that implimentations can provide higher quality interfaces because they can rely on platform
    specific behavior.
  - Tom reported having recently searched for uses of `u8string` and `generic_u8string` on Github and found
    only incorrect uses.  For example, cases where the programmer passed the result of `generic_u8string` to `fopen`.
  - Steve said he would be in favor of deprecating the `std::filesystem::path` `u8string` and `generic_u8string`
    member functions for C++23.
  - Tom suggested we could deprecate them in favor of new names that indicate they are for display only.  But asked
    if Zach thought they should exist at all.
  - Zach responded, no, they shouldn't exist as members of `std::filesystem::path`.  Rather, we should have better
    separation of concerns and an independent interface for translating file names to displayable strings.
  - Corentin opined that it is better for programmers to have to think about encoding issues.
- Tom verified that we'll keep with the new meeting time slot for the forseeable future and that the next meeting
  will be February 13th.


# January 9th, 2019

## Draft agenda:
- Preparation for the Kona pre-meeting mailing deadline on 1/21.
  - Review the SG16 rupric assuming a draft is available.
  - Review the char8_t remediation paper assuming a revision is available.
  - Review other papers requiring an update for Kona (P1041, P1097).

## Meeting summary:
- Attendees:
  - Cameron Gunnin
  - JeanHeyd Meneide
  - Mark Zeren
  - Michael Spencer
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Zach Laine
- Tom stated that he was unable to get a revision of the `char8_t` remediation paper ready for this
  meeting, so no further discussion on it for now.
- We then started reviewing Steve's [draft SG16 rubric](http://www.open-std.org/pipermail/unicode/2019-January/000195.html).
  - Victor asked about locales as he and Howard have been working on chrono updates that add overloads
    based on locale.
  - Tom said, yes, bring to SG16 anything involving locales.
  - Zach expressed a preference for just those locale features that relate to Unicode.
  - Tom stated a preference for having a chance to offer our expertise; to help ensure appropriate use
    of locales.
  - Michael asserted that we don't want new Unicode stuff dependent on `std::locale`.
  - Zach observed that it is very hard to write portable code that uses `std::locale` due to implementation
    defined things.  For example,
    - the set of locales is not specified.
    - even the "C" locale is not portable.
  - Tom suggested that the language regarding "requires review" by SG16 be softened as we don't have standing
    to actually require review.
  - Zach disagreed and offered the perspective that this paper should be adopted by the LEWG and EWG chairs
    with the expectation that the chairs will enforce review requirements.
  - Tom expresseed enthusiasm for that perspective; this paper should be targeted to LEWG and EWG to get their
    buy-in.
  - Tom asked about the SG-7 rubric in the hopes that we could compare/contrast with it.
  - Michael located it and provided a link:
    - http://wiki.edg.com/pub/Wg21sandiego2018/SG7/d1354r0.html?twiki_redirect_cache=c261eaeb64220cb36ab24bdb6fb29d4c
  - Tom suggested we should have a section on text containers and string builders.
  - Zach asked if we care about string builders.  If a string builder is used in such a way that it slices code
    unit sequences, isn't that just an incorrect use of the builder?
  - Tom stated he wants to catch any new operations that are problematic for some encodings.  For example,
    reliance on broken interfaces like `std::ctype::widen`
  - Cameron suggested we're interested in any new overloads involving Unicode types.
  - Zach proposed adding a section detailing encoding assumptions.
  - Tom agreed and suggested that can appear in the text encoding section; we need to make it explicit that char
    based values of unknown origin are assumed to have execution encoding.
  - Zach disagreed with the assumption of execution encoding stating that they should instead have an unknown encoding
    and their contents should only be forwarded and operated on generically (e.g., as a bag of bytes), not examined
    as having data in any particular encoding.
  - Tom challenged this noting that reasonable assumptions can be made.  On Windows, execution encoding matches the
    system code page, on POSIX it corresponds to the `LANG` or `LC_CTYPE` environment variables, and is generally
    ASCII elsewhere (except z/OS).
  - Zach noted that assumption doesn't work for file names.
  - Tom agreed that filenames are special; they don't have a known encoding.  But C++17 at least offers `std::filesystem`
    with means to get a filename in a displayable format via the `*string` and `generic_*string` member functions of
    `std::filesystem::path`.
  - Zach asserted those member functions are a trap; the names retrieved via those member functions don't necessarily
    round trip.
  - Michael observed that programmers need to be able to display file names and, if the standard doesn't provide a way
    to do it, programmers will do it themselves, probably badly.
  - Steve noted that file names may not be presentable at all
  - Michael reiterated that we need interfaces that do the right thing easily; e.g., to create a display name for a file
    in something other than `std::filesystem::path`.
  - JeanHeyd observed that some of these problems would go away with a new I/O layer that uses `std::filesystem::path`
    instead of `const char*` interfaces.
  - Steve noted that we can't replace the OS interfaces though.
  - Tom stated that we need to update the paper to require consultation with SG16 for anything involving file names.
- [P1378R0: std::string_literal](http://wg21.link/p1378r0)
  - JeanHeyd provided a link to an updated draft revision of the paper:
    - https://thephd.github.io/vendor/future_cxx/papers/d1378.html
  - JeanHeyd introduced the motivation; to provide means to guarantee that a string literal is used in invocations
    of `std::embed` in order to enable dependency discovery in build systems.  Additional motivation is to provide
    means to avoid unintended array-to-ponter decay and to handle string literals with embedded null characters without
    having to depend on deduction via array reference in order to obtain the actual array size of the literal.
  - JeanHeyd acknowledged that the proposal changes the type of all string literals in ways that are unlikely to
    be acceptable.
  - Michael observed that the proposed design doesn't actually meet the motivation requirements for `std::embed` since
    the proposed type is copyable and therefore can be produced by many kinds of expressions, not just literals.
  - Steve suggested another motivation: requiring string literals for things like format strings and SQL; requiring
    a literal would avoid the possibility of consuming user provided input that could be used as an attack vector as
    in SQL injection attacks.
  - Zach observed that immediate (`consteval`) functions can help in this regard since they can't consume run-time
    input by design.
  - Tom asked about a different implementation strategy; making all of the class constructors private and befriending
    a UDL.  This would ensure the class could only be constructed by calling a UDL (assuming copy constructors are
    deleted).
  - Michael suggested the constructors could also use compiler magic to require construction via a literal.
  - Steve noted that having the size of a string literal readily available would be useful.
  - Michael noted that this design impacts type deduction for `auto` declared variables and template parameters.
  - Zach suggested that two-step conversion as would be required for backward compatibility would be problematic.
  - JeanHeyd responded that any number of builtin implicit conversions are already permitted.
  - Tom wondered if the number of conversions might impact overload resolution.
  - JeanHeyd suggested the design might be useful to limit when error handling and encoding validation would be
    necessary for `std::text`.
  - Zach countered that string literals can form ill-formed code unit sequences.
  - Zach acknowledged that the ability to avoid `strlen` could be a big deal.
  - Michael asserted that the motivational use cases can largely be met with immediate (`consteval`) functions.
  - JeanHeyd provided an additional motivation; comparison between string literals.  Today, whether `"foo" == "foo"`
    is unspecified.  The proposed `std::string_literal` could make such comparisons work as expected.
  - Mark asserted that an implementation is needed to evaluate backward compatibility impact.
  - Mark noted having previously had a desire to determine if a pointer pointed to a string literal; to avoid
    storing the string contents.
  - Zach and Tom both expressed having used or encountered string pool classes that exist to collapse matching strings
    to a single copy.
- WG21 Direction group [response to P1238R0: SG16: Unicode Direction](http://www.open-std.org/pipermail/unicode/2019-January/000196.html)
  - Steve summarized the response.
  - Tom noted that the DG did not comment on the constraints listed in the paper.
  - Mark noted the DG request to clarify scope.
  - Zach stated that we need an elevator pitch and suggested: We want all Unicode algorithms available via standard
    interfaces for C++23.
- Tom announced that the next meeting will start an hour later than usual.


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
