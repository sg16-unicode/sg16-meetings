# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, February 1st, 2023, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20230201T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- [D2749R0: Down with ”character”](https://isocpp.org/files/papers/D2749R0.pdf)


# Past SG16 meetings
- [January 11th, 2023](#january-11th-2023)
- [Meetings held in 2022](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2022.md)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
