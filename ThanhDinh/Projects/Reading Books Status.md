📚 The modern day reading list includes more than just books. We've created a dashboard to help you track books, articles, podcasts, and videos. Each media type has its own view based on the Type property. 


👇 Click through the different database tabs to see other views. Sort content by status, author, type, or publisher.

```dataview
TABLE
  Type,
  Status,
  Score,
  Author,
  Completed,
  StartDate,
  EndDate,
  link(file.link, "📘 Open") AS Link
FROM "Reading List"
```