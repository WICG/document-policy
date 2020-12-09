# Defining Document Policy configuration points

This guide is for authors of other standards who want to use Document Policy
as a mechanism for enabling, disabling, or otherwise configuring their features.
It's a collection of principles and guidelines (more than actual rules) for
coming up with sensible defaults, whether the feature in question is a
long-standing feature on the web, or something brand new.

## Referencing the Document Policy spec

There is no central registry for configuration points. Feature authors who wish
to allow Document Policy to control their features on the web can do so by
referencing the Document Policy specification.

The following example shows how a feature could be declared as a document policy
configuration point:

> Example:
>
>### Section N: Document Policy Integration
> The Sample API defines a [*configuration point*](https://wicg.github.io/document-policy/#configuration-point)
> whose [*name*](https://wicg.github.io/document-policy/#configuration-point-name)
> is "`sample`". Its [type](https://wicg.github.io/document-policy/#configuration-point-type)
> is 'boolean', and its [default value](https://wicg.github.io/document-policy/#configuration-point-default-value)
> is 'false'. \[[DOCUMENT-POLICY](https://wicg.github.io/document-policy/)\].

The specification could then refer to this feature, and test its value in a
specific document, with text similar to this:

> Example:
>
> If the result of calling [policy value](https://wicg.github.io/document-policy/#get-policy-value)
> for "`sample`" in [this](https://heycam.github.io/webidl/#this)'s
> [responsible document](https://html.spec.whatwg.org/multipage/webappapis.html#responsible-document)
> is 'false', then throw a `SecurityError`
> [DOMException](https://heycam.github.io/webidl/#dfn-DOMException) and abort these steps.

(This is an example only. The actual behavior of any algorithm when a
policy-controlled feature is disabled is left up to the specification which
defines that feature.)

## Choosing a default value

The default value for a configuration point affects how the feature will behave
when there is no declared policy for that feature. Generally, the default should
be chosen so that there is no behaviour change for existing documents (which
will not be served with a Document-Policy header). As a rough guide:

* Features which have already been widely available on the web platform, but
which Document Policy can now disable selectively, should be boolean features
with a value of 'true'.

* New opt-in limitations on existing features are likely to be numeric (int or
float) features, with a default value of 'infinity'.
