# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, March 9th, 2022, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20220309T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- ICU features to consider for C++26 (see feature list [here](https://docs.google.com/document/d/1f-CLhYZIf_L0q1QBEqe2sVHyAofGx8Akt_xJKDGhcgA/edit?usp=sharing)).


# Past SG16 meetings
- [February 23rd, 2022](#february-23rd-2022)
- [February 9th, 2022](#february-9th-2022)
- [January 26th, 2022](#january-26th-2022)
- [January 12th, 2022](#january-12th-2022)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
