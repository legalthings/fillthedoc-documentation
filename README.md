---
description: 'fillthedoc is an advanced document engine, powered by JavaScript'
---

# Getting started

## Step 1. Create a template

The template consists of a form, which may be filled out by the end user, and text content. The content contains placeholders that are filled with the data of the form. More advanced functions can be used, like if statements and formatting.

{% page-ref page="templates/" %}

## Step 2. Create a document

Use the API to create a new document based on a template. Send some initial data and allow the end user to fill out the rest. You may specify a callback URL to let your system know that the user is done.

{% page-ref page="api/document-api.md" %}

## Step 3. Download the document and data

One the user has filled out the form, use the API to generate a PDF and fetch the data so it can be processed.

