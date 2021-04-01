= TicketQuery Wiki Macro

The TicketQuery macro lets you display information on tickets within
wiki pages. The query language used by the
[`TicketQuery`](TicketQuery "wikilink") macro is described in
\[TracQuery\#UsingtheTicketQueryMacro TracQuery\] page.

== Usage

[MacroList(TicketQuery)](MacroList(TicketQuery) "wikilink")

== Example

  = \*\*Example\*\* =   = \*\*Result\*\* =   = \*\*Macro\*\* =
  --------------------- -------------------- -------------------

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of [Triage tickets](query:status=new&milestone=): =                                               \\
  --------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=new&milestone=,count)](TicketQuery(status=new&milestone=,count) "wikilink")\*\*   \\
  [`TicketQuery(status=new&milestone=,count)`](TicketQuery(status=new&milestone=,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of new tickets: =                                                           \\
  ----------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=new,count)](TicketQuery(status=new,count) "wikilink")\*\*   \\
  [`TicketQuery(status=new,count)`](TicketQuery(status=new,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of reopened tickets: =                                                                \\
  --------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=reopened,count)](TicketQuery(status=reopened,count) "wikilink")\*\*   \\
  [`TicketQuery(status=reopened,count)`](TicketQuery(status=reopened,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of assigned tickets: =                                                                \\
  --------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=assigned,count)](TicketQuery(status=assigned,count) "wikilink")\*\*   \\
  [`TicketQuery(status=assigned,count)`](TicketQuery(status=assigned,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of invalid tickets: =                                                                                                   \\
  ------------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=closed,resolution=invalid,count)](TicketQuery(status=closed,resolution=invalid,count) "wikilink")\*\*   \\
  [`TicketQuery(status=closed,resolution=invalid,count)`](TicketQuery(status=closed,resolution=invalid,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of worksforme tickets: =                                                                                                      \\
  ------------------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=closed,resolution=worksforme,count)](TicketQuery(status=closed,resolution=worksforme,count) "wikilink")\*\*   \\
  [`TicketQuery(status=closed,resolution=worksforme,count)`](TicketQuery(status=closed,resolution=worksforme,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of duplicate tickets: =                                                                                                     \\
  ----------------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=closed,resolution=duplicate,count)](TicketQuery(status=closed,resolution=duplicate,count) "wikilink")\*\*   \\
  [`TicketQuery(status=closed,resolution=duplicate,count)`](TicketQuery(status=closed,resolution=duplicate,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of wontfix tickets: =                                                                                                   \\
  ------------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=closed,resolution=wontfix,count)](TicketQuery(status=closed,resolution=wontfix,count) "wikilink")\*\*   \\
  [`TicketQuery(status=closed,resolution=wontfix,count)`](TicketQuery(status=closed,resolution=wontfix,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of fixed tickets: =                                                                                                 \\
  --------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(status=closed,resolution=fixed,count)](TicketQuery(status=closed,resolution=fixed,count) "wikilink")\*\*   \\
  [`TicketQuery(status=closed,resolution=fixed,count)`](TicketQuery(status=closed,resolution=fixed,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Total number of tickets: =                                   \\
  ------------------------------------------------------------- ----
  \*\*[TicketQuery(count)](TicketQuery(count) "wikilink")\*\*   \\
  [`TicketQuery(count)`](TicketQuery(count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of tickets reported \*\*or\*\* owned by current user: =                                                             \\
  --------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(reporter=\$USER,or,owner=\$USER,count)](TicketQuery(reporter=$USER,or,owner=$USER,count) "wikilink")\*\*   \\
  [`TicketQuery(reporter=$USER,or,owner=$USER,count)`](TicketQuery(reporter=$USER,or,owner=$USER,count) "wikilink")           

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Number of tickets created this month: =                                                              \\
  ----------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(created=thismonth..,count)](TicketQuery(created=thismonth..,count) "wikilink")\*\*   \\
  [`TicketQuery(created=thismonth..,count)`](TicketQuery(created=thismonth..,count) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

  =Last 3 modified tickets: =                                                                                               \\
  ------------------------------------------------------------------------------------------------------------------------- ----
  \*\*[TicketQuery(max=3,order=modified,desc=1,compact)](TicketQuery(max=3,order=modified,desc=1,compact) "wikilink")\*\*   \\
  [`TicketQuery(max=3,order=modified,desc=1,compact)`](TicketQuery(max=3,order=modified,desc=1,compact) "wikilink")         

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

    #th rowspan=2, style="text-align: left;"
    Details of ticket #1:

    #td style="border-bottom: 0;"

    #td
    <tt>[[TicketQuery(id=1,col=id|owner|reporter,rows=summary,table)]]</tt>

\|-

    #td colspan=2, style="border-top: 0;"
    [[TicketQuery(id=1,col=id|owner|reporter,rows=summary,table)]]

\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

== Using the [`TicketQuery`](TicketQuery "wikilink") Macro

The \[trac:TicketQuery TicketQuery\] macro lets you display lists of
tickets matching certain criteria anywhere you can use WikiFormatting.

Example:

    [[TicketQuery(version=0.6|0.7&resolution=duplicate)]]

This is displayed as:

` `[`0.7&resolution=duplicate)`](TicketQuery(version=0.6 "wikilink")

Just like the [wiki links](TracQuery\#UsingTracLinksquery: "wikilink"), the parameter of this macro expects a query string
formatted according to the rules of the simple
[ticket querylanguage](TracQuery\#QueryLanguage "wikilink"). This also displays the link and description of a single
ticket:

    [[TicketQuery(id=123)]]

This is displayed as:

` `[`TicketQuery(id=123)`](TicketQuery(id=123) "wikilink")

A more compact representation without the ticket summaries is:

    [[TicketQuery(version=0.6|0.7&resolution=duplicate, compact)]]

This is displayed as:

` `[`0.7&resolution=duplicate,`` ``compact)`](TicketQuery(version=0.6 "wikilink")

Finally, if you wish to receive only the number of defects that match
the query, use the `count` parameter:

    [[TicketQuery(version=0.6|0.7&resolution=duplicate, count)]]

This is displayed as:

` `[`0.7&resolution=duplicate,`` ``count)`](TicketQuery(version=0.6 "wikilink")

------------------------------------------------------------------------

See also: TracQuery, TracTickets, TracReports, TracGuide

