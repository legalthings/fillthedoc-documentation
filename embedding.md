# Embedding

With the document API you can create a new document. The response of this request will contain an `edit_url` property. This URL can be send directly to the end user or it can be used to embed filling out the document in your application.

## iframe

To allow a user to edit the document in your application, embed fillthedoc using an iframe. The URL of the iframe is the `edit_url` of the document.

```markup
<iframe id="fillthedoc" src="{{ document.edit_url }}" />
```

\_\_

![](.gitbook/assets/screenshot-localhost-8000-2019.08.30-14-01-50%20%281%29.png)

_The UI has a minimalistic style without any branding, so it doesn't look out of place when embedded in most cases. The design is mobile friendly. It's **not** possible to customize the style._

### Preview

If the template has a help view, it will be displayed by default, with the option of switching to the document preview. If there is no help view for the template, the document preview is displayed.

Use the `?preview=<mode>` query parameter to toggle what is shown

| mode |  |
| :--- | :--- |
| never | Never show the document preview. Shows the help if available, otherwise just the form. |
| off | Show the help by default _\(if available\)_ |
| on | Show the document preview by default |
| always | Don't show the help _\(even if available\)_ |

## Completion message

The iframe will send a message to the parent window when the user finishes the form using [`window.postMessage()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage). The parent window can add a even listener for the `"message"` event. In the handler, make sure the message originated from `https://filthedoc.com` to prevent abuse with this feature.

```markup
<script>
  window.addEventListener("message", function (event) {
    if (event.origin !== "http://localhost:8000") return;

    // Optionally use document data
    let documentData = event.data;

    // Next...
  }, false);
</script>
```

The message contains the JSON of the document, which can be used to display information to the user in a rich web application. Data that is not be available for the end user is omitted from the event data.

{% hint style="warning" %}
You should NOT rely on the message for processing the data. Instead, always specify a `callback` URL when creating the document.
{% endhint %}

## Full example

```markup
<!DOCTYPE html>
<html>
  <head>
	  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /> 
	  <title>fillthedoc iframe</title>

    <style>
      body {
        margin: 0;
        padding: 0;
        height: 100vh;
        width: 100vw;
      }

      iframe {
        height: 100%;
        width: 100%;
        border: none;
      }
    </style>

    <script>
      window.addEventListener("message", documentCompleted, false);

      function documentCompleted(event) {
        if (event.origin !== "http://localhost:8000") return;

        // Optionally use document data
        let documentData = event.data;

        // Show a different page
        window.location.href = 'https://example.com';
      }
    </script>
  </head>
  <body>
	  <iframe id="fillthedoc" src="https://fillthedoc.com/legalthings/4gc4wow40gkg808040ck8scwwkskwc40okwkc00skws48848s8wo48k0k8c4c04w" />
  </body>
</html>

```

