---
title: Elasticsearch - Autocomplete suggestions
date: "2016-05-28"
layout: post
path: "/elasticsearch-autocomplete-suggestions"
category: "elasticsearch"
description: "Ideally, auto-complete functionnality should be as fast as the user typing to provide instant feedback. If you're doing your autocomplete implementation by using regex-like searches in your DB (ie: gith*), you're doing it wrong"
---

Ideally, auto-complete functionnality should be as fast as the user typing to provide instant feedback. If you're doing your autocomplete implementation by using regex-like searches in your DB (MySQL, Mongo, ES), you're doing it wrong, and sadly, I know this from experience :(

<img src="https://i.giphy.com/h6pWFVxVhOXZK.gif" width="500" height="500"/>

You're going to encounter a few issues:
- Regex searches uses a lot of resources
- They are slow (ie: > 100ms + network latency)   
- Most of the time, you can't do fuzzy queries (ie: if you search for Github but you type Gitjub, the result won't appear)

## Elasticsearch autocomplete suggestions

Elasticsearch provides you with a powerful API to do autocomplete: https://www.elastic.co/guide/en/elasticsearch/reference/current/search-suggesters-completion.html

#### Why it's better?

The completion suggester is optimized for speed. The suggester uses data structures that enable fast lookups and are stored in-memory.

In my case, I recently switched an autocomplete with 100k results from classical ES Search to this completion suggester. I went from an autocomplete with an average latency of 150ms to one with 5ms of latency.

<img src="https://i.giphy.com/maIEBUU5OmrMA.gif" width="500" height="500"/>
