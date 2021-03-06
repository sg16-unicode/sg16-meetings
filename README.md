# SG16 Meeting Summaries

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.

The next SG16 meeting is scheduled for
Wednesday, March 10th, 2021, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20210310T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- Continue discussion from the last telecon with updated draft paper revisions:
  - [D2314R1: Character sets and encodings](https://wiki.edg.com/pub/Wg21virtual2021-02/SG16/d2314r1.html)
  - [D2297R1: Wording improvements for encodings and character sets](https://isocpp.org/files/papers/D2297R1.pdf)

Summaries of past meetings:
- [February 10th, 2021](#february-10th-2021)
- [January 27th, 2021](#january-27th-2021)
- [January 13th, 2021](#january-13th-2021)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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

## Meeting summary:
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
  - **Poll: Forward P2093R3 to LEWG..**
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
  ([Tutorial](https://foonathan.net/lexy/tutorial.html), [Reference](https://foonathan.net/lexy/reference.html)),
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
