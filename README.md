# SG16 Meeting Summaries

SG16 meetings are typically held on Wednesdays from 3:30pm-5:00pm EST5EDT4 on the 2nd
and 4th weeks of each month, but scheduling conflicts or other time pressures sometimes
force alternative scheduling.  Meeting invitations are sent to the mailing list and
prior attendees.

The next SG16 meeting is scheduled for Wednesday, April 24th 2019, from 3:30-5:00pm EST.

- [April 10th, 2019](#april-10th-2019)
- [March 27th, 2019](#march-27th-2019)
- [March 13th, 2019](#march-13th-2019)
- [February 13th, 2019](#february-13th-2019)
- [January 23rd, 2019](#january-23rd-2019)
- [January 9th, 2019](#january-9th-2019)
- [December 19th, 2018](#december-19th-2018)
- [December 5th, 2018](#december-5th-2018)
- [October 17th, 2018](#october-17th-2018)
- [October 3rd, 2018](#october-3rd-2018)
- [August 29th, 2018](#august-29th-2018)
- [July 25th, 2018](#july-25th-2018)
- [July 11th, 2018](#july-11th-2018)
- [June 20th, 2018](#june-20th-2018)
- [May 30th, 2018](#may-30th-2018)
- [May 16th, 2018](#may-16th-2018)
- [April 25th, 2018](#april-25th-2018)
- [April 11th, 2018](#april-11th-2018)
- [March 28th, 2018](#march-28th-2018)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
Meeting summary:
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

## Draft agenda:
- Continue discussion of char8_t remediation for backward compatibility impact.
  - Discuss pros/cons of keeping u8 literals char based and introducing new char8_t based U8 literals.
- Review P1072 following San Diego LEWGI feedback.

## Meeting summary:
- Attendees:
  - Bryce Adelstein Lelblach
  - JeanHeyd Meneide
  - Mark Zeren
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
- Continued discussion of char8_t remediation for backward compatibility impact.
  - Tom introduced the discussion topic.  One approach to minimizing backward compatibility impact
    would be to restore `u8` literals being `char`-based and to introduce a new `U8` literal prefix
    for `char8_t` based UTF-8 literals.
  - Mark suggested following up with Google folks to determine if this would address their concerns.
  - Tom stated he talked to Chandler following the San Diego vote.  Concerns expressed were that the
    potential backward compatibility impact exceeded the benefits.
  - Tom asked for pros and cons for a new `U8` literal prefix.
  - JeanHeyd was first to note the obvious primary benefit, avoids backward compatibilty issues.
  - Tom agreed, but added that P0482 does have other minor breakage; the changes to the return types
    of the `u8string` member functions of `std::filesystem::path`.
  - JeanHeyd pointed out that the visual difference between `u8` (lowercase) and `U8` (uppercase) is
    subtle and bad for readability.
  - Bryce agreed and pointed out that MISRA forbids identifiers that look similar.
  - Bryce further stated that use of `u` and `U` for `char16_t` and `char32_t` literals was a mistake
    for the same reason.
  - Mark mentioned a pro, this approach preserves investment in any increased use of `u8` literals
    in code over the next few years before migration to C++20.
  - Bryce suggested that compiler warnings could be added to help educate programmers about the change
    when compiling in pre-C++20 language modes.  This still depends on compiler upgrades of course.
  - Tom agreed and noted that Clang trunk already issues such a warning when invoked with
    `-Wc++2a-compat`.
  - Mark asked if a cast or similar approach for converting `u8` literals to `char`-based types doesn't
    suffice.
  - Tom responded that Zach expressed a desire for existing code to continue working at our last
    meeting.
  - Tom asked what adoping an additional literal prefix would mean for messaging.  What would we be
    telling programmers going forward?  We could deprecate `u8` literals and promote `U8` going
    forward.
  - JeanHeyd responded that deprecation doesn't really help to move programmers towards use of `char8_t`.
    He'd prefer to break things, get over the migration hump, and keep a cleaner design.
  - Mark asked why the `as_char` approach suggested in the draft paper doesn't suffice.
  - JeanHeyd responded that it requires markup, so existing code requires changes.
  - Mark pondered, a new prefix does kind of fix everything.  It doesn't have to be `U8`, we could use
    `utf8` or similar.
  - JeanHeyd suggested we could introduce new prefixes for all of UTF-8, UTF-16, and UTF-32 in order to
    maintain symmetry and to address the subtle `u` vs `U` concerns.
  - Tom suggested another pro; a new prefix avoids potentially forking the language by unintentionally
    encouraging use of a `-fno-char8_t` option as has happened with `-fno-rtti` and `-fno-exceptions`.
  - Mark asked where we're at with proposing `char8_t` to WG14.
  - Tom responded that he would like to get a proposal in front of WG14 at their October 2019 meeting
    in Ithaca.  In addition, he'd like to have proposals ready for our other proposals targeting core
    language features:
    - [P1097](http://wg21.link/p1097) - "Named character escapes"
    - [P1041](http://wg21.link/p1041) - "Make char16_t/char32_t string literals be UTF-16/32"
    - Source file encoding tags (no proposal yet).
  - Tom added another pro, or con, depending on perspective; a new prefix maintains the ability to
    continue writing UTF-8 based applications with `char`-based types.
  - Mark opined that moving away from `char` aliasing issues is compelling.
  - Steve noted that UTF-8 in `char`-based types often seems to work, but works for the wrong
    reasons.  For example, UTF-8 encoded source files compiled as "8-bit ASCII" such that the UTF-8
    code units just get copied from the source file.
  - Tom asked about messaging again, what message are we sending to library authors?  Do they write
    their UTF-8 based interfaces against `char` or `char8_t`?  How do they choose?
  - Mark observed that this isn't a new problem.  Library authors code against `std::string` today
    and it isn't a universal string type or a great type for Unicode.  We'll have similar concerns
    with the introduction of `std::text` vs `std::string`.
  - Tom concluded, sounds like templates will be the way to go.
  - JeanHeyd commented that views help.  For example, `text_view` can effectively type erase the code
    unit type.  But what does one assume for encoding for `char`?
  - Tom responded that the execution encoding must be assumed per existing precedent in the standard.
  - Mark concluded that he doesn't see a way out of the `char` vs `char8_t` problem.  But, with `char8_t`
    being available, we'll get experience using it that will inform future library efforts.  In the short
    term, being able to use either `char` or `char8_t` is advantageous.
  - Peter chimed in from chat (due to a non-functioning microphone):
    - "looks like my mic is completely broken. From what I can tell this is like the uptake of uint8_t,
      it takes some time but over time everybody learns that these types have a given fixed meaning and
      others are a :shrug: type"
  - Tom presented a few polls.
    - Poll 1: Add defined-as-deleted overloads for `operator<<` for `basic_ostream<char, ...>` specializations.

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   3 |   3 |   0 |   0 |   0 |

    - Poll 2: Allow deprecated `std::filesystem::u8path` to be called with sources with `char8_t` value type.

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   2 |   3 |   0 |   1 |   0 |
    - - Peter explained his against vote; this maintains working around something that we don't really
          want to work in the first place.

    - Poll 3: Restore `char`-based `u8` literals and introduce new `char8_t` based literals with a new prefix.

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   1 |   3 |   1 |   1 |   0 |
    - - Bryce explained his against vote; we'll need to converge on a very short prefix, 2 characters at
        most.  That seems unlikey.
      - JeanHeyd commented that he still prefers to go with a solution that pushes the community in a
        new and consistent direction.  `u8` literals aren't widely used, so we still have time to course
        correct.
      - Mark asked if tooling could be used to fix existing code by converting `u8` literals to ordinary
        literals encoded with escapes.
      - Tom responded that we discussed tooling possibilities at the last meeting.  Specifically Zach's
        suggestion that this could be a good test for Titus' goals for tooling.

    - Poll 4: Assuming `u8` literals remain `char8_t` based, allow `char` arrays to be initialized with `u8` string literals.
      - Tom stated that the reason to consider this is that the `as_char` approach doesn't work for
        array initialization.
      - Bryce stated he wanted more time to think about this.
      - Mark agreed with wanting more time.
      - Poll not taken.
- Review P1072 following San Diego LEWGI feedback.
  - Mark provided a summary of changes:
    - No buffer moving features; feedback from San Diego was negative regarding that due to exposure of
      implementation details.
    - `resize_default_init()` resizes the string such that the added content is default initialized.
      Failure to write to the added elements results in undefined behavior.
    - This approach matches Google's existing implementation.
    - This approach is compatible with existing allocators.
    - libc++ is already using this approach as part of its `std::filesystem` implementation to remove
      an allocation.
    - This doesn't preclude a buffer migration feature in the future.
    - The paper establishes that `basic_string` is allocator aware.


# December 5th, 2018

## Draft agenda:
- Draft guidelines for other WGs and SGs to request SG16 review.
- char8_t remediation for backward compatibility impact.
- Review P1072 following San Diego LEWGI feedback.

## Meeting summary:
- Attendees:
  - Bryce Adelstein Lelblach
  - Cameron Gunnin
  - Corentin Jabot
  - Florin Trofin
  - JeanHeyd Meneide
  - Mark Zeren
  - Markus Sherer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Draft guidelines for other WGs and SGs to request SG16 review.
  - Tom introduced the topic.  Bryce had suggested that SG16 produce a rubric detailing guidance
    for when other WGs and SGs should consult SG16.  SG7 recently produced such a document.  Tom
    felt this was an excellent idea and is now bringing it before SG16 for discussion.
  - Tom first asked Bryce where SG7's rupric can be found.
  - Bryce replied that it will be in the San Diego post-meeting mailing.
  - Tom then asked for suggested guidance.
  - Steve suggested a simple litmus test; "if it smells like Unicode..."
  - Corentin mentioned having discussed this with Titus in San Diego and suggested that anything
    having to do with text processing should be sent our way.
  - Bryce asked about locales and it was agreed that Unicode has locale dependencies.
  - Peter mentioned the {fmt} library; code units vs code points?
  - Tom replied that we discussed {fmt} with Victor in SG16 on several occassions.
  - Bryce asked if {fmt} is in C++20 and whether SG16 has any concerns about it.
    \[Editor's note: not yet, but it passed LEWG review in San Diego\].
  - Zach replied that it is certainly no worse than what we have now.
  - Mark commented, bird in hand... even if we had issues with the {fmt} library, there is no
    competing proposal.
  - Corentin mentioned that {fmt} does not yet handle `char16_t` and `char32_t`, but can be extended
    later.
  - JeanHeyd elaborated, template overloads are present, but formatting strings must be `char`
    or `wchar_t` at the moment.
  - Zach suggested a requirement; that we need to reserve the right to explicitly specialize standard
    library templates that might be instantiated by users with `char8_t`.
  - Tom asked for a volunteer to identify such templates.
  - Zach volunteered.  Hooray for Zach!
  - Steve suggested that anything involving command lines, file names, and environment variables should
    be sent our way.
  - Mark added, any kind of encoding.  Including source encoding.
  - Tom asked, do we want SG13 (HMI) members consulting us for text input and presentation issues?
  - Steve replied, when they get to that point, yes.
  - Tom asked for a volunteer to draft the rubric paper.
  - Steve volunteered.  Hooray for Steve!
- char8_t remediation for backward compatibility impact.
  - Tom gave a brief introduction and pointed the group at a rough draft paper posted to the mailing list
    (http://www.open-std.org/pipermail/unicode/2018-December/000180.html).
  - Time was given for those who had not yet seen it to quickly scan it.
  - Steve commented on the proposed change to make ostream inserters for `char16_t` and `char32_t`
    ill-formed; for anyone actually relying on printing pointer values, a fix should be easy, add a
    cast to `void*`.
  - Corentin wondered if anyone actually does `std::cout << u8"text"`.
  - Zach observed that someone could conceivably want to use the ostream inserters to print `char16_t`
    values formatted as hex integers, say when dumping UTF-16 code units for diagnostic purposes.
  - Steve asked if it would be problematic to allow `std::string` to be constructed with `char8_t` based
    data.
  - Zach responded that he didn't see any harm.
  - Peter chimed in that `std::string` always holds UTF-8 in the code base he works on.
  - Tom stated that supporting `std::string` interoperability with `u8` literals would require a lot of
    overloads for the `char` based specialization of `std::basic_string`.  Implementors would not like
    that.
  - Zach asserted that he wants, somehow, to be able to construct `std::string` objects initialized with
    `u8` literals.
  - Tom asked if using a factory function would suffice.
  - Zach responded that would require updates and therefore doesn't address existing code.
  - Markus advised thinking of `std::string_view` in addition to `std::string`.
  - JeanHeyd asked about allowing `std::u8string` to be convertible to `std::string`.
  - Tom stated he thought that might allow most existing code to just work.  But, would we really want
    that?  Implicit conversions are often undesirable.
  - Peter responded that he thought so, yes.  Existing code mixes UTF-8 with `char`.
  - Corentin observed that implicit conversion from `std::u8string` could lead to mojibake.
  - Zach acknowledged that `std::string` doesn't guarantee any encoding.
  - Peter asked about the possibility of making it UB for `std::u8string` to contain non-UTF-8 data.
  - Zach requested not adding encoding guarantees for strings.
  - Peter responded, it doesn't actually work anyway since you couldn't update a string without
    introducing UB.
  - Tom asked if the UDL approach to providing UTF-8 data in `char` via `u8` literals was realistic.
  - Zach stated we shouldn't be suggesting macros as solutions.  \[Editor's note, macros are not required
    to create a solution that works for C++17 and C++20, but source code changes are required\].
  - Tom asked if use of `-fno-char8_t` is a valid option noting that it forks the language.
  - Zach suggested, perhaps this is our first good opportunity to put tooling to use as part of a C++20
    migration story.
  - Corentin observed that it should be easy to use `clang-tidy` to update code.
  - JeanHeyd asked if `char8_t` could implicitly convert to `char`.
  - Corentin stated that he wants conversions to be explicit.
  - Tom mentioned that the draft paper is intended to tell a migration story.
  - Markus explained that he felt the economics are not right.  The current situation puts the burden of
    addressing breakage on many programmers.
  - Zach suggested adding tooling automation to the paper.
  - Tom said he could add `clang-tidy`, what else should be mentioned?
  - Zach stated he'd like to see compilers do fix-ups themselves.
  - Corentin observed that implementors are unlikely to have something in place in the necessary time frame.
  - Tom asked about experimentation.
  - Peter stated his code base isn't using `u8` literals today and won't be able to.
  - Markus observed that not all code is equally modifiable.  For example, Google's code base has a lot of
    Google specific code, but also uses a lot of third party code.  Updating the third party code and
    potentially maintaining differences from upstream, is more difficult than updating Google's own code.
  - Tom suggested a C++17 compatibility library could be made available that implements some of the
    remediation approaches noted in the draft paper.
  - Bryce asked about the possibility that the `char8_t` proposal might be re-litigated due to backward
    compatibility concerns.
  - Tom replied, sure, anything is possible.
  - Bryce suggested adding data about expected brekage to the remediation paper to avoid scaring people.
- Peter requested time in SG16 for presenting and collecting feedback on a simple 2D graphics library
  he has been working on.


# October 17th, 2018

## Draft agenda:
- char8_t: Markus' concerns, motivation, type safety, Unicode sandwich, most C++ code is yet to be written, transition story.
- Code points, EGCs, or explicit ranges for text views/containers?
  - How to decide? Pick a direction now? Write a pros/cons paper for the committee?

## Meeting summary:
- Attendees:
  - Artem Tokmakov
  - Cameron Gunnin
  - JeanHeyd Meneide
  - Mark Zeren
  - Markus Scherer
  - Martinho Fernandes
  - Sergey Zubkov
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- [Issue #30: Unclear behavior for octal and hex escape sequences in Unicode character and string literals](https://github.com/sg16-unicode/sg16/issues/30)
  - Tom explained the current situation; [CWG#2333](http://wg21.link/cwg2333) tracks this
    issue.  CWG discussed at their August 2017 teleconference and decided that numeric escape
    sequences should be ill-formed in UTF-8 character literals.  Mike Miller offered to reconsider
    the issue if requested by SG16.
  - Markus mentioned the utility in using numeric escapes to create ill-formed strings for testing
    purposes.
  - Markus also presented an alternative possibility, that numeric escapes only be ill-formed if
    used to encode a code unit value that is never valid in a UTF string, e.g., `0xff`.
  - Markus additionally noted that there is a distinction between Unicode strings (may contain
    ill-formed contents) and UTF strings (must be well-formed).
  - Zach asserted that the ability to use numeric escapes is more important than preventing
    encoding of ill-formed UTF sequences.
  - Tom noted that the current CWG resolution seems evolutionary given that it contradicts existing
    practice.
  - Markus noted a further benefit, maintaining consistency with languages like Java.  Additionally,
    he explained that some logging libraries write strings with non-printable characters replaced
    with escape sequences and that the ability to copy and paste those strings verbatim into code
    is useful.
  - Tom noted an additional use case; strings encoded as Modified UTF-8.  Modified UTF-8 requires
    use of escapes to encode U+0000 as an overlong two-byte sequence.
  - Markus added that the same use case applies to creation of CESU-8 strings; escape sequences are
    needed for the individual encoding of UTF-16 surrogate pairs.
  - Tom stated that it is useful to embed a null terminator with `\0`, though it would still be
    possible to do so using `\u0000`.
  - Mark observed that implementations can warn if a literal that contains numeric escape sequences
    produces an ill-formed UTF string.
  - Poll: Continue to allow hex and octal escapes that indicate code unit values, requiring only
    that they fit into the range of the code unit type.

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   8 |   1 |   0 |   0 |   0 |
    
- char8_t:
  - Zach started the discussion by noting that use of `char8_t` does not help to enfore
    preconditions; ill-formed UTF-8 can appear in sequences of `char8_t` just as it can in sequences
    of `char`.  How does `char8_t` help?
  - Mark acknowledged that preconditions can always be violated.
  - Tom offered `make_text_view` and UDLs as examples.  `char8_t` enables writing generic functions
    that work with ordinary and UTF-8 string literals.
  - Zach summarized, I see, it allows authors of overload sets to differentiate behavior.
  - Markus chimed in, starting to see the motivation for `char8_t`; generic code can't distinguish
    encodings unless it is represented in the type system.
  - Markus further noted that the standard library has a high percentage of generic code relative to
    code outside the standard.
  - Tom agreed, but noted there is more focus on generic libraries now than in the past and that the
    committee is working hard to improve support for generic programming as exemplified by Concepts.
  - Tom mentioned that we have multiple encodings we have to support.
  - Markus acknowledged the dilemma; many other languages have settled on a single internal encoding,
    but C++ supports multiple encodings and there is no clear dominant one across the industry.
  - Mark added that there is considerable baggage with `char` and the implementation definedness of
    the execution encoding.
  - Markus acknowledged the existence of many incompatible string types in C++ that are all similar
    in intent.
  - Tom stated that Concepts helps to bring these different string types together such that they
    can be supported by generic code.
  - Markus observed that the `char8_t` proposal changes existing behavior.
  - Mark noted that `u8` literals aren't used much in C++.
  - Markus mentioned that Google uses `unsigned char` and ensures use of UTF-8 internally.
  - Tom responded that there is a backward compatibility story that is aided by C++20 support for
    class types as non-type template parameters as proposed in [P0732](http://wg21.link/p0732).
- Code points vs grapheme clusters:
  - Martinho lead the discussion by expressing concern that grapheme cluster boundaries are not
    stable.  The situation with Swift today is that behavior depends on the version of ICU installed
    on the system.  Behavior is therefore non-portable.
  - Mark mentioned that we have a similar issue with the timezone database and `<chrono>`.  Behavior
    depends on which version of the database is installed.
  - Tom acknowledged the concern; we won't have portable grapheme breaking in C++ either.
  - Markus provided a link to a recent document authored by Mark Davis and noted a limitation imposed
    by the instability of grapheme cluster boundaries; stored EGC indexes are invalidated when
    changing Unicode versions.
    - https://docs.google.com/document/d/1wuzzMOvKOJw93SWZAqoim1VUl9mloUxE0W6Ki_G23tw/edit
  - Zach asked, as someone without a lot of end user experience, how often do programmers make poor
    choices regarding handling of Unicode text?
  - Steve responded that he sees bug reports frequently where programmers inadvertently sliced
    grapheme clusters.
  - Martinho provided links to a couple of example defects:
    - https://bugs.swift.org/browse/SR-3582
    - https://stackoverflow.com/questions/26862282/swift-countelements-return-incorrect-value-when-count-flag-emoji
  - Tom asked, so how do we make a decision about how to proceed.
  - Martinho countered that we don't need to yet.
  - Steve chimed in with, how do we make them less scary?
  - Mark responded with a question, how are things going to look?  new types on top of `std::string_view`
    and `std::string`?
  - Zach provided a brief overview of how Boost.Text handles grapheme clusters.
  - Markus asked, does Boost.Text enforce well-formed UTF-8?
  - Zach responded that it encourages, but does not require well-formed UTF-8.
  - Markus mentioned that validation can be expensive.  If you know your input is well-formed, then
    lookups can be optimized without having to decode.
  - Tom described this as a design trade off; validate up front and reap performance benefits later,
    or skip validation and lazily validate later.
  - Markus noted that it is common for programmers to slam content into strings and then validate
    them later.
  - Mark mentioned that [P1072](http://wg21.link/p1072) helps to support that use case.
  - Tom asked, assuming that we standardize a type that enforces well-formedness, is there room for
    standardizing a non-validating type as well?  Or does that become an expert level do-it-yourself
    feature?
  - JeanHeyd advocated an adapter-over-range approach for `std::text`; tags can suppress validation
    when it isn't necessary.
  - Tom observed that it isn't possible to enforce well-formedness on views without introducing
    validation costs.
  - Steve mentioned that adapters over containers make memory allocation someone else's problem, for
    better or worse.
  - Martinho advocated that, if performing validation on container construction, would prefer
    replacement character substitution since throwing gives you nothing.  Invalid input can be used
    as an attack vector; if UTF-8 input is all `0x80`, replacement will triple the buffer size.
  - Zach expressed openness to an adapter approach for Boost.Text.
  - Mark expressed a preference for the adapter approach as it supports underlying containers with
    reference counts or small buffer optimizations.
  - Mark also mentioned that wrapping `std::string` provides a nice transition story.
- Tom then summarized the plan for the San Diego meeting: discussion of the
  [Unicode Direction paper](http://wg21.link/p1238), [P1072](http://wg21.link/p1072), Isabella
  Muerte's [P1275](http://wg21.link/p1275), and then small groups to focus on further proposal
  incubation.


# October 3rd, 2018

## Draft agenda:
- Last meeting before the San Diego pre-meeting mailing deadline on October 8th.
- Review the draft SG16 direction paper that Tom plans to have ready for this meeting and
  the pre-meeting mailing.
- Code points, EGCs, or explicit ranges for text views/containers?
  - How to decide? Pick a direction now? Write a pros/cons paper for the committee?

## Meeting summary:
- Attendees:
  - Artem Tokmakov
  - Corentin Jabot
  - JeanHeyd Meneide
  - Mark Zeren
  - Markus Scherer
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- We started off with a round of introductions in honor of a new first time attendee,
  Markus Scherer, chair of the ICU Technical Committee.
- Tom provided a brief overview of the agenda; to review draft papers discussing
  SG16 direction, to collect feedback, and submit a paper for the San Diego pre-meeting
  mailing that represents the group's consensus on our general direction.
  \[Editor's note: these drafts later became [P1238R0](http://wg21.link/p1238).\]
- Zach raised a concern regarding support for generic interfaces.  The draft paper asked
  whether generic interfaces for Unicode algorithms could reasonably support segmented
  data structures like ropes.  Zack felt segmented data structures are supported naturally
  as long as they provide standard iterators.
- Tom explained that the question was meant more to ask if generic interfaces could provide
  performance that users would expect.  Or whether interfaces specialized for contiguous
  memory would be necessary and, if so, whether they could be used to service ropes.  Perhaps
  it would make sense to have a low level C API wrapped in a generic interface.  This would
  require the low level API to support tracking state (e.g., code unit sequences split across
  segment boundaries).
- Zach expressed concern about giving the impression that we want to provide equivalent
  functionality in C and C++.
- Corentin chimed in that contributing to C isn't something we've talked much about.
- Tom clarified, only when it makes sense.
- Markus noted some experience; prior attempts to provide generic interfaces in ICU
  resulted in performance complaints.  ICU could do more of this, but users are able to do
  it themselves.
- Zach responded that his own performance tests involving arrays of code points vs code point
  iterators on top of code units indicated negligible performance differences.  Table lookups
  dominated.
- Markus commented that performance improvements come about largely due to support for fast
  paths.
- Mark observed that we heard similarly from Swift developers regarding the need to support
  fast paths.
- Markus then asked a fundamental question: why bother standardizing Unicode support?  Why
  not just use ICU?
- Mark responded that programmers continue to struggle with classes of bugs that we could
  potentially minimize, handling of grapheme clusters for example.
- Steve also noted continued mishandling of strings in general.
- Tom mentioned distribution and packaging issues.  Having something provided with the standard
  library helps to sidestep legal obstacles and package versioning problems.
- Corentin commented that programmers need more easy to use functionality, libraries that
  encourage correct use.
- Tom agreed, noting that we want to bring down the learning curve for working with Unicode.
- JeanHeyd added that not all programmers need all of Unicode, some would benefit just by having
  support for encodings built in.
- Changing topics, Mark asked to add a reference to P1072 in the paper, noting its relevance to
  text/string buffer transference.
- Steve asked about some of the terminology in the paper.  Why the inconsistent mention of UTF-8
  vs `char16_t` and `char32_t`?
- Tom explained that this is consistent with the standard where `u8` literals are explicitly
  UTF-8, but `u`, `U`, and other uses of `char16_t` and `char32_t` currently have implementation
  defined encodings.
- Corentin observed that `char16_t` and `char32_t` are explicitly used for UTF-16 and UTF-32
  respectively in the filesystem library.
- Changing subjects again, Tom asked for thoughts regarding the first constraint in the paper,
  that the ordinary and wide execution encodings are implementation defined.  Can we lift that
  constraint?
- Tom went on, Microsoft is working on adding better UTF-8 support to Windows and their
  compiler.  IBM does not provide a publicly available C++11 compliant compiler for z/OS, though
  they do provide Swift on z/OS and that depends on Clang.  IBM doesn't publicly provide Clang
  on z/OS, but it seems they have an internal port of it.
- Markus noted that ICU dropped support for IBM's z/OS, i, and AIX operating systems when
  upgrading to C++11 due to lack of C++11 support in IBM's xlC compiler.
- Corentin mentioned that we're targeting C++23 or C++26 for our work.  What will things look
  like then?
- Changing topics again, Markus commented on ICU's switch to using `char16_t` as the code unit
  type for its internal encoding.  This was challenging due to interoperability issues with
  code that used, and continues to use, `wchar_t` or `uint16_t` for UTF-16 data.  Overloads were
  added to make it eaiser to integrate with code using these types.
- Tom asked to confirm his historical understanding, that ICU used to use a typedef for the code
  unit type that consumers could set to `wchar_t` or `uint16_t` as required for their
  application.
- Markus confirmed that users can still do so, but that the default is now `char16_t` when
  compiling as C++11.
- Zach asked to talk about UTF-8 and type safety.  He was recently surprised when, due to a
  mismatch between the encoding used for a source file (UTF-8) and the encoding the compiler
  used to read that source file (Windows 1252), `u8` string literals didn't have the expected
  contents at run-time.  He concluded (accurately) that he can't depend on `u8` string literals
  containing well-formed UTF-8 text.  This caused him to question his perception of the type
  safety that `char8_t` provides.
- Markus expressed further concerns about `char8_t` leading to the same type interoperability
  issues that were encountered with `char16_t` in ICU.
- Mark noted that we are still lacking deployment results with `char8_t`.
- JeanHeyd described prior experience using a `char8_t` like type to help avoid encoding confusion
  and that it was useful.
- Tom stated that he will add discussion of `char8_t` to the agenda for the next meeting and
  update discussion in the direction paper.
- Changing topics, Markus mentioned a wish list item, that `char` be made unsigned everywhere.
- Mark thought floating the idea would be worthwhile.
- Tom asked Steve about merging the two draft papers.  Steve was favorable to the idea.
- Steve also mentioned that the paper needs to discuss concerns with allocators.  Tom agreed.
- Mark expressed a desire to discuss allocators in San Diego.
- Steve also suggested that the paper address the expected delivery time for features we're
  discussing.  In particular, to make it clear that `std::text` is not targetting C++20.
- Tom agreed.  Mark stated the paper should also address the intended target for existing papers
  in flight.
  

# August 29th, 2018

## Draft agenda:
- SG16 direction.  Where are we heading?  Big picture.
- Code points, EGCs, or explicit ranges for text views/containers?
  - How to decide?  Pick a direction now?  Write a pros/cons paper for the committee?

## Meeting summary:
- Attendees:
  - Artem Tokmakov
  - JF Bastien
  - Mark Zeren
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- With apologies from the editor, this summary writeup was very much delayed.
- Zach started off with an update on Boost.Text.  He noted that implementing the
  Uncode bidirectional algorithm was challenging.  Noone was surprised.
- Tom provided a brief summary for the agenda.  Basically to review our direction and
  confirm common goals and scope.
- JF asked what we have planned for C++20 to which Tom replied that we have a few small
  features in the queue and might otherwise take on some wording cleanup.
- Steve asked about timing for a potential TS and discussion ensued regarding how to
  get usage experience vs the benefits of going straight into the standard.
- Tom proposed a few statements to be considered as axioms, guidelines, questions, or
  possible directives for our work.
- (Axiom) 1: C++ has a long history of supporting non-Unicode encodings; we can't abandon legacy encodings.
  - JF brought up the concept of bridging with a comparison to `std::thread` and `native_handle`.
    E.g., an interface could provide a Unicode centric interface that abstracts support
    for legacy encodings.
- (Axiom) 2: execution and wide execution character encoding will remain run-time
   properties, `char8_t`, `char16_t`, and `char32_t` encodings will remain compile-time
   properties.
  - Tom asserted that legacy compatibility prevents mandating that the execution and wide
    execution encodings be fully known at compile time and noted that they can be changed
    dynamically by calling `setlocale`.
  - Tom also noted that WG14 is considering allowing a program's locale to be dynamically
    changed on a per-thread basis.  See [WG14 N2226](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2226.htm).
  - Artem asked how much we've been looking at existing locale support.
  - Zach responded that the existing locale support is insufficient to implement some parts
    of Unicode, in particular, support for tailoring.
  - JF mentioned that Javascript internationalization may be a good resource with regard to
    how to map locale information to Unicode.
- (Guideline) 3: Encourage the internal vs external encoding model with UTF-8 as the
  preferred internal encoding.
  - Tom asked if it is reasonable to encourage use of a particular encoding as the internal
    encoding.
  - Zach replied that he feels we must in order to avoid having to perform internal conversion
    rather than (only) conversions at component boundaries.
  - Mark suggested that extensions could enable support for other encodings.
  - Peter emphasized existing advocacy and trends with regard to UTF-8:
    - https://utf8everywhere.org
    - https://w3techs.com/technologies/overview/character_encoding/all
  - Tom asked JF if he could comment regarding how UTF-8 fits into the Apple ecosystem.
  - JF responded that, as long as convenient transcoding interfaces are available, that it
    wouldn't be an issue.
  - Tom asked if restricting access to code units in `std::text` (in order to allow the
    internal encoding to be implementation detail) would break use cases.
  - Zach responded yes, that prevents passing the underlying code unit sequence to C APIs.
    \[Editor's note: this response presumes that the underlying code unit sequence contains
    a nul terminator\]
- (Directive) 4: Improve support for transcoding at program borders (command line, env vars,
  stdin, stdout, text files, network).
  - Zach suggested not focusing on improving this now; let `fmt` deal with I/O; don't
    enhance iostreams.
  - Mark stated that we don't have to fix all of the problems with the standard library.
- (Question) 5: Do `std::text` and `std::text_view` replace `std::string` in new programs?
  - Mark stated no, not as a drop in replacement.
  - Zach noted that we want to continue using `std::string` for simple cases.
  - Tom asked, for new code, do we advocate a preference for `std::text` and `std::string`
    only when needed?
  - Zach stated no, for performance reasons.
  - Tom clarified: that indicates a specific reason to prefer `std::string` in some context,
    but in general, can we advocate use `std::text` unless there is a reason not to?
  - Zach responded that an AAT (Almost Always Text) rule would make sense.
  - Peter asked if it would ever be wrong to use `std::text` instead of `std::string`.
  - Zach replied, no.
  - Peter provided an example by way of `set<text>`.  If `std::text` comparisons are
    expensive (e.g., canonical equivalence vs lexicographical), use as a container element
    may not be desirable.
  - Zach noted that might be a reason to specialize `std::less`.
  - Zach observed that comparison cost is only an issue for relational comparison, equivalence
    is inexpensive if the text is already normalized.
  - Mark summarized, `std::text` provides storage, comparisons need specialized support.
- (Question) 6: How do we manage `std::text` and `std::string` conversions?
  - Tom asked if we need the ability to transfer buffer ownership between `std::string` and
    `std::text`.
  - Mark replied, yes, and that it needs to handle short buffer optimizations, but that this
    is lower priority than making the Unicode algorithms available.
  - Artem observed that `std::string_view` helps here.
- (Question) 7: Where do null terminated strings fit in?
  - Tom asked, can we try to reduce demand for them?  Perhaps propose a string/text type to WG14?
  - Everyone replied, not quickly :)
  - Mark asked if `std::text` needs null termination.
  - Zach replied that it can be provided at the code unit level for C compatibility, but doesn't
    make sense to provide null termination for code point or grapheme cluster sequences.
- (Question) 8: Where do Unicode algorithms fit into the library and are they independent of
  `std::text`?
  - Tom stated a preference that Unicode algorithms are usable with arbitrary string types.
  - Zach agreed stating that we should have code point range/iterator based interfaces as well as
    grapheme cluster range based interfaces.
- (Directive) 9: Adopt useful features from other languages.
  - Tom clarified, for example, named escapes as proposed in [P1097](http://wg21.link/p1097).
  - No disagreement.
- (Directive) 10: Fix existing issues as needed.
  - No disagreement.
- (Question) 11: What role do we take with WG14?
  - Tom asked, the question is really how much time to spend here.
  - Zach stated that engaging with WG14 over `char8_t` and terminology updates makes sense.
  - Mark observed that making Unicode data available via a C API could be useful.
- (Question) 12: What is our target schedule?
  - Steve suggested mostly targeting C++23, not a TS.
  - Zach noted that we need to ensure usage experience and that we have bandwidth limitations.


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
    the set of functionality to replicate at code point or higher levels?

    |  SF |   F |   N |   A |  SA |
    | --: | --: | --: | --: | --: |
    |   5 |   1 |   1 |   0 |   0 |

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
