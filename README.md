# SG16 Meeting Summaries

The next SG16 meeting is scheduled for Wednesday, April 25th, from 2:30-4:00pm EST.

- [April 11th, 2018](#april-11th-2018)
- [March 28th, 2018](#march-28th-2018)
- [Prior std-text-wg meetings](#prior-std-text-wg-meetings)


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
      repo_view).
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
  - R. Martinho Fernandes
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
