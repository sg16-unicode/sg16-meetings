# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, March 26th, 2025, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20250326T193000&p1=1440&p2=tz_pdt&p3=tz_mdt&p4=tz_cdt&p5=tz_edt&p6=tz_cet)).

Draft agenda:
- [P3491R1: define_static_{string,object,array}](https://wg21.link/p3491r1).
- [P3391R0: constexpr std::format](https://wg21.link/p3391r0).


# Past SG16 meetings
- [March 12th, 2025](#march-12th-2025)
- [February 26th, 2025](#february-26th-2025)
- [February 5th, 2025](#february-5th-2025)
- [January 22nd, 2025](#january-22nd-2025)
- [November 6th, 2024](#november-6th-2024)
- [October 23rd, 2024](#october-23rd-2024)
- [October 9th, 2024](#october-9th-2024)
- [September 25th, 2024](#september-25th-2024)
- [September 11th, 2024](#september-11th-2024)
- [August 14th, 2024](#august-14th-2024)
- [July 31st, 2024](#july-31st-2024)
- [June 12th, 2024](#june-12th-2024)
- [May 22nd, 2024](#may-22nd-2024)
- [May 8th, 2024](#may-8th-2024)
- [April 24th, 2024](#april-24th-2024)
- [April 10th, 2024](#april-10th-2024)
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


# March 12th, 2025

## Agenda
- [P3395R0: Formatting of std::error_code](https://wg21.link/p3395r0).
- [P2873R2: Remove Deprecated locale category facets for Unicode from C++26](https://wg21.link/p2873r2).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Corentin Jabot
  - Eddie Nolan
  - Hubert Tong
  - Jens Maurer
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3395R0: Formatting of std::error_code](https://wg21.link/p3395r0):
  - **Poll 1: Forward P3395R0 to LEWG amended to specify an encoding for `std::error_category::name()`
    and for transcoding to be to UTF-8 if that matches the ordinary literal encoding and to an
    implementation-defined encoding otherwise.**
    - Attendees: 9 (two abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   6 |   0 |   0 |   0 |
    - Strong consensus.
- [P2873R2: Remove Deprecated locale category facets for Unicode from C++26](https://wg21.link/p2873r2):
  - **Poll 2: Forward D2873R3 to LWG with the acknowledgement that LEWG has already forwarded it pending
    SG16 approval.**
    - Attendees: 8 (two abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   4 |   0 |   0 |   0 |
    - Strong consensus.


# February 26th, 2025

## Agenda
- [P3263R0: Encoding annotated char](https://wg21.link/p3263r0).
- [P3412R1: String interpolation](https://wg21.link/p3412r1).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Bengt Gustafsson
  - Braden Ganetsky
  - Eddie Nolan
  - Hubert Tong
  - Jens Maurer
  - Peter Bindels
  - Steve Downey
  - Tiago Freire
  - Tom Honermann
  - Victor Zverovich
  - Ville Voutilainen
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3263R0: Encoding annotated char](https://wg21.link/p3263r0):
- [P3412R1: String interpolation](https://wg21.link/p3412r1):


# February 5th, 2025

## Agenda
- [P3560R0: Error Handling in Reflection](https://wg21.link/p3560r0).
- [P2758R4: Emitting messages at compile time](https://wg21.link/p2758r4).

## Meeting summary
- Attendees:
  - Barry Revzin
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Inbal Levi
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3560R0: Error Handling in Reflection](https://wg21.link/p3560r0):
  - **Poll 1: P3560R0: std::meta::exception should support both char and char8_t-based construction and accessors.**
    - Attendees: 8 (one abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   2 |   3 |   1 |   0 |
    - No consensus (too many neutrals).
  - **Poll 2: P3560R0: Forward to LEWG as is.**
    - Attendees: 9 (one abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   4 |   0 |   1 |   0 |
    - Consensus.
- [P2758R4: Emitting messages at compile time](https://wg21.link/p2758r4):
  - **Poll 3: P2758R4: Add overloads that allow the message to be passed as std::u8string_view.**
    - Attendees: 9 (two abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   2 |   1 |   0 |   0 |
    - Consensus.
  - **Poll 4: P2758R4: Add overloads that allow the message to be passed as std::wstring_view.**
    - Attendees: 9 (two abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   2 |   2 |   2 |   1 |
    - No consensus.
    - A/SA: `std::wstring_view` is mostly useful on Windows at run-time, we don't really need it
      at compile-time.
  - **Poll 5: P2758R4: Add overloads that allow the message to be passed as std::u16string_view and std::u32string_view.**
    - Attendees: 9 (two abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   1 |   5 |   1 |   0 |
    - No consensus.
  - **Poll 6: P2758R4: Forward to LEWG modified to include std::u8string_view overloads.**
    - Attendees: 9 (two abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   4 |   0 |   0 |   0 |
    - Strong consensus.


# January 22nd, 2025

## Agenda
- Decide on a meeting schedule for before/after the Hagenberg meeting.
- [P2019R7: Thread attributes](https://wg21.link/p2019).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Lauri Vasama
  - Jens Maurer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P2019R7: Thread attributes](https://wg21.link/p2019):
  - **Poll 1: P2019R7: Forward to LEWG modified to use the ordinary literal encoding for name hint.**
    - Attendees: 9 (one abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   3 |   1 |   0 |   0 |
    - Strong consensus in favor.


# November 6th, 2024

## Agenda
- [P3258R0: Formatting of charN_t](https://wg21.link/p3258r0).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Jens Maurer
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3258R0: Formatting of charN_t](https://wg21.link/p3258r0):
  - **Poll 1: It is more important to avoid implicit loss of information during transcoding operations
    than to provide support for formatting `charN_t` in the standard library.**
    - Attendees: 7
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   3 |   1 |   1 |   1 |
    - Weak consensus in favor.
  - **Poll 2: Encourage more work on P3258R0, particularly with regard to handling of transcoding failures.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   0 |   0 |   2 |   1 |
    - No consensus.
  - **Poll 3: Encourage work on support for `std::format` and `std::print` with `charN_t` format strings.**
    - Attendees: 6
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   2 |   1 |   0 |   0 |
    - Consensus in favor.


# October 23rd, 2024

## Agenda
- [P3374R0: Adding formatter for fpos<mbstate_t>](https://wg21.link/p3374r0).
- [P2019R7: Thread attributes](https://wg21.link/p2019r7).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Eddie Nolan
  - Jens Maurer
  - Liang Jiaming
  - Nathan Owen
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3374R0: Adding formatter for fpos<mbstate_t>](https://wg21.link/p3374r0):
  - \[ Editor's note: Liang's presentation slides are avilable
    [here](presentations/2024-10-23-p3374r0-presentation.pdf). \]
  - **Poll 1: P3374R0: The C++ standard library should include a formatter for `std::fpos<State>`.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   5 |   2 |   1 |   0 |
    - Consensus in favor.
  - **Poll 2: P3374R0: The C++ standard library should include a formatter for `std::mbstate_t`.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   1 |   3 |   4 |   0 |
    - Consensus against.
  - **Poll 3: P3374R0: The `std::fpos<State>` and/or `std::mbstate` formatter should only indicate whether the state is in an initial state.**
    - Attendees: 9 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   2 |   2 |   1 |   0 |
    - Consensus in favor.
    - A: Requiring this overconstrains implementations and I would prefer the full data be included.
- [P2019R7: Thread attributes](https://wg21.link/p2019r7):


# October 9th, 2024

## Agenda
- [P3094R3: std::basic_fixed_string](https://wg21.link/p3094r3).
- [P3045R1: Quantities and units library](https://wg21.link/p3045r1).
- [P3258R0: Formatting of charN_t](https://wg21.link/p3258r0).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Henrik Nyhammer
  - Mateusz Pusz
  - Peter Bindels
  - Jens Maurer
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3094R3: std::basic_fixed_string](https://wg21.link/p3094r3):
  - **Poll 1: P3094R4: Amend the proposal to remove the `traits` template parameter and dependence on `std::char_traits`.**
    - Attendees: 12 (2 abstentions)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   5 |   1 |   0 |   0 |
    - Strong consensus in favor.
  - **Poll 2: P3094R4: Forward as amended to LEWG.**
    - Attendees: 12
    - No objection to unanimous consent.
- [P3045R1: Quantities and units library](https://wg21.link/p3045r1):
- [P3258R0: Formatting of charN_t](https://wg21.link/p3258r0):


# September 25th, 2024

## Agenda
- [P2319R1: Prevent path presentation problems](https://wg21.link/p2319r1).
- [P2019R7: Thread attributes](https://wg21.link/p2019r7).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Jens Maurer
  - Tom Honermann
  - Steve Downey
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P2319R1: Prevent path presentation problems](https://wg21.link/p2319r1):
  - **Poll 1: P2319R2: Forward to LEWG.**
    - Attendees: 8
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   6 |   0 |   0 |   0 |
    - Strong consensus in favor.
- [P2019R7: Thread attributes](https://wg21.link/p2019r7):
  - **Poll 2: P2019R7: Name hint should be provided in the ordinary literal encoding.**
    - Attendees: 8
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   3 |   1 |   3 |   1 |   0 |
    - Weak consensus in favor.
  - **Poll 3: P2019R7: Name hint should be provided as an NTMBS in the C locale encoding.**
    - Attendees: 8
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   1 |   5 |   1 |   0 |   1 |
    - Consensus in favor.


# September 11th, 2024

## Agenda
- [P2319R0: Prevent path presentation problems](https://wg21.link/p2319r0).
- [P3364R0: Remove Deprecated u8path overloads From C++26](https://wg21.link/p3364r0).
- [P2019R6: Thread attributes](https://wg21.link/p2019r6).

## Meeting summary
- Attendees:
  - Alisdair Meredith
  - Braden Ganetsky
  - Corentin Jabot
  - Eddie Nolan
  - Fraser Gordon
  - Jens Maurer
  - Jiaming Liang
  - Tom Honermann
  - Steve Downey
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P2319R0: Prevent path presentation problems](https://wg21.link/p2319r0):
  - **Poll 1: P2319R0: The `string()` member function of `std::filesystem::path` should be deprecated.**
    - Attendees: 9
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   2 |   4 |   1 |   0 |   0 |
    - Consensus in favor.
  - **Poll 2: P2319R0: The proposed `system_string()` member function should be added to `std::filesystem::path`.**
    - Attendees: 9
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   0 |   2 |   4 |   1 |   0 |
    - No consensus.
- [P3364R0: Remove Deprecated u8path overloads From C++26](https://wg21.link/p3364r0):
  - **Poll 3: P2319R0: In the long term we want to remove `std::filesystem::u8path`
    (with the implication that, if we don't, that we will undeprecate it).**
    - Attendees: 10
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   4 |   2 |   0 |   0 |   2 |
    - Consensus in favor.
- [P2019R6: Thread attributes](https://wg21.link/p2019r6):


# August 14th, 2024

## Agenda
- [P2996R5: Reflection for C++26](https://wg21.link/p2996r5).
- [P2319R0: Prevent path presentation problems](https://wg21.link/p2319r0).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Dan Katz
  - Daveed Vandevoorde
  - Eddie Nolan
  - Inbal Levi
  - Jens Maurer
  - Steve Downey
  - Tomasz Kamínski
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P2996R5: Reflection for C++26](https://wg21.link/p2996r5):
  - \[ Editor's note: D2996R5 was the active paper under discussion at the telecon.
    The agenda and links used here reference P2996R5 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - **Poll 1: Provide a generic `define_static_array(span<const T>) -> span<const T>` function and remove
    `define_static_string()` until we have clarity on how to satisfy desires for a null terminated string
    and a return type of `string_view` (or similar).**
    - Attendees: 10 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   6 |   2 |   1 |   0 |   0 |
    - Consensus in favor.
  - **Poll 2: Forward P2996R5 with a recommendation to amend per prior poll to replace
    `define_static_string` with a generic `define_static_array` function.**
    - Attendees: 10 (1 abstention)
      | SF  | F   | N   | A   | SA  |
      | --: | --: | --: | --: | --: |
      |   7 |   3 |   0 |   0 |   0 |
    - Consensus in favor.
- [P2319R0: Prevent path presentation problems](https://wg21.link/p2319r0):


# July 31st, 2024

## Agenda
- [P3068R2: Allowing exception throwing in constant-evaluation](https://wg21.link/p3068r2).
- [LWG issue 4087: Standard exception messages have unspecified encoding](https://cplusplus.github.io/LWG/issue4087).

## Meeting summary
- Attendees:
  - Eddie Nolan
  - Hana Dusìkovà
  - Inbal Levi
  - Jens Maurer
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [P3068R2: Allowing exception throwing in constant-evaluation](https://wg21.link/p3068r2):
- [LWG issue 4087: Standard exception messages have unspecified encoding](https://cplusplus.github.io/LWG/issue4087):


# June 12th, 2024

## Agenda
- [LWG issue 4070: Transcoding by std::formatter&lt;std::filesystem::path&gt;](https://cplusplus.github.io/LWG/issue4070).
- [LWG issue 4087: Standard exception messages have unspecified encoding](https://cplusplus.github.io/LWG/issue4087).
- [LWG issue 4090: Underspecified use of locale facets for locale-dependent std::format](https://cplusplus.github.io/LWG/issue4090).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Jens Maurer
  - Mark de Wever
  - Nathan Owen
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- \[ Editor's note: The SG16 chair has fallen far behind his obligations but will publish a proper summary
  of this meeting in due time. \]
- [LWG issue 4070: Transcoding by std::formatter&lt;std::filesystem::path&gt;](https://cplusplus.github.io/LWG/issue4070):
- [LWG issue 4087: Standard exception messages have unspecified encoding](https://cplusplus.github.io/LWG/issue4087):
- [LWG issue 4090: Underspecified use of locale facets for locale-dependent std::format](https://cplusplus.github.io/LWG/issue4090):


# May 22nd, 2024

## Agenda
- Fraser to report on the May 3rd Text Terminal WG meeting.
- Review results of the 2024 C++ Developer Survey.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Fraser Gordon
  - Mark de Wever
  - Peter Bindels
  - Robin Leroy
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
- Fraser to report on the May 3rd Text Terminal WG meeting:
  - Fraser provided an overview:
    - This was the third meeting of the WG.
    - Outreach to the terminal community resulted in many new attendees.
    - Simon Tatham of PuTTY fame attended and demonstrated considerable experience in this area.
    - Representation from WG14 would be appreciated.
    - Representation from the Rust community would also be appreciated.
    - Most of the discussion was process related.
    - No attendees have objected to working in the open.
    - Near term efforts will include deployment of collaboration tools.
    - The next meeting will probably be in July and is expected to focus on establishing scope
      for the group and beginning technical discussion.
    - The group is feeling positive about making improvements.
  - Tom suggested reaching out to the WG14 convenor regarding WG14 participation.
  - Robin responded that such participation might fall to him as SC22 liaison.
  - Tom noted that Eddie had previously reported discussion about `wcwidth()` at the TTWG meeting.
  - Fraser explained that a replacement for `wcwidth()` is likely necessary but might run into opposition
    in WG14.
  - Corentin responded that `wcwidth()` is part of POSIX, but not included in standard C.
  - Victor asked for more details regarding participation from the terminal community.
  - Fraser responded that participants on the mailing list include people from iTerm, MoSH, PuTTY, xterm,
    ncurses, and the Far Manager TUI application.
  - Robin noted that the initial effort that resulted in formation of the TTWG group came from Microsoft and
    that Apple is a Unicode Consortium member.
  - Tom asked if there are still people from Microsoft involved.
  - Fraser replied that there are and that they include the original TTWG chair and people working on
    [Windows Terminal](https://github.com/microsoft/terminal).
  - PBindels reported having attended and summarized the discussion that led to the determination that
    `wcwidth()` is not salvageable and will need to be replaced; it can't accommodate variation selectors.
  - Tom explained that the Austin group that maintains the POSIX specification is open and welcoming and
    offered to help facilitate introduction if doing so would be helpful.
  - Victor asked for more details regarding `wcwidth()` vs `wcswidth()`.
  - PBindels responded that `wcwidth()` is fundamentally broken since it only accepts a single `wchar_t`
    code unit as input but that `wcswidth()` might be salveageable.
  - Fraser noted that WG14 did consider standardizing the POSIX interfaces back in the C99 time frame.
  - Fraser extended a thank you to anyone that is able to attend future TTWG meetings.
- Review results of the 2024 C++ Developer Survey:
  - Tom briefly reviewed the Unicode related survey results and comments.
  - Tom stated that he was not surprised by the results.
  - Victor expressed surprise that only 16% of respondents reported Unicode related issues as a major pain point.
  - PBindels responded that programmers that write code solely for use in their local region don't tend to have
    issues because ASCII suffices.
  - Tom pondered how much pain would be reduced by adding conversion facilities.
  - Victor observed that five or six of the Unicode related comments mentioned use of UTF-8 with `char` and noted
    that as a good fraction of the comments.
  - Victor asserted that we should continue focusing on that like what we did for `std::format()`.
  - Tom expressed strong agreement; Linux, the BSDs, and macOS comprise a huge chunk of the ecosystem.
  - Corentin asserted that we can't just focus on that segment of the ecosystem though and noted that this isn't
    new information; we are well aware of the need to support UTF-8 with `char`-based types.
  - Victor responded by stating that the new information is the explicit requests to support UTF-8 with no
    corresponding mention of support for code pages.
  - Corentin stated that we can't extrapolate such comments to the entire C++ community; the number of
    respondents to the survey is a small fraction of the community and too small to draw conclusions from.
  - Corentin added that we are in a situation of being resource constrained; there are things we know we want,
    but wanting doesn't make it happen; someone needs to write the corresponding papers.
  - Tom directed discussion to other comments and noted that the mentions regarding `char8_t` also didn't
    surprise him.
  - Corentin stated that we did the community a disservice by not providing library support for a useful type;
    `char8_t` is relatively useless right now.
  - Corentin insisted the difficulty with using the type doesn't mean that the motivation for the type has
    gone away.
  - Tom expressed being a little surprised by the explicit requests to extend `std::from_chars()` and
    `std::to_chars()` to support `charN_t` types.
  - Corentin expressed uncertainty regarding what was actually being requested; there are several
    interpretations:
    - Programmers might just want to use these functions without having to transcode.
    - Programmers might want these functions to support non-ASCII numbers.
  - Victor replied that `std::from_chars()` and `std::to_chars()` were designed to function as a low level
    feature and asserted that it wouldn't be right to add internationalization features to them.
  - Victor opined that the author probably just wants support for the `charN_t` code unit types.
  - Victor explained that, since these functions are low level, that he isn't really interested in seeing
    them expanded; not even to add support for `std::string_view`.
  - Steve noted that `std::from_chars()` and `std::to_chars()` don't even support `wchar_t` right now; these
    functions were designed to support JSON or XML with basic characters.
  - Corentin agreed with Victor up to the comment regarding `std::string_view`.
  - Corentin noted that `std::from_chars()` is difficult to implement and suggested that we shouldn't make
    it harder.
  - Steve observed that different names would be required for other character types since it wouldn't be
    possible to overload `std::to_chars()`.
  - Victor stated that, with regard to `std::string_view`, the interface for these functions is awkward.
  - Victor insisted that we don't want to turn these functions into `std::format`; they should remain
    minimal.
  - Robin noted that some number systems are not positional and that it would not be advised to add support
    for them to these functions.
- [P2626R0: charN_t incremental adoption: Casting pointers of UTF character types](https://wg21.link/p2626r0):
  - Corentin lamented the absence of core language experts and stated that assistance is needed to make
    progress as we still have the same questions as the last time the paper was discussed.
  - Corentin presented:
    - We introduced the `charN_t` code unit types, but they can't interoperate easily with existing
      functions that operate on `char` or `wchar_t` based storage; we need a mechanism that avoids
      problems due to type based aliasing.
    - We would ideally allow implicit conversions but that can't work in C++.
    - The currently available options for interoperation include:
      - performing inefficient copies in and out of temporary buffers; this works without UB.
      - using `reinterpret_cast`; this results in UB.
      - using `start_lifetime_as`; this results in UB.
    - The paper proposes a magic library function to facilitate conversions with an appropriate aliasing
      barrier that prevents UB in very specific circumstances.
    - The proposed semantics effectively end the lifetime of an object and begin the lifetime of a
      replacement object in place of the original using the same object representation.
    - This is a very sharp tool and we need CWG to assist in specifying what the constraints are; those
      constraints will help guide what the interface should look like.
    - I'm not interested in a general tool to enable selective aliasing; I want something that is UTF
      aware with variants that check for well-formed UTF sequences.
    - The proposal is inspired by similar functionality available in Rust; Rust relies on the concept
      of a safe borrow to ensure the type system is not violated.
    - The proposal includes two functions; one that works on bytes and another that works on code units.
  - Victor commented on the desire to ensure well-formed UTF sequences but noted that we don't actually
    enforce well-formed UTF elsewhere.
  - Corentin acknowledged the lack of preconditions on UTF-8 encoded literals or in the standard library
    at present.
  - Corentin stated that, if he could, he would require UTF-8 literals to be well-formed.
  - Corentin explained that the proposed "unchecked" variant is intentionally named to sound scary.
  - Robin opined that it seems a bit odd to impose such considerations for the proposed conversions when
    the subscript operator doesn't impose preconditions on data being well-formed.
  - Robin explained that it seems weird since the type itself doesn't offer any guarantees.
  - Corentin replied that the standard library is, unfortunately, focused solely on code units;
    `std::basic_string` is just a sequence of code units.
  - Corentin described the use case he has in mind; passing data to a function that has such a
    precondition.
  - Corentin noted that nothing otherwise prevents unintentionally passing, e.g., EBCDIC, to a function
    that expects UTF-8 when performing a conversion from `char` to `char8_t`.
  - Robin observed that Latin-1 data will appear to be valid UTF-8 when the data contains only ASCII
    characters; it is the semantic that is important.
  - Corentin agreed that it isn't possible, in general, to know if data was correctly constructed because
    mojibake doesn't necessarily produce ill-formed encoded text.
  - Robin expressed some discomfort with the "unchecked" terminology since the check doesn't ensure that
    the semantic was honored.
  - Tom observed that, with a suitable contracts facility, a function with a narrow contract that consumes
    the converted data would have a precondition for well-formed text.
  - Corentin responded by stating that a checked version isn't proposed at this point; the intent is to
    provide a scary looking function that makes sure the programmer is aware that they don't necessarily
    have valid UTF-8 following the conversion.
  - Tom expressed gratitude for that explanation as helpful to explain the motivation for the "unchecked"
    terminology.
  - Corentin directed discussion back to core functionality concerns and noted that the proposed functions
    are intended to provide a low level interface; one for which there might be motivation to add a wrapper.
  - Corentin expressed concern that an ergonomic wrapper might provide a false sense of security and noted
    that it would be very easy to produce UB if a called function stashes pointers.
  - Tom asked how close `std::start_lifetime_as_array()` comes to being the core language facility needed.
  - Corentin replied that it is very close to being what is needed, but that Clang doesn't implement it yet.
  - Tom shared a Compiler Explorer link: https://godbolt.org/z/9Tejj9TPs.
  - Robin commented that ICU is one of the projects that uses `char16_t`.
  - Robin stated that the ICU maintainers have looked at `char8_t` and have added some functions that work
    with it.
  - Robin noted that the ICU maintainers have asked how they can enable interoperability with all of the
    character types but that they have not received a helpful answer.
  - Robin offered to get Corentin in touch with the ICU maintainers to discuss how this would be useful to
    ICU.
  - Corentin replied that Tom has investigated what ICU does at present; it uses a volatile asm statement
    as a rudimentary alias barrier, but that doesn't fully work.
  - Robin asked if the proposed feature would work for ICU.
  - Tom replied that the intent is for it to work for ICU and stated that if it doesn't, then we probably
    wouldn't want to standardize it.
  - Mark asked if the proposed functions provide access to just the element a pointer points to or if they
    provide access to a range of elements.
  - Corentin replied that answers to such questions are dependent on what we can do within the core language;
    we need to determine if the interface requires an explicit range.
  - Tom noted that it is complicated and posed a hypothetical question of whether replacing a portion of the
    elements in an array via the converted type would end the lifetime of the entire array.
  - Corentin replied that the same core question applies for any replacement of a subobject.
  - Corentin noted that such questions might be more relevant for the specification than for implementations.
  - Mark objected to referring to the proposed operation as a cast.
  - Corentin responded by stating that it is similar to `reinterpret_cast`.
    Corentin expressed that he is open to a better name, but that he wants a name that will scare programmers
    away from casually using it.
  - Tom directed discussion back to the previously shared
    [Compiler Explorer link](https://godbolt.org/z/9Tejj9TPs)
    and asked if `g()` looks representative of a common use case.
  - Corentin noted that the example is unsafe if `f()` stashes the pointer passed to it.
  - Corentin stated that he would expect libraries to provide overloads that use these conversions as
    implementation detail when it is known to be safe to do.
  - Robin provided a hypothetical example of a date parsing function that accepts a pointer to `wchar_t` and
    uses the proposed features to forward it internally to a function that works with `char16_t`.
  - Robin asked whether the use of the proposed conversion feature would destroy the caller's `wchar_t` string.
  - Corentin responded that the caller is only affected if the callee doesn't undo the operation.
  - Corentin noted that the proposed functionality would only work with types like `char` that are transparently
    replaceable.
  - Tom asked if `std::start_lifetime_as` has been implemented for gcc yet.
  - Corentin replied that he is unaware of it being implemented anywhere yet.
  - Corentin noted that implementation requires more than just frontend work.
  - Robin stated that, given the low level interfaces proposed, the first thing he would do is write an RAII
    wrapper to ensure conversions are reversed.
  - Robin asked if the standard library should provide such a wrapper.
  - Corentin replied that he and Tom have discussed that multiple times.
  - Tom opined that Robin is right; that programmers will implement an RAII type to be sure conversions are undone.
  - Tom suggested we do the following:
    - Ask Jens to schedule time in CWG to discuss the object model concerns.
    - Once we have a better idea of the core language constraints, schedule time with the ICU TC to discuss how
      and whether the feature could be used with ICU.
- Tom announced that the next meeting will be 2024-06-12 and that we have LWG issues to discuss ahead of the
  St. Louis meeting.
- Robin informed the group that be will be unable to attend the next meeting on June 12th.


# May 8th, 2024

## Agenda
- [D3258R0: Formatting of charN_t](https://wg21.link/p3258r0).
- [P2996R2: Reflection for C++26](http://wg21.link/p2996r2).

## Meeting summary
- Attendees:
  - Braden Ganetsky
  - Corentin Jabot
  - Dan Katz
  - Eddie Nolan
  - Lauri Vasama
  - Mark de Wever
  - Nathan Owen
  - Peter Bindels
  - Robin Leroy
  - Tom Honermann
  - Victor Zverovich
- Robin provided a report on UTC #179:
  - \[ Editor's note: Minutes from the UTC #179 meeting are recorded in
    [L2/24-061](https://www.unicode.org/L2/L2024/24061.htm). \]
  - The alpha review period closed several weeks before the meeting and the UTC WGs then
    had one week to prepare any material responses for the meeting.
  - The agenda for this meeting included reviewing the alpha feedback and authorizing the
    beta release with stable specifications.
  - The character repertoire is now frozen.
  - Two recently added characters were removed at the request of the Indian government; see
    [consensus item 179-C43](https://www.unicode.org/L2/L2024/24061.htm#179-C43).
  - Significant changes were made to the line breaking algorithm, but these changes don't
    affect current C++.
    - Improvements were made to the handling of quotation marks in simplified Chinese.
    - Changes were made to the handling of hyphens and numeric expressions.
  - Recommendations from the CJK & Unihan Working Group were accepted that will impact the
    wording currently present in
    [\[format.string.std\]p13](https://eel.is/c++draft/format.string.std#13)
    when the C++ standard is rebased on Unicode 16; the set of code points included in
    bullet 13.2 will be subsumed by 13.1 due to acceptance of
    [L2/24-059 (Proposal to change the East_Asian_Width property of the Yijing symbols)](https://www.unicode.org/L2/L2024/24059-eaw-yijing-symbols.pdf).
  - Tom stated that we should create an issue to track doing that update when we rebase
    on Unicode 16 or later.
  - \[Editor's note: Tom created
    [SG16 issue 81 (Unicode 16: Updates needed for \[format.string.std\]p13 field widths)](https://github.com/sg16-unicode/sg16/issues/81)
    to do so. \]
- Robin wondered why the code points listed in
  [\[format.string.std\]p13](https://eel.is/c++draft/format.string.std#13)
  bullets 13.3 (U+1f300 - U+1f5ff (Miscellaneous Symbols and Pictographs))
  and 13.4 (U+1f900 - U+1f9ff (Supplemental Symbols and Pictographs) are
  listed with a field width of 2; these code points aren't wide in text presentation form,
  but would be in emoji presentation form.
- Robin shared a
  [link](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=%5B%5Cx%7B1F300%7D-%5Cx%7B1F5FF%7D%5D&g=ea&i=)
  listing all of the characters covered by bullet 13.3 and noted that some of them,
  🖗 for instance, are presented in a narrow form in the Windows terminal for him.
- Corentin explained that testing revealed that these characters were predmoninantly
  displayed as wide characters in existing terminals.
- Eddie reported relevant discussion having occured during the recent meeting of the Unicode
  Text Terminal Working Group (TTWG); the POSIX `wcswidth()` function maps a code point to a
  width, but does not account for variation selectors.
- Eddie stated that there is supposed to be a default for whether text vs emoji presentation
  form is used, but there is implementation divergence.
- [D3258R0: Formatting of charN_t](https://wg21.link/p3258r0):
  - \[ Editor's note: D3258R0 was the active paper under discussion at the telecon.
    The agenda and links used here reference P3258R0 since the links to the draft paper were ephemeral.
    The published document may differ from the reviewed draft revision. \]
  - Corentin provided an overview of the paper:
    - The motivation for the paper is to enable the ability to print `char8_t`-based UTF-8 text
      via `std::format()`.
    - The intent is for something like `std::format("...", std::meta::name_of(^XX))` to just do
      the right thing.
    - The goal is for semantics to be consistent.
    - The proposal includes support for formatting arguments of type `char8_t`, `char16_t`, and
      `char32_t` for both `""` and `L""` format strings.
    - No support is proposed for use of `u8""`, `u""`, or `U""` literals as format strings.
    - A replacement character will be substituted for ill-formed code unit sequences.
    - No error mechanism is proposed but one could be added later by adding format specifier
      options.
    - No support is proposed for formatting arguments of type `char` with a `L""` format string
      or for formatting arguments of type `wchar_t` with a `""` format string due to potentially
      ambiguous encoding associations.
    - Formatting of escaping characters and strings will work as expected.
    - For a non-UTF encoding, the replacement character will be `?`; this matches substitutions
      currently observable with the Microsoft compiler on Windows.
    - No special behavior is proposed for `std::print()`.
    - A prototype implementation was completed for libc++, but libc++ only supports the ordinary
      literal encoding being UTF-8, so that doesn't exercise transcoding scenarios.
    - The C and C++ standards don't provide transcoding facilities other than `mbrtoc8()` and
      such, but conversions can be done using `iconv`, ICU, or other existing converters.
    - Some transcoding facilities do not offer flexibility for error handling.
    - Support for formatting single code units of `char8_t`, `char16_t`, and `char32_t` is
      proposed; this is consistent with existing support for `char` and `wchar_t`.
    - `constexpr` implementations of `std::format()` already have the ability to perform
      conversions between the set of literal encodings.
  - Victor observed that a number of the `std::format()` examples in the paper are
    syntactically incorrect as presented; likely due to markup issues.
  - Victor explained that `std::vprint_unicode()` and `std::vprint_nonunicode()` are not
    exposition only so that programmers can provide overloads for their own types with
    differentiation for UTF and non-UTF encodings.
  - Victor noted that locking variations of these functions are now specified as well.
  - \[ Editor's note: Locking variations were recently added via the adoption of
    [P3107R5 (Permit an efficient implementation of std::print)](https://wg21.link/p3107r5)
    during the Tokyo meeting. \]
  - Tom asked for an explanation of the ABI limitations on extending format specifiers.
  - Mark explained that the ABI is restricted by `std::basic_format_arg<Context>::visit()`;
    `std::basic_format_arg` is effectively a discriminated union and the number of discernible
    types is constrained by the type used to identify them.
  - \[ Editor's note: See
    [Mark's follow up post to the SG16 mailing list](https://lists.isocpp.org/sg16/2024/05/4302.php). \]
  - Victor replied that it would be possible to use the normal formatter API instead of
    `std::basic_format_arg`.
  - Victor stated that
    [{fmt}](https://github.com/fmtlib/fmt)
    already supports `constexpr`, but that there are no immediate plans to propose support for
    `std::format()` as `constexpr` in the standard.
  - Victor suggested that the paper simply state that `constexpr` support is implementable.
  - Tom directed discussion to whether the proposed capabilities would suffice to meet the minimum
    requirements for printing of identifiers as desired for the reflection proposal.
  - Dan opined that it does, noted that Daveed would like to have iostream support, but commented that
    he doesn't feel as strongly about that.
  - Corentin said that he would like to know if anyone felt very strongly about support for iostreams.
  - Corentin stated he would rather focus on support for `std::format()` and `std::print()`, but that he
    can understand why others might want iostream support specifically.
  - Corentin explained that he did not propose iostream support because he didn't feel like he was the
    right person to do so.
  - Victor stated that he views the proposed capabilities as a partial solution that is not inline with the
    `std::format()` design intent to not mix encoding concerns.
- [P2996R2: Reflection for C++26](http://wg21.link/p2996r2):
  - Victor expressed strong opposition to only exposing identifiers in `char8_t` and asserted that we need
    to figure out the story for support of `char`.
  - Dan interpreted Victor's response as meaning that the proposed facilities with only support for
    `char8_t` does not provide a sufficient solution.
  - Dan stated that the idea of using a magic proxy type seems good and that Daveed has expressed support
    for it.
  - Eddie reported having recently discussed the proxy type with other attendees of C++Now and that some
    found it to be an overcomplicated solution.
  - Corentin responded that, if done right, programmers shouldn't be much affected by it.
  - Corentin opined that a proxy type is fine but that a solution that uses an escape mechanism to
  - effectively create a new encoding is not.
  - Tom pondered whether there is a need to distinguish between names and identifiers and noted that many
    functions, like conversion operators and overloaded operators, don't have associated identifiers but
    do have names.
  - Corentin indicated that is probably not an SG16 concern.
  - Corentin suggested that reflection use cases are best addressed by performing code injection rather
    than defining overloaded operators.
  - Corentin agreed that reflection might want to differentiate names and identifiers in a similar manner
    to how Clang does internally.
  - Dan advised caution regarding exposing a meta type for a name when already working with a meta type.
  - Victor asked if the hypothetical proxy name type might be exposition only with conversion operators.
  - Victor asked what the plan is for exploring the idea of such a type.
  - Corentin asked with a smile whether Victor was volunteering to do so.
  - Dan responded that the P2996 authors can propose a shape for the type.
  - Tom summarized his impression of consensus so far; that it seems that there is good consensus for
    supporting both `char` and `char8_t`, but since we can't overload based on return types, that use of
    a distinct type is needed to avoid having to specify distinct names; such a type enables future
    extension.
  - Corentin asked what the motivation would be for an exposition only type.
  - Dan replied with a smile that it would avoid a bike shedding exercise in LEWG.
  - Dan stated there is a need to be able to perform string comparisons for implementation of
    `enum_to_string`.
  - Corentin acknowledged that a proxy type makes things easier by adding a layer of indirection.
  - Eddie asked for reasons not to define separate functions for `std::meta::name_of()` and related
    functions.
  - Dan replied that doing so creates a combinatorial explosion.
  - Eddie asked what would happen in the case of an enumeration that has a set of enumerators that cannot
    all be converted losslessly to the ordinary literal encoding and where transliteration might produce
    the same name.
  - Dan suggested use of `char8_t` to avoid such cases.
  - Eddie responded that his concern is whether such a scenario should be possible since it makes it easy
    to do the wrong thing.
  - Corentin noted that the compiler's internal representation is always able to distinguish such cases.
  - Corentin asked Robin if there are duplicated characters that are valid for use in identifiers and that
    canonicalize to the same representation.
  - Robin replied that there are reasonable mappings to other character sets that result in ambiguity.
  - Robin provided a reference and some examples in the chat:
    - [Unicode 15.1, chapter 7, section 7.2, "Greek", paragraph starting with "Greek Letters as Symbols"](https://www.unicode.org/versions/Unicode15.1.0/ch07.pdf#G12477):
   
          For compatibility purposes, a few Greek letters are separately encoded as symbols in other
          character blocks. Examples include U+00B5 µ MICRO SIGN in the Latin-1 Supplement character
          block and U+2126 Ω OHM SIGN in the Letterlike Symbols character block. The ohm sign is
          canonically equivalent to the capital omega, and normalization would remove any distinction.
          Its use is therefore discouraged in favor of capital omega. The same equivalence does not
          exist between micro sign and mu, and use of either character as a micro sign is common. For
          Greek text, only the mu should be used.

    - μ, µ, 𝛍, 𝜇, 𝝁, 𝝻, and 𝞵 are all compatibility equivalent to μ and all are valid C++ identifiers.
  - Corentin asked whether the roundtrip requirement can actually be satisfied in the presence of arbitrary
    encodings.
  - Victor replied to the overloading concerns by mentioning that Daveed's original suggestion was for
    `std::meta::name_of()` and friends to be templated on a character type.
  - Victor noted that roundtrip support can be facilitated with an escape mechanism as in Daveed's
    preferred option.
  - Tom stated that roundtrip support cannot tolerate lossy conversions and that an attempted conversion
    that would be lossy must result in an error or substitution of an escape sequence.
  - Eddie expressed concern that conversion to `char` won't work everywhere, but since it will work in
    most cases such support can lead to broken code that isn't caught by testing.
  - Eddie suggested that the function template idea seems ok if the character template type parameter is
    specified with a default template argument of `char8_t`.
  - Dan asked what the advantage of a template parameter would be over an opaque type.
  - Eddie replied that it can't be completely hidden away; that it will appear in error messages, on
    cppreference.com, etc...
  - Corentin stated that programmers don't want to care about this and that they just want the identifier
    to be printed; if we can make it just work, that is a win.
- Tom announced that the next SG16 meeting will be on 2020-05-22 and that he intends to put
  [P2626R0 (charN_t incremental adoption: Casting pointers of UTF character types)](https://wg21.link/p2626r0)
  on the agenda, perhaps along with some recently created LWG issues.


# April 24th, 2024

## Agenda
- [P1953R0: Unicode Identifiers And Reflection](https://wg21.link/p1953r0).
- [P2996R2: Reflection for C++26](http://wg21.link/p2996r2).

## Meeting summary
- Attendees:
  - Andrei Alexandrescu
  - Braden Ganetsky
  - Corentin Jabot
  - Dan Katz
  - Daveed Vandevoorde
  - Eddie Nolan
  - Giuseppe D'Angelo
  - Jens Maurer
  - Mark de Wever
  - Nathan Owens
  - Steve Downey
  - Tom Honermann
  - Victor Zverovich
  - Wyatt Childers
- [P1953R0: Unicode Identifiers And Reflection](https://wg21.link/p1953r0):
  - Corentin provided an introduction:
    - This is an older paper and reflection has changed in the meantime, but it is still relevant.
    - [P1949 (C++ Identifier Syntax using Unicode Standard Annex 31)](https://wg21.link/p1949r7)
      clarified the syntax for identifiers to provide better support for non-English speakers and
      mathematicians.
    - String literals are converted from the source file encoding to an implementation-defined
      literal encoding that might not be Unicode.
    - [P1854R4 (Making non-encodable string literals ill-formed)](https://wg21.link/p1854r4)
      changed string literals to be ill-formed if they specify characters that are not
      representable in the associated literal encoding.
    - Characters can always be converted to Unicode encodings without loss of data in C++.
    - Reflection needs to specify the type and encoding used to reflect an identifier.
    - The only solution that works in all cases is to expose identifiers in a UTF encoding.
    - It is not possible to infer the encoding of a string just by looking at the values of its
      code units.
  - Daveed commented that there are some encodings that have characters that lack representation
    in Unicode.
  - Corentin acknowledged such limitations and explained that new characters are regularly
    invented in some cultures but are not widely used or encoded.
  - Corentin noted that trademarks and various other symbols likewise are not encoded in Unicode.
  - \[ Editor's note: The editor's Bluetooth stack regretably crashed and a minute or so of
    Corentin's continued elaborations were not captured. \]
  - Victor stated that having reflection expose names solely in `char8_t` would be user hostile
    since there is little support for `char8_t` in the standard library.
  - Victor reported that his organization bans use of `u8` literals.
  - Victor expressed support for the approach described in section 4.4.6,
    "`name_of`, `display_name_of`, `source_location_of`" that limits names to characters in the
    [*basic character set*](http://eel.is/c++draft/lex.charset#def:character_set,basic).
  - Victor asserted that reflection must provide good support for the common case where the
    ordinary literal encoding is UTF-8.
  - Daveed asked about implications for EBCDIC based platforms.
  - Corentin replied that EBCDIC and UTF-8 encoded data can't be discerned just by looking at the
    string contents, so reflecting names in UTF-8 in `char`-based storage would be problematic
    for such platforms.
  - Tom replied that there are EBCDIC code pages that are missing representation for some characters
    from the basic character set but that digraphs are available for those characters so we don't
    really concern ourselves with them in practice.
  - Steve corrected Tom in the chat; EBCDIC code pages provide representation for all the characters
    in the basic character set, but not all such characters are encoded with the same value.
  - Jens explained that, for the purpose of this discussion, it is important to recognize that
    EBCDIC and ASCII map characters of the basic character set to different code points and are
    therefore not compatible.
- [P2996R2: Reflection for C++26](http://wg21.link/p2996r2):
  - Daveed presented:
    - \[ Editor's note: Daveed's presentation slides are avilable
      [here](presentations/2024-04-24-p2996r2-presentation.pdf). \]
    - An overview of the proposed reflection syntax was provided.
    - There are three functions that reflect the names of entities at present, but more might be added.
    - There is only one function that consumes names as strings right now, but more might be added.
    - Names provided by some reflection interfaces must be consumable in the same form by other
      reflection interfaces.
    - The ability to write names to `std::cout` is required.
    - It is ok for the names to not be source-like; `std::meta::display_name_of()` can use a descriptive
      notation.
    - The translation model is Unicode based so names can be provided in Unicode encodings, but the
      standard library is missing support for text in `char8_t`.
    - Proposal sketch #1:
      - Provide names in both `char` and `char8_t` based storage and associated encodings.
      - Require names to round-trip.
    - Proposal sketch #2:
      - Provide names only in `char8_t` based storage and UTF-8; names naturally round-trip.
      - Make `std::cout` work with UTF-8 text in `char8_t`.
    - \[ Editor's note: Proposal sketch #3 in the linked slides was added after the meeting as
      inspired by ensuing discussion. \]
  - Jens asked if `name_of()` is proposed as a `consteval` function.
  - Daveed confirmed that it is.
  - Tom asked for clarification regarding the intended use cases for `name_of()`, `qualified_name_of()`,
    and `display_name_of()`.
  - Daveed replied that `name_of()` is intended to return an identifier or a canonical name such as
    `operator X` and that `qualified_name_of()` and `display_name_of()` are intended to return
    potentially localized descriptive text.
  - Andrei observed that programmers might want to pass a `data_member_options_t` object around and
    that the `optional<string_view>` `name` member is potentially problematic for lifetime reasons.
  - Daveed acknowledged that the data member type might need to be changed to an owning string type.
  - Corentin explained that conversion from an arbitrary encoding to Unicode might not roundtrip
    because characters like Å (U+212B ANGSTROM SIGN) and Å (U+00C5 LATIN CAPITAL LETTER A WITH RING ABOVE)
    are distinct in Unicode, but might not be distinct in the ordinary literal encoding.
  - \[ Editor's note: The Å (U+00C5 LATIN CAPITAL LETTER A WITH RING ABOVE), Å (U+212B ANGSTROM SIGN), 
    A (U+0041 LATIN CAPITAL LETTER A), and  ̊ (U+030A COMBINING RING ABOVE) characters are all individually
    permitted in Unicode identifiers. However, since C++ identifiers are required to be in Unicode
    normalization form C (NFC), only the first form (U+00C5) is permitted in a C++ identifier. The
    ordinary literal encoding is not restricted to NFC, so this character could be converted to one
    of the other forms and therefore fail to round-trip. This could result in a requirement for
    implementations to perform conversion to NFC when consuming names. See the "Singleton Exclusions"
    section of
    [UAX #15 (Unicode Normalization Forms)](https://unicode.org/reports/tr15). \]
  - Steve asked if there is a desire or requirement to be able to emit text containing names at compile-time.
  - Daveed responded negatively and stated that the `std::cout` requirement is intended as a debugging aid.
  - Corentin responded to Victor's earlier statements regarding lack of support for `char8_t` in the standard
    library and asserted that we should fix that.
  - Corentin expressed support for providing names in both `char` and `char8_t`.
  - Corentin stated that reflection is an important feature and that we shouldn't implement hacks just to
    workaround the missing support for `char8_t`.
  - Corentin insisted that improving support for `char8_t` is a tractable problem and that we have some time
    for improvements in C++26.
  - Victor opined that reflection should not be dependent on `std::string_view`.
  - Victor stated that it took a long time to properly specify `std::print()` and that we shouldn't implement
    hacks in iostreams just to make `std::cout` work with `char8_t` in the C++26 timeframe.
  - Victor explained that the model we are moving towards is one where the ordinary literal encoding is UTF-8.
  - Victor suggested that an identifier or name type could be provided instead of a string; this would enable
    writing formatters for it.
  - Eddie asked Corentin if there are round-trip normalization concerns and whether renormalization is required.
  - Corentin replied negatively and stated that there are characters that are duplicated in Unicode and do not
    normalize to each other.
  - Eddie replied that identifiers are required to be in NFC.
  - Tom stated that we are not going to be able to reach a conclusion on round-tripping and renormalization now
    and that we'll need to research and revisit.
  - Tom said he is not convinced that normalization is a significant issue.
  - Daveed asked what the deadline is for new library feature proposals for C++26.
  - Jens provided a link to
    [P1000R5 (C++ IS schedule)](https://wg21.link/p1000)
    and reported that the Wrocław meeting in November is the last meeting for core language features that require
    a response from LEWG and that the Hagenberg meeting in February is the last meeting to forward papers to
    CWG and LWG.
  - Tom expressed support for Victor's suggestion of a distinct formattable type for names and identifiers.
  - Tom agreed with Victor regarding optimizing for the case where UTF-8 is the ordinary literal encoding, but
    disagreed with the suggestion that `char` will ever imply UTF everywhere.
  - Tom expressed a preference for exposing names in both `char` and `char8_t` based storage.
  - Daveed described limitations of constant evaluation that make use of `std::string` problematic, but noted
    that implementations can provide views backed by data in a string literal pool.
  - Corentin noted that the encoding challenges remain the same if a unique type is used; a solution is still
    needed to enable printing of it.
  - Corentin acknowledged that an opaque type might confer other benefits.
  - Jens agreed with Tom that, while we might like for UTF-8 to take over everywhere, environments that rely
    on EBCDIC are likely to remain.
  - Jens asserted that we must take backward compatibility into account.
  - Jens observed that there are two levels of encoding:
    - At compile-time, data might or might not be UTF-8, but the encoding is known if a name is produced and
      consumed during constant evaluation.
    - At run-time, the encoding of the environment might be different and might require transcoding or some
      form of escaping to not lose data.
  - Jens noted that we explicitly decided not to interfere with the existing behavior of `std::cout` and
    introduced `std::print()` as a new interface.
  - Jens asked how programmers will produce new names based on reflected ones given that `std::format()` is
    not declared `constexpr`.
  - Jens expressed uncertainty regarding what locale means during constant evaluation.
  - Jens suggested that returning an opaque type might be useful, but is also not so different from returning
    `std::string_view` and providing additional library support.
  - Daveed stated that the addition of a distinct type creates some complexity but that it could be associated
    with statically allocated memory.
  - Daveed noted that the creation of lots of names could produce massive numbers of string literals if names
    are backed by string pools and stated there could be an advantage to the distinct type approach.
  - Eddie observed that an opaque type that converts to both `std::string_view` and `std::u8string_view` could
    result in ambiguous conversions for formatted printing.
  - Dan observed that an opaque type helps to make it clear to the user that they might want to perform some
    operations on it before printing it.
  - Corentin responded to Eddie's observation by stating that, as long as the opaque type doesn't require
    conversion in order to be printed, then there are no ambiguous conversion concerns.
  - Corentin observed that SG16 talks about EBCDIC a lot, but noted that Windows is not UTF-8 by default and
    that Shift-JIS is still the main encoding used in Japan.
  - Corentin agreed with Victor that it would be nice to have `char` be synonomous with UTF-8 but stated that
    isn't the world we live in.
  - Corentin noted that, when writing output to a terminal, we can't guarantee that an identifier can be
    accurately displayed due to encoding limitations, encoding conversion limitations, and fonts.
  - Corentin stated that `std::format()` and `std::print()` do a much better job than iostreams and that
    `std::print()` will print Unicode correctly on Windows; that can't be fixed for iostreams.
  - Corentin asked Daveed if non-transient memory allocation is still being pursued.
  - Daveed responded that it probably is not feasible to deliver in C++26.
  - Victor also responded to Eddie's observation by opining that he doesn't think implicit conversions from an
    opaque type would be an issue for `std::format()` but that he wasn't sure about iostreams.
  - Victor noted that writing `char8_t` to iostreams will be lossy or produce mojibake.
  - Victor stated that `constexpr` support for `std::format()` is frequently requested and asserted that we
    should prioritize that over adding new support for `char8_t`.
  - Victor reported that proposals for compile-time messages have expressed interest in `constexpr` support
    for `std::format()`.
  - Tom posted the following candidate polls in the chat:
    - Candidate poll 1: P2996R2: identifier names should be made available via `char`, `wchar_t`, `char8_`,
      `char16_t`, and `char32_t` consistent with `std::filesystem::path` and
      [\[fs.path.native.obs\]](https://eel.is/c++draft/fs.path.native.obs).
    - Candidate poll 2: P2996R2: identifier names returned by `name_of()` in `char`-based storage should be
      encoded in the ordinary literal encoding with non-representable characters rendering the call ill-formed.
    - Candidate poll 3: P2996R2: identifier names returned by `display_name_of()` in `char`-based storage
      should be encoded in the ordinary literal encoding with non-representable characters escaped as in
      [\[format.string.escaped\]](https://eel.is/c++draft/format.string.escaped).
    - Candidate poll 4: P2996R2: `char`-based identifier names accepted by `data_member_spec()`
      (via `data_member_options_t`) should be encoded in the ordinary literal encoding.
  - Corentin expressed concern about memory footprint if names are backed by string literals and made
    available in multiple encodings.
  - Daveed responded that the strings are only generated when you actually use them; Victor's opaque type
    would effectively have a handle to an internal representation backed by static storage.
  - Tom pointed out that conversions from the internal representation could then be performed at run-time.
  - Victor expressed curiosity about candidate poll 1.
  - Tom explained the thoughts that motivated that poll suggestion; `std::filesystem::path` provides a
    precedent for providing conversions to various encodings; if this poll has consensus, then there is no
    need to poll support for individual encodings; if not, we can.
  - Tom posted the following alternatives to candidate poll 1 in the chat:
    - Candidate poll 1.1: P2996R2: identifier names should be made available in `char`-based storage.
    - Candidate poll 1.2: P2996R2: identifier names should be made available in `char8_t`-based storage.
    - Candidate poll 1.3: P2996R2: identifier names should be made available in `char16_t`-based storage.
    - Candidate poll 1.4: P2996R2: identifier names should be made available in `char32_t`-based storage.
    - Candidate poll 1.5: P2996R2: identifier names should be made available in `wchar_t`-based storage.
  - Victor expressed support for candidate poll 2, noted that we didn't discuss it yet, but likes that it
    enables support for all possible identifiers in UTF-8 in `char`-based interfaces when the ordinary
    literal encoding is UTF-8.
  - Steve noted that there is the possibility of problems caused by translation units being compiled
    with different ordinary literal encodings.
  - Steve suggested that it might be useful to provide a library interface that can produce strings with
    UCN-like sequences substituted.
  - Steve noted that use of an opaque type would enable use with any of the range encoding libraries.
  - Daveed stated that the P2996 authors would be opposed to support for all five character types but
    that they are ok with support for `char` and `char8_t`.
  - Tom asked for clarification regarding opposition for support of the other character types.
  - Daveed responded that common storage can be used to back the same representation for `char` and
    `char8_t`, but that isn't the case for the other character types.
  - Corentin noted that `char16_t` and `char32_t` are also less efficient to store.
  - Corentin stated that he is not opposed to an opaque type as long as it can be printed as Unicode
    with good results.
  - Corentin asserted that we still need to make `char8_t` work in the standard library regardless.
  - Corentin expressed opposition to introduction of an escape mechanism that effectively introduces
    an additional encoding.
  - Corentin suggested that if we want to support `wchar_t`, `char16_t`, and `char32_t`, that we should
    provide a translation interface rather than duplicating interfaces throughout the standard library.
  - Daveed responded with "Amen, brother!"
  - Eddie stated that
    [P2728 (Unicode in the Library, Part 1: UTF Transcoding)](https://wg21.link/p2728)
    is fully constexpr and would provide support for conversion to UTF-16 in `char16_t` and UTF-32 in
    `char32_t`.
- Tom requested that Daveed make his presentation available for inclusion in the meeting summary.
- Daveed immediately obliged.
- Tom announced that the next meeting will be held May 8th and that we'll continue discussion of this
  paper then.
- Tom apologized to Corentin and lamented that this will once again delay further review of
  [P2626 (`charN_t` incremental adoption: Casting pointers of UTF character types)](https://wg21.link/p2626).


# April 10th, 2024

## Agenda
- [P2758R2: Emitting messages at compile time](https://wg21.link/p2758r2).

## Meeting summary
- Attendees:
  - Barry Revzin
  - Corentin Jabot
  - Fraser Gordon
  - Jens Maurer
  - Mark de Wever
  - Tom Honermann
  - Victor Zverovich
- Due to a scheduling conflict, Barry was delayed in joining the meeting and review of
  P2758R2 was thus delayed. The time was filled with informal chat of various items
  including but not limited to:
  - Progress on [P2873 (Remove Deprecated Locale Category Facets For Unicode from C++26)](https://wg21.link/p2873).
  - The need, or lack thereof, for `u8streampos`, `u16streampos`, and `u32streampos`.
  - The Unicode Text Terminal Working Group.
  - U+FDFD (ARABIC LIGATURE BISMILLAH AR-RAHMAN AR-RAHEEM) and other characters with
    very wide display widths.
  - The past Tokyo and future St. Louis meetings.
  - Locales, `std::format()`, and `char8_t` support.
  - The Unicode Message Formatting Working Group.
  - [ICU4X](https://docs.rs/icu/latest/icu).
- [P2758R2: Emitting messages at compile time](https://wg21.link/p2758r2):
  - Barry provided an introduction:
    - The goal is to allow programmers to produce more friendly diagnostics.
    - `static_assert` has limitations and clever hacks only go so far.
    - Producing errors is great, but there is value in being able to produce
      informational messages and warnings that can be elevated to errors.
    - `std::format()` is not declared `constexpr`, but probably could be.
    - The proposal is minimal and intended to provide infrastructure on which better
      interfaces can be built.
  - Victor posited that it would be useful to have a portable way to suppress a warning
    in a portable manner; a portable version of the `#pragma` directives that many
    implementations support today.
  - Victor stated that the paper needs updates to reflect the adoption of
    [P2741R3 (user-generated `static_assert` messages)](https://wg21.link/p2741r3).
  - Mark expressed support for the paper and commented that he recently asked Clang
    developers about such a feature.
  - Victor noted that clang-tidy allows a comment-based annotation to suppress diagnostics
    that emanate from specified source code lines.
  - Barry asked if such annotations would be expected to suppress diagnostics that would be
    produced from a specific call to one of these functions.
  - Victor replied affirmatively and stated that it would be difficult for his organization
    to enable these warnings otherwise without a way to suppress false positives.
  - Jens explained that clang-tidy annotations are written at the line where the diagnostic
    is issued from and that the annotation Victor is interested in would have to work
    differently.
  - Victor agreed and stated this suppression would be more complicated.
  - Tom suggested it would probably have to be an annotation that suppresses any indicated
    warnings that emanate from within the constant evaluation of the annotated source line.
  - Corentin opined that this paper doesn't need to address suppression of a diagnostic.
  - Corentin noted that display of a diagnostic is within the purview of the implementor.
  - Corentin asserted that, as long as there is a tag available, that implementors can
    provide a means to suppress it.
  - Tom replied that a tag is specified for `constexpr_warning_str()`, but not for the
    other cases.
  - Tom stated that, from an implementation stand point, he could see treating errors as
    discretionary errors that can be demoted to warnings.
  - Barry replied that production of an error is intended to halt constant evaluation.
  - Barry said that there are use cases for both fatal and discretionary errors, but that
    he doesn't really agree with motivation for the latter.
  - Victor expressed opposition to being able to demote an error to a warning.
  - Corentin observed that the wording needs to require that the message is provided in the
    ordinary literal encoding.
  - Corentin reported that wording examples can be found in the wording for `static_assert`.
  - \[ Editor's note: see [\[dcl.pre\]p12](http://eel.is/c++draft/dcl.pre#12). \]
  - Jens clarified that the elements of the `std::string_view` that holds the message will
    be considered code units of the ordinary literal encoding.
  - Barry reported having located the wording and indicated he can copy it.
  - Jens asked if `constexpr_error_str()` is equivalent to `static_assert(false, "message")`.
  - Barry replied that it is very similar.
  - Corentin explained that the evaluation is performed at a different time and potentially
    for a different number of occurrences; a `static_assert` will be evaluated once at
    translation or template instantiation time where as `constexpr_error_str()` may be
    evaluated multiple times during constant evaluation.
  - Corentin asked what the expectations for a call to `constexpr_error_str()` are; for
    example, whether a diagnostic with different color highlighting would be produced.
  - Corentin asserted that it should be possible to suppress each message kind; they should
    all have a tag for this reason.
  - Corentin asked if escape sequences may appear in the message strings.
  - Barry asked what `static_assert` does and was informed it is implementation-defined.
  - \[ Editor's note: examples with hilariously predictable implementation divergence can
    be seen at https://godbolt.org/z/xasvnMPre. \]
  - Victor agreed with the suggestion to add a tag to `constexpr_print_str()`.
  - Victor asked how ill-formed tags are handled.
  - Tom replied that tags should be restricted to the basic literal character set.
  - Corentin stated that implementations should escape non-printable characters and
    ill-formed code unit sequences in the diagnostics they produce.
  - Tom asked for confirmation that text in the message that looks like a
    *universal-character-name* would not be treated as such.
  - Corentin confirmed.
  - Jens observed that the paper proposes a library facility but that he is uncertain that
    it is.
  - Jens stated that [\[intro.compliance.general\]](http://eel.is/c++draft/intro.compliance.general)
    would need an update.
  - Jens noted that section was updated to address the requirement for the `#warning` and
    `#error` directives to produce a diagnostic message.
  - Jens asked why it would be necessary to state that the program is ill-formed rather than
    that the expression is not a core constant expression.
  - Jens explained that ill-formed means a diagnostic must be produced, but an implementation
    can do what it wants otherwise.
  - Jens asked if specifying these as ill-formed requires an implementation to refuse to
    translate the program and noted that this is currently only required for `#error`.
  - Tom asked Barry if the intent is to match `#error`.
  - Barry expressed uncertainty.
  - Jens advised reading [\[intro.compliance.general\]](http://eel.is/c++draft/intro.compliance.general).
  - Corentin stated that the characters permitted in tags needs to be clarified; quotes,
    semicolon, and other characters that have special meaning in command line shells should
    be prohibited.
  - Tom pondered whether this should really be a core language facility.
  - Tom suggested the tag should be required to be an unevaluated string to facilitate audits.
  - Victor expressed a preference for the tag being a string literal.
  - Corentin observed that requiring a string literal would require a core language feature.
  - Barry replied that he would eventually like to expose this functionality with more
    `std::format()` like capabilities but doing so wouldn't be possible if this is specified
    as a language feature; at least not without expression aliases or some other way to pass
    a tag through a library interface.
  - Tom stated he would like to review the proposal in SG16 again to review limitations on
    tags and wording for encoding requirements.
  - Jens indicated that CWG will need to review the paper as well and stated he has a gut
    feeling that there is something missing.
  - Jens noted that erroneous behavior is increasing motivation for producing something akin
    to diagnostics at run-time.
  - Jens suggested that LEWG might not have a lot of input since the library interface would
    just forward calls to a builtin function; that builtin function will require input from
    core implementors.
- Tom announced that the next meeting will be on 2024-04-24 and that he would work with
  authors to get papers scheduled with more advance notice this time.


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
