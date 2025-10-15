**Municipal Services SA — Windows Forms (.NET Framework)
**
A C# Windows Forms application that helps South African residents report municipal issues, browse local events & announcements, and (foundation for) track request status. Built for PROG7312 Part 1 & Part 2 with an emphasis on custom data structures and user-centric UX.

Tech stack: C# (.NET Framework 4.8), WinForms, Visual Studio 2022


**Features**
Part 1

Main Menu (polished UI): Card-based landing page with header banner and municipality logo.

Report Issues:

Location, category, rich description, and media attachments (JPG/PNG/PDF).

Engagement progress bar and encouraging messages as you fill the form.

Validation with ErrorProvider and success feedback.

Custom data structure for attachments (SimpleLinkedList<string>).

Disabled (placeholder): Local Events & Announcements, Service Request Status.

**Part 2
**
Local Events & Announcements:

Events list with search, date range, category filter, and sort by Date/Category/Name.

Announcements section (always visible, not filtered).

Recommendations: events suggested based on recent searches (category preference) + fallback keyword/month scoring.

Data structures showcased: SortedDictionary, Dictionary, HashSet, Stack, Queue, and custom SimplePriorityQueue<Event>.

Screens

MainForm — header banner, logo (top-right), three action cards: Report Issues, Local Events & Announcements, Service Status (coming).

ReportIssueForm — inputs, attachments, progress bar, validation, submit.

EventsForm — filters row (category/date/search/sort), events ListView, Recommendations list, Announcements list.

**Data Structures & Algorithms**

This project avoids built-in generic collections where required (per brief) and demonstrates custom-built structures alongside standard ones.

Custom

SimpleLinkedList<T>

Minimal singly-linked list with Add, Contains, Clear, Count, ForEach, and RemoveWhere(Predicate<T>).

Used for attachments in the Issue form to satisfy the “custom data structure” requirement.

SimplePriorityQueue<T>

Lightweight min-priority queue keyed by DateTime priority, supports Enqueue(key,value), Dequeue(), Peek(), Count.

Used in events module as UpcomingByDate to manage next events by soonest date.

**Standard (explicitly required)**

Primary Storage:

SortedDictionary<DateTime, List<Event>> _byDate — primary, naturally sorted by calendar day.

Dictionary<string, Event> _byId — O(1) lookup by event ID.

Event Management:

Stack<Event> LastViewed — records event details the user opened most recently (LIFO).

Queue<Event> NewSubmissions — staging area for new events (FIFO).

SimplePriorityQueue<Event> UpcomingByDate — prioritises soonest events.

Uniqueness / Lookup:

HashSet<EventCategory> _categories — unique category set to populate the filter dropdown.

These choices align with the Part 2 technical requirements:

Stacks/Queues/Priority Queues (15) ✅

Hash Tables/Dictionaries/Sorted Dictionaries (15) ✅

Sets (10) ✅

**How to Build (Visual Studio 2022)**

Open the solution

Double-click MunicipalServicesApp.sln (inside the cloned repo).

Target Framework

Project targets .NET Framework 4.8 (recommended with VS 2022).

If needed: Right-click project → Properties → Application → Target framework: .NET Framework 4.8.

Restore NuGet packages (if any; this solution is mostly BCL/WinForms).

Build

Build → Build Solution (Ctrl+Shift+B).

Ensure no compile errors.

If you get a C# language version error, set Project → Properties → Build → Advanced… → Language version: Latest major version.

**How to Run**

Press F5 (Debug) or Ctrl+F5 (Run without debugging).

App starts on MainForm.

Logo: Ensure municipality_logo.png is added in Project → Properties → Resources as municipality_logo. The code references Properties.Resources.municipality_logo.

How to Use
Report Issues

Main Menu → Report Issues.

Fill Location, Category, and Description (≥ 20 chars).

Optional: Add attachments (JPG/PNG/PDF).

Watch the progress bar reach 100% as fields are completed.

Click Submit → you’ll see a confirmation with a reference number.

Choose to submit another or return to main menu.

Local Events & Announcements

Main Menu → Local Events & Announcements.

Filter by Category, From/To dates, Search (title/description/location), and Sort.

Double-click an event to see details (this also records LastViewed on the stack).

See Recommended for you populated from your recent searches.

Announcements appear at the bottom—always visible, not filtered.

**Sample Data / Seeding**

On first open of the events page, if total events < 15, the app seeds demo events via EventSeeder.Seed().

You can replace or extend seed data to match your municipality context.

**Recommendation Logic**

Primary rule: infer the top category from your recent searches using SearchTracker, then recommend upcoming events in that category (even if the typed keyword doesn’t appear in the event text).

Fallback: if no category preference is detected, a blended score is used:

+1 if event month matches a top searched month

+1 per matching top keyword in title/description/location (capped at +3)

Results are sorted by score desc, then date asc, then top N (default 5).

**Design & UX Notes**

Consistent palette: brand blue #0A6EBD, accent green #34A853, neutral whites/greys.

Header banner + logo on MainForm and EventsForm.

Clear labels & validation (ErrorProvider, message boxes).

Responsive layout using Anchors and resize handlers for picture boxes and buttons.

Accessibility: tab order, meaningful button text, modal forms for flows.

**Demo Video & Repo**

YouTube demo link: add your video link here

