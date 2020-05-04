# SG16 Meeting Summaries

SG16 meetings are typically held on Wednesdays from 19:30-21:00 UTC on the 2nd and 4th
weeks of each month, but scheduling conflicts or other time pressures sometimes force
alternative scheduling.  Meeting invitations are sent to the mailing list and prior
attendees.  To request an invitation, please contact tom@honermann.net.

The next SG16 meeting is scheduled for
Wednesday, May 13th 2020, from 19:30-21:00 UTC
([timezone conversion](https://www.timeanddate.com/worldclock/converter.html?iso=20200513T193000&p1=1440)).
The draft agenda is:
- D1949R4: C++ Identifier Syntax using Unicode Standard Annex 31 
  - Review updates since the April 22nd review.
- Review the queue for C++23:
  - How are we doing relative to the directives in [P1238R1](https://wg21.link/p1238r1)?
  - What is our vision for C++23?  (What would be our elevator pitch?)
  - What features are we on track to deliver?
  - What features need additional prioritization?

Summaries of past meetings:
- [April 8th, 2020](#april-8th-2020)
- [March 25th, 2020](#march-25th-2020)
- [March 11th, 2020](#march-11th-2020)
- [February 26th, 2020](#february-26th-2020)
- [February 5th, 2020](#february-5th-2020)
- [January 22nd, 2020](#january-22nd-2020)
- [January 8th, 2020](#january-8th-2020)
- [Meetings held in 2019](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2019.md)
- [Meetings held in 2018](https://github.com/sg16-unicode/sg16-meetings/blob/master/README-2018.md)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


# April 8th, 2020

## Agenda:
- Discuss whether to hold telecons at the current UTC time year round and discontinue observing day light
  savings time.
- Discuss and poll to adopt the proposed SG16 operational plan:
  - https://github.com/sg16-unicode/sg16/blob/78d6b4052ed561a6f5d384d6b5a4c7f30ac523c6/OperatingProcedures.md
- Discuss whether to switch from Bluejeans to Zoom for future meetings.
  - WG21 is encouraging (but not requiring) all SGs to use Zoom for consistency and for polling features.
- Unicode Message Format Working Group liaison report.
- D1949R3: C++ Identifier Syntax using Unicode Standard Annex 31
  - https://isocpp.org/files/papers/D1949R3.html
  - New draft revision review.


## Meeting summary:
- Attendees:
  - David Wendt
  - Hubert Tong
  - Jens Maurer
  - Mark Zeren
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- Discussion of telecons and daylight savings time:
  - Tom introduced the topic.
    - We've historically observed daylight savings time as observed in the EST5EDT4 timezone.
    - Adjustments to meeting times due to timezone changes are a cause for confusion.
    - Proposing to keep telecon times at the same UTC time year round.
    - Any concerns?
  - Everyone tried to work out what local telecon times would be when timezone adjustments next occur.
    As might be expected, there was some initial confusion.
  - Jens cleared up the confusion; when timezone changes are made in the fall, telecons will start one hour
    earlier for locales that observe daylight savings time.
  - Mark indicated that the earlier time might make for some tight scheduled for him, but probably ok.
  - Tom stated that we'll try this and can always adjust if necessary.
- Discussion and polls to adopt the proposed SG16 operational plan:
  - Tom introduced the topic.
    - As discussed during our last telecon, changes happening in WG21 in response to the COVID-19 crisis will
      require that we begin polling papers during telecons.
    - Tom circulated a draft document with proposed procedures for SG16 telecons and meetings:
      - https://github.com/sg16-unicode/sg16/blob/78d6b4052ed561a6f5d384d6b5a4c7f30ac523c6/OperatingProcedures.md
  - PBrett asked for clarification regarding forwarding of papers and whether a requested change means that we'll
    need to wait for an updated revision and re-poll.
  - Tom responded, no; we can approve with feedback and audit the next revision to ensure that our feedback was
    addressed.  Such auditing may require naming a delegate to follow up in some cases.
  - Steve noted that the isocpp.org paper management system allows for P-numbered papers that have not yet appeared
    in a mailing to be updated.  Such updates should be avoided for P-numbered papers that have been shared prior
    to appearance in a mailing.
  - Jens stated that we should strive to avoid revision inflation but that it is probably beneficial to have a
    P-numbered revision when polling to forwarding a paper to an upstream subgroup.
  - **Poll: Adopt the proposed document as SG16's operating procedures**
    - No objection to unanimous consent.
 - Discussion of whether to switch from Bluejeans to Zoom for future meetings.
  - Tom introduced the topic:
    - WG21 leadership has suggested that all subgroups and study groups adopt Zoom for their telecons for
      consistency, familiarity, and polling features.
    - SG16 has been using Bluejeans successfully for the last two years.
    - We haven't encountered many technical issues with Bluejeans.
    - Bluejeans doesn't provide polling features.  Now that we'll need to be polling in telecons, such features
      could prove helpful.
    - Should we switch to Zoom?
  - PBrett noted that there have been reports of serious privacy and security issues with Zoom.
  - Tom responded that Herb has provided guidance on how to configure Zoom to address some of these issues.
  - PBrett added that there are also concerns regarding how Zoom makes money.
  - Tom responded that the ISO funds accounts for chairs that need them.  In my case, my ISO registration is
    via my work email address and I have a Zoom account funded by my employer.
  - PBrett noted that WebEx doesn't monetize usage monitoring; Zoom seems to have a we-can-do-whatever-we-want
    approach to usage monitoring.
  - Jens responded that eavesdropping concerns are probably not a strong concern for the ISO.  And SG16 is a
    public group.
  - Tom agreed.
  - Jens stated that he has been having technical issues with Bluejeans; it fails to populate the participant
    list and chat.  No such issues have been experienced with the Zoom client.
  - Tom asked if there were any strong objections to switching to Zoom.
  - PBrett responded that, if the question was phrased as, would I stop attending SG16 telecons if we switched
    to Zoom, then the answer is no.
  - Tom restated the question to just ask for preferences.
  - Zach responded that he has no preference; both Bluejeans and Zoom work for him.
  - Mark responded likewise.
  - Steve responded that he has both installed and noted that the moderation features are better in Zoom.  If
    SG16 were a larger group, we would need such features, but Bluejeans works fine for the size of our group.
  - Zach stated that the LEWG telecon hosted with Zoom this week worked pretty well.  There were some challenges
    getting everything on the screen; chat was pretty active, the raise hand feature was being used and that
    required the participant list.  He had to tile windows to make everything fit.  The hand raise feature was
    nice.  The LEWG chair struggled a little bit keeping tabs on chat, hands, screen.
  - Zach added that he wasn't sure the raise hands feature is needed for groups of our size.
  - PBrett reported having had a similar experience; it can be challenging to use Zoom without using multiple
    monitors.
  - Mark noted additional issues with the Zoom UI layout; widgets may obscure the main window.
  - PBrett stated that we should have more motivation for switching.
  - Jens reminded the group that Bluejeans is not working correctly for him.
  - Tom suggested that we wait a month or so to evaluate how things go with other groups and then revisit.
- Unicode Message Format Working Group liaison report.
  - PBrett reported that, like everyone, they have been impacted by the COVID-19 pandemic, but they have worked
    out a system for rotating chairs for meetings.
  - PBrett added that, if anything interesting happens, that he will notify Tom to put an item on the agenda;
    there is no reason to have a liaison report at each of our meetings at this time.
- [D1949R3: C++ Identifier Syntax using Unicode Standard Annex 31](https://isocpp.org/files/papers/D1949R3.html)
  - Steve introduced changes since [P1949R2](https://wg21.link/p1949r2):
    - The most significant changes relate to when normalization occurs.
    - There is implementation divergence with regard to preprocessor identifiers.
    - gcc requires that preprocessor identifiers meet the general identifier requirements, but Clang and Visual
      C++ do not.  gcc rejects the following code because `\u0300` is not a valid initial character for an
      identifier.
      ```
       #define accent(x) x##\u0300
       constexpr int accent(A) = 2;
       constexpr int gv2 = A\u0300;
       static_assert(gv2 == 2, "whatever");
      ```
  - PBrett expressed a preference for gcc's behavior.
  - Tom stated that the operands to the `##` operator are not identifiers.
  - Jens agreed; they are preprocessing tokens.
  - Steve responded that the grammar for preprocessing tokens includes identifier.
  - Hubert agreed; the grammar for preprocessing tokens is stated in terms of identifiers.
  - PBrett: provided a link to the grammar for `preprocessing-token` showing identifier.
    - http://eel.is/c++draft/lex.pptoken#nt:preprocessing-token
  - PBrett asked if it would be reasonable to modify the preprocessing grammar to require adherence to
    [UAX#31](https://unicode.org/reports/tr31).
  - Hubert responded that the question previously raised on the mailing list was, after token pasting, is it
    required to check that a resulting preprocessor token that is ostensibly an identifier is in NFC and,
    if not, is the result undefined-behavior (UB); in other words, is a non-NFC identifier a valid preprocessing
    token?
  - \[ Editor's note: that question was raised in the email thread that started at
    https://lists.isocpp.org/sg16/2020/02/1122.php. \]
  - Zach stated that, in general, yes, checking is required because combining two NFC sequences doesn't
    necessarily produce an NFC sequence.  If we're going to diagnose ill-formedness, we need to check for that.
    Otherwise we end up with ill-formed-no-diagnostic-required (IFNDR) and that should be avoided.
  - PBrett mentioned that the draft paper doesn't have an example of pasting two NFC tokens that produce a
    non-NFC result.
  - Steve responded that the example in the paper is such an example.
  - \[ Editor's note: The example in the paper is such an example, though not necessarily the kind of example
    that Zach and Peter had in mind.  Including an example from the
    [UAX#15 section on concatenation of normalized strings](https://unicode.org/reports/tr15/#Concatenation)
    might be helpful. \]
  - Jens noted that the second operand is not a valid UAX#31 identifier.
  - Steve acknowledged that, but noted that a digit is not an identifier, but can be concatentated to a valid
    identifier to produce a different one.
  - PBrett asked if a bare combining character can be a valid preprocessing token; whether, in C++20, `\u0300`
    is a valid preprocessor token.
  - Jens responded, no; [[lex.name]p1 table 3](http://eel.is/c++draft/lex.name#tab:lex.name.disallowed)
    lists U+0300 in the list of combining characters that are not permitted to start an identifier.
  - PBrett summarized; Clang and Visual C++ are non-conformant because they allow `\u0300` as a preprocessing
      token, but gcc handles this correctly.  This is the status quo.
  - Jens stated that the lexer permits much undefined behavior, so we need to be careful.
  - PBrett agreed and added that, for cases of existing UB, we can change behavior.
  - Jens opined that the example ought to be ill-formed, but that there are oddities in the lexer and
    preprocessor specifications.  For example there is wording that if the result of a concatenated token is
    not a valid preprocessor token, then the result is UB; would like this example to be ill-formed.
  - PBrett asked if this issue should be reviewed by SG12.
  - Jens responded, no; so long as we're not removing allowances for UB or adding new UB, SG12 doesn't need
    to be involved.  The example appears to be ill-formed.
  - Tom asked for clarification; Clang and Visual C++ are missing a diagnostic?
  - Jens responded, yes.
  - Zach stated that this suggests that the NFC check should be performed later in translation as opposed to
    checking that each operand of the `##` operator is in NFC.
  - Jens disagreed with that approach.
  - Steve observed that there are interesting interactions with header units since they externalize
    preprocessor macros and require comparisons of them.
  - Tom opined that the issue applies equally for headers since different header files can have different
    source encodings.
  - Jens suggested that implementations could convert to NFC as part of translation phase 1.
  - Hubert reported having investigated implementation divergence and found that there seems to be confusion
    regarding how max munch works for identifiers.
    [preprocessing-token](http://eel.is/c++draft/lex.pptoken#nt:preprocessing-token)
    has a rule to match non-white-space characters that don't otherwise fit in the grammar.  Max munch fails
    to consume a `\u0300`, so `\u0300` is a valid preprocessing token.
  - Jens noted the change in perspective; so the example is well-formed and gcc is wrong to reject it.
  - PBrett concluded that, if `\u0300` is a non-white-space preprocessing token and is therefore a valid
    operand for the `##` operator, then that means that the earliest we can diagnose non-NFC identifiers is
    after token pasting.
  - Steve summarized that the diagnostic options are translation phases 4 and 7.
  - Hubert stated that there is a difference between writing `\u0300` and the actual U+0300 character
    in the physical file.
  - \[ Editor's note: Hubert clarified after the call that he was speaking to a need to consider the user
    expectations in both cases.  The conversation got away before this point could be clarified. \]
  - Jens responded that, in translation phase 1, all extended characters are converted to
    _universal-character-name_; bare character don't exist afterwards.
  - Tom noted that differences are observeable in raw literals.
  - Steve acknowledged, but noted that isn't relevant for identifiers.
  - Zach stated that Hubert's point is important; macros need to be NFC checked.  But we want to make things
    easy for implementors.  In the example, if we wanted to check the result of the contatenation in
    translation phase 7, is there a simple rule to just check for macro names?  Or a simple rule to check all
    identifiers in translation phases 4 and 7?  It may be worth asking implementors for opinions.
  - PBrett stated that the check should be performed at the point that something becomes an identifier.  That
    solves the problem for `#define` since it requires an identifier.
  - Hubert responded that he is ok with the lexing portion of that.  The question is, when you try forming a
    preprocessing token and it is supposed to be an identifier, do you need to check again?  If not, then
    further checking is needed when converting preprocessing tokens to tokens.  Deferral would be preferred
    in order to avoid interaction with the UB that Jens pointed out regarding token pasting producing invalid
    preprocessing tokens.
  - Zach summarized; we do need to check that preprocessing tokens used as identifiers are NFC.  And we need
    to check that the result of token pasting is a NFC preprocessing token if used as an identifier.  And we
    need to check identifiers at translation phase 7.
  - Jens replied that the wording we have is already what we want; it doesn't differentiate between preprocessor
    or translation phase 7 identifiers.  The result of token pasting is just a preprocessing token, so there is
    no need to perform an NFC check since it isn't an identifier yet.
  - Hubert clarfied his understanding of Zach's description; Jens stated that the result of token concatenation
    is just a preprocessing token, but it can be any of the preprocessing token possibilities.  If it matches
    an identifier, than we can check if it is NFC.
  - PBrett stated that, in
    [[cpp.concat]p3](http://eel.is/c++draft/cpp.concat#3),
    if the result is not a preprocessing token, then the behavior is UB.  So we don't have to check for NFC
    because it is already UB.
  - Hubert responded that the question is then whether we care for this use case.
  - Jens noted that caring for this use case is more expensive.
  - PBrett stated that the case he is concerned about is where token pasting produces a name that is then used
    to define a macro; a diagnostic should be issued in such cases.
  - Jens responded that UB has already occurred at that point, so a diagnostic doesn't apply.
  - Jens noted that the only use cases we have for producing non-NFC preprocessing tokens are for use with the
    stringize operator
  - Hubert added, or for discarding tokens.  The stringize case isn't too compelling because regular string
    concatenation suffices.
  - Hubert brought up another concern that had been previously raised; *preprocessing-token* includes
    *pp-number*.  For user defined literals (UDLs), if we only check the identifier grammar, then we only check
    at phase 7 when these tokens become UDL suffixes.
  - Steve observed that this is where the discussion regarding use of currency characters in UDLs comes into
    play.
  - Jens stated that the current rules for
    [[lex.name]](http://eel.is/c++draft/lex.name)
    are reasonable and good enough since they restrict what identifiers can be.
  - Zach asked if the implication is that we need to check for NFC at translation phases 4 and 7.
  - Jens responded, yes.
  - PBrett added that the example is then ill-formed because substituting the accent in the first `constexpr`
    line produces UB, and the second `constexpr` is ill-formed because `A\u0300` is not in NFC.
  - Steve stated that he will try to update the paper to clarify this.
  - \[ Editor's note: Several minutes of discussion were not recorded because the editor was having a hard
    time following it. \]
  - Jens stated that we may need to introduce a *pp-identifier* preprocessing token kind to replace use of
    *identifier*; the NFC check would then happen when converting a *pp-identifier* to an *identifier*.
  - PBrett expressed support for this direction as it avoids the UB and difficulties with lexing the source
    code.
  - Jens asked Hubert if he is content with the introduction of a new *pp-identifier* term.
  - Hubert responded that he is.
  - Steve summarized the direction.  A new *pp-identifier* will be introduced that matches the preprocessor
    notion of an identifier and for which an NFC check will be performed at the point that it is converted to
    an identifier.  This avoids potentially needing to perform incremental NFC analysis during lexing.
  - PBrett asked if the new *pp-identifier* could require conformance with UAC#31, but just not be in NFC.
  - Zach replied, yes.
  - PBrett asked for confirmation that a *pp-identifier* will never need to be compared.
  - Jens replied, correct.
  - Hubert added that this retains the case where a lone `\u0300` is neither a *pp-identifier* nor an
    *identifier*; it is one of those lone non-white-space preprocessing tokens.
  - Jens confirmed; right, because a *pp-identifier* must start with an `XIDStart` character.
  - Steve asked for confirmation that *pp-identifier* will appear in the grammar roughly like *pp-number* does.
  - Jens confirmed, yes.
  - Tom asked Steve if additional feedback is needed.
  - Hubert asked if there is any further question about how to apply the UAX#31 conformance statmeents.
  - Steve replied that he would welcome recommendations on how to present that.  At present, the paper documents
    a profile for conformance with R1, and an NFC requirement for conform to R4.  The remaining requirements are
    intentionally unmet or not applicable.
  - Jens replied that the phrasing doesn't seem right.  The intent of UAX#31 is to require documentation stating
    what requirements apply and why or why not; the paper is lacking some introductory text.
  - Steve acknowledged, something along the lines "profile is, ..., and the others are not applicable".
  - Jens requested that the paper be updated to use complete sentences.
  - Steve agreed to do so.
  - Tom noted that, in section 9.3.1, there appears to be a formatting issue.
  - Steve acknowledged and stated he would correct it.
  - Jens volunteered to follow up with suggested wording on the mailing list.
  - \[ Editor's note: Jens did so; the email thread is available at https://lists.isocpp.org/sg16/2020/04/1235.php. \]
  - \[ Editor's note: After the meeting, Hubert sent a message to the mailing list arguing that attempted concatenation
    of `\u0300` concatenates only the `\` character because the lexer observes `\`, `u`, `0`, `3`, `0`, `0`, not the
    single *universal-character-name*.  The result is UB because the concatenation doesn't produce a valid preprocessing
    token.  The email thread is available at
    https://lists.isocpp.org/sg16/2020/04/1229.php. \]
- Tom reminded the group that WG21 is moving to monthly mailings and that the next mailing deadline is April 15th.
- Tom confirmed that the next meeting will be on April 22nd.


# March 25th, 2020

## Draft agenda:
- Follow up on our meeting with the Unicode Message Format Working Group
  - Draft volunteers to function as liaisons between our groups.
- Plans to acquire implementation experience for:
  - P1949R1: C++ Identifier Syntax using Unicode Standard Annex 31
  - P2071R0: Named universal character escapes
- D2124R0: std::regex should be deprecated starting in C++23
  - https://htmlpreview.github.io/?https://github.com/dascandy/fiets/blob/master/html/D2124R0_Deprecate_std_regex.html
  - Initial SG16 review.

## Meeting summary:
- Attendees:
  - David Wendt
  - Hubert Tong
  - JeanHeyd Meneide
  - Jens Maurer
  - Lyberta
  - Mark Zeren
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- Summer plans in lieu of the Varna meeting.
  - Tom introduced the topic.
    - With the cancellation of the Varna meeting, the library and language subgroups are going to start
      hosting telecons.  This raises two concerns:
      - We'll face increased competition for our respective telecon time budgets.
      - We traditionally have not conducted polls during telecons, but we'll need to start doing so if
         we are to get papers forwarded to the subgroups for review during their telecons.
    - Tom also mentioned that mailings will now occur monthly.
  - Tom asked if anyone had concerns about continuing to attend SG16 telecons due to potentially having
    to choose between SG16 or other subgroup telecons.  No concerns were reported.
  - PBrett asked how polling will be conducted.
  - Tom explained his current thoughts; we can adopt a tentatively ready approach and affirm decisions at
    the next face-to-face meeting.
  - PBrett suggested providing some method of async polling for those that are unable to attend telecons
    due to time zone or other challenges.
  - Tom replied that it is important that those voting are present for discussion leading up to a poll.
  - Mark stated that the current schedule is ok, but that we could consider setting aside two time slots
    favorable to different time zones and swap between them.
  - PBrett suggested that having a tentatively ready queue provides an opportunity for a two tier
    approach to decision making.
  - JeanHeyd suggested adopting the LWG approach of monday emails preceding a meeting; that would invite
    more participation from those that cannot attend a telecon.
  - Tom expressed support for that suggestion.
  - Mark opined that polling should not occur without an author present as we'd be unlikely to converge on
    consensus.
  - Mark suggested that, perhaps, we could record discussion.
  - Tom replied that he could follow up with Herb regarding that possibility.
  - PBrett suggested that we can publicize tentatively ready decisions, request feedback, and revisit based
    on new information.
  - Hubert stated that meeting minutes are useful, but that he would object to sharing recordings since
    this group is open.  Trust between committee members is built over time and we have to trust people to
    understand mis-statements.
  - Tom asked Hubert that, if Herb were to approve some kind of recording, if this is something he could
    potentially be open to.
  - Hubert responded with maybe, but only if a demonstrable need is recognized that can't be addressed in
    another way.
  - Tom agreed with that criteria; recordings are sensitive, we can revisit this if need arises.
  - Steve stated that more frequent mailings will help give us notice of poor responses to previous decisions.
    Writing a short paper with new information should not be a high bar.
  - Hubert replied that mailings are a heavy weight way of providing feedback.  During face to face meetings,
    we accept and address feedback in real-time; sometimes including in plenary.
  - Tom agreed, but added that writing a paper is always an option.
  - Steve expressed a preference that there be a relatively high bar for reopening discussions.
  - Tom agreed and provided an example case where discussion was reopened.  SG16 approved
    [P1885R0](http://wg21.link/p1885r0) in Belfast, discussion afterwards resulted in the paper being
    revisited in Prague where
    [P1885R2](http://wg21.link/p1885r2) was approved.
  - Hubert stated that, since SG16 is a study group, objections can always be raised with EWG, LEWG, or
    in plenary.
  - Tom returned to the mechanics of polling.  Bluejeans doesn't have polling features built in.  We could
    switch to Zoom so that we could make use of its "raise hand" feature.  Otherwise, we'll have to figure
    out another way to conduct polls.
  - Tom stated that he would document a process to use and we can evaluate consensus on it at an upcoming
    telecon.
- Follow up on the prior meeting with the Unicode Message Format Working Group
  - Tom asked if there were any volunteers to function as a liaison between our groups.
  - PBrett volunteered to do so.
- Plans to acquire implementation experience for:
  - [P1949: C++ Identifier Syntax using Unicode Standard Annex 31](https://wg21.link/p1949):
    - Tom asked Steve if he had any thoughts on implementation.
    - Steve responded that he had not strongly considered it, but that he didn't think it should be too
      difficult, at least for gcc where warnings are already emitted.
    - Steve added that the immediate priority is to free up time to answer new questions raised since the
      Prague meeting.
    - Tom suggested that it may suffice to audit the warnings that gcc provides and, if they closely match
      the proposal, to consider that sufficient implementation experience.
    - Steve stated that the complicated part is the filter for what characters are allowed.
    - Tom suggested another approach might be to analyze the gcc tests and add more as necessary to cover
      edge cases.
    - Steve responded that there is a table for allowed characters already and that he could probably
      evaluate that prior to the New York meeting.
  - [P2071: Named universal character escapes](https://wg21.link/p2071):
    - Tom stated that he has not started on an implementation yet; he is currently focused on getting
      implementations of `mbrtoc8` and `c8rtomb` ready to submit to glibc.
    - Tom added that he might start an implementation after that, but if anyone else wants to work on it,
      that would be great.
    - JeanHeyd asked if an implementation was needed given the prior work that Corentin did.
    - Tom responded that, technically no, but having an implementation available helps with consensus;
      it means we're standardizing an existing practice.
    - PBrett agreed; an implementation increases confidence in a design.
    - Hubert stated that the implementation impact for C vs C++ may be much higher; WG14 may object.
    - Jens noted that WG14 will want two implementations, but that acceptance in C++ counts as one.
    - JeanHeyd asked if anyone was aware of a simple C compiler that would be good for experimentation.
    - PBrett replied that
      [TCC](https://bellard.org/tcc)
      might be a good choice, but that it appears to be unmaintained.
    - Jens noted that the implementation doesn't require a modern C compiler.
    - JeanHeyd suggested that
      [SDCC](http://sdcc.sourceforge.net)
      may be another option.
    - Steve stated that he would be surprised if there was significant code size impact as opposed to
      data size.
    - Jens responded that it doesn't much matter; growth is growth and potentially impactful for
      constrained use cases.  Even 300K could be significant.
    - Steve provided an example impact; the compiler may no longer fit on a floppy disk.
    - Jens suggested it may make sense for this feature to be optional for C.
    - Jens noted that Richard Smith had asked about allowing `\N` in identifiers and suggested they
      should be allowed there.
    - Tom responded that it is on his todo list to address that in a revision.  We'll then want to discuss
      that option at a future telecon.
    - Jens added that, from a core wording perspective, it would be simpler to specify these as
      `universal-character-name`; allowed uses could still be differentiated.
- [D2124R0: std::regex should be deprecated starting in C++23](https://htmlpreview.github.io/?https://github.com/dascandy/fiets/blob/master/html/D2124R0_Deprecate_std_regex.html):
  - PBindels introduced the draft:
    - `std::regex` doesn't work with variable length encodings.
    - Performance is poor to the point it is faster to fork and exec a process to do the regex in another
      language.
    - We can't fix the problems due to ABI concerns.
    - There is no plan to remove; just to deprecate until a suitable replacement is provided, as was done
      for `std::auto_ptr`.
    - We don't want to spend more committee time on `std::regex`.
  - PBrett added that he has drafted additional changes that discuss what a new regex implementation
    could provide and had planned to target those changes to the Varna pre-meeting mailing.
  - Hubert noted that we now have monthly meetings.
  - Tom noted that the next mailing deadline is now April 15th.
  - Hubert stated that the relatively large set of supported RE grammars is a problem; we should avoid
    POSIX ones that require implementation-defined behavior.
  - PBrett noted that this concern is mentioned in the paper, but needs more detail.
  - PBrett also noted that the paper would benefit from a reference to
    [UTS#18](http://www.unicode.org/reports/tr18/tr18-19.html).
  - Tom suggested that, perhaps, a separate paper listing requirements for a `std::regex` replacement
    would be useful.
  - JeanHeyd responded that is useful to have that information in this paper to guide authors who might
    like to propose a replacement.
  - PBrett suggested that a requirements paper could be provided later.
  - PBindels opined that direction for a replacement should be documented in a new paper.
  - Steve suggested that inability to handle Unicode is reason enough to deprecate `std::regex`.
  - PBrett noted that `std::regex` can be used for UTF-8 if the regular expression author is very careful
    and text is normalized.
  - PBrett also noted that `std::regex` can be used on strings that are not text.
  - PBindels aded a comparison; just like `std::string` can be used for non-text.
  - Mark gently steered the group back to the topic of deprecation.
  - PBrett asked if anyone that regularly attends LEWG or LWG has additional guidance.
  - Hubert responded that including relevant LWG issues would be helpful.
  - Mark responded that it would be useful to include links to relevant papers that discussed issues with
    `std::regex` in the past and provided a list of such papers going back to 2005:
    - [P0169R0: regex and Unicode character types](https://wg21.link/p0169r0)
    - [P0014R1: Proposal to add the multiline option to std::regex for its ECMAScript engine](https://wg21.link/p0014r1)
    - [P0757R0: regex_iterator should be iterable](https://wg21.link/p0757r0)
    - [P1149R0: Constexpr regex](https://wg21.link/p1149r0)
    - [P1844R1: Enhancement of regex](https://wg21.link/p1844r1)
  - Mark added that references to closed LWG issues would also be useful.
  - Hubert agreed; the existence of significant issues may be sufficient motivation for removal.
  - PBrett noted that relevant LWG issues can be found by searching for "regex" on the
    [LWG active issues list](https://cplusplus.github.io/LWG/lwg-active.html).
  - Hubert provided a link to such an issue:
    https://cplusplus.github.io/LWG/issue2546.
  - Jens noted that `export` was removed, so there is precedent for removal without replacement.
  - Jens suggested that someone follow up with Peter Dimov since he was involved with `boost::regex` and
    the introduction of `std::regex` in C++11.
  - PBrett suggested that, perhaps, the paper should include an option for removal.
  - Jens cautioned against doing so.
  - PBindels opined that there is plenty to gain by deprecation, but that noting the possibility of removal
    is an option.
  - Jens added another prior deprecation example; `<strstream>` deprecation was not particularly difficult
    despite there still not being a full replacement for all use cases.
  - JeanHeyd commented that
    [P0448](https://wg21.link/p0448)
    provides a span that is a full replacement for `<strstream>`, so removal may be possible relatively soon.
  - Jens expressed a desire for an analysis of how a replacement could be evolved without running into the
    same ABI issues.
  - PBindels agreed with that desire, but opined that should be done in a different paper.
  - Tom provided a list of suggestions:
    - Drop all uses of "very", "much", "bad", "many", "entirely", "large", etc...
    - In 3.1.1, the example is good, but confusing.  It may be worth emphasizing that use of braces denotes
      a set of individual code units (not characters!) to be matched.  It may be helpful to explain the intent
      and the observed behavior separately.
    - In 3.1.2, it may be worth mentioning explicitly that Unicode has multiple ways to represent some characters.
    - In 3.1.3, it isn't stated what character is used as a space character in the example string.
    - Explicitly list the signatures of interfaces in `std:regex_traits` that are problematic.  Having the
      signatures available makes some of the issues very clear.  For example, what does it mean to translate a
      standalone code unit?
      - `CharT std::regex_traits<CharT>::translate(CharT c) const`
    - Explain why a replacement for `std::regex_traits` wouldn't suffice to address significant problems; the
      interfaces provided by `std::regex` are not problematic by themselves.
    - Reference failed papers.
  - PBrett stated that people reading the paper should be aware of normalization.
  - Jens responded that some won't and that they will form an opinion and vote on the paper regardless.
  - Hubert asserted that the paper does not need to focus on details of Unicode; an additional problem is that
    `std::regex` doesn't differentiate between the encoding of the pattern and the subject.
  - Hubert provided a link to a
    [gcc bug report](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=81200)
    demonstrating that WG21 didn't understand the `std::regex` functionality when they standardized it.
  - PBrett asked if anyone has major concerns about deprecating `std::regex`.
  - Mark responded that, when his organization moved to C++11, `std:regex` was the only new feature programmers
    were told not to use.
  - PBindels responded that he once tried to use `std::regex` to do an alternation on a few patterns and
    performance made it clear this wasn't going to work out.
  - PBrett responded that his organization usees `std::regex` in production, in limited cases, with known
    Latin1 text.
  - Hubert responded that he has come across cases where `std::regex` matching behavior is sensitive to
    compiler language dialect options.
  - Steve responded that deprecating it would make code reviews easier since all uses of it could be rejected
    on the basis that deprecated features shouldn't be used.
  - PBrett noted that `-Wno-deprecated` is ubiquitous in their code base.
- Tom confirmed that the next meeting will be Wednesday, April 8th.


# March 11th, 2020

## Draft agenda:
- Meet and greet for SG16 and the new Unicode Message Format Working Group (MFWG)
  - Individual introductions.
  - A brief history of each group.
  - Current efforts and plans for each group.
  - General discussion of message formatting.
  - Discussion of how we might work together to mutual benefit.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - Elango Cheran
  - JeanHeyd Meneide
  - Jens Maurer
  - Lyberta
  - Mark Zeren
  - Markus Scherer
  - Mihai Nita
  - Peter Brett
  - Romulo Cintra
  - Shane Carr
  - Steve Downey
  - Steven R. Loomis
  - Tom Honermann
- The meeting started off with a round of introductions.
- Tom provided a brief history of SG16 and changes championed for C++20.
  - Tom mentioned the work that went into `std::format` via
    [P1868](https://wg21.link/p1868)
    in order to produce correctly aligned text for monospaced presentation formats.
  - SLoomis stated that character display width is an important problem that is deserving of its own project.
  - PBrett asked if there were plans to enable `std::format` to handle text translation.
  - Tom stated that our current direction is captured in
    [P1238: SG16 Unicode Direction](https://wg21.link/p1238).
  - Markus provided some references for work being done in ICU to address C++20 incompatibilities:
    - https://github.com/unicode-org/icu/pull/979 (a pull request providing minimal changes to allow ICU to
      compile with C++20; basically a bunch of added `reinterpret_cast` casts for uses of `u8` string literals
      to continue using them as arrays of `const char`)
    - https://unicode-org.atlassian.net/browse/ICU-20984 (a proposal for a more principled change that avoids
      the need for many of the `reinterpret_cast` casts)
- Members of the MFWG provided an introduction and current status summary.
  - Romulo gave a general introduction:
    - The initial impetus for the group was the observed demand for client side message formatting and a lack
      of browser features needed to effectively enable it two years ago.
    - There are currently a number of libraries available that cumulatively account for millions of weekly
      downloads:
      - NPM trends:<br/>
        https://www.npmtrends.com/i18n-vs-i18next-vs-messageformat-vs-polyglot-vs-intl-messageformat-vs-fluent-vs-fbt-vs-format-message
      - Overview and analysis of various libraries:<br/>
        https://docs.google.com/presentation/d/1RujNFCq3gH9TUEKDB_uFdKWNG1A1j2_NBCdnTmnEqv0/edit#slide=id.g4af2a8f783_0_210
    - A recommendation was provided to join
      [ECMA TC39](https://tc39.es)
      and contribute to the group chaired by Shane Carr that is responsible for
      [ECMA-402](https://tc39.es/ecma402).
    - Discussed the idea of a new group with Shane focused on message formatting last year.
    - Shane brought lots of new people, got them talking, and worked with the Unicode consortium to create
      the new group.
  - Shane continued:
    - Message formatting was already recognized as an item to focus on for ECMAScript.
    - The problem isn't unique to ECMAScript; it is a big problem space.
    - A big question is, how much of the localization stack is to be covered?
    - The Unicode consortium formed the new group in January, 2020 as a Unicode subcommittee.
    - Romulo was named chair of the new group.
  - Mihai continued with an overview of the scope and design direction:
    - Think of message formatting like a locale aware implementation of `printf`.
    - But one that can handle plurals.
    - The idea is to separate the string from the localization data model.
    - For `printf`, the format is a sequence of parts, each of which contributes raw text or a placeholder
      with formatting data.
    - Proper internationalization requires a more complicated data model.
    - There are three major pieces needed:
      - The data model.
      - A serialization form.
      - A message store.
    - A goal is to provide a standard data model that can be mapped to various localization interchange
      formats; not to produce yet another message format.
  - Romulo wrapped up:
    - Have had 5 meetings so far.
    - Are still in the design and requirements discovery phase.
    - Are still working on design processes to ensure efficient operation.
- General discussion ensued:
  - PBrett asked about challenges faced where ICU is currently deficient.
  - Mihai responded that he has a document he can share:
    - A major challenge is that ICU has the only widely deployed formatting implementation.
    - There are some ECMAScript libraries.
    - ICU does not support inflections well.  For example, in English, one might say "the book", but in other
      languages, instead of inserting "the", the word "book" is changed.
    - ICU also doesn't handle combinations of plurals well.  For example, a statement like
      "I bought 5 books and 2 posters" requires a complext nested switch format due to combinatorial explosion
      and the syntax is clunky.
  - Markus provided an example of plural complexities.  Arabic has six different plural forms and more may be
    added to say "exactly one" or for "none".  Two instances of pluralization in a message can lead to dozens
    of possibilities.
  - Shane stated that the ICU message format is the defacto standard right now, but there is no specification
    for it.
  - Elango responded that there are different defacto standards across different language ecosystems.  Data
    literals in ECMAScript provide flexibility.  Many programmers roll their own solutions and this results in
    inconsistency.  The goal is to create a specification to encourage normalizing behavior across disparate
    implementations.
  - Jens commented on the complication of language bindings and extensive behavioral options.
  - Mihai agreed; message formatters congregate lots of functionality.
  - Mihai mentioned his prototype of a formatter that uses
    [Protocol Buffers](https://developers.google.com/protocol-buffers)
    to translate syntax between different formatters.  A comprehensive core data model is essential to be able
    to do so.
  - Elango stated that the general facility has just one output for message formatting; date formatting is
    provided by a plugin.
  - Mihai opined that it would be useful to have support for ranges as well.
  - PBrett stated that the ability to stream output is important for C++ and that this covers several
    orthogonal areas of concern:
    - The data model.
    - The abstract representation.
    - The concrete representation.
    - The sinks that messages go to.
    - Authoring of the translation database.
  - PBrett added that the above raises an important question for the MFWG to address: what are you trying to
    solve and what is the abstraction?
  - Jens observed that there appears to be little overlap between SG16 and the MFWG; when the MFWG specification
    is complete, SG16 will consume it.
  - Tom provided some of his perceptions of the benefits of working together.  First, we ensure that the output
    of the MFWG works for purposes that we envision.  Second, we get informed about infrastructure requirements
    that may require new facilities to meet in order to adopt the MFGW output.  For example, enhancements to
    locale support.
  - Jens noted that, for `std::format` to be able to provide message formatting, it would have to be able to
    access the message catalog.
  - PBrett observed that adding that complexty to `std::format` may be challenging; it may be difficult to
    separate dependencies.
  - Markus noted that the mechanism used to pluralize a message is distinct from the source of the
    pluralization data.
  - Tom asked for clarification; pluralization is more of an algorithm than a lookup?
  - Markus responded that the way ICU has worked for the last 25 years is to parcel out strings or states, and
    then combine them according to specific rules.
  - Jens stated that WG21 has shied away from localization isseus because the C++ story is so poor; serious work
    is needed here.
  - Mihai explained that, in the data model the MFWG is working on, a place holder is a cross reference to
    another string.  If the mapping is generic, then a generic binding can be used, but loading can be customized.
  - Jens expressed caution; we're wary of costs for features that are not used.  Paying such costs is fine when
    needed, but should not pose overhead when not being used.
  - Tom asked if the design can avoid such costs when such features aren't used.
  - Jens responded that that isn't a fair question for a data model.  A more appropriate question would be what
    the impact is to the tables used for pluralization data.
  - Mihai responded that pluralization is not a large data set.  The question is more relevant for inflection.
    Some languages are regular, but others are quite unregular and sorting requires a lot of data.
  - Mihai added that message formatting brings algorithms together, but the information needed to guide the
    formatter is distinct.
  - Jens asked if support for pluralization and inflections is in scope.
  - Elango responded that pluralization is, but that inflections may not be; this is work in progress.
  - Shane further responded that support for inflections is in scope as part of the effort to make a standard
    interface that enables plugging in extensions.
  - Shane added that the focus is to provide a solution that does not require an implementor to implement
    everything.  Implementors should be able to provide only the subset of features needed for a particular
    deployment.
  - Markus elaborated on ICU's pluralization support.  ICU doesn't attempt to determine the plural form for
    any word in any language.  Rather, it identifies ranges of numbers for 100+ languages where things must
    be done differently.  Translators are then required to author different messages.  Translation tools are
    designed to prompt translators for each translation form that is needed.  The pluralization form is then
    used for message selection.
  - Jens observed that the ICU design is exactly what causes the combinatorial explosion.
  - Mihai noted that the goal is to simplify the syntax, not to reduce the number of translations required.
  - PBrett asked how translators can provide translations conveniently in those cases.
  - Mihai responded that translation tools can do fuzzy matches and offer suggestions.
  - PBrett asked about the MFWG road map; is it a goal to produce a Unicode TS?
  - SLoomis responded, yes.
  - PBrett asked if there is a tentative time line.
  - Romulo responded that they are still in the design phase, so there is no clear road map right now.
  - Mihai added that they have been focused on collecting use cases and feature requests; the rate of additions
    is decreasing.
  - Mihai elaborated that getting consensus on a data model being a goal took some time.
  - Corentin stated that it would be great to support a common syntax in C++ and ECMAScript so that translators
    have consistent experiences.  For `std::format`, Python's syntax was adopted thereby enabling developers to
    switch easily.
  - Mihai responded that a common format is anticipated for translators, but that does not necessarily correspond
    to what a programmer writes.
  - PBrett hypothesized that a C++ implementation could have a `constexpr` solution that uses C++, but that can be
    translated to some other syntax.
  - PBrett added that we need to think of how to deprecate and replace `std::message`.
  - Jens noted that understanding the data model is important to envision how the various parts fit together and
    asked if a draft data model exists.
  - Mihai responded that there are currently two documents on the data model.  Elango provided a document that
    argues for a data model, and Mihai provided one that maps a model to one of several implementations and
    discusses how it can be modified to add features.  There is no final draft.
    - Elango's doc:<br/>
      https://docs.google.com/presentation/d/1fBfawWNfniCFox-PltCMyVtbcVwYGYkk78GUbWzas5o/edit#slide=id.g8254abe56c_0_0
    - Mihai's doc:<br/>
      https://docs.google.com/presentation/d/1dyW29SlqjPRZVScobqEXjnP29fhbqMkCfgxPOWj3Tnw <br/>
      (currently requires permission to access)
  - Corentin asked if there is a reference syntax available and noted that none of us our linguistics experts.
  - Mihai responded that a syntax for ECMAScript is anticipated along with a language independent form in
    a structured data format like JSON.
  - Markus suggested that SG16 should consider whether it wants to do something in this area or whether this
    functionality should be left to non-standard libraries.
  - Tom responded that the design direction would allow for a standard implementation, but doesn't restrict the
    use of non-standard implementations.
  - Jens suggested that it would be good to appoint someone from SG16 to be a liazon to attend MFWG meetings and
    keep tabs on things.
  - Shane agreed with that approach; it would help to maximize utility to consumers.
  - Jens commented that what the committee needs is a standard that we can defer to that was produced by
    experts since, if left to our own devices, we'd probably produce a poor design.  Dependence on such a standard
    needs to be figured into our road map.
  - PBrett asked about the
    [MFWG mailing list](https://groups.google.com/a/chromium.org/forum/#!forum/message-format-wg)
    and
    [MFWG github site](https://github.com/unicode-org/message-format-wg);
    neither looks particularly active.
  - SLoomis replied that most activity is happening in github issues.
  - Shane added that there is a
    [Slack Unicode channel](https://unicode-org.slack.com).
  - PBrett suggested that SG16 should discuss more, reflect, and contemplate how we want to move forward.
  - PBrett asked what SG16 can do to help facilitate work by the MFWG.
  - Mihai responded; try not to invent something new.
  - Corentin noted that we need to re-design our locale facilities before we can take on message localization
    and that we need to implement facilities matching those in
    [ECMA-402](https://www.ecma-international.org/publications/standards/Ecma-402.htm).
  - Tom returned to the subject of requirements and asked if there are cases where multiple locales need to be
    consulted for the same message.
  - Markus responded that mixtures of locales appear in cases where a placeholder refers to, for example, a name.
  - Steve stated that such scenarios are common with currency; it is common, for example, to use USD outside of
    US locales.
  - Mihai added that this also happens with dates.  Dates may be presented in multiple formats.
  - Steve added that use of a locale independent date format might be consistently used regardless of locale.
  - Mihai stated that these scenarios should be possible to address, but not optimized for.
  - Tom asked if the notion of locale independent message formatting is relevant to the MFWG.
  - Markus replied that there are good use cases for locale independent formatting; logging for example.
  - Steve added that JSON output should not be localized.


# February 26th, 2020

## Draft agenda:
- Post-Prague follow up.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - David Wendt
  - JeanHeyd Meneide
  - Jens Maurer
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- [P2071R0: Named universal character escapes](https://wg21.link/p2071r0):
  - Tom provided a status update.  Waiting on a response to add an additional co-author.  Working on
    updates to address EWG feedback.  Wording will need to be re-done for P2029.  On track for review
    by EWG again in Varna; will hopefully be made tentatively ready then.
- [P2029R0: Proposed resolution for core issues 411, 1656, and 2333; numeric and universal character
  escapes in character and string literals](https://wg21.link/p2029r0):
  - Tom stated an update will be submitted for the Prague post-meeting mailing with the intent that it
    be discussed at the next core issues processing meeting.
  - Jens stated that the next core issues processing meetings are planned for March 23rd and April 20th.
- Renaming universal-character-name:
  - Corentin brought up an
    [email](https://lists.isocpp.org/sg16/2020/02/1152.php)
    that he had sent to the SG16 and core mailing lists regarding a desire to rename
    *universal-character-name* to *universal-character-codepoint* since no names are actually used in these
    productions (code point values are).
  - Jens stated that it can be difficult to get consensus on a change via the core reflector; such a change
    needs core buy in.
  - Corentin asked how he should proceed.
  - Jens replied that the issue could be discussed in the next core issues processing meeting.  The process
    to get an item on the agenda for those meetings is to get it on the CWG wiki page for Varna, but the
    Varna wiki hasn't been populated yet.  Jens said that he would poke at someone to get the wiki
    structure in place.
  - Tom asked for more details about this process and whether it is really ok to get changes like this
    initiated without a paper or core issue.
  - Jens replied that a paper is best to ensure proper attention and progress.
  - Jens added that an updated core issues list hasn't been published for some time now.
  - \[ Editor's note: The last published core issues list is revision 100 and has a date of 2018-04-11. \]
  - Jens asked if *universal-character-codepoint* is what we want and suggested *unicode-code-point* as an
    alternative.
  - Tom expressed support for Jen's suggested alternative.
  - Zach expressed a preference for something more specific since this production is for one particular way
    to express a code point.
  - Jens responded that this is a grammar term and asked if the grammar term for P2071 should also be named
    *something-codepoint* because it designates one.
  - Corentin expressed support for that sentiment.
  - Zach asked if the implication is that both `\uNNNN` and `\N{...}` would fall under *unicode-code-point*.
  - Jens replied that they are distinct because `\uNNNN` can be generated from characters not in the basic
    source character set that appear in identifiers in the source code.  `\N{...}` likely gets effectively
    quickly translated to `\uNNNN`.
  - Jens opined that the name isn't super important since this is just a grammar term and people should
    expect to have to look up exactly what it means.
  - Zach stated that *unicode-code-point* seems like the right choice then.
  - Tom asked about using the names *unicode-code-point* for `\uNNNN` and *unicode-code-point-name* for
    `\N{...}`.
  - Corentin suggested that, in P2071, *named-escape-sequence* be renamed to *unicode-named-escape-sequence*
    for the `\N{...}` case.
  - Jens asked if `\N{...}` is allowed in identifiers.
  - Tom replied that it is not.
  - Jens noted that being a significant difference from `\uNNNN`.
  - Tom expressed some hesitation with regard to adding "unicode" to *named-escape-sequence* since, in theory,
    we could support non-Unicode names like D does.
  - \[ Editor's note: D uses HTML 5 entity names for its named character escapes. \]
  - Jens expressed a preference for *named-escape-sequence* as it is simple and matches nearby grammar terms
    like *octal-escape-sequence* and *hexadecimal-escape-sequence*.
  - PBindels asked about just using *code-point* for `\uNNNN`.
  - Corentin stated that Unicode is needed in this case.
  - Jens agreed noting that the syntax is specific to Unicode code points.
  - Jens asked to confirm that there is no requirement for an implementation to have a list of acceptable or
    unacceptable code points for `\uNNNN` other than for surrogate code points and the range of code point
    values (0-0x1FFFF).
  - Tom confirmed; implementations are not required or allowed to map an unrecognized code point to a
    replacement code point.
  - Jens acknowledged and added that programs that specify an unassigned code point will not be rejected either.
  - Jens asked if naming this *unicode-code-point* implies a valid character.
  - Steve suggested that, perhaps, the right name is *unicode-scalar-value*.
  - Everyone expressed profound distate for the scalar value term.
  - Jens suggested that P2071 be updated to add editorial direction to rename *universal-character-name* to
    *unicode-code-point*.
  - Tom agreed to do so.
  - \[ Editor's note: concurrent with this meeting, a prominent core member replied to Corentin's email and
    requested that we retain the *unversal-character-name* name since it has been in use in C99 and C++23 for
    20 years now and is referenced in existing literature.  Due to there being opposition to the name change,
    Tom then decided not to pursue the editorial rename via P2071.  Anyone wishing to pursue the rename
    should therefore write a separate paper. \]
- [P0592R4: To boldly suggest an overall plan for C++23](https://wg21.link/p0592r4):
  - Tom introduced the topic.  At plenary in Prague, Peter Bindels asked what the process would be to amend
    P0592.  Tom was approached by several committee members arguing that Unicode support should be added as
    a priority for C++23.  Tom is concerned about spending committee time addressing a problem that might not
    exist and is worried that attempting to add our favorite topic to the priority list might inspire other
    groups to argue for adding theirs potentially consuming significant amounts of committee time.
  - Jens asked what papers aren't making progress.
  - Tom replied that, right now, SG16 is the bottleneck for SG16 work.  The EWG and LEWG chairs have been
    quite supportive of making progress on Unicode matters.
  - PBindels stated that he raised this in plenary partially to encourage people to write papers; we want to
    ensure that EWG and LEWG are prepared for additional work that builds on the ground work we've been laying.
  - Steve suggested a potential bad scenario.  Two years from now, there could be a glut of pattern matching
    papers consuming lots of committee time just as C++23 is wrapping up.
  - Tom agreed that is a possible concern, but added that he doesn't think we can preempt it.
  - PBindels stated that P0592 is meant as a general guideline and that we need a plan for ourselves so that
    we know what we are aiming for in C++23.
  - PBrett agreed and added that knowing what we want, when we want it by, and who is responsible would be
    helpful.
  - Tom responded that the SG16 github site has issues tracking the SG16 work currently in motion as well as other
    tentative ideas.  Many of those issues are marked as "help wanted" and are available for volunteers to take
    on.
  - Tom added that [P1238](https://wg21.link/p1238) is due for an update.  That paper could be updated to list
    items that we want help with.  Perhaps we need to do more outreach to enlist additional help.  We could post
    help wanted tweets or ask more people to get involved when giving talks.
- [P1949R1: C++ Identifier Syntax using Unicode Standard Annex 31](https://wg21.link/p1949r1):
  - Tom summarized the current status; Steve has been preparing a revision following EWG review in Prague.
  - Steve stated that the paper is ready for the post-meeting mailing.
  - Tom stated that we lost the tentatively ready status in EWG for this paper following
    [additional email discussion](https://lists.isocpp.org/sg16/2020/02/1122.php)
    that raised concerns about possible undefined behavior in conjunction with token pasting.
  - Tom asked if the paper needs to address token syntax as well as identifier syntax.
  - Corentin replied that NFC checking should happen after preprocessing.
  - Tom asked if the grammar for identifiers is relevant for tokens.
  - Jens replied that *preprocessing-token* is distinct and that they get converted into identifiers, keywords,
    etc... at a particular translation phase.
  - Jens added that this occurs in translation phase 7 per
    [[lex.phases]p1.7](http://eel.is/c++draft/lex.phases#1.7) and
    [[lex.token]p1](http://eel.is/c++draft/lex.token#1).
    Core language wording should be added here to state that an identifier shall be in NFC form.
  - \[ Editor's note: In the draft wording, this is added to
    [[lex.name]](http://eel.is/c++draft/lex.name). \]
  - Steve asked if this is a "shall" or "must" situation.
  - Jens replied that "shall" is correct because a diagnostic is required and that "must" is a forbidden term
    in normative wording.
  - Tom mentioned that Peter Bindels has drafted a paper arguing for P1949 to be designated as a DR for C++20.
  - Jens stated that the DR process would be to get P1949 adopted for C++23, and then get a plenary straw poll
    to apply it as a DR against C++20.
  - Steve agreed to add content to the paper arguing for treating the matter as a DR.
  - PBindels told Steve to take whatever content he wanted from his DR draft and that he will abandon it.
    - [Peter's draft](https://github.com/dascandy/fiets/blob/master/papers/DxxxxR0_P1949_as_DR.fiets)
  - Jens suggested putting content directly in both the paper's front matter and at the beginning of the
    core wording that this be considered a DR.
  - Jens added that to ensure this is highlighted in core discussion.
  - Tom asked if there would then be two core motions.  One to accept the paper for C++23 and another to
    accept it as a DR for C++20.
  - Jens replied that it could be one motion: "adopt for C++23 and consider as a DR for C++20"
- [P1844R1: Enhancement of regex](https://wg21.link/p1844r1):
  - Tom summarized the Prague outcome.  We declined to forward this paper on and Peter Bindels has authored a
    draft paper to deprecate `std::regex`.
  - Tom aplogized for not yet reviewing Peter's deprecation paper.
  - PBindels stated he is waiting for review feedback from a select group of reviewers before sharing the draft
    more widely.
  - PBindels summarized the paper; it includes rationale for why programmers shouldn't use `std::regex`,
    performance numbers, ABI issues, votes in Prague, etc...
  - PBindels added that he would like to add more details on why the Visual C++ implementation is presumably
    so heavily impacted by ABI concerns.
  - Tom replied that the Visual C++ implementation exposes the entire state machine in template instantiations,
    so no changes can be made that affect the state machine.
  - Corentin suggested additional content stating that the design is overly complicated because it supports
    so many regex languages and that the requirement to do so impacts performance.
- [P1885R1: Naming Text Encodings to Demystify Them](https://wg21.link/p1885r1):
  - Tom suggested adding a list of encodings that are supported by ICU, iconv, Windows, etc..., but that are
    not present in the IANA database.
  - Corentin replied that he would try to do so.
  - Tom suggested that we try to register an encoding to see how burdensome doing so is to assuage fears about
    support for unrepresented encodings.
  - Corentin replied that he didn't think that would be a good use of our time.
  - PBrett added that doing so would be an abuse of process; the IANA registration process should only be used
    to register encodings for which there is a demonstrable need.
  - Tom acknowledged and agreed.
  - Tom suggested adding additional use cases to the paper to make it more evident to LEWG(I) how this functionality
    is expected to be used.
  - Tom added that such use cases should include intended future direction as well; e.g., interaction with
    [P1629: Standard Text Encoding](https://wg21.link/p1629).
  - Corentin agreed to do so.
  - JeanHeyd stated that he would look into prototyping integration between P1885 and P1629 and making it available
    on godbolt.
- [P1953R0: Unicode Identifiers And Reflection](https://wg21.link/p1953r0):
  - Tom expressed uncertainty as to what the next steps are.
  - Corentin stated that we need to get P1949 accepted first.  We can then revisit reflection and provide our
    recommendations to SG7.
  - Corentin added that we do need to keep on top of what SG7 is targeting for C++23.
- [P1040R5: std::embed](https://wg21.link/p1040r5):
  - Tom summarized the Prague outcome.  EWG expressed support for a file/directory handle `#depend` based
    solution.  That solves SG16 concerns; unless there is still a need to support paths that are relative to a
    handle at translation phase 7.
  - JeanHeyd stated that there are lots of issues with the VFS/node/handle approach.  But regardless, the SG16
    recommendation to use `char8_t` and UTF-8 resolves any SG16 related concerns.
- Tom stated that the next meeting will be March 11th and that we'll be meeting with the new Unicode Message
  Format Working Group.


# February 5th, 2020

## Draft agenda:
- Preparations for Prague.
- P2020R0: Locales, Encodings and Unicode
  - https://wg21.link/p2020r0
  - General discussion, corrections, suggestions, etc...
- P1629R0: Standard Text Encoding
  - https://wg21.link/p1629r0
  - Status update from JeanHeyd.

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - JeanHeyd Meneide
  - Jens Maurer
  - Lyberta
  - Peter Bindels
  - Peter Brett
  - Steve Downey
  - Tom Honermann
- Preparations for Prague.
  - PeterBr asked if it would be possible to attend the SG16 meeting in Prague remotely.
  - Jens provided some background:
    - Historically, remote attendance has not been allowed for a variety of reasons including but not limited to:
      - voting concerns
      - confidientiality concerns
      - attendance by people not familiar with our processes
    - SG and WG chairs have facilitated remote attendance on occasion for paper authors or well known experts.
    - For Prague, the Corona virus outbreak has prompted an exception for this meeting for paper authors.
    - SG chairs can choose to facilitate remote attendance subject to technology support.
  - PeterBr stated that the UK national body is considering making a request to enable remote access for people
    facing attendance challenges due to issues like VISA access and child care responsibilities.
  - Tom indicated that a member of the UK national body had reached out to him to ask how SG16 conducts our telecons.
  - Jens stated that the number of meeting attendees is raising logistial and hosting challenges.
  - Jens added that hotel wifi may not suffice for video conferencing.
  - Tom asked if Jens could provide audio gear that SG16 could use to facilitate remote attendance.
  - Jens confirmed he could.
  - Tom confirmed that a best effort approach will be made to facilitate remote attendance via BlueJeans.
  - Tom asked everyone to review the tentative schedule
    - http://wiki.edg.com/bin/view/Wg21prague/SG16
  - Jens suggested removing the Wednesday afternoon time slots since we don't have a room reserved for that time.
  - Tom agreed to do so.  \[Editor's note: and did so.\]
- Tom announced that the newly formed Message Formatting Unicode Working Group has been invited to attend the SG16
  meeting planned for March 11th.
  - https://github.com/unicode-org/message-format-wg
- P2020R0: Locales, Encodings and Unicode
  - https://wg21.link/p2020r0
  - Corentin introduces:
    - The paper chould be updated to include additional motivation for support of localization in the standard
      library.  However, since locale support is already present in the standard library, there is a desire not
      to distract from other topics and attempt to motivate unnecessarily.
    - The intent of the paper is to provide guidance and establish direction.
    - The existing locale support in the standard library is deficient, but in use regardless.  We could seek to
      deprecate it in favor of new facilities, though actually marking these interfaces `[[deprecated]]` could
      be problematic for some projects due to compiler warnings.
    - A primary point in this paper is that character encodings and locales are distinct concerns, though they
      have been historically conflated, particularly in POSIX.
    - High quality locale support depends on Unicode algorithms.
    - Attempting to provide locale support for non-UTF encodings is not realistic.
    - Whether a character is an uppercase or lowercase letter is not locale dependent.  However, case conversion
      is locale dependent.
    - The existing character classification functions are deficient since they operate on code units as opposed
      to sequences of code units or code points.
    - New locale facilities must be Unicode based.  For support of legacy encodings, conversion to Unicode and
      back will suffice.
    - Iostreams and locale are closely tied and operate on individual code units.  Proper localization cannot
      be provided using code unit based operations.
    - Linux and macOS deployments nearly exclusively use a UTF-8 locale.  At program startup, the program
      locale is set to "C".  Setting it to "C" is desirable; programs should opt-in to localization behavior.
      However, setting it to "C" also has the effect of changing the encoding and that is not desirable.
  - PeterBr stated that support for multiple encodings is not required for locale support.
  - Corentin agreed with a caveat; that is true for Unicode encodings, but when not using Unicode encodings,
    switching locales requires switching encodings.
  - Steve stated that, for one of their internal facilities, encoding is important for understanding what is
    provided by the locale library since the library provides `char` based interfaces and the localization data
    is encoding dependent.  It would be possible to retranslate all existing messages, but would be a large
    undertaking and getting localization wrong is expensive.  We need to enable bridges to the past.
  - PeterBr noted that we can't expect UTF-8 locale support on Windows; it will be UTF-16.
  - Corentin responded stating that is ok so long as it is Unicode since conversion to UTF-8 doesn't lose data.
  - Steve remarked that it is impressive how much locale related code works by accident.
  - Corentin supplied a list of operations affected by locale: case mapping, collation, search.  Search was
    surprising; it depends on locale because matching base characters is desired for some locales, but not for
    others.  The break algorithms are also locale dependent.
  - Corentin added that, thanks to Han unification, text rendering is locale dependent.
  - Jens observed that section 4 omits some items; number formatting for example.
  - PeterBr stated it would be helpful to have some Japanese contributors in SG16 to answer questions about
    formatting in their locales.
  - Corentin opined that it is best to just follow Unicode; it specifies how to handle locales.
  - Corentin added that, in some locales, multiple numeric formats may be used.  For example, in India.
  - PeterBr asked if the character classification functions could we deprecated if replacements were made
    available.
  - Corentin replied that they tend to be used in cases where programmers explicitly expect ASCII.
  - Jens stated that we all likely agree that the current character classification functions are defficient
    and that new facilities are required in order to deprecate them.
  - PeterBr asked how likely implementors are to be willing to ship a Unicode DB.
  - Corentin suggested that discussion of that be postponed to discussion of
    [P1628 -  Unicode character properties](https://wg21.link/p1628r0).
  - Jens objected to the idea of defaulting the program's startup encoding to UTF-8 if the environment
    specifies a UTF-8 encoding.  The "C" locale only supports the basic execution character set, e.g., ASCII.
    Programs that want to support extended characters should call `setlocale(..., "")` at program startup to
    opt-in.
  - Corentin stated that the choice C made to default the locale to "C" was a good choice for formatting
    facilities; many programs aren't intended to produce locale dependent formatting.  But encoding is different.
  - Steve stated that the as-if rule is leaned on here as implementations don't actually call
    `setlocale(..., "C")` during startup; adding a call to `setlocale(..., "")` would be a major change.
  - Tom clarified that Corentin's intent is only to adopt the encoding from the environment locale on program
    startup, not the locale formatting settings.  The proposal states that if, for example, the locale specified
    an encoding of UTF-8, then the as-if call on program startup would be something like
    `setlocale(LC_ALL, "C.UTF-8")`.
  - Corentin acknowledged that the way C and C++ are tied is a valid concern and that implementors depend on the
    underlying OS for locale support.
  - Jens expressed skepticism regarding the ability to change the program startup behavior, suggested that a
    new interface to retrieve the environment specified encoding be provided, and that `setlocale` be left alone.
  - Tom agreed that new functionality doesn't have to follow current behaviors.
  - Jens continued; new functionality can be provided that is independent of `setlocale`.
  - Jens opined that "C.UTF-8" doesn't make sense.
  - Tom stated that Python made a change to assume UTF-8 for the "C" locale and that the Python
    [PEP-538: Coercing the legacy C locale to a UTF-8 based locale](https://www.python.org/dev/peps/pep-0538) and
    [PEP-540: Add a new UTF-8 Mode](https://www.python.org/dev/peps/pep-0540)
    documents are informative for motivation.
  - PeterBr asked if use of the "C" locale implies use of the encoding of the execution character set.
  - Jens replied that, effectively, yes, but wording could make that more clear.
  - Tom stated his goal for this paper in Prague; to poll a subset of the possible future directions listed in
    section 6 to establish priorities for them; we can then identify tasks and papers to write.
  - Jens expressed a desire for a road map for the future before moving forward with deprecation.
  - PeterBr agreed and stated that a desire for a road map underscored the need for good motivation.
  - Corentin stated that we need to identify all of the current implicit and explicit locale dependencies.
  - PeterBr suggested incremental improvements may be made by adding overloads with explicit locale parameters.
  - Tom suggested that we spend an evening in Prague going through the paper in more detail with the intent to
    improve presentation and fill in gaps.
- P1629R0: Standard Text Encoding
  - https://wg21.link/p1629r0
  - JeanHeyd introduced:
    - [N2440](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2440.pdf) and
      [P1629](https://wg21.link/p1629) are intended to provide text decoding, encoding, and transcoding interfaces.
    - These replace `wstring_convert` and friends.
    - UTF-8 is difficult to enforce in `char` because non-UTF-8 data arrives in `char` based strings.
    - C provides few useful interfaces in this area.
    - WG14 approved parts of N2440 and an implementation is available in a standalone library.
    - Plans to submit implementations of N2440 to glibc and musl libc are pending.
    - P1629 provides extensible encoding objects.
    - There is an implementation of P1629 that provides encoding, decoding, transcoding, validation, and code point
      counting services.
  - Corentin asked what the motivation is for contributing new interfaces to C.
  - JeanHeyd responded that it makes sense to do so and that WG14 has already approved direction to add the mbs to
    UTF conversion variants.
  - Tom expressed his motivation for contributing to C; doing so reduces friction between the languages.
  - PeterBr asked if the implementation of N2440 uses SIMD instructions.
  - JeanHeyd replied that it does not yet, partially because the musl maintainers will want straight C implementations.
  - Jens asked why the single-character interfaces are not proposed.
  - JeanHeyd replied that only the restartable variants are being proposed.
  - Jens stated that WG14 will consider a WG21 approved proposal to qualify as implementation experience.
  - PeterBr asked about `replacement_code_unit` and how a replacement character that requires multiple code units
    would be specified; it seems like the replacement character should be provided as a string.
  - Tom expressed confusion about the existence of `replacement_code_unit` as he expected a replacement code point
    to be specified.
  - \[Editor's note: Tom later started an email thread on the SG16 mailing list regarding this:
    https://lists.isocpp.org/sg16/2020/02/1101.php. \]
  - JeanHeyd replied that a replacement code point is preferred and that the replacement code unit is a fall back.
  - Corentin stated that he didn't think `replacement_code_unit` is needed at all.
  - JeanHeyd replied that it is used to distinguish between errors happening in different encode/decode directions.
  - Steve suggested that, perhaps, better names are needed to communicate their intent.
  - JeanHeyd replied that he will update the replacement names and make them ranges or strings.
  - Jens observed that the design appears to be all compile-time based and asked how run-time dependent encoding
    is handled.
  - JeanHeyd replied that the compile-time implementation can be wrapped in a run-time design.
  - Jens expressed a desire to see the design specified in terms of concepts.
  - JeanHeyd replied that the proposal will use concepts, but that the current implementation is intended to work
    with pre-C++20 compilers.
  - Tom asked how much of the proposal is implemented.
  - JeanHeyd replied that interfaces have been implemented for decoding, encoding, transcoding, validation, and
    code point counting.
  - JeanHeyd added that support for normalization hasn't been completed, but normalization can be done later.
- Tom stated that the next meeting will be February 26th and the focus will be on post-Prague follow up.

  
# January 22nd, 2020

## Draft agenda:
- P1885R0: Naming Text Encodings to Demystify Them
  - https://wg21.link/p1885
  - Follow up on recent mailing list discussions.
  - Identify and discuss intended use cases.
- P2020R0: Locales, Encodings and Unicode
  - https://isocpp.org/files/papers/P2020R0.pdf
  - General discussion, corrections, suggestions, etc...

## Meeting summary:
- Attendees:
  - Corentin Jabot
  - David Wendt
  - Hubert Tong
  - Jens Maurer
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- P1885R1: Naming Text Encodings to Demystify Them
  - https://wg21.link/p1885r1
  - Tom introduced the topic for discussion:
    - SG16 approved P1885R0 to forward to LEWG in Belfast.
      - http://wiki.edg.com/bin/view/Wg21belfast/SG16P1885R0
    - Corentin has now provided an R1 with minor updates.
    - Since then, concerns were raised on the SG16 mailing list:
      - https://lists.isocpp.org/sg16/2019/12/0993.php
      - (See email thread continuation in January as well)
    - Questions of use cases have been raised.
  - Corentin stated that use cases haven't changed from his perspective and that the discussion on the
    mailing list went off on a tangent.
  - Tom replied that the discussion suggested a lack of consensus on the importance of a name vs a MIB ID.
  - Corentin stated that what is proposed is just a name intended to resolve issues with names not being
    portable across platforms.  The proposal relies on MIB IDs to correlate names for use with third party
    products.  The proposal does not allow dynamically adding names so as to avoid the possibility of
    inconsistent results.
  - Tom asked what the motivation was for not including enumerators for all MIB IDs in `text_encoding::id`,
    but to require the implementation to support all names and aliases from the
    [IANA Character Set Registry](https://lists.isocpp.org/sg16/2019/12/0993.php).
  - Corentin replied that the requirements were changed in R1.  Hosted implementations are now required to
    support all of the names, but freestanding implementations need not.
  - Tom asked for clarification regarding omission of enumerator IDs.
  - Corentin replied that, if we specify enumerator names for all registered character sets, then we'll
    have to maintain that list.  Additionally, if implementors can add names, that could lead to portability
    or compatibility issues.  Discussion with others prior to Belfast suggested more names were not needed.
  - Jens summarized the concern; the RFC has ~150 names and we would have to put all 150 names into the
    enumeration and deal with the maintenance.  If we select just a few names, then we don't have a
    maintenance burden.
  - Tom countered that use of the `cs` prefixed identifiers described in section 2.3 of
    [RFC 2978](https://tools.ietf.org/html/rfc2978) and maintained in the
    [IANA Character Set Registry](https://lists.isocpp.org/sg16/2019/12/0993.php)
    would avoid the portability and compatibility concerns and provide a specification we can defer to.
  - Corentin replied that it isn't quite that simple because of version skew and that exposing MIB IDs to
    programmers has limited value to begin with.
  - Tom countered that, in the example use case provided in Belfast, you don't necessarily know what the
    name is.
  - \[Editor's note: That example use case is:
    ```
    template<class traits, class Rep, class Period>
    void print_fancy_suffix(basic_ostream<char, traits>& os, const duration<Rep, Period>& d)
    {
      if constexpr (text_encoding::literal().mib == UTF-8) {
        os << d.count() << "\u00B5s";
      } else {
        os << d.count() << "us";
      }
    }
    ```
    \]
  - Corentin replied that the use case could still be covered by comparing the implementation provided
    `text_encoding` object with one constructed by the programmer with a name.
  - \[Editor's note: Presumably something like:
    ```
    template<class traits, class Rep, class Period>
    void print_fancy_suffix(basic_ostream<char, traits>& os, const duration<Rep, Period>& d)
    {
      if constexpr (text_encoding::literal() == text_encoding("UTF-8")) {
        os << d.count() << "\u00B5s";
      } else {
        os << d.count() << "us";
      }
    }
    ```
    \]
  - Tom opined that string names are good for interaction with current third party libraries, but IDs are
    preferred for the example provided
  - Corentin replied that adding more enumerators is ok, but expressed discomfort with deferring to the
    IANA registry due to the possibility of incompatibilities arising from version skew.
  - Steve noted that the proposal only intends to provide portable names; there is no requirement for
    encoders and decoders to be provided.
  - Zach observed that no enumerator is provided for Windows-1252 and asked how an implementor that
    frequently traffics in that encoding would provide support.
  - Corentin responded that a `text_encoding` object can be constructed by name or that the fixed numeric
    value from the IANA registry can be used.
  - JeanHeyd asked if we could reserve a range of MIB IDs for use by implementations similar to the Private
    Use Area in Unicode.
  - Corentin replied that he is strongly opposed to doing so.
  - Corentin asked if we really want all of these names to be available as identifiers when we can just
    use strings.
  - Zach responded that he thinks it makes sense for cases where we know compilers default to certain encodings.
  - Corentin repeated that he doesn't want implementors to add their own names.
  - Jens asked about the source for the names whether as strings or identifiers.
    [RFC 3808](https://tools.ietf.org/html/rfc3808) lists the MIB names with interesting spellings, and
    [RFC 2978](https://tools.ietf.org/html/rfc2978) defines a registration process, but neither provides
    the latest names.
  - Steve provided the URL to the IANA registry and explained that the RFCs don't change, but specify the
    URL for the registry; which doesn't change often.
    - https://www.iana.org/assignments/character-sets/character-sets.xhtml
  - Tom added that the IANA registry mostly changes for administrative reasons, not because of new character
    set registrations.
  - Jens asked how it is determined which names are good for enumerators.
  - Tom replied that
    [RFC 2978](https://tools.ietf.org/html/rfc2978) specifies that each registered character set have an
    associated name prefixed with "cs" that is appropriate for use as an identifier.
  - Jens asked why the names in the proposal do not match the "cs" names.
  - Corentin responded that he picked names that he preferred.
  - Jens asserted that, in that case, implementors cannot extend the list.
  - Zach stated that there isn't much cost in taking the list of "cs" prefixed names, removing dashes, and
    dumping that list in the wording and asked again for motivation for omitting them.
  - Corentin replied that he thought they were not needed.
  - Zach agreed that many would not be used much, but determining which ones are important would be difficult
    where as just including them all would be easy.
  - Tom asked Corentin, why he felt comfortable deferring to the IANA registry for string names, but not for
    enumerator names?
  - Corentin replied that he felt that the names and alias names were definitive, but that the enumerator
    names seemed more fuzzy.
  - Corentin asked Jens if there are concerns regarding the use of trademark names in the standard; many of
    the character set names include trademark names.
  - Jens replied that we already use trademarked names like Windows and POSIX in the filesystem specification.
  - Steve added that these names have already been vetted by their respective owners, if necessary, for
    inclusion in the registry.
  - Jens asked if the names in the IANA registry might already be reflected in an ISO standard that we could
    reference instead.
  - Corentin replied that he was unaware of such an ISO standard.
  - Tom asked Jens how a search for such an ISO standard could be conducted.
  - Jens suggested searching for "character set" in the ISO list.
  - Steve noted that the RFC describing the IANA registration process does mention ISO standards such as
    ISO 10646, ISO 8859, and ISO 2022.
  - Corentin stated that web browsers, iconv, ICU, etc... all use the IANA registry; it is the defacto standard.
  - Jens expressed some uncertainty with regard to how to refer to these RFCs from the standard, but mentioned
    that we did similarly for the time zone database which is even less regulated.
  - Jens raised a concern about impact to small/embedded implementations.  As proposed, they would have to
    include an instance of the string name table with every instance of the program and that could be problematic
    even for some hosted implementations.
  - Tom suggested that, if the string table is not referenced; e.g., if none of the `text_encoding` factory
    functions is referenced or if the `<text_encoding>` header is not included, that the implementation might
    be able to omit it.
  - Jens suggested that it would be helpful if the paper addressed cost of implementation and anticipated
    impact to deployments.
  - JeanHeyd suggested that the guarantee we make should be that if only `text_encoding::system()` or
    `text_encoding::literal()` are called, then there should be no string table overhead.
  - Jens asked if an implementation could provide support for a reduced set of names.  If not, the discussion of
    how to reduce deployment cost is warranted since, as proposed, this is not a zero-cost of zero-overhead
    solution.
  - Jens also stated a preference for the `system()` and `wide_system()` functions to return a MIB ID rather
    than a `text_encoding` object.
  - Corentin responded that there may be cases where the system encoding is not registered with IANA.  In that
    case, the MIB ID would be "unknown"; and a different interface would have to be used to retrieve the string
    name of the encoding anyway.
  - JeanHeyd provided WTF-8 and Modified UTF-8 as examples of encodings that are not registered with IANA but
    that are known to be in use on Android and elsewhere on the web.
  - Jens suggested that, in such cases, the implementation register their encoding.
  - Zach asked to clarify what the motivation is for supporting string names at all.
  - Tom responded that third party products like iconv and ICU have interfaces that require use of string names.
  - Corentin confirmed.
  - Tom added that the IANA registry is effectively a common subset of recognized names.
  - Zach stated a preference for omitting string names and just relying on MIB IDs.
  - Corentin responded that doing so would complicate use of iconv.
  - Hubert expressed a lack of motivation for an interface that relies on numeric values that no one knows;
    the string names make sense.
  - Jens pondered if string name to MIB ID lookup was an orthogonal feature.
  - Tom stated that question was posed in the mailing list discussion as well.
  - Corentin mentioned existing host system interfaces.  Windows provides a code page with an ID.  POSIX systems
    provide a name and no ID.
  - Jens suggested that an interface that provides a string name does not suit all use cases.  For example,
    a programmer might desire to assert a specific system encoding; that shouldn't require a full string table.
  - Zach expressed a desire for the interface to provide more safety and that he would prefer a list of
    identifiers over a list of string names.
  - Hubert suggested other benefits of the string names, 1) useful for interaction with the system and third party
    libraries, and 2) useful for interchange or serialization.
  - Hubert expressed concern about use of a string interface for looking up an encoding name and asked what name
    is provided in response to a lookup of a MIB ID.
  - Corentin replied that there is no proposed lookup interface that accepts a MIB ID.  The factory interfaces
    like `text_encoding::system()` return a preferred name, but otherwise, the name provided when constructing
    a `text_encoding` object is preserved.
  - Jens expressed a desire for a low-level interface that just returns an integer that could be used to assert
    the environment is UTF-8 without having to compare with a bunch of strings; that could be a zero overhead
    facility.
  - Hubert asked if there is overhead if neither of `text_encoding::system()` or `text_encoding::wide_system()`
    is called.
  - Corentin responded that yes, there is, but it is low.
  - Hubert cautioned that some standard library implementors are likely to oppose anything that increases
    startup cost or requires "static constructors".
  - Tom asked why the interface couldn't perform a lazy lookup.
  - Corentin responded that calls to `setlocale()` could interfere; `text_encoding::system()` is intended to
    return the locale dependent encoding known at program startup time.
  - \[Editor's note: Later discussion on the SG16 mailing list revealed that it is possible on POSIX systems
    to retrieve the locale dependent encoding known at program startup time regardless of intervening calls
    to `setlocale()` with code like:
    ```
     locale_t loc = newlocale(LC_CTYPE_MASK, "", (locale_t)0);
     const char* name = nl_langinfo_l(CODESET, loc);
     ...
     freelocale(loc); 
    ```
    \]
  - Hubert suggested that programmers can collect this information on their own and that they should be aware if
    some library is calling `setlocale()` before `main()` is invoked.
  - Tom agreed, but stated that doing so is hard in practice, particularly for library authors.
  - JeanHeyd observed that the C library behavior depends on the currently set locale and asked what benefit
    is provided by `test_encoding::system()` if it's not in sync with the C and C++ libraries.
  - Tom responded that it indicates what encoding is expected for I/O outside of the process.
- Tom confirmed that the next meeting will be on February 5th and that it will be the last meeting before we
  meet in Prague.


# January 8th, 2020

## Draft agenda:
- LWG issue 3341: basic_regex range constructor: Missing requirements for iterator types
  - https://cplusplus.github.io/LWG/issue3341
  - Billy O'Neal copied SG16 on this issue; see https://lists.isocpp.org/sg16/2019/12/0990.php
  - What should be the proposed resolution?
- P1949: C++ Identifier Syntax using Unicode Standard Annex 31:
  - https://wg21.link/p1949
  - Which UAX #31 requirements do we intend to satisfy (see section 2)?
  - Which UAX #31 specific character adjustments do we want (see section 2.4)?
  - Which UAX #31 NFKC modifications we we want (see section 5.1)?

## Meeting summary:
- Attendees:
  - David Wendt
  - JeanHeyd Meneide
  - Lyberta
  - Peter Bindels
  - Steve Downey
  - Tom Honermann
  - Zach Laine
- LWG issue 3341: basic_regex range constructor: Missing requirements for iterator types
  - https://cplusplus.github.io/LWG/issue3341
  - Tom introduced the topic:
    - Billy O'Neal copied SG16 on this issue.  His email is available in the SG16 mailing list archives
      at https://lists.isocpp.org/sg16/2019/12/0990.php.
    - What should be the proposed resolution?
  - Zach asked why we should be concerned about this issue.
  - Tom responded that Billy copied us on it, presumably seeking our input.
  - Zach stated that implicit transcoding should not occur; The safest thing to do would be to require
    `ForwardIterator::value_type` to be exactly `charT`.
  - JeanHeyd agreed with the no implicit transcoding stance; that would make `std:regex` even slower!
  - Peter chimed in via chat agreeing with an exact type requirement and the following constraint:
    - `std::is_same_t<value_type, decltype(*std::declval<ForwardIterator>()>`
  - Peter asked if we should enable views to be used as inputs.
  - Steve stated that would be a more difficult challenge given the recent difficulties faced when
    attempting to add range constructors for standard containers.
  - Zach agreed that adding range support could be difficult and is out of scope for this issue anyway.
  - Peter concurred and noted that view support can always be added later.
  - Tom observed that if a same type constraint is added, then SFINAE will kick in, but it might be
    preferred to make it a hard error if the iterator value type doesn't match.
  - Zach suggested leaving that for LWG to decide.
  - Tom agreed and stated he would respond to Billy's email and LWG with our thoughts.
- P1949: C++ Identifier Syntax using Unicode Standard Annex 31:
  - https://wg21.link/p1949
  - https://github.com/cplusplus/nbballot/issues/28
  - Tom introduced the topic.
    - In Belfast, EWG did not accept
      [SG16's recommended resolution for NL029](http://wiki.edg.com/bin/view/Wg21belfast/SG16NBNL029)
      for C++20.
    - Tom volunteered to submit a core issue for C++20 in order to allow us to resolve the concern as
      a defect, but he doesn't have a PR to propose.
    - Tom is thinking about bailing on submitting that core issue, but thought he would check if SG16
      might have consensus on what solution we would want.  In particular, if we were to adopt
      [UAX #31](https://www.unicode.org/reports/tr31/tr31-31.html), what would be our answers to these
      questions?
      - Which UAX #31 requirements do we intend to satisfy (see section 2)?
      - Which UAX #31 specific character adjustments do we want (see section 2.4)?
      - Which UAX #31 NFKC modifications we we want (see section 5.1)?
  - Zach suggested we skip C++20 and just proceed with addressing this for C++23.
  - Steve provided motivation for dealing with this as a DR; some compilers are just starting to allow
    extended characters in identifiers.  Previously, programmers had to go out of their way to create
    weird identifiers.  Clang has allowed extended characters forever (since Clang 3.3 or so), gcc
    support was added for gcc 10.  The window for changing behavior is shrinking.
  - Zach asked if the concern was about breaking existing code given that this isn't the kind of break
    we usually worry too much about.
  - Tom replied that the breakage could be silent if Unicode normalization affects whether two
    identifiers match.
  - Steve added that breakage could occur due to excluded characters like the poop emoji.  Compilers
    could provide backward compatibility options; Hyrum's law.
  - Steve continued stating that, if we don't get this nailed down for C++23, we could probably still
    do it because it probably won't affect that much code.
  - Zach observed that the impact would mostly be due to banning emoji.
  - Steve agreed; emoji is the only case people are likely to notice.  Programmers aren't likely to
    want right-to-left characters in identifiers for example.
  - Which UAX #31 requirements do we intend to satisfy (see section 2)?
    - Tom stated that we need to choose whether to use the `ID_Start`/`ID_Continue` or
      `XID_Start`/`XID_Continue` properties to define identifier syntax.  P1949 suggests using the
      `XID_Start`/`XID_Continue` variants and doing so is necessary to meet the requirements for
      [UAX31-R1](https://www.unicode.org/reports/tr31/tr31-31.html#R1) without defining a profile;
      though, we'll need a profile to add `_` as a start character.
    - Steve recommended we adopt the XID variants and add `_` as a start character.  However, this
      doesn't suffice to guarantee identifier stability.
    - Tom stated that, in order to meet requirement
      [UAX31-R1a](https://www.unicode.org/reports/tr31/tr31-31.html#R1a), that he thinks we'll need
      to specify additional characters to exclude.  The NL029 NB comment specified a particular range
      to exclude, but he is not sure if or how that matches UAX31.
    - Steve corrected Tom's interpretation; that requirement allows opting in to characters that are
      disallowed by default.
    - Peter stated that section 2.3 explains that some character that are restricted by default are
      needed in some cases for some scripts.
    - Peter continued stating that he thinks we lack the experience to make choices in this regard and
      suggested we proceed with more restrictions now and relax them later based on experience and
      motivation.
    - Tom asked about meeting the requirements for
      [UAX31-R1b](https://www.unicode.org/reports/tr31/tr31-31.html#R1b); assuming we want to meet
      that requirement, how would we do so?
    - Steve responded that, given ABI issues, we should commit to meeting this requirement.  In
      practice, that means that, for example, if a future Unicode standard were to remove characters
      from `XID_CONTINUE`, that we would update our profile to add them back in.
    - Peter asked if the `XID_Start`/`XID_Continue` properties are stable.
    - Zach responded that he understood them to be stable.
    - Steve responded that they are derived properties and are not guaranteed to be stable, but
      probably will be in practice.  \[Editor's note: in later email discussion, Steve offered a
      correction to this statement: `XID_Start` and `XID_Continue` are guaranteed stable, just not
      immutable. Immutability is the property that things that are not identifiers remain not
      identifiers. \]
    - Zach mentioned that he wasn't previously aware that UAX31 had options, but it seems our goal
      now needs to be to identify the options, select them, and then make sure proposed wording
      reflects our intent.
    - Tom agreed.
  - Which UAX #31 specific character adjustments do we want (see section 2.4)?
    - Peter, reviewing section 2.4, stated no observed need for exceptions other than for `_` in
      the start position; a choice that is already explicitly listed as an option.
  - Which UAX #31 NFKC modifications we we want (see section 5.1)?
    - Tom stated that we need to figure out how to deal with normalization if we want stable
      identifiers.
    - Zach provided some background on NFC, NFD, compatibility, comparisons, and conversions.
    - Zach professed support for standardizing on NFC; NFD is not really usable since combining
      marks don't tend to be represented by themselves in identifiers.
    - Tom asked if standardizing on NFC commits implementors to perform normalization.
    - Steve responded that gcc 10 already emits a warning for identifiers that are written in
      non-NFC forms in source code.
    - Zach stated that checking for NFC is fast, at least for common cases, so diagnosing is
      reasonable, but stating that non-NFC identifiers are IFNDR (ill-formed no diagnostic required)
      is also a possibility.
    - Tom observed that conversions from other character sets like Windows-1252 probably always
      result in NFC.
    - Zach agreed noting that such conversion is probably done via the compiler's internal encoding.
    - Peter stated that there are other character sets that have combining marks, but none of those
      are probably supported by compilers.
    - Tom, considering source code that is encoded as UTF-8 in NFD, asked if requiring NFC could be
      problematic for existing editors and tools.
    - Steve observed that this issue already exists and that tools today already expect NFC.
    - Peter recommended that we make use of non-NFC normalized source code IFNDR and encourage tools
      to diagnose violations.
    - Zach responded that IFNDR is generally reserved for cases where something can't be reasonably
      diagnosed; since diagnosis is reasonable here, non-NFC forms should be considered ill-formed.
    - Steve added that compiler implementors can support options to relax NFC checking.
    - Tom noted that this creates a specification issue since, if source encoding is not UTF-8, it
      needs to be transcoded to NFC, but if it is UTF-8, source code needs to already be in NFC.
    - Zach responded that we don't have to; we just specify the characters that are valid based on
      `XID_Start`/`XID_Continue`.
    - Steve added that the NFC check has to be done after conversion from source encoding to internal
      encoding and that he is unaware of any encoding that does not naturally transcode to NFC.
    - Peter observed that combining diacritics are part of `XID_Continue` and that there are
      therefore two spellings of café; a 4 code point variant using
      U+00E9 {LATIN SMALL LETTER E WITH ACUTE} and a 5 code point variant using
      U+0301 {COMBINING ACUTE ACCENT}.
    - Zach stated that this feature requires the compiler's internal encoding to be Unicode.
    - Tom responded that, since C++11, the internal encoding must already be isomorphic to Unicode.
    - Zach suggested that both forms of café should not be allowed; that NFC should be required, and
      that use of combining characters should be disallowed in our profile.
    - Steve responded that disallowing all combining characters probably isn't feasible; there aren't
      precomposed forms of all characters; in NFC, combining characters will still appear, but only
      when they are actually required.
    - Zach suggested this is a restriction that could be relaxed later.
    - Steve observed that this would make specification of the profile more difficult.
    - Zach agreed and suggested just specifying a list of start and continue characters; this avoids
      implementors having to do hard things.
    - Peter noticed a problem with that approach; new Unicode characters could not be used unless and
      until the standard is updated with a new list of start/continue characters.
    - Tom added that this is why we want to defer to the implementation-defined Unicode version.
    - Steve added this is also why we want the identifier stability guarantee; otherwise we get
      linkage problems.
    - Peter suggested it should be ok to define a profile with `<Start>` defined as `XID_Start` + '_',
      and `<Continue>` defined as `XID_Continue` - <all_combining_characters>.
    - Steve noted that we have a floating Unicode reference today.
    - Tom agreed but noted that we have not yet required implementors to state which version of Unicode
      they conform to.
    - Steve agreed and added that, technically, we only have a floating reference to ISO/IEC 10646; this
      may not cover the normalization algorithm.
    - Steve summarized some options; there are two ways to deal with NFC: 1) source must be NFC normalized,
      and 2) the compiler internal encoding must be NFC.  Not allowing combining characters gives us the
      stability that we need without having to distinguish between those options.
    - Steve continued that omitting combining characters avoids the problem of Unicode introducing new
      precomposed characters that previously had to be represented with a combining character thereby
      changing NFC.
    - Tom responded that he thought the Unicode standard has a stability guarantee that new precomposed
      characters will not be introduced.
    - Peter observed that allowing combining characters is therefore required for new characters.
    - Tom suggested we need to do some more research.
    - Steve, after checking the Unicode standard, reported that normalization forms are guaranteed to be
      stable.
    - Zach quoted from section 3 of [UAX #15](https://www.unicode.org/reports/tr15/tr15-48.html):
      - "It is crucial that Normalization Forms remain stable over time. That is, if a string that does
        not have any unassigned characters is normalized under one version of Unicode, it must remain
        normalized under all future versions of Unicode."
    - Peter repeated his guidance that combining characters must be allowed in order to support some
      scripts.
    - Tom agreed and acknowledged that we probably therefore need to require NFC.
    - Tom summarized options identified so far:
      - 1) The compiler converts to NFC internally.  This could technically break some existing code.
      - 2) Require UTF encoded source files to be NFC and that non-UTF encoded source files be transcoded
           (noting that we believe that transcoding from any existing character sets will produce NFC).
    - Zach observed that the implementation effort is equivalent for those cases since an NFC check can
      bail out early if the check fails, but is otherwise same amount of work so that the complexity cost
      is the same.
    - Steve stated that he may not be in Prague, but that others can champion the paper as needed.
    - Peter and Zach both volunteered to champion.
    - Steve stated he would try to get an updated revision submitted for the Prague pre-meeting mailing.
- Tom stated that the next meeting will be January 22nd.


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
