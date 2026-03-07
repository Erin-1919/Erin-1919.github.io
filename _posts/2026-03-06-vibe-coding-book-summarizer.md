---
title: "Building a Book Summarizer with Vibe Coding: Zero Lines Written by Hand"
layout: post
---

![app](/assets/img/20260306/screenshot-app.jpg)

**I recently built a fully functional web application without writing a single line of code myself. Using Claude Code as my AI programming partner, I went from idea to a working Book Page Summarizer in under an hour, entirely through conversation.**

The term "vibe coding" has been floating around the AI community lately, and I wanted to put it to the test with a real project. The idea: a reading companion app that lets me photograph book pages or upload PDFs, extract the text, and generate concise summaries using GPT-4o. The entire development process happened through natural language: describing what I wanted, reviewing what Claude Code produced, requesting modifications, and testing iteratively.

The result is [Book Page Summarizer](https://github.com/Erin-1919/book-summarizer), an open-source tool now on GitHub.

## What the App Does

Book Page Summarizer is a Flask-based web application designed around a simple reading workflow:

- **Upload book pages** as photos (JPG, PNG, WebP, etc.) or PDFs
- **Extract text** automatically. Images go through GPT-4o's vision capability, while PDFs are processed locally with PyMuPDF.
- **Generate summaries** with key points structured as one-paragraph bullet points
- **Organize everything** hierarchically by book, chapter, and sub-chapter
- **Persist data** across sessions in a local JSON file

The app comes pre-loaded with the structure for *Prediction Machines* by Ajay Agrawal, Joshua Gans, and Avi Goldfarb, but users can add any book and customize the chapter hierarchy freely.

## How It Works Under the Hood

The tech stack is deliberately simple. The backend is a single Flask file (~520 lines) handling all routes, API calls, and data persistence. The frontend uses vanilla JavaScript with Jinja2 templates, with no framework overhead. Styling is custom CSS with a warm, book-friendly aesthetic: cream backgrounds, brown headers, and serif typography.

A few implementation details stand out:

- **Single API call for images**: Rather than making separate calls for text extraction and summarization, the app sends each image to GPT-4o once and parses both the extracted text and summary from a single response using delimiter markers. This cuts API costs in half.
- **Drag-and-drop file ordering**: When uploading multiple pages, a reordering panel lets you arrange them before processing. Pages are then summarized in the confirmed order.
- **Google Photos integration**: An optional OAuth flow connects to Google Photos, allowing direct import of book page photos without manual download.
- **Low temperature (0.3)**: The summarization prompts use low temperature for consistency, with directive language that states ideas as facts rather than hedging with "the author suggests."

## The Vibe Coding Experience

The entire development took less than one hour across several rounds of conversation with Claude Code. Each round followed a natural pattern: I described a feature or pointed out something to fix, Claude Code generated or modified the code, and I tested it locally. No copy-pasting from Stack Overflow, no manual debugging of syntax errors, no switching between documentation tabs.

What surprised me most was how well the iterative workflow handled complexity. The Google Photos integration, for example, involves OAuth 2.0, a picker session API, and polling. That is the kind of plumbing that would normally eat up an afternoon of reading documentation. Through conversation, it came together in minutes.

A few observations from this experiment:

- **Describing intent is faster than writing code** for well-understood patterns. Flask routes, API calls, and CRUD operations are exactly the kind of boilerplate that AI handles well.
- **Reviewing AI-generated code is a different skill** than writing code from scratch. I focused on architecture decisions and user experience rather than syntax.
- **Testing still matters**. Each round included running the app and checking that things worked as expected. The conversational loop of "try it, report back, adjust" was the real workflow.
- **The code is clean and readable**. This was not throwaway prototype quality. The project has proper error handling, file cleanup, and a clear structure that I could maintain going forward.

## The Bigger Picture: The End of the App Store Model

This project is a small example of something much larger. Andrej Karpathy recently [posted on X](https://x.com/karpathy/status/2024583544157458452) about vibe coding a custom cardio tracking dashboard in one hour, a hyper-specific tool that no app store would ever carry. His point resonated: the idea of browsing a discrete set of pre-built apps and hoping one fits your exact need is starting to feel outdated. When an LLM agent can improvise a ~300-line app on the spot, tailored precisely to your use case, the long tail of niche software no longer needs to exist as downloadable products.

My book summarizer fits this pattern exactly. There is no app on any store that does precisely what I wanted: photograph pages from a physical book, extract text via vision AI, generate structured summaries, and organize them by chapter hierarchy. It is too specific. Too personal. But that is exactly the kind of software that vibe coding makes trivial to create. The future Karpathy describes, where you simply say "help me summarize this book as I read it" and a custom tool materializes after a brief conversation, is not far off.

What still takes an hour today should eventually take minutes. The bottlenecks are clear: AI agents need better access to services (APIs and CLIs instead of human-readable web interfaces), more personal context to reduce the back-and-forth, and reusable skill libraries to avoid rebuilding common patterns from scratch. But the direction is unmistakable. We are moving from choosing apps to describing intent.

## Takeaway

Vibe coding is not about replacing programming knowledge. Understanding what you want to build, how components fit together, and what good software looks like still matters. But the mechanical act of translating those ideas into syntax? That part is increasingly handled by AI. For a side project like this, the productivity gain is remarkable: a functional, polished tool in under an hour, with zero lines of code written by hand.

The project is open source: [github.com/Erin-1919/book-summarizer](https://github.com/Erin-1919/book-summarizer)
