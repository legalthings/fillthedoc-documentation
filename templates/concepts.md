---
description: General concepts for building templates
---

# Glossary

<table>
  <thead>
    <tr>
      <th style="text-align:left">Document builder</th>
      <th style="text-align:left">The environment in which the documents/templates are created.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Form</td>
      <td style="text-align:left">List of all steps and fields, is on the left side of a template.</td>
    </tr>
    <tr>
      <td style="text-align:left">If-statement</td>
      <td style="text-align:left">An if/then condition. If X, then Y</td>
    </tr>
    <tr>
      <td style="text-align:left">Mustaches</td>
      <td style="text-align:left">To dynamically create a document, mustaches {{ }} are used. To make a
        field editable in the text, the name of the field must be covered by two
        mustaches on both sides: {{ field }}. Without mustaches, the fields are
        not usable.</td>
    </tr>
    <tr>
      <td style="text-align:left">Operator</td>
      <td style="text-align:left">
        <p>A symbol that is used with variables to perform various functions. Think
          of arithmetic or logical functions. The most commonly used operators are
          explained below:</p>
        <p></p>
        <p><b>Arithmetic operators</b>
        </p>
        <ul>
          <li><code>+</code> Add</li>
          <li><code>-</code> Subtract</li>
          <li><code>*</code> Multiply</li>
          <li><code>/</code> Divide</li>
        </ul>
        <p><b>Comparison operators</b>
        </p>
        <ul>
          <li><code>==</code> is equal to</li>
          <li><code>!=</code> is not equal to</li>
          <li><code>&gt;</code> is greater than</li>
          <li><code>&lt;</code> is smaller than</li>
          <li><code>&gt;=</code> is greater than or &gt; equal to</li>
          <li><code>&lt;=</code> is smaller than or &gt; equal to</li>
        </ul>
        <p><b>Logical operators</b>
        </p>
        <ul>
          <li><code>&amp;&amp;</code> AND (&quot;and&quot;)</li>
          <li><code>||</code> OR (&quot;or&quot;)</li>
          <li><code>!</code> NOT (&quot;not&quot;)</li>
        </ul>
        <p><b>String operators</b>
        </p>
        <p>With the plus symbol (<code>+</code>), we can combine two strings.</p>
        <p>For example:
          <br /><code> text1 = &quot;Two strings &quot;<br /> text2 = &quot;combined&quot;<br /> text3 = text1 + text2</code>
        </p>
        <p>The content of variable text 3 is now: <code>&quot;Two strings combined&quot;</code>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Programming</td>
      <td style="text-align:left">Term for making pieces of text in a template dynamic.</td>
    </tr>
    <tr>
      <td style="text-align:left">Template</td>
      <td style="text-align:left">A template is a digitized document.</td>
    </tr>
    <tr>
      <td style="text-align:left">Text</td>
      <td style="text-align:left">The text is understood to mean the text of a template and is to the right
        of the form.</td>
    </tr>
    <tr>
      <td style="text-align:left">User</td>
      <td style="text-align:left">The user is understood to mean the end user of the software.</td>
    </tr>
  </tbody>
</table>