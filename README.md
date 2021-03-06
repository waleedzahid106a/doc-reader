# Simple Annotations Parser(DocReader) in PHP

Just a Simple Annotation Parser in PHP

## Installation

Just Download this Repository and Place `src` folder on your server directory.

## Examples

### Type conversion example

```php
<?php

include_once "src/DocReader/DocReader.php";

class MyClass
{
	/**
	 * @var0 1.5
	 * @var1 1
	 * @var2 "123"
	 * @var3 abc
	 * @var4 ["a", "b"]
	 * @var5 {"x": "y"}
	 * @var6 {"x": {"y": "z"}}
	 * @var7 {"x": {"y": ["z", "p"]}}
	 *
	 * @var8
	 * @var9 null
	 *
	 * @var10 true
	 * @var11 tRuE
	 * @var12 false
	 * @var13 null
	 * 
	 */
	private function MyMethod()
	{
	}
};

$reader = new DocReader\Reader("MyClass", "MyMethod");

var_dump($reader->getParams());
```

### Multi value example

```php
<?php

include_once "src/DocReader/DocReader.php";

class MyClass
{
	/**
	 * @var x
	 * @var2 1024
	 * @param string x
	 * @param integer y
	 * @param array z
	 */
	private function MyMethod()
	{
	}
};

$reader = new DocReader\Reader("MyClass", "MyMethod");

var_dump($reader->getParams());
```

will print


<pre class='xdebug-var-dump' dir='ltr'>
<b>array</b> <i>(size=3)</i>
  'var' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'x'</font> <i>(length=1)</i>
  'var2' <font color='#888a85'>=&gt;</font> <small>int</small> <font color='#4e9a06'>1024</font>
  'param' <font color='#888a85'>=&gt;</font> 
    <b>array</b> <i>(size=3)</i>
      0 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'string x'</font> <i>(length=8)</i>
      1 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'integer y'</font> <i>(length=9)</i>
      2 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'array z'</font> <i>(length=7)</i>
</pre>

### Variables on the same line

```php
<?php

include_once "src/DocReader/DocReader.php";

class MyClass
{
	/**
	 * @get @post
	 * @ajax
	 * @postParam x @postParam y
	 * @postParam z
	 */
	private function MyMethod()
	{
	}
};

$reader = new DocReader\Reader("MyClass", "MyMethod");

var_dump($reader->getParams());
```

will print

<pre class='xdebug-var-dump' dir='ltr'>
<b>array</b> <i>(size=4)</i>
  'get' <font color='#888a85'>=&gt;</font> <small>boolean</small> <font color='#75507b'>true</font>
  'post' <font color='#888a85'>=&gt;</font> <small>boolean</small> <font color='#75507b'>true</font>
  'ajax' <font color='#888a85'>=&gt;</font> <small>boolean</small> <font color='#75507b'>true</font>
  'postParam' <font color='#888a85'>=&gt;</font> 
    <b>array</b> <i>(size=3)</i>
      0 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'x'</font> <i>(length=1)</i>
      1 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'y'</font> <i>(length=1)</i>
      2 <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'z'</font> <i>(length=1)</i>
</pre>

### Variable declarations functionality example

I found below functionality useful for filtering `$_GET`/`$_POST` data in CodeIgniter. Hopefully I will soon release my CodeIgniter's modification.

```php
<?php

include_once "src/DocReader/DocReader.php";

class MyClass
{
	/**
	 * @param string var1
	 * @param integer var2
	 */
	private function MyMethod()
	{
	}
};

$reader = new DocReader\Reader("MyClass", "MyMethod");

var_dump($reader->getVarDeclarations("param"));
```

will print

<pre class='xdebug-var-dump' dir='ltr'>
<b>array</b> <i>(size=2)</i>
  0 <font color='#888a85'>=&gt;</font> 
    <b>array</b> <i>(size=2)</i>
      'type' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'string'</font> <i>(length=6)</i>
      'name' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'var1'</font> <i>(length=4)</i>
  1 <font color='#888a85'>=&gt;</font> 
    <b>array</b> <i>(size=2)</i>
      'type' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'integer'</font> <i>(length=7)</i>
      'name' <font color='#888a85'>=&gt;</font> <small>string</small> <font color='#cc0000'>'var2'</font> <i>(length=4)</i>
</pre>
