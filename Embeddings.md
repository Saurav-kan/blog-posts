---
title: "The Power of Embeddings"
date: "Mar 14, 2026"
---
# The Power of Embeddings

My first exposure to embeddings and vectors was a while ago when I was first learning about ML models and transformers. I thought it was super cool how you could distill meaning through a set of numbers, but it didn't really stand out as much to me at the time because I wasn't thinking about their functionality outside of that context—like, vectors were just a thing that happened inside these models.

More recently when I was learning about RAG systems and context engineering, I realized how versatile they were. The whole idea of taking a user query, embedding it, and then searching through a database of embedded documents to find the most semantically relevant ones just clicked for me. And that's when I started seeing vectors everywhere.

## Inspiration behind Gist

I lose files constantly. Not in an organizational way, but in a "I named this file something random 6 months ago and now I can't remember what I called it" or "I didn't update the name of my Algorithm's homework file from its default name of hw5" kind of way. The entire paradigm of file systems is based on naming and folder hierarchies, which means if you're bad at naming things, you're going to have a hard time. When I was thinking about RAG and semantic search, the obvious thought was: why can't I do this for my own files?

That's how Gist came about. Instead of searching for filenames, you describe what you're looking for, and the system finds files based on semantic similarity. It's not revolutionary, but it's genuinely useful, and it made vectors stop being this abstract concept and start being a tool I actually used.

## Seeing the Pattern

Once you build something with embeddings, you start noticing them everywhere. Browser Search results, Amazon recommendations, facial recognition, all Vectors. It's kind of wild how prevalent they are in products we use daily.

Now whenever I have a comparison problem my first thought is can I/should I use vectors here? Resume matching? Embed the job description and the resume, measure the l2 distance or cosine similarity. Finding similar support tickets? Embed them and cluster. Detecting duplicate content? Same thing. It became this mental model where my first instinct for "how do I compare these two non-standardized items" was always vectors.

## Experimenting 

I built a resume matcher that compared job postings with resumes. Traditional approach: parse the job description, look for keywords in the resume, count matches. Mine: embed both, measure cosine similarity. The traditional way breaks if someone uses different words for the same skill. The vector approach just understands that "full-stack engineer" and "I build web applications from frontend to backend" mean basically the same thing.

As I began to work with vectors more I learned about how they're organized, from vector databases like ChromaDB to search algorithms like HNSW (Hierarchical Navigable Small World) and IVF (Inverted File Index), which let you search for vectors much more efficiently. 

I implemented HNSW in Gist because I was curious about it. But then I realized that with 3,000 file embeddings, linear search was actually much faster than building and maintaining an HNSW graph. To be exact it was 3x faster, I then shifted my approach to only using HNSW if there were more than 10k vectors in the database but that might still be too little.

## Beyond Text

Embeddings aren't just for text. You can embed audio, images, or basically anything you can represent numerically. There are even models that do cross-modal embeddings—they can embed both an image and a text description in the same vector space, which means you can compare them directly.

I experimented with some of these models because they were cool, not because I needed them. They're slower and more resource-intensive than text-only models, so they didn't make sense for Gist, but the fact that they exist is interesting. It suggests where things are heading: systems that can understand multiple modalities together, not in isolation.

It made me wonder though how do we process information and is it similar to a multimodal embedding model. 
