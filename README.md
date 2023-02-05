# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, February 22nd, 2023, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20230222T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- [D2773R0: Considerations for Unicode algorithms](https://wg21.link/d2773r0).


# Past SG16 meetings
- [January 25th, 2023](#january-25th-2023)
- [January 11th, 2023](#january-11th-2023)
- [Meetings held in 2022](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
    broadly applied.
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
  - Hubert pointed out a category error in the proposed wording change for the `codecvt`
    facets; "code point" is used where "code unit" would be more appropriate.
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
