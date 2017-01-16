# MvcCore Extension - View Helper Assets

View helper extension for:
- grouping files together to deliver them in one response
- optional rendering PHP code inside group files
- optional completing assets url adresses targeting into index.php
  packed result, where small data sources (icons, image maps...),
  shoud be packed into, if you want to develop and build single
  file application.
  - Example: `<?php echo $this->AssetUrl('favicon.ico'); ?>`
- saving grouped files in application temp directory `'/Var/Tmp'`
- checking changed sources by file modification time or by file md5 imprint
- no source files checking in application compiled mode (packed into PHP package)
- optional CSS or JS minification by external library `mrclay/minify ^2.2.0`
- optional downloading external js files into result group

## Example

Base controller code:
```php
class App_Controllers_Base {
	public function PreDispatch () {
		parent::PreDispatch();
		MvcCoreExt_ViewHelpers_Assets::SetGlobalOptions(array(
			cssMinify	=> TRUE,
			cssJoin		=> TRUE,
		));
		$this->Css('head')
			->AppendRendered('/app/root/rel/path/to/first.css')
			->Append('/app/root/rel/path/to/second.css');
	}
}
```

Layout template code:
```html
<html>
	<head>
		<!-- only one file will be delivered: '/Var/Tmp/temp-file-name.css' -->
		<?php echo $this->->Css('head')->Render(); ?>
	</head>
	<body>...</body>
</html>
```