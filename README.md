# SG16 Meeting Summaries

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.

The next SG16 meeting is scheduled for
Wednesday, January 27th, 2021, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20210127T193000&p1=1440&p2=tz_pst&p3=tz_mst&p4=tz_cst&p5=tz_est&p6=tz_cet)).
The draft agenda is:
- Presentation and discussion with Jonathan Müller regarding his
  [lexy parser combinator library](https://github.com/foonathan/lexy)
  ([Tutorial](https://foonathan.net/lexy/tutorial.html), [Reference](https://foonathan.net/lexy/reference.html)),
  and the text and Unicode related challenged he faced, how he solved them, and what C++ standard
  language or library features he would have benefitted from.
- [WG14 N2620: Restartable and Non-Restartable Functions for Efficient Character Conversions | r4](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2620.htm)

Summaries of past meetings:
- [January 13th, 2021](#january-13th-2021)
- [Meetings held in 2020](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2020.md)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
