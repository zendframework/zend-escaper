# Introduction to Zend\\Escaper

The [OWASP Top 10 web security risks](https://www.owasp.org/index.php/Top_10_2010-Main) study lists
Cross-Site Scripting (XSS) in second place. PHP's sole functionality against XSS is limited to two
functions of which one is commonly misapplied. Thus, the `Zend\Escaper` component was written. It
offers developers a way to escape output and defend from XSS and related vulnerabilities by
introducing **contextual escaping based on peer-reviewed rules**.

`Zend\Escaper` was written with ease of use in mind, so it can be used completely stand-alone from
the rest of the framework, and as such can be installed with Composer using
zendframework/zend-escaper.

For easier use of the Escaper component within the framework itself, especially with the `Zend\View`
component, a \[set of view helpers\](zend.view.helpers) is provided.

> ### Warning
The `Zend\Escaper` is a security related component. As such, if you believe you found an issue with
this component, we ask that you follow our [Security Policy](http://framework.zend.com/security/)
and report security issues accordingly. The Zend Framework team and the contributors thanks you in
advance.

## Overview

The `Zend\Escaper` component provides one class, `Zend\Escaper\Escaper` which in turn, provides five
methods for escaping output. Which method to use when, depends on the context in which the outputted
data is used. It is up to the developer to use the right methods in the right context.

`Zend\Escaper\Escaper` has the following escaping methods available for each context:

* **escapeHtml**: escape a string for the HTML Body context.
* **escapeHtmlAttr**: escape a string for the HTML Attribute context.
* **escapeJs**: escape a string for the Javascript context.
* **escapeCss**: escape a string for the CSS context.
* **escapeUrl**: escape a string for the URI or Parameter contexts.

Usage of each method will be discussed in detail in later chapters.

## What Zend\\Escaper is not

`Zend\Escaper` is meant to be used only for escaping data that is to be output, and as such should
not be misused for filtering input data. For such tasks, the \[Zend\\Filter
component\](zend.filter), [HTMLPurifier](http://htmlpurifier.org/) or PHP's
[Filter](http://php.net/manual/en/book.filter.php) component should be used.
