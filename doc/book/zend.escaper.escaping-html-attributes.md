# Escaping HTML Attributes

Escaping data in the **HTML Attribute context** is most often done incorrectly, if not overlooked
completely by developers. Regular \[HTML escaping\](zend.escaper.escaping-html) can be used for
escaping HTML attributes, *but* only if the attribute value can be **guaranteed as being properly
quoted**! To avoid confusion, we recommend always using the HTML Attribute escaper method in the
HTML Attribute context.

To escape data in the HTML Attribute, use `Zend\Escaper\Escaper`'s `escapeHtmlAttr` method.
Internally it will convert the data to UTF-8, check for it's validity, and use an extended set of
characters to escape that are not covered by `htmlspecialchars` to cover the cases where an
attribute might be unquoted or quoted illegally.

## Examples of Bad HTML Attribute Escaping

An example of incorrect HTML attribute escaping:

``` sourceCode
<?php header('Content-Type: text/html; charset=UTF-8'); ?>
<!DOCTYPE html>
<?php
$input = <<<INPUT
' onmouseover='alert(/ZF2!/);
INPUT;
/**
 * NOTE: This is equivalent to using htmlspecialchars($input, ENT_COMPAT)
 */
$output = htmlspecialchars($input);
?>
<html>
<head>
    <title>Single Quoted Attribute</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>
    <div>
        <?php 
        // the span tag will look like:
        // <span title='' onmouseover='alert(/ZF2!/);'>
        ?>
        <span title='<?php echo $output ?>'>
            What framework are you using?
        </span>
    </div>
</body>
</html>
```

In the above example, the default `ENT_COMPAT` flag is being used, which does not escape single
quotes, thus resulting in an alert box popping up when the `onmouseover` event happens on the `span`
element.

Another example of incorrect HTML attribute escaping can happen when unquoted attributes are used,
which is, by the way, perfectly valid HTML5:

``` sourceCode
<?php header('Content-Type: text/html; charset=UTF-8'); ?>
<!DOCTYPE html>
<?php
$input = <<<INPUT
faketitle onmouseover=alert(/ZF2!/);
INPUT;
// Tough luck using proper flags when the title attribute is unquoted!
$output = htmlspecialchars($input,ENT_QUOTES);
?>
<html>
<head>
    <title>Quoteless Attribute</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>
    <div>
        <?php 
        // the span tag will look like:
        // <span title=faketitle onmouseover=alert(/ZF2!/);>
        ?>
        <span title=<?php echo $output ?>>
            What framework are you using?
        </span>
    </div>
</body>
</html>
```

The above example shows how it is easy to break out from unquoted attributes in HTML5.

## Examples of Good HTML Attribute Escaping

Both of the previous examples can be avoided by simply using the `escapeHtmlAttr` method:

``` sourceCode
<?php header('Content-Type: text/html; charset=UTF-8'); ?>
<!DOCTYPE html>
<?php
$input = <<<INPUT
faketitle onmouseover=alert(/ZF2!/);
INPUT;
$escaper = new Zend\Escaper\Escaper('utf-8');
$output = $escaper->escapeHtmlAttr($input);
?>
<html>
<head>
    <title>Quoteless Attribute</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>
    <div>
        <?php 
        // the span tag will look like:
        // <span title=faketitle&#x20;onmouseover&#x3D;alert&#x28;&#x2F;ZF2&#x21;&#x2F;&#x29;&#x3B;>
        ?>
        <span title=<?php echo $output ?>>
            What framework are you using?
        </span>
    </div>
</body>
</html>
```

In the above example, the malicious input from the attacker becomes completely harmless as we used
proper HTML attribute escaping!
