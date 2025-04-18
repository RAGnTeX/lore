---
layout: post
title:  "From PDFs to Presentations: How We Used GenAI to Auto-Generate Presentation Slides"
date:   2025-04-18 21:33:10 +0200
categories: RAGnTeX description
---
<img src="/lore/assets/images/long_logo.png" alt="logo" width="900"/>

> "I need a presentation about Retrieval-Augmented Generation."
> What if an AI could build it for you?


Imagine this: You're burning the midnight oil, drowning in a sea of academic papers and technical documents. The clock is ticking down to your presentation deadline, and all you can think is, "How on earth will I synthesize this mountain of information into a coherent slide deck in time?"

Isn't it all too familiar? During our student years and in the depths of academic research, we've all faced the overwhelming task of digesting complex texts. It's a lurking nightmare—so much valuable knowledge trapped in lengthy papers but far too little time to convert it into impactful presentations.

That's why we decided to take matters into our own hands and build a transformative tool—a GenAI-powered assistant that doesn't just help you navigate the academic labyrinth but also creates a polished presentation from scratch.

We envisioned a tool that could not only understand what users need but also scour through vast document collections to find the most relevant information. What if researchers could summarize papers, marketers could transform whitepapers into engaging slides, or busy professionals could quickly prep for a pitch? The potential applications for this tool are limitless:
- **Students** preparing for finals could quickly create summaries of essential readings.
- **Working professionals** could distill extensive reports into executive summaries.
- **Educators** could generate lesson materials or presentations for seminars.
- **Content creators** can use it to build engaging slide decks for webinars or online courses.

## Let's dive into how it all works!

### 1. Semantic Search with Embeddings

Our journey begins with a semantic search. We embed chunks of PDF text using Google's GenAI embeddings and store them in a Chroma vector database, complete with metadata about images—an essential aspect of an engaging visual presentation!

When users enter a topic, our system embarks on its quest for knowledge:

```python
# Query embedding + retrieval results
db.query(query_embedding, top_k=5)
```

### 2. Slide Generation with Gemini
Our tool retrieves the most pertinent document chunks in seconds, ready to be transformed into a captivating narrative.

We use a lightweight Gemini 2.0 Flash to retrieve content and mold it into a structured LaTeX Beamer presentation. We instruct it to create a clear, concise, and engaging presentation that organizes information and highlights imagery that enhances comprehension.

Here's a sneak peek at the presentation structure we provide:

```latex
\documentclass{beamer}
\usetheme{Madrid}

\title{[Presentation Title]}
\author{AI-generated}
\date{\today}

\begin{document}

\frame{\titlepage}

\begin{frame}
\frametitle{Introduction}
- What's the topic?
- Why is it important?
\end{frame}

\begin{frame}
\frametitle{Core Idea 1}
- Key point 1
- Key point 2
\end{frame}

\begin{frame}
\frametitle{Core Idea 2}
\begin{columns}
\begin{column}{0.5\linewidth}
- Key point 1
- Key point 2
\end{column}
\begin{column}{0.5\linewidth}
\center{\includegraphics[width=1\linewidth]{pdf_images/image} \\ image caption}
\end{column}
\end{columns}
\end{frame}

\begin{frame}
\frametitle{Core Idea 3}
\center{\includegraphics[width=1\linewidth]{pdf_images/image} \\ image caption\\}

- Key point 1
- Key point 2
\end{frame}

...

\begin{frame}
\frametitle{Summary}
- Key takeaway 1
- Key takeaway 2
\end{frame}

\end{document}
```

With such a well-structured format, all that is left to do is save it as a text file and compile it to get the presentation right away!

```python
tex_file = os.path.join(work_dir, 'presentation.tex')
with open(tex_file, "w") as f:
    f.write(latex_code)

# Compile with pdflatex
os.chdir(work_dir)  # Change working directory
# We compile it twice to ensure proper slide enumeration
!pdflatex -interaction=nonstopmode presentation.tex > output.log
!pdflatex -interaction=nonstopmode presentation.tex > output.log
```
As a result, not only do you get a well-structured summary presentation covering all the essential points, but you also save your precious time! Though our initial output is remarkable, there's always room for growth. Imagine the possibilities:

- Style Customization: Choose any presentation theme or incorporate your own design.
- Tone Adjustment: Need your presentation more formal? Or perhaps humorous? With added options, users can easily tweak the tone to suit their audience.
- Enhanced Features: Let's include speaker notes and narration scripts for a truly immersive experience.

This project proved that even with lightweight tools, it's possible to go from "I need a presentation about X" to a structured, informative, AI-generated slide deck — all in a few minutes.

In a world where information is vast but time is limited, our GenAI-powered system stands ready to empower users to turn complexity into clarity. Are you prepared to embrace the future of presentations?