# SG16 meetings

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.


# Future SG16 meetings

The next SG16 meeting is scheduled for
Wednesday, February 9th, 2022, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20220209T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- [P2498R1: Forward compatibility of text_encoding with additional encoding registries](https://wg21.link/p2498r1)
  - Continue prior discussion and poll.
- [P2513R0: char8_t Compatibility and Portability Fixes](https://wg21.link/p2513r0)
  - Initial review.


# Past SG16 meetings
- [January 12th, 2022](#january-12th-2022)
- [Meetings held in 2021](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2021.md)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
